# Kafka数据源

Kafka数据源（`KafkaSource`）从指定Kafka集群的一个或多个指定主题中消费数据。

注: 请在生产环境下,  务必在任务参数一栏填写"execution.checkpoint.interval": 1000参数, 详情: [消费位点提交](https://nightlies.apache.org/flink/flink-docs-master/zh/docs/connectors/datastream/kafka/#%e6%b6%88%e8%b4%b9%e4%bd%8d%e7%82%b9%e6%8f%90%e4%ba%a4)

------

### [Options]()

| name                       | type         | required | default value |
| -------------------------- | ------------ | -------- | ------------- |
| [topics]()                 | array/string | yes      | -             |
| [group.id]()               | string       | no       | -             |
| [bootstrap.servers]()      | string       | yes      | -             |
| [schema]()                 | string       | yes      | -             |
| [format.type]()            | string       | yes      | json          |
| [format.field_delimiter]() | String       | no       | ,             |
| [consumer.*]()             | string       | no       | -             |
| [offset.reset]()           | string       | no       | -             |
| [common-options]()         | string       | no       | -             |

## 属性

##### topics (array[string])

topic名称。

##### group_id (string) (optinal)

订阅组id。如果不指定，每次运行时都会根据组件id自动生成一个。如果组件id没有显示指定而是自动生成的话，则不能保证每次执行时都会分配到相同的订阅组，因此建议指定。

##### consumer.bootstrap.servers (string)

Kafka集群地址，多个地址用`,`隔开。

##### schema (String)

用于生成source表的schema, 如果数据和schema字段不一致, 则会出现字段为空的问题

##### format.type (string)

输入格式，支持Json,csv和与text格式

##### format.field_delimiter (optinal)

仅在format.type为csv时生效, 指定分隔符, 且只能是一个char字符

##### offset.reset

  以何种方式消费kafka数据, 分别是:

    earliest: 尽可能从最早消费数据
    
    latest: 从最新处消费数据
    
    fromTimestamp: 指定时间戳消费, // TODO
    
    fromGroupOffsets: 从当前的offset消费, 若果不存在offset, 则和latest一致
##### 其他配置 consumer.* (optinal)

除了以上必备的kafka consumer客户端必须指定的参数外，用户还可以指定多个consumer客户端非必须参数，覆盖了[kafka官方文档指定的所有consumer参数](http://kafka.apache.org/documentation.html#oldconsumerconfigs).

------

## 配置示例

```yaml
{
      "plugin_name": "KafkaTableStream",
      "consumer.group.id": "waterdrop15",
      "topics": "batchSend",
      "result_table_name": "KafkaTableStreamTable",
      "format.type": "json",
      "schema": "{\"host\":\"192.168.1.103\",\"source\":\"datasource\",\"MetricsName\":\"cpu\",\"value\":\"49\",\"_time\":1626571020000}",
      "offset.reset": "earliest",
      "consumer.bootstrap.servers": "192.168.100.189:9092",
      "parallelism": 1,
      "name": "mykafka"
    }
```
