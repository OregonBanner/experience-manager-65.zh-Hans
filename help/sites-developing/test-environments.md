---
title: 需要哪些测试环境？
description: 测试时应考虑多个环境
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
exl-id: 05f7a513-5ee7-4870-a691-4a0602e0cbb2
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# 需要哪些测试环境？{#which-test-environments-will-be-needed}

要定义哪些配置用于测试，应考虑以下事项：

**开发**  — 用于单元和某些集成测试。

**测试**  — 对于大多数测试。

**实时**  — 进行最终性能和压力测试。 此外，还要与客户进行验收测试。

确定您需要哪些实例以及在何处进行（通常对于所有级别的测试，每个实例至少一个）：

**作者**  — 此实例允许作者输入和发布内容。

**Publish**  — 此实例以发布的形式展示网站，以供访客访问。

已通过Dispatcher进行测试。

最后，必须考虑实际的硬件 — 任何性能测试都应在尽可能接近最终实时环境的配置下在系统上进行。 因此，还建议将项目启动拆分为：

**软启动**  — 降低了可用性；允许在生产环境的实际条件下进行性能测试、调整和优化。

**硬启动**  — 完全可用。
