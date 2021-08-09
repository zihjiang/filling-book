# Elasticsearch

# Sql

### Description

sink到elasticsearch

### Options

| name                                     | type   | required | default value |
| ---------------------------------------- | ------ | -------- | ------------- |
| [hosts](#hosts)                          | string | yes      | -             |
| index                                    | String | yes      |               |
| es.bulk.flush.max.actions                | int    | no       |               |
| es.bulk.flush.max.size.mb                | int    | no       |               |
| es.bulk.flush.interval.ms                | int    | no       |               |
| es.bulk.flush.backoff.enable             | bool   | no       |               |
| es.bulk.flush.backoff.delay              | int    | no       |               |
| es.bulk.flush.backoff.retries            | int    | no       |               |
| [common-options](#common-options-string) | string | no       | -             |

##### hosts [string]

es的host地址, 格式为host:端口, 例如: 10.11.12.1:9200

##### index [string]

es的索引名称, 

##### es.bulk.flush.max.actions options [string]

刷新前要缓冲的最大文档数

##### es.bulk.flush.max.size.mb options [string]

刷新前要缓冲的最大数据大小( 单位是M)

##### es.bulk.flush.interval.ms options [string]

无论缓冲操作的数量或大小如何，刷新的时间间隔。

##### es.bulk.flush.backoff.enable options [string]



##### es.bulk.flush.backoff.delay options [string]



##### es.bulk.flush.backoff.retries options [string]



##### common options [string]

`Transform` 组件通用参数，详情参照 [Transform]()

### Examples

```json
{
    "source_table_name": "DataSelector_other",
    "plugin_name": "Elasticsearch",
    "hosts": [
      "10.10.14.51:9200"
    ],
    "index": "waterdrop_other",
    "es.bulk.flush.max.actions": 1000,
    "es.bulk.flush.max.size.mb": 2,
    "es.bulk.flush.interval.ms": 1000,
    "es.bulk.flush.backoff.enable": true,
    "es.bulk.flush.backoff.delay": 50,
    "es.bulk.flush.backoff.retries": 8
}
```

