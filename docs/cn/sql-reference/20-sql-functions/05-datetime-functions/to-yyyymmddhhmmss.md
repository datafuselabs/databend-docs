---
title: TO_YYYYMMDDHHMMSS
---

将日期或带时间的日期（时间戳/日期时间）转换为包含年份和月份编号的 UInt64 数字（YYYY * 10000000000 + MM * 100000000 + DD * 1000000 + hh * 10000 + mm * 100 + ss）。

## 语法

```sql
TO_YYYYMMDDHHMMSS(<expr>)
```

## 参数

| 参数       | 描述         |
|-----------|--------------|
| `<expr>`  | 日期/时间戳  |

## 返回类型

`BIGINT`，返回格式为 `YYYYMMDDhhmmss`。

## 示例

```sql
SELECT
  to_yyyymmddhhmmss('2023-11-12 09:38:18.165575');

┌─────────────────────────────────────────────────┐
│ to_yyyymmddhhmmss('2023-11-12 09:38:18.165575') │
├─────────────────────────────────────────────────┤
│                                  20231112000000 │
└─────────────────────────────────────────────────┘

SELECT
  to_yyyymmddhhmmss(to_timestamp('2023-11-12 09:38:18.165575'));

┌───────────────────────────────────────────────────────────────┐
│ to_yyyymmddhhmmss(to_timestamp('2023-11-12 09:38:18.165575')) │
├───────────────────────────────────────────────────────────────┤
│                                                20231112093818 │
└───────────────────────────────────────────────────────────────┘
```