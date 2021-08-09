# Sql

### Description
使用SQL处理数据，使用的是flink的sql语法，支持其各种udf

### Options
| name                                     | type   | required | default value |
| ---------------------------------------- | ------ | -------- | ------------- |
| [sql](#sql-string)                       | string | yes      | -             |
| [common-options](#common-options-string) | string | no       | -             |


##### common options [string]

`Transform` 组件通用参数，详情参照 [Transform]()

### Examples

```
{
    "source_table_name": "FileSourceTable",
    "result_table_name": "sql_table19",
    "plugin_name": "Sql",
    "sql": "select hostid, auth from  FileSourceTable where metric='CPU' "
}
```
