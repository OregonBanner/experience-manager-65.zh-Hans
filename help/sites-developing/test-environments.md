---
title: 需要哪些测试环境？
seo-title: Which Test Environments are needed?
description: 应将多个环境视为测试的一部分
seo-description: Several environments should be considered as part of testing
uuid: bb725e50-edae-4c20-8107-d1c8df2e60e2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: db528b9b-3407-462d-8254-20b3cc2c3ccf
exl-id: 05f7a513-5ee7-4870-a691-4a0602e0cbb2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# 需要哪些测试环境？{#which-test-environments-will-be-needed}

要定义用于测试的配置，应考虑以下事项：

**开发**  — 用于单元和某些集成测试。

**测试**  — 进行大多数测试。

**实时**  — 进行最终性能和压力测试。 此外，还要与客户进行验收测试。

您还需要确定在何处需要哪些实例（通常每个实例至少有一个用于所有级别的测试）：

**作者**  — 此实例允许作者输入和发布内容。

**Publish**  — 此实例以发布的形式显示网站，以供访客访问。

应结合Dispatcher进行测试。

最后，必须考虑实际的硬件 — 任何性能测试都应在尽可能接近最终实时环境的配置下进行。 因此，还建议将项目启动拆分为：

**软启动**  — 降低了可用性；允许在生产环境中的实际条件下进行性能测试、调整和优化。

**硬启动**  — 完全可用。
