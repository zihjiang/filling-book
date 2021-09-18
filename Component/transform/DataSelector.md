# DataJoin

* Author: zihjiang
* Version: 0.0.1

### Description

一个数据表拆分成用条件拆两个数据表

| name                                     | type   | required | default value |
| ---------------------------------------- | ------ | -------- | ------------- |
| select.result_table_name                 | Array  | yes      |               |
| select.*.where                           | string | yes      |               |
| [common-options](#common-options-string) | string | no       | -             |



##### select.result_table_name [array]

要生成的数据表表名,

##### join.*.where [string]

\*号和select.result_table_name对应, 这里指两张表的条件

##### common options [string]

`Transform` 组件通用参数，详情参照 [Transform]()

配置示例

```json
    {
      "source_table_name": "KafkaTableStreamTable_default",
      "result_table_name": "DataSelector_default",
      "plugin_name": "DataSelector",
      "select.result_table_name": [
        "DataSelector_unknown",
        "DataSelector_other"
      ],
      "select.DataSelector_unknown.where": " serial_no ='未知'",
      "select.DataSelector_other.where": " serial_no !='未知'"
    }
```

