# Console

* Author: zihjiang
* Version: 0.0.1

### Description

输出结果到控制台, 仅供调试

### Options

|                                          | string | yes  | -    |
| ---------------------------------------- | ------ | ---- | ---- |
| [common-options](#common-options-string) | string | no   | -    |



只有基础的参数`source_table_name`, 输出数据表的数据, 仅供调试

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
