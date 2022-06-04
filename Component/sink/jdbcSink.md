## Sink plugin : JDBC

* Author: zihjiang
* Version: 0.0.1

### Description

通过jdbc的方式sink到数据库

### Options

| name                                     | type   | required | default value |
| ---------------------------------------- | ------ | -------- | ------------- |
| [driver](#driver-string)                 | string | yes      | -             |
| [url](#url-string)                       | string | yes      | -             |
| [username](#username-string)             | string | no       | -             |
| [password](#password-string)             | string | no       | -             |
| [query](#query-string)                   | string | yes      | -             |
| Params                                   | Array  | Yes      |               |
| [batch_size](#batch_size)                | int    | no       | 5000          |
| batch_interval_ms                        | int    | No       | 200           |
| max_retries                              | Int    |          | 5             |
| [common-options](#common-options-string) | string | no       | -             |

##### driver [string]

驱动名，如`com.mysql.jdbc.Driver`

默认支持包含mysql(com.mysql.jdbc.Driver)和clickhouse(ru.yandex.clickhouse.ClickHouseDriver)驱动

##### url [string]

JDBC连接的URL。如：`jdbc:mysql://localhost:3306/test`

##### username [string]

用户名

##### password [string]

密码

##### query [string]

插入数据库的sql语句, 默认为	`insert into main({columns}) values({questionMark})`,

 其中{columns}为占位符, 与参数`params`一致, 如params的字段参数为: ['id', 'host'], 则这里的{columns}为id,host,

 其中{questionMark}为占位符, 与参数`params`数量一致, 如params的字段参数为: ['id', 'host'], 则这里的{questionMark}为?,?



也可以不用占位符, 使用原生插入语句`insert into main(id,host) values(?,?)`

##### batch_size [int]

每个批次多少数据

##### batch_interval_ms  [int]

多久提交一个批次

##### max_retries  [int]

重试最大次数

##### common options [string]

`Source` 插件通用参数，详情参照 [Source Plugin](/zh-cn/v2/flink/configuration/source-plugins/)

## 配置示例

```yaml
    {
      "source_table_name": "JdbcSourceTable",
      "plugin_name": "ClickHouseSink",
      "driver": "ru.yandex.clickhouse.ClickHouseDriver",
      "url": "jdbc:clickhouse://192.168.100.15:8123/aiops",
      "query": "insert into host_metric10(host, metric, value, system, instance, _time) values(?,?,?,?,?,?)",
      "batch_size": "2000",
      "params": ["host", "metric", "value", "system", "instance", "_time"],
      "parallelism": 5,
      "name": "mytest"
    }
```

或

```json
{
  "name": "ClickHouse",
  "plugin_name": "ClickHouseSink",
  "parallelism": "1",
  "driver": "ru.yandex.clickhouse.ClickHouseDriver",
  "url": "jdbc:clickhouse://192.168.1.200:8123/default",
  "username": "",
  "password": "",
  "query": "insert into main({columns}) values({questionMark})",
  "params": [
    "id",
    "host",
    "source",
    "MetricsName",
    "value",
    "_time"
  ],
  "batch_size": "20000",
  "source_table_name": "FieldOperation_ee6875e9_56f1",
  "id": "ClickHouseSink-87cf626f-2147"
}
```

