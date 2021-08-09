# 任务

任务是Filling数据摄取任务的主要抽象，允许用户配置处理数据的输入、流程、输出及其它运行时设定，追踪任务执行的状态和日志，并提供样例输入测试等附加功能。

## 任务属性

### 基本属性

- result_table_name：source或transfrom生成的目标表
- source_table_name: transfrom或sink的数据来源
- name：任务名称命名，任务标识, 也用于flink生成的jobgraph的名称
- parallelism: 定义任务正式运行时对资源的需求量，默认为1
- describe：任务描述信息

并行度需要根据集群剩余的资源数（task slot数）和任务复杂度、处理数据量进行设置。

### 任务DAG

任务DAG是由[组件](http://192.168.1.13:8080/concepts/Plugin.html)、组件的属性配置及组件之间的数据流动关系定义构成的，是一个**有向无环图**。它定义了任务的数据处理逻辑：数据由一个或者多个数据源流入，经过多个转换器的处理后，流入一个或者多个输出从而落盘到文件、Kafka或者其他输出端。

任务DAG其内容的脚本化示例（以json格式为例）如下：

```json
{
  "env": {
    "execution.parallelism": 1,
    "job.name": "filling-01"
  },
  "source": [
    {
      "plugin_name": "KafkaTableStream",
      "consumer.group.id": "filling15",
      "topics": "batchSend",
      "result_table_name": "KafkaTableStreamTable",
      "format.type": "json",
      "schema": "{\"host\":\"192.168.1.103\",\"source\":\"datasource\",\"MetricsName\":\"cpu\",\"value\":\"49\",\"_time\":1626571020000,\"trade_type\":\"未知\"}",
      "format.allow-comments": "true",
      "format.ignore-parse-errors": "true",
      "offset.reset": "earliest",
      "consumer.bootstrap.servers": "192.168.100.189:9092",
      "parallelism": 10,
      "name": "mykafka"
    }
    {
      "plugin_name": "JdbcSource",
      "driver": "com.mysql.jdbc.Driver",
      "result_table_name": "JdbcSourceTable",
      "url": "jdbc:mysql://10.10.14.17:3306/tmp",
      "username": "aiops",
      "password": "aiops",
      "query": "select * from t_group"
    }
  ],
  "transform": [
    {
      "source_table_name": "KafkaTableStreamTable",
      "result_table_name": "KafkaTableStreamTable_default",
      "plugin_name": "DataJoin",
      "join.source_table_name": [
        "JdbcSourceTable"
      ],
      "join.JdbcSourceTable.where": "workgroup = host",
      "join.JdbcSourceTable.type": "left"
    },
    {
      "source_table_name": "KafkaTableStreamTable_default",
      "result_table_name": "DataSelector_default",
      "plugin_name": "DataSelector",
      "select.result_table_name": [
        "DataSelector_unknown",
        "DataSelector_other"
      ],
      "select.DataSelector_unknown.where": " serial_no ='未知'",
      "select.DataSelector_other.where": " serial_no !='未知'"
    }
  ],
  "sink": [
    {
      "source_table_name": "DataSelector_unknown",
      "plugin_name": "Elasticsearch",
      "hosts": [
        "10.10.14.51:9200"
      ],
      "index": "filling_unknown",
      "es.bulk.flush.max.actions": 1000,
      "es.bulk.flush.max.size.mb": 2,
      "es.bulk.flush.interval.ms": 1000,
      "es.bulk.flush.backoff.enable": true,
      "es.bulk.flush.backoff.delay": 50,
      "es.bulk.flush.backoff.retries": 8
    },
    {
      "source_table_name": "DataSelector_other",
      "plugin_name": "Elasticsearch",
      "hosts": [
        "10.10.14.51:9200"
      ],
      "index": "filling_other",
      "es.bulk.flush.max.actions": 1000,
      "es.bulk.flush.max.size.mb": 2,
      "es.bulk.flush.interval.ms": 1000,
      "es.bulk.flush.backoff.enable": true,
      "es.bulk.flush.backoff.delay": 50,
      "es.bulk.flush.backoff.retries": 8
    }
  ]
}
```

上面的DAG定义了从一个kafka数据源订阅数据, 和一个mysql数据源的数据，进行join后对数据进行分流，输出到Elasticsearch端的处理流程。其中，<font color=#0099ff>serial_no 字段等于'未知'</font>的数据会写入到elasticsearch 的filling_unknown 索引, 相反, 其他不等于未知的数据会写到filling_other索引, （source）进提供输出数据表KafkaTableStreamTable和JdbcSource.（transfrom）算子 DataJoin 的输入表(source_table_name)为<font color=#0099ff>KafkaTableStreamTable</font>, join.source_table_name参数为 <font color=#0099ff>JdbcSourceTable</font>， 查询类型为<font color=#0099ff>left</font>, 意味这表KafkaTableStreamTable 和表JdbcSourceTable 做join查询, 且join的条件为 <font color=#0099ff>workgroup = host</font> 输出（sink）仅需求输入数据表，而（transform）既提供输出数据表，也需求输入数据表，而且可能不止一个。每个输出数据表必须要存在相同名称的输入数据流来满足，这也构成了组件之间的数据流动关系。

流程图:

```Mermaid
graph TD
KafkaTableStream-kafka(kakfa-topic is batchSend) --> DataJoin(join-where is workgroup = host)
KafkaTableStream-jdbc(mysql-table is t_group) --> DataJoin(join-where is workgroup = host)
DataJoin(join-where is workgroup = host) --> DataSelector{DataSelector}
DataSelector{DataSelector} --serial_no ='未知'--> sink-elasticsearch-[filling_unknown]
DataSelector{DataSelector} --serial_no !='未知'--> sink-elasticsearch[filling_other]
```

注意，任务DAG，其组件与数据流构成的有向图必须是无环的。与可能存在迭代运算的批式处理场景不同，数据摄取是典型的流式处理场景，数据流不能以循环的方式进行流动，从而多次进入同一个处理逻辑。在DAG的配置脚本中，亦要求多个组件（主要是多个transfrom组件）的编写顺序是符合DAG的拓扑顺序的。

编辑任务DAG，从而定义任务处理逻辑，是配置任务的主体工作。目前只支持一种方式进行：

- 直接编辑任务文件：直接编写DAG配置脚本，支持以json的方式编写。编写好的文件可以直接通过Filling-core提交执行。参见[配置文件](http://192.168.1.13:8080/concepts/Pipeline.html#配置文件)部分。

------

## 配置文件

Filling推荐使用图形化界面完成任务的配置和运行。然而，你可以从界面导出或自行编写你的任务配置文件。配置文件可以用于通过界面导入以建立对应的任务，也可以直接通过提交到flink cluster运行的Filling-core程序执行。

配置文件支持以json, 格式为例说明配置文件的内容：

```json
{
  "env": {
  },
  "source": [
  ],
  "transform": [
  ],
  "sink": [

  ]
}
```

配置文件中dag以配置为object（包含了source、transform和sink三个字段，为组件分类列表）还有额外的env全局参数,。其中:

env: flink相关的参数, [详见](xxx), 

source: 数据来源, [详见](xxx), 

transfer: 数据处理算子, [详见](xxx),  

Sink: 数据存储位置, [详见](xxx),  

，
