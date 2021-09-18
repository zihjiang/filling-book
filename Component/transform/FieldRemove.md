# FieldRemove

* Author: zihjiang
* Version: 0.0.1

### Description

删除一个, 或多个列

| name                                     | type   | required | default value |
| ---------------------------------------- | ------ | -------- | ------------- |
| field                                    | array  | yes      |               |
| [common-options](#common-options-string) | string | no       | -             |

##### field [array]

要删除的列

##### common options [string]

`Transform` 组件通用参数，详情参照 [Transform]()

配置示例

```json
{
            "source_table_name": "sql_table23",
            "result_table_name": "sql_table24",
            "plugin_name": "FieldRemove",
            "field": [
                "hostid"
            ]
 }
```

