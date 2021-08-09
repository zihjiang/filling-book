## Source plugin : JDBC [Flink]

* Author: zihjiang
* Version: 0.0.1

### Description
生成可用的测试数据, 用来模拟流数据

### Options
| name                                | type       | required | default value |
| ----------------------------------- | ---------- | -------- | ------------- |
| [rows-per-second](#rows-per-second) | int        | yes      | -             |
| [number-of-rows](#url-string)       | int        | yes      | -             |
| [fields](#username-string)          | array      | yes      | -             |
| [schema]()                          | jsonString | yes      | -             |

##### rows-per-second [string]

一秒之内, 生成多少条数据

##### [number-of-rows] [string]

本次任务一共要生成多少条数据

##### fields [array]

生成数据的格式, 详细格式如下:
```json
[
        {
          "id": { // 字段名称, 和schema对应
            "kind": "SEQUENCE", // 生成数据模式, SEQUENCE是顺序, 每次+1, RANDOM是随机, 只有在type为int的时候, 次参数才有效
            "type": "Int", // 生成的数据类型
            "start": 0, // 从哪里生成数据, 只有在type为int的时候, 次参数才有效
            "end": 10000000 // 生成到多少结束, 只有在type为int的时候, 次参数才有效
          }
        },
        {
          "host": {
            "type": "String",// 生成的数据类型
            "length": 1 // 生成的数据长度, 只有在type为String的时候, 次参数才有效
          }
        },
        {
          "value": {
            "type": "Long",// 生成的数据类型为Long
            "min": 1,				// 随机生成的数据最小值, 只有在type为Long的时候, 此参数才有效
            "max": 2				// 随机生成的数据最大值, 只有在type为Long的时候, 此参数才有效
          }
        }
 ]
```

##### schema [jsonString]
###### 注意, 这里必须是json字符串, 且包含转义字符`\`

{\"id\":1, \"host\":\"192.168.1.103\",\"value\":49}


### 配置示例

```json
{
      "plugin_name": "DataGenTableStream",
      "result_table_name": "dataGenTableStreamTable",
      "schema": "{\"id\":1, \"host\":\"192.168.1.103\",\"source\":\"datasource\",\"MetricsName\":\"cpu\",\"value\":49}",
      "rows-per-second": 1000000,
      "number-of-rows": 100000000,
      "fields": [
        {
          "id": {
            "kind": "SEQUENCE",
            "type": "Int",
            "start": 0,
            "end": 10000000
          }
        },
        {
          "host": {
            "type": "String",
            "length": 1
          }
        },
        {
          "source": {
            "type": "String",
            "length": 10
          }
        },
        {
          "MetricsName": {
            "type": "String",
            "length": 10
          }
        },
        {
          "value": {
            "type": "Int",
            "min": 1,
            "max": 2
          }
        }
      ],
      "parallelism": 5,
      "name": "my-datagen-source"
    }

```
