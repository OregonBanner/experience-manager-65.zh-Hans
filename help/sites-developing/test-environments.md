---
title: 需要哪些测试环境？
seo-title: 需要哪些测试环境？
description: 应将多个环境视为测试的一部分
seo-description: 应将多个环境视为测试的一部分
uuid: bb725e50-edae-4c20-8107-d1c8df2e60e2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: db528b9b-3407-462d-8254-20b3cc2c3ccf
exl-id: 05f7a513-5ee7-4870-a691-4a0602e0cbb2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# 需要哪些测试环境？{#which-test-environments-will-be-needed}

要定义测试的配置，您应考虑以下事项：

**开发**  — 针对设备和某些集成测试。

**测试**  — 适用于大多数测试。

**实时**  — 用于最终性能和压力测试。也用于与客户进行验收测试。

您还需要确定在什么位置需要哪些实例（通常在所有测试级别中每个实例至少需要一个）：

**作者**  — 此实例允许作者输入和发布内容。

**发布**  — 此实例以其发布的形式显示网站，以供访客访问。

应与Dispatcher一起测试。

最后，必须考虑实际硬件 — 在配置尽可能接近最终实时环境的系统上进行任何性能测试。 因此，还建议将项目启动项拆分为：

**软启动**  — 降低可用性；这样，就可以在生产环境中的实际条件下进行性能测试、调整和优化。

**硬启动**  — 完全可用。
