# EncodeBase64


* Author: zihjiang
* Version: 0.0.1

### Description

debase64某一个字段

| name                                     | type   | required | default value |
| ---------------------------------------- | ------ | -------- | ------------- |
| source_field                             | string | yes      |               |
| target_field                             | string | yes      |               |
| [common-options](#common-options-string) | string | no       | -             |



##### source_field [string]

源字段名

##### target_field [string]

目标字段名

##### common options [string]

`Transform` 组件通用参数，详情参照 [Transform]()

配置示例

```json
{
    "source_table_name":"sql_table22",
    "result_table_name":"sql_table23",
    "plugin_name":"DecodeBase64",
    "source_field":"metric2",
    "target_field":"metric"
}
```

