---
title: HUMANIZE_NUMBER
---

返回一个可读的数字。

## 语法

```sql
HUMANIZE_NUMBER(x);
```

## 参数

| 参数      | 描述                |
|-----------|---------------------|
| x         | 数值大小。           |


## 返回类型

字符串。

## 示例

```sql
SELECT HUMANIZE_NUMBER(1000 * 1000)
+-------------------------+
| HUMANIZE_NUMBER((1000 * 1000)) |
+-------------------------+
| 1 million               |
+-------------------------+
```