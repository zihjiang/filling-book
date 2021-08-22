# DataParsing

* Author: zihjiang
* Version: 0.0.1

### Description

把不规则数据转换成规则数据, 例如日志等

| name                                     | type   | required | default value |
| ---------------------------------------- | ------ | -------- | ------------- |
| source_field                             | string | yes      |               |
| fields                                   | Array  | yes      |               |
| [common-options](#common-options-string) | string | no       | -             |



##### source_field [string]

源字段, 需要解析的字段

##### fields [array]

要解析的字段名称对象, 例如:

```json
"fields":[
        {
          "index_id":0, #
          "type":"string", # 字段类型, 可选string, datatime, number
          "pattern":"", # 当type为datatime时有效, 时间的格式, 例如: yyyyMMDD
          "format":"^(\\d+\\.\\d+\\.\\d+\\.\\d+)\\s", # 从原字段解析出来的正则表达式
          "name":"clientip", # 字段名称
          "title":"客户端地址", # 显示名称
          "ref":"@message" # 来源字段, 默认为source_field
        },
        {
          "index_id":1,
          "type":"datetime",
          "pattern":"yyyy/MM/dd HH:mm:ss",
          "format":"\\d+\\/\\d+\\/\\d+ \\d+:\\d+:\\d+",
          "name":"timestamp",
          "title":"时间戳",
          "ref":"@message"
        },
        {
          "index_id":2,
          "type":"string",
          "pattern":"",
          "format":"\\]\\s\"(\\w+)\\s",
          "name":"verb",
          "title":"请求类型",
          "ref":"@message"
        },
        {
          "index_id":3,
          "type":"string",
          "pattern":"",
          "format":"\\]\\s\\\"\\w+\\s(.*)\\sHTTP",
          "name":"request",
          "title":"请求地址",
          "ref":"@message"
        },
        {
          "index_id":4,
          "type":"string",
          "pattern":"",
          "format":"HTTP\\/[\\d\\.]",
          "name":"rspcode",
          "title":"返回码",
          "ref":"@message"
        },
        {
          "index_id":5,
          "type":"number",
          "pattern":"bigint",
          "format":"HTTP\/[\\d\\.]+\\\"\\s\\d+\\s(\\d+)\\s",
          "name":"bytes",
          "title":"字节数",
          "ref":"@message"
        },
        {
          "index_id":6,
          "type":"string",
          "pattern":"",
          "format":"\\\"\\s\"(.*)\\\"$",
          "name":"agent",
          "title":"浏览器",
          "ref":"@message"
        }
      ]
```

##### common options [string]

`Transform` 组件通用参数，详情参照 [Transform]()

配置示例

```json
{
      "source_table_name":"KafkaTableStreamTable",
      "result_table_name":"DataParsing_p",
      "plugin_name":"DataParsing",
      "source_field":"value",
      "fields":[
        {
          "index_id":0,
          "type":"string",
          "pattern":"",
          "format":"^(\\d+\\.\\d+\\.\\d+\\.\\d+)\\s",
          "name":"clientip",
          "title":"客户端地址",
          "ref":"@message"
        },
        {
          "index_id":1,
          "type":"datetime",
          "pattern":"yyyy/MM/dd HH:mm:ss",
          "format":"\\d+\\/\\d+\\/\\d+ \\d+:\\d+:\\d+",
          "name":"timestamp",
          "title":"时间戳",
          "ref":"@message"
        },
        {
          "index_id":2,
          "type":"string",
          "pattern":"",
          "format":"\\]\\s\"(\\w+)\\s",
          "name":"verb",
          "title":"请求类型",
          "ref":"@message"
        },
        {
          "index_id":3,
          "type":"string",
          "pattern":"",
          "format":"\\]\\s\\\"\\w+\\s(.*)\\sHTTP",
          "name":"request",
          "title":"请求地址",
          "ref":"@message"
        },
        {
          "index_id":4,
          "type":"string",
          "pattern":"",
          "format":"HTTP\\/[\\d\\.]",
          "name":"rspcode",
          "title":"返回码",
          "ref":"@message"
        },
        {
          "index_id":5,
          "type":"number",
          "pattern":"bigint",
          "format":"HTTP\/[\\d\\.]+\\\"\\s\\d+\\s(\\d+)\\s",
          "name":"bytes",
          "title":"字节数",
          "ref":"@message"
        },
        {
          "index_id":6,
          "type":"string",
          "pattern":"",
          "format":"\\\"\\s\"(.*)\\\"$",
          "name":"agent",
          "title":"浏览器",
          "ref":"@message"
        }
      ]
    }
```

