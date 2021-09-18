# FieldOperation

* Author: zihjiang
* Version: 0.0.1

### Description

生成一个全新字段, 支持sql函数

| name                                     | type   | required | default value |
| ---------------------------------------- | ------ | -------- | ------------- |
| target_field                             | string | yes      |               |
| script                                   | string | yes      |               |
| [common-options](#common-options-string) | string | no       | -             |

##### target_field [string]

目标字段名

##### script [string]

sql脚本, 可以是sql函数, 也可以是常量字符串, 常量字符串必须用单引,  [完整的支持的函数列表](https://ci.apache.org/projects/flink/flink-docs-release-1.13/zh/docs/dev/table/functions/systemfunctions/)

常用函数

|                          函数/范例                           |                             说明                             |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
|                     string1 \|\| string2                     |               返回 STRING1 和 STRING2 的相加。               |
|         CHAR_LENGTH(string) CHARACTER_LENGTH(string)         |                   返回 STRING 中的字符数。                   |
|                        UPPER(string)                         |                   以大写形式返回 STRING。                    |
|                        LOWER(string)                         |                   以小写形式返回 STRING。                    |
|                 POSITION(string1 IN string2)                 | 返回 STRING2 中第一次出现 STRING1 的位置（从 1 开始）；如果在 STRING2 中找不到 STRING1，则返回 0。 |
|  TRIM([ BOTH \| LEADING \| TRAILING ] string1 FROM string2)  | 返回从 STRING1 中删除前导和/或尾随字符 STRING2 的字符串。默认情况下，两边的空格都会被删除。 |
|                        LTRIM(string)                         | 返回一个从 STRING 中删除左边空格的字符串。例如，'这是一个测试字符串。'.ltrim() 返回“这是一个测试字符串。”。 |
|                        RTRIM(string)                         | 返回一个从 STRING.Eg 中删除正确空格的字符串。例如，'这是一个测试字符串。 '.rtrim() 返回“这是一个测试字符串。”。 |
|                     REPEAT(string, int)                      | 返回一个字符串，它重复基本字符串整数次。例如，REPEAT('This is a test String.', 2) 返回“这是一个测试字符串。这是一个测试字符串。”。 |
|          REGEXP_REPLACE(string1, string2, string3)           | 从 STRING1 返回一个字符串，其中所有与正则表达式 STRING2 匹配的子字符串连续被 STRING3 替换。例如， 'foobar'.regexpReplace('oo\|ar', '') returns "fb". |
| OVERLAY(string1 PLACING string2 FROM integer1 [ FOR integer2 ]) | 返回一个字符串，该字符串从位置 INT1 用 STRING2 替换 STRING1 的 INT2（默认为 STRING2 的长度）字符。例如，'xxxxxtest'.overlay('xxxx', 6) 返回“xxxxxxxxx”； 'xxxxxtest'.overlay('xxxx', 6, 2) 返回“xxxxxxxxxst”。 |
|       SUBSTRING(string FROM integer1 [ FOR integer2 ])       | 返回 STRING 的子字符串，从位置 INT1 开始，长度为 INT2（默认到结尾）。 |
|              REPLACE(string1, string2, string3)              | 返回一个新字符串，该字符串将所有出现的 STRING2 替换为 STRING1 中的 STRING3（非重叠）。例如，'hello world'.replace('world', 'flink') 返回 'hello flink'; 'ababab'.replace('abab', 'z') 返回 'zab'。 |
|         REGEXP_EXTRACT(string1, string2[, integer])          | 从 string1 返回一个字符串，该字符串使用指定的正则表达式 string2 和正则表达式匹配组索引整数提取。正则表达式匹配组索引从 1 开始，0 表示匹配整个正则表达式。此外，正则表达式匹配组索引不应超过定义的组数。例如 REGEXP_EXTRACT('foothebar', 'foo(.*?)(bar)', 2)" 返回 "bar"。 |
|                       INITCAP(string)                        | 返回新形式的 STRING，其中每个单词的第一个字符转换为大写，其余字符转换为小写。这里的单词表示字母数字字符序列。 |
|                 CONCAT(string1, string2,...)                 | 返回连接 string1、string2、...的字符串。如果任何参数为 NULL，则返回 NULL。例如，CONCAT('AA', 'BB', 'CC') 返回“AABBCC”。 |
|           CONCAT_WS(string1, string2, string3,...)           | 返回将 STRING2、STRING3、... 与分隔符 STRING1 连接起来的字符串。在要连接的字符串之间添加分隔符。如果 STRING1 为 NULL，则返回 NULL。与 concat() 相比， concat_ws() 会自动跳过 NULL 参数。例如， concat_ws('~', 'AA', Null(STRING), 'BB', '', 'CC') 返回“AA~BB~~CC”。 |
|               LPAD(string1, integer, string2)                | 返回一个新字符串，从 string1 左边填充 string2 到整数字符的长度。如果 string1 的长度小于 integer，则返回 string1 缩短为整数字符。例如，LPAD('hi',4,'??') 返回“??hi”； LPAD('hi',1,'??') 返回“h”。 |
|               RPAD(string1, integer, string2)                | 从 string1 中返回一个新字符串，用 string2 右填充，长度为整数字符。如果 string1 的长度小于 integer，则返回 string1 缩短为整数字符。例如，RPAD('hi',4,'??') 返回“hi??”，RPAD('hi',1,'??') 返回“h”。 |
|                     FROM_BASE64(string)                      | 从字符串返回 base64 解码的结果；如果字符串为 NULL，则返回 NULL。例如，FROM_BASE64('aGVsbG8gd29ybGQ=') 返回“hello world”。 |
|                      TO_BASE64(string)                       | 从字符串返回 base64 编码的结果；如果字符串为 NULL，则返回 NULL。例如，TO_BASE64('hello world') 返回“aGVsbG8gd29ybGQ=”。 |
|                        ASCII(string)                         | 返回字符串第一个字符的数值。如果字符串为 NULL，则返回 NULL。例如，ascii('abc') 返回 97，而 ascii(CAST(NULL AS VARCHAR)) 返回 NULL。 |
|                         CHR(integer)                         | 返回二进制等效于整数的 ASCII 字符。如果整数大于 255，我们将先得到整数除以 255 的模数，并返回模数的 CHR。如果整数为 NULL，则返回 NULL。例如，chr(97) 返回 a，chr(353) 返回 a，而 ascii(CAST(NULL AS VARCHAR)) 返回 NULL。 |
|                    DECODE(binary, string)                    | 使用提供的字符集（'US-ASCII'、'ISO-8859-1'、'UTF-8'、'UTF-16BE'、'UTF-16LE'、'UTF- 16')。如果任一参数为空，则结果也将为空。 |
|                   ENCODE(string1, string2)                   | 使用提供的 string2 字符集（'US-ASCII'、'ISO-8859-1'、'UTF-8'、'UTF-16BE'、'UTF-16LE'、'UTF- 16')。如果任一参数为空，则结果也将为空。 |
|                   INSTR(string1, string2)                    | 返回 string2 在 string1 中第一次出现的位置。如果任何参数为 NULL，则返回 NULL。 |
|                    LEFT(string, integer)                     | 返回字符串中最左边的整数字符。如果整数为负，则返回 EMPTY 字符串。如果任何参数为 NULL，则返回 NULL。 |
|                    RIGHT(string, integer)                    | 返回字符串中最右边的整数字符。如果整数为负，则返回 EMPTY 字符串。如果任何参数为 NULL，则返回 NULL。 |
|             LOCATE(string1, string2[, integer])              | 返回 string2 中 string1 在位置 integer 之后第一次出现的位置。如果未找到，则返回 0。如果任何参数为 NULL，则返回 NULL。 |
|            PARSE_URL(string1, string2[, string3])            | 从 URL 返回指定的部分。 string2 的有效值包括“HOST”、“PATH”、“QUERY”、“REF”、“PROTOCOL”、“AUTHORITY”、“FILE”和“USERINFO”。如果任何参数为 NULL，则返回 NULL。例如，parse_url('http://facebook.com/path1/p.php?k1=v1&k2=v2#Ref1', 'HOST')，返回 'facebook.com'。还可以通过提供键作为第三个参数 string3 来提取 QUERY 中特定键的值。例如， parse_url('http://facebook.com/path1/p.php?k1=v1&k2=v2#Ref1', 'QUERY', 'k1') 返回 'v1'。 |
|                   REGEXP(string1, string2)                   | 如果 string1 的任何（可能为空）子字符串与 Java 正则表达式 string2 匹配，则返回 TRUE，否则返回 FALSE。如果任何参数为 NULL，则返回 NULL。 |
|                       REVERSE(string)                        |         返回翻转的字符串, 如果参数为null, 则返回null         |
|           SPLIT_INDEX(string1, string2, integer1)            | 通过分隔符 string2 拆分 string1，返回拆分字符串的第整数（从零开始）字符串。如果整数为负，则返回 NULL。如果任何参数为 NULL，则返回 NULL。 |
|           STR_TO_MAP(string1[, string2, string3]])           | 使用分隔符将 string1 拆分为键/值对后返回一个映射。 string2 是对分隔符，默认为 ','。而 string3 是键值分隔符，默认为 '='。 |
|            SUBSTR(string[, integer1[, integer2]])            | 返回字符串的子字符串，从位置 integer1 开始，长度为 integer2（默认到末尾）。 |



##### common options [string]

`Transform` 组件通用参数，详情参照 [Transform]()

配置示例

```json
    {
      "source_table_name": "dataGenTableStreamTable",
      "result_table_name": "FieldOperation_time",
      "plugin_name": "FieldOperation",
      "target_field": "_time",
      "script": "UNIX_TIMESTAMP()*1000"
    }
```

