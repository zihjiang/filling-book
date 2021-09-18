# FieldRename

* Author: zihjiang
* Version: 0.0.1

### Description

重命名一个字段

| name                                     | type   | required | default value |
| ---------------------------------------- | ------ | -------- | ------------- |
| source_field                             | string | yes      |               |
| target_field                             | string | yes      |               |
| [common-options](#common-options-string) | string | no       | -             |

##### source_field [array]

原字段

##### source_field [array]

目标字段

##### common options [string]

`Transform` 组件通用参数，详情参照 [Transform]()

配置示例

```json
{
            "source_table_name": "sql_table25",
            "result_table_name": "sql_table26",
            "plugin_name": "FieldRename",
            "source_field": "value",
            "target_field": "value2"
}
```

