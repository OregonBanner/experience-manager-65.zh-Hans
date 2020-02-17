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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 需要哪些测试环境？{#which-test-environments-will-be-needed}

要定义测试的配置，您应考虑以下事项：

**开发** -针对单元和某些集成测试。

**测试** -适用于大多数测试。

**实时** -用于最终性能和压力测试。 还适用于客户的接受测试。

您还需要确定哪些实例需要在以下位置（通常，所有测试级别的每个实例中至少有一个）:

**作者** -此实例允许作者输入和发布内容。

**发布** -此实例以其发布的表单显示网站，供访客访问。

应与调度程序一起测试。

最后，必须考虑实际硬件——在最接近最终实时环境的配置中，在系统上进行任何性能测试。 因此，还建议将项目启动项拆分为：

**软启动** -可用性降低；它允许在生产环境的真实条件下进行性能测试、调整和优化。

**硬启动** -完全可用。
