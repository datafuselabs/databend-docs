---
title: Airbyte
---

<p align="center">
<img src="/img/integration/integration-airbyte.png"/>
</p>

## [Airbyte](https://airbyte.com/)是什么？

- Airbyte 是一个开源的数据集成平台，能够从应用程序、API 和数据库同步数据到数据仓库、湖和数据库。
- 您可以从任何 Airbyte 源加载数据到 Databend。

目前我们实现了一个实验性的 Airbyte 目的地，允许您将数据从您的 Airbyte 源发送到 Databend

**注意**

目前我们只实现了`append`模式，这意味着目的地将只会向表中追加数据，并不会覆盖、更新或删除任何数据。
另外，我们假设您的 Databend 目的地是**S3 兼容的**，因为我们使用预签名来从 Databend Stage 复制数据到表。

要检查您的后端是否支持集成，您可以简单地运行以下命令

```sql
CREATE STAGE IF NOT EXISTS airbyte_stage FILE_FORMAT = (TYPE = CSV);
PRESIGN UPLOAD @airbyte_stage/test.csv;
```

如果您收到了像`Code: 501, Text = Presign is not supported`这样的错误，那么您就不能使用这个集成。
请阅读[此文档](../../10-deploy/01-deploy/01-non-production/00-deploying-local.md)了解如何使用 S3 作为存储后端。

## 创建一个 Databend 用户

使用 MySQL 客户端连接到 Databend 服务器：

```shell
mysql -h127.0.0.1 -uroot -P3307
```

创建一个用户：

```sql
CREATE USER user1 IDENTIFIED BY 'abc123';
```

创建一个数据库：

```sql
CREATE DATABASE airbyte;
```

为用户授予权限：

```sql
GRANT ALL PRIVILEGES ON airbyte.* TO user1;
```

## 配置 Airbyte

要将 Databend 与 Airbyte 一起使用，您应该将我们的自定义连接器添加到您的 Airbyte 实例中。
您可以在设置 -> 目的地 -> 自定义目的地 -> 添加自定义目的地页面中添加目的地。
我们的自定义目的地镜像是`datafuselabs/destination-databend:alpha`

<p align="center">
<img src="/img/integration/integration-airbyte-plugins.png"/>
</p>

## 设置 Databend 目的地

**注意**

您应该有一个正在运行且可以从您的 Airbyte 实例访问的 Databend 实例。
对于本地 Airbyte，您不能将 docker compose 与您的 localhost 网络连接。
您可以看看[ngrok](https://ngrok.com/)来隧道您的服务（**永远不要**在您的生产环境中暴露它）。

<p align="center">
<img src="/img/integration/integration-airbyte-destinations.png"/>
</p>

## 测试您的集成

您可以使用 Faker 源来测试您的集成，在同步完成后，您可以运行以下命令来查看预期的上传数据。

```sql
select * from default._airbyte_raw_users limit 5;
```
