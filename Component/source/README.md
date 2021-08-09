# SOURCE

从指定的输入源读入数据形成数据表，对每条读入数据按照格式规则处理为数据。

------

## 配置方式

### 界面配置

【TODO：前端完成后】

### DAG脚本配置

可以在DAG脚本中添加数据源。

```json
    {
      "plugin_name": "KafkaTableStream",
      "result_table_name": "KafkaTableStreamTable",
      "parallelism": 1,
      "name": "mykafka"
       ...
    }
```

------

## 通用属性

##### 名称 name (string) (optional)

组件的类型名称, 也是flink生成jobgraph的名称。

##### 组件并行度 parallelism (Int) (optional)

该组件实的并行度, 主要用于source和sink, 

##### 使用的组件名称 plugin_name (string)

使用那个组件处理数据

##### 输出表 result_table_name (string)

输出数据流名称，可以作为transfrom/输出的输入。

##### 数据样例 schema (json/csv/text)

测试样例, 会根据此消息生成表结构

------

## 格式化输入源

对于无Schema输入源（目前支持的文本数据源、Kafka数据源等），输入条目原以纯文本或者字节码的方式提供。此时需要指定从输入到数据条目的反序列化方式。

目前支持的反序列化方式包括：

- **JSON** 将每条原始输入条目作为一条JSON格式化字符串进行反序列化。
- **CSV** 将每条原始输入条目作为多个字段进行反序列化。此时需要指定`分隔符`，作为多个字段之间的分隔符；
- **纯文本** 将每条原始输入条目不进行反序列化，直接转化为table。此时需要指定`数据表只有一列f0`，作为将原始输入条目内容放入f0中

后续我们将会逐渐添加对于XML等常见字符串序列化协议，以及Avro、ProtoBuffer等常见字节码序列化协议的支持。
