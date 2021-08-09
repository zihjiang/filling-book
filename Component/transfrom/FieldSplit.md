# FieldSplit

* Author: zihjiang
* Version: 0.0.1

### Description

根据分隔符, 把一个字段分割成多列

| name                                     | type   | required | default value |
| ---------------------------------------- | ------ | -------- | ------------- |
| fields                                   | array  | yes      |               |
| separator                                | string | yes      |               |
| [common-options](#common-options-string) | string | no       | -             |

##### fields [array]

要分割的字段

##### separator [string]

分隔符

##### common options [string]

`Transform` 组件通用参数，详情参照 [Transform]()

配置示例

```json
{
            "source_table_name": "sql_table27",
            "result_table_name": "sql_table28",
            "plugin_name": "FieldSplit",
            "source_field": "auth",
            "fields": [
                "n1",
                "n2",
                "n3",
                "n4",
                "n5",
                "n6"
            ],
            "separator": "\\|"
}
```



