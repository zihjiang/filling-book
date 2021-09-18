# FieldSelect

* Author: zihjiang
* Version: 0.0.1

### Description

显示的声明要保留的列

| name                                     | type   | required | default value |
| ---------------------------------------- | ------ | -------- | ------------- |
| field                                    | array  | yes      |               |
| [common-options](#common-options-string) | string | no       | -             |

##### field [array]

要保留的字段

##### common options [string]

`Transform` 组件通用参数，详情参照 [Transform]()

配置示例

```json
{
            "source_table_name": "sql_table26",
            "result_table_name": "sql_table27",
            "plugin_name": "FieldSelect",
            "field": [
                "categoryName",
                "metric",
                "auth"
            ]
}
```



