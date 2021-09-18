# DataAggregates

* Author: zihjiang
* Version: 0.0.1

### Description
基于翻滚时间窗口的聚合

### Options
| name                                                         | type   | required | default value |
| ------------------------------------------------------------ | ------ | -------- | ------------- |
| [rowtime.watermark.field](#rowtime.watermark.field)          | string | yes      | -             |
| [rowtime.watermark.tumble.ms](#rowtime.watermark.tumble.ms)  | int    | yes      |               |
| [rowtime.watermark.tumble.delay.ms](#rowtime.watermark.tumble.delay.ms) | int    | yes      |               |
| [group.fields](#group.fields)                                | Array  | Yes      |               |
| [group.*.function](#group.*.function)                        | Array  | no       | ["count"]     |
| [custom.fields](#custom.fields)                              | Array  | no       |               |
| [custom.field.*.script](#custom.field.*.script)              | string | no       |               |
| [common-options](#common-options-string)                     | string | no       | -             |

##### rowtime.watermark.field [string]

时间字段, 必须是13位时间戳类型

##### rowtime.watermark.tumble.ms [int]

翻滚窗口的大小, 单位是毫秒

##### rowtime.watermark.tumble.delay.ms [int]

允许数据迟到时间, 单位是毫秒

##### group.fields [int]

聚合的字段, rowtime时间字段不需要显示的指定,

##### group.*.function [int]

\*是指每个 ``group.fields``, 需要显示的指定每个字段聚合使用的函数, 可选择: max, count, min, 默认为count

##### custom.fields [array]

除了对``group.fields``字段聚合, 还可以自定义聚合字段, 这里设置的是字段名称

##### custom.field.*.script [string]

每个``custom.field``的具体函数, 可选择: max, count, min


##### common options [string]

`Transform` 插件通用参数，详情参照 [Transform Plugin]()

### 配置示例

```json
{
      "source_table_name": "FieldOperation_message_time2",
      "result_table_name": "DataAggregates_01",
      "plugin_name": "DataAggregates",
      "rowtime.watermark.field": "_time",
      "rowtime.watermark.tumble.ms": 1000,
      "rowtime.watermark.tumble.delay.ms": 1000,
      "group.fields": [
        "fixed"
      ],
      "group.fixed.function": ["count"],
      "custom.field": ["max_value", "min_value"],
      "custom.field.max_value.script": "max(value)",
      "custom.field.min_value.script": "min(value)"
    }
```

这个配置相当于指定watermark字段为_time, 按照1秒钟做时间窗口, 允许延迟1秒, 根据fixed聚合,并求出fixed值和value的max, min值
