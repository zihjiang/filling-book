# FieldTypeConver

* Author: zihjiang
* Version: 0.0.1

### Description

转换一个或多个字段的类型

| name                                     | type   | required | default value |
| ---------------------------------------- | ------ | -------- | ------------- |
| target_field_type                        | string | yes      |               |
| source_field                             | array  |          |               |
| [common-options](#common-options-string) | string | no       | -             |

##### target_field_type [array]

目标字段类型, 可选int/String/Long

##### source_field [array]

源字段名称

##### common options [string]

`Transform` 组件通用参数，详情参照 [Transform]()

配置示例

```json
{
    "source_table_name": "sql_table29",
    "result_table_name": "sql_table30",
    "plugin_name": "FieldTypeConver",
    "target_field_type": "int",
    "source_field": [
      "newfield"
    ]
}
```

