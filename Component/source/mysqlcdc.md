## Source plugin : mysql cdc

* Author: zihjiang
* Version: 0.0.1

### Description
通过cdc的方式读取数据, 建表语句用{table}占位符表示表名, 后续不需要这个表名, 固定写法, 使用cdc时需要在任务参数增加``` , "execution.checkpoint.interval": "3000"```



注: 目前filling为不完整的cdc, 只支持插入语法, 暂不支持删除和修改, 当对一个表进行修改过删除时, 会出现位置错误, 设置可能导致任务停止, 请谨慎使用

### Options
| name | type | required | default value |
| --- | --- | --- | --- |
| [sql](#sql) | string | yes | - |

##### sql [string]

建表sql, 参考[MySQL CDC Connector — Flink CDC  documentation](https://ververica.github.io/flink-cdc-connectors/master/content/connectors/mysql-cdc.html#how-to-create-a-mysql-cdc-table)



##### common options [string]

`Source` 插件通用参数，详情参照 [Source Plugin](/zh-cn/v2/flink/configuration/source-plugins/)

## 配置示例

```yaml
CREATE TABLE {table} (
    `id` bigint,
    `itemid` STRING,
    `clock` INT,
    `value` DOUBLE,
    `ns` INT,
    PRIMARY KEY (`id`)  NOT ENFORCED
  ) WITH (
    'connector' = 'mysql-cdc',
    'hostname' = '192.168.100.141',
    'port' = '3306',
    'username' = 'root',
    'password' = '1qaz@WSX',
    'database-name' = 'zabbix',
    'table-name' = 'history'
  )
```
