---
title: "监控 Databend Cloud"
---

Databend Cloud 提供监控功能，帮助您全面了解您和您的组织成员在平台上的使用情况。要访问**监控**页面，请在首页的侧边菜单中点击**监控**。该页面包括以下标签页：

- [指标](#metrics)
- [SQL 历史](#sql-history)
- [审计](#audit)

:::note
**SQL 历史**和**审计**标签页仅对管理员成员可见。
:::

## 指标

**指标**页面展示了图表，直观地说明了以下指标的使用统计数据，覆盖过去一小时、一天或一周的数据：

- 存储大小
- SQL 查询计数
- 会话连接
- 数据扫描/写入
- 仓库状态
- 行扫描/写入

## SQL 历史

**SQL 历史**页面显示了您的组织内所有用户执行的 SQL 语句列表。通过点击列表顶部的**过滤**，您可以按多个维度过滤记录。

在**SQL 历史**页面上点击一条记录，将展示 Databend Cloud 执行 SQL 语句的详细信息，提供以下标签页的访问：

- **查询详情**：包括查询状态（成功或失败）、扫描的行数、仓库、扫描的字节数、开始时间、结束时间和处理器类型。
- **查询概况**：说明了 SQL 语句是如何执行的。更多信息，请参见[了解查询概况](#understand-query-profile)。

### 查询概况

查询概况指的是如何执行特定 SQL 语句的图形表示或视觉分解。它本质上是 [EXPLAIN](/sql/sql-commands/explain-cmds/explain) 命令的图形版本，提供了查询的执行计划和性能细节的见解。

这是一个查询概况的示例，包括一组三个操作节点的层次结构。执行 SQL 语句时，Databend Cloud 按照从下到上的顺序处理这些节点。查询概况包含的操作节点的数量和类型取决于您的 SQL 语句的具体情况。有关常见操作符及其统计字段，请参见[常见操作符和字段](/sql/sql-commands/explain-cmds/explain#common-operators-and-fields)。

![alt text](../../../../public/img/cloud/query-profile-1.png)

*请注意，每个节点标题中的括号数字代表节点 ID，并*不*表示执行步骤。*

查询概况附带一组信息面板，提供更多细节。上面的示例包括两个信息面板：

| 面板                 | 描述                                                                                                                                                                                            |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 最耗时节点 | 列出执行时间最长的节点。                                                                                                                                                      |
| 概况概览     | 显示在 CPU 和 I/O 上花费的时间百分比。请注意，如果您选择了一个节点，这个信息面板将显示您所选择的节点的信息，而不是整个查询的信息。 |

如果您点击 `TableScan [4]` 节点，您会注意到右侧增加了两个额外的信息面板：

![alt text](../../../../public/img/cloud/query-profile-2.png)

| 面板       | 描述                                                                                                                         |
|------------|-------------------------------------------------------------------------------------------------------------------------------------|
| 统计信息 | 包括扫描进度、扫描的字节、从缓存扫描的百分比、扫描的分区等信息。 |
| 属性 | 显示特定于节点的详细信息。显示的字段根据节点的功能而变化。                                |

## 审计

**审计**页面记录了所有组织成员的操作日志，包括操作类型、操作时间、IP 地址和操作者的账户。通过点击列表顶部的**过滤**，您可以按多个维度过滤记录。