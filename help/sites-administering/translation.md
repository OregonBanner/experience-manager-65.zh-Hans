---
title: 翻译多语言站点的内容
seo-title: 翻译多语言站点的内容
description: 了解如何翻译多语言站点的内容。
seo-description: 了解如何翻译多语言站点的内容。
uuid: 69b3e3a9-6773-4759-8178-aaa612e4c170
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 1e0a68c5-1583-4103-9dbb-7a53faa03c06
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/third-party-services/machine-translation
translation-type: tm+mt
source-git-commit: 8b53e79e3a88f58423e99477db930a4912a1ba09

---


# 翻译多语言站点的内容 {#translating-content-for-multilingual-sites}

自动翻译页面内容、资产和用户生成的内容，以创建和维护多语言网站。 要实现翻译工作流程的自动化，您可以将翻译服务提供商与AEM集成，并创建用于将内容翻译为多种语言的项目。 AEM支持人工和机器翻译工作流程。

* 人文翻译：内容将发送给您的翻译提供商，并由专业翻译人员翻译。 完成后，将返回译文内容并将其导入AEM。 将翻译提供商与AEM集成后，内容会在AEM与翻译提供商之间自动发送。
* 机器翻译：机器翻译服务会立即翻译您的内容。

翻译内容涉及以下步骤：

1. [将AEM与翻译服务提供商连接](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider) ，并 [创建翻译集成框架配置](/help/sites-administering/tc-tic.md)。
1. [将语言主页的页面与翻译服务](/help/sites-administering/tc-tic.md#configuring-pages-for-translation) 和框架配置相关联。
1. [确定要翻译的内容类型](/help/sites-administering/tc-rules.md) 。
1. [通过创作语言母版](/help/sites-administering/tc-prep.md) ，并创建语言副本的根页面，准备要翻译的内容。
1. [创建翻译项目](/help/sites-administering/tc-manage.md) ，以收集要翻译的内容并准备翻译过程。
1. 使用翻译项目管 [理内容翻译流程](/help/sites-administering/tc-manage.md)。

如果您的翻译服务提供商不提供与AEM集成的连接器，则AEM支持以XML格式手动提取和重新插入翻译内容。

>[!NOTE]
>
>您的用户必须是项目管理员组的成员才能使用语言副本功能。

## 最佳实践 {#best-practices}

“翻 [译最佳实践](/help/sites-administering/tc-bp.md) ”页包含有关您的实施的重要信息。
