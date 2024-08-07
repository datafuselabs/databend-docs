---
title: TO_UNIX_TIMESTAMP
---

将日期/时间格式的 timestamp 转换为 Unix timestamp 格式。Unix timestamp 表示自 1970 年 1 月 1 日 00:00:00 UTC 以来经过的秒数。

## 语法

```sql
TO_UNIX_TIMESTAMP(<expr>)
```

## 参数

| 参数        | 描述         |
| ----------- | ------------ |
| `<expr>`    | 时间戳       |

有关时间戳数据类型的更多信息，请参阅 [日期与时间](../../00-sql-reference/10-data-types/20-data-type-time-date-types.md)。

## 返回类型

`BIGINT`

## 示例

```sql
SELECT
  to_unix_timestamp('2023-11-12 09:38:18.165575');

┌─────────────────────────────────────────────────┐
│ to_unix_timestamp('2023-11-12 09:38:18.165575') │
├─────────────────────────────────────────────────┤
│                                      1699781898 │
└─────────────────────────────────────────────────┘
```