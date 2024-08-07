---
title: TO_YYYYMMDD
---

将日期或带时间的日期（时间戳/日期时间）转换为包含年份和月份编号的 UInt32 数字（YYYY * 10000 + MM * 100 + DD）。

## 语法

```sql
TO_YYYYMMDD(<expr>)
```

## 参数

| 参数       | 描述         |
|------------|--------------|
| `<expr>`   | 日期/日期时间 |

## 返回类型

`INT`，返回格式为 `YYYYMMDD`。

## 示例

```sql
SELECT
  to_yyyymmdd('2023-11-12 09:38:18.165575');

┌───────────────────────────────────────────┐
│ to_yyyymmdd('2023-11-12 09:38:18.165575') │
├───────────────────────────────────────────┤
│                                  20231112 │
└───────────────────────────────────────────┘
```