---
title: XXHASH32
---

计算字符串的 xxHash32 32 位哈希值。返回值为 UInt32 类型，如果参数为 NULL，则返回 NULL。

## 语法

```sql
XXHASH32(expr)
```

## 示例

```sql
SELECT XXHASH32('1234567890');

┌────────────────────────┐
│ xxhash32('1234567890') │
├────────────────────────┤
│             3896585587 │
└────────────────────────┘
```