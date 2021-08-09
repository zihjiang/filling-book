## Source plugin : JDBC

* Author: zihjiang
* Version: 0.0.1

### Description
通过jdbc的方式读取数据

### Options
| name | type | required | default value |
| --- | --- | --- | --- |
| [driver](#driver-string) | string | yes | - |
| [url](#url-string) | string | yes | - |
| [username](#username-string) | string | yes | - |
| [password](#password-string) | string | no | - |
| [query](#query-string) | string | yes | - |
| [fetch_size](#fetch_size-int) | int | no | - |
| [common-options](#common-options-string)| string | no | - |

##### driver [string]

驱动名，如`com.mysql.jdbc.Driver`

默认支持包含mysql(com.mysql.jdbc.Driver)和clickhouse(ru.yandex.clickhouse.ClickHouseDriver)驱动

##### url [string]

JDBC连接的URL。如：`jdbc:mysql://localhost:3306/test`

##### username [string]

用户名

##### password [string]

密码

##### query [string]
查询语句

##### fetch_size [int]
拉取数量

##### common options [string]

`Source` 插件通用参数，详情参照 [Source Plugin](/zh-cn/v2/flink/configuration/source-plugins/)

## 配置示例

```yaml
    {
      "plugin_name": "JdbcSource",
      "driver": "com.mysql.jdbc.Driver",
      "result_table_name": "JdbcSourceTable",
      "url": "jdbc:mysql://10.10.14.17:3306/tmp",
      "username": "aiops",
      "password": "aiops",
      "query": "select * from t_group"
    }
```
