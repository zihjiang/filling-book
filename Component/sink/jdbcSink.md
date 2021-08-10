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
| [username](#username-string)             | string | yes      | -             |
| [password](#password-string)             | string | no       | -             |
| [query](#query-string)                   | string | yes      | -             |
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

查询语句

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
