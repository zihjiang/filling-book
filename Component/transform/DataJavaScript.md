# DataJavascript

* Author: zihjiang
* Version: 0.0.1

### Description

用javascript的语法来处理数据, 实现process函数, 和FieldJavaScript不同的是, DataJavascript 返回的是所有行数据, 也就是返回的格式应该是一个JSON对象, 这就意味着当process返回的数据只包括一个属性时, 此算子的返回结果也只包括一个字段

| name                                     | type   | required | default value |
| ---------------------------------------- | ------ | -------- | ------------- |
| script                                   | string | yes      |               |
| [common-options](#common-options-string) | string | no       | -             |



##### script [string]

javascript的脚本文件, 主要实现process的函数, 返回了一个字符串
```json
function process(d) {
 // 固定返回字符串 
 // d为所有字段的对象
 // 格式为{"key": "value"} 
	return d;
}
```

##### common options [string]

`Transform` 组件通用参数，详情参照 [Transform]()

配置示例

```json
{
  "name": "DataJavascript",
  "plugin_name": "DataJavascript",
  "script": "function process(d) {d.jsfields='123'; \n return d;\n}",
  "parallelism": "1",
  "source_table_name": "FieldOperation_63aa796e_7ffa",
  "result_table_name": "FieldJavascript_2233ac0e_5b7e"
}
```

返回实例

```json
// 源数据
[
  {
    "randint": "2dda16efea31ea25df7c5fd57dfd242b",
    "host": "192.168.1.103",
    "id": 1,
    "source": "datasource",
    "MetricsName": "cpu",
    "value": 49,
    "_time": 1654956631000
  }
]
```

```json
// 处理后的数据
[
  {
    "randint": "2dda16efea31ea25df7c5fd57dfd242b",
    "host": "192.168.1.103",
    "id": 1,
    "source": "datasource",
    "jsfields": "123",
    "MetricsName": "cpu",
    "value": 49,
    "_time": 1654956631000
  }
]
```

