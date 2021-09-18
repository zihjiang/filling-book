# DataJoin

* Author: zihjiang
* Version: 0.0.1

### Description

两个数据表做join, 最好是一张流表(kafka或datagen的source), 和一张批表(jdbc或file的source)

| name                                     | type   | required | default value |
| ---------------------------------------- | ------ | -------- | ------------- |
| join.source_table_name                   | Array  | yes      |               |
| join.*.where                             | string | yes      |               |
| join.*.type                              | string | yes      | left          |
| [common-options](#common-options-string) | string | no       | -             |



##### join.source_table_name [array]

需要和``source_table_name``做join的表, 可以是多个

##### join.*.where [string]

\*号和``join.source_table_name``对应, 这里指两张表join的条件

##### join.*.type [string]

\*号和``join.source_table_name``对应, 这里指join的类型, left和right

##### common options [string]

`Transform` 组件通用参数，详情参照 [Transform]()

配置示例

```json
    {
      "source_table_name": "KafkaTableStreamTable",
      "result_table_name": "KafkaTableStreamTable_default",
      "plugin_name": "DataJoin",
      "join.source_table_name": [
        "JdbcSourceTable"
      ],
      "join.JdbcSourceTable.where": "workgroup = host",
      "join.JdbcSourceTable.type": "left"
    }
```

