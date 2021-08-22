# FileSink

* Author: zihjiang
* Version: 0.0.1

### Description

输出结果到文件

### Options

| name                                     | type   | required | default value |
| ---------------------------------------- | ------ | -------- | ------------- |
| path                                     | string | yes      | -             |
| write_mode                               | string | yes      | -             |
| format                                   | string | Yes      | -             |
| [common-options](#common-options-string) | string | no       | -             |



##### path [string]

输出的文件全路径, 

##### write_mode [string]

输出模式, 可选: 

​	OVERWRITE: 如果存在文件, 则覆盖

​	NO_OVERWRITE: 如果存在文件, 则追加

##### format [string]

json, csv, text, 

##### common options [string]

`Source` 插件通用参数，详情参照 [Source Plugin](/zh-cn/v2/flink/configuration/source-plugins/)

## 配置示例

```yaml
{
    "path": "/tmp/1",
    "write_mode": "OVERWRITE",
    "format": "json",
    "source_table_name": "sql_table19",
    "plugin_name": "FileSink"
}
```
