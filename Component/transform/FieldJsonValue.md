# FieldJsonValue

* Author: zihjiang
* Version: 0.0.1

### Description

从一个json字符串的字段里, 提取值, 并生成一个新的字段

| name                                     | type   | required | default value |
| ---------------------------------------- | ------ | -------- | ------------- |
| target_field                             | string | yes      |               |
| source_field                             | string | Yes      |               |
| path                                     | string | yes      |               |
| return_type                              | String | no       | STRING        |
| [common-options](#common-options-string) | string | no       | -             |

##### target_field [string]

目标字段名

##### source_field [string]

源字段名

##### path [string]

json的xpath表达式, 如数据为{"name": "张三"}, 则表达式应填写$.name

##### return_type [string]

target_field字段类型, 可选, 默认为STRING

INT, DOUBLE, FLOAT, DATE, BIGINT, BOOLEAN

##### common options [string]

`Transform` 组件通用参数，详情参照 [Transform]()

配置示例

```json
// "{\"name\": \"张三\"}"
{
      "source_table_name": "FieldJsonValue",
      "result_table_name": "FieldJsonValue_34545",
      "plugin_name": "FieldJsonValue",
      "source_field": "message1231",
      "path": "$.name",
      "target_field": "message1232"
    }
```

