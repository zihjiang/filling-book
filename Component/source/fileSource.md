## Source plugin : File

* Author: zihjiang
* Version: 0.0.1

### Description
从文件系统中读取数据

### Options
| name                                     | type   | required | default value |
| ---------------------------------------- | ------ | -------- | ------------- |
| [format.type](#format-string)            | string | yes      | -             |
| [path](#path-string)                     | string | yes      | -             |
| [schema](#schema-string)                 | string | yes      | -             |
| [common-options](#common-options-string) | string | no       | -             |

##### format.type [string]

从文件系统中读取文件的格式，目前支持`csv`、`json`、`parquet` 、`orc`和 `text`。

##### path [string]

需要文件路径，hdfs文件以hdfs://开头，本地文件以file://开头。

##### schema [string]

- csv
   - csv的schema是一个jsonArray的字符串，如`"[{\"type\":\"long\"},{\"type\":\"string\"}]"`，这个只能指定字段的类型，不能指定字段名，一般还要配合公共配置参数`field_name`。
- json
   - json的schema参数是提供一个原数据的json字符串，可以自动生成schema，但是需要提供内容最全的原数据，否则会有字段丢失。
- parquet
   - parquet的schema是一个Avro schema的字符串，如`{\"type\":\"record\",\"name\":\"test\",\"fields\":[{\"name\":\"a\",\"type\":\"int\"},{\"name\":\"b\",\"type\":\"string\"}]}`。
- orc
   - orc的schema是orc schema的字符串，如`"struct<name:string,addresses:array<struct<street:string,zip:smallint>>>"`。
- text 
   - text的schema填为string即可。
   

##### common options [string]

`Source` 插件通用参数，详情参照 [Source Plugin]()

### 配置示例

```
{ 
  "schema": "{\"hostid\": \"host01\",\"metric\": \"cpu_user\",\"value\": 13, \"auth\": \"1,2,3,4,5\"}", 
  "path": "/tmp/user.json", 
  "result_table_name": "FileSourceTable", 
  "plugin_name": "FileSource", 
  "format.type": "json" 
}
```
