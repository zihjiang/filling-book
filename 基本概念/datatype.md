# 数据类型

Flink采用了强Schema设计。意味着对于每个source需要显示地指明其字段格式内容（默认都是以schema属性自动生成schema, 这避免了用户描述、枚举数据格式的复杂度, ）个别source除外。

Filling的自动属性生成，数据类型如下：

- The default planner supports the following set of SQL types:

  | schema 样例           | Data Type | Remarks for Data Type |
  | --------------------- | :-------- | :-------------------- |
  | {"name": "zihjiang"}  | `VARCHAR` |                       |
  | {"age": 18}           | `INT`     |                       |
  | {"ts": 1584597899669} | LONG      |                       |

> **注意**
>
> Filling需要你对字段类型进行检查，但这要求用户自己需要确保类型是符合操作特性的，否则将会导致运行时的默认行为，甚至错误。

------

## 嵌套字段

