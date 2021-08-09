# FieldOrder

* Author: zihjiang
* Version: 0.0.1

### Description

排序数据表

| name                                     | type   | required | default value |
| ---------------------------------------- | ------ | -------- | ------------- |
| field_and_sort                           | array  | yes      |               |
| [common-options](#common-options-string) | string | no       | -             |

##### field_and_sort [array]

格式: 需要排序的字段名.排序方式

##### common options [string]

`Transform` 组件通用参数，详情参照 [Transform]()

配置示例

```json
{
    "source_table_name": "sql_table24",
    "result_table_name": "sql_table25",
    "plugin_name": "FieldOrder",
    "field_and_sort": [
        "value.desc",
        "metric.desc"
    ]
}
```

