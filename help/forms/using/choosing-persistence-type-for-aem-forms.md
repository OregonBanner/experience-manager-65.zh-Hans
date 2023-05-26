---
title: 为AEM Forms安装选择持久性类型
seo-title: Choosing a persistence type for an AEM Forms installation
description: 明智地选择持久性类型。 它可帮助您构建高效且可扩展的AEM Forms环境。
seo-description: Choose a persistence type wisely. It helps you build an efficient and scale able AEM Forms environment.
uuid: 1c692502-5039-4757-9358-1772772b3904
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: a972fb35-38a7-4b83-99bd-6a6dddf8043b
role: Admin
exl-id: 621fe107-f4ac-42b1-8c7b-8abbcaac7380
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 1%

---

# 为AEM Forms安装选择持久性类型 {#choosing-a-persistence-type-for-an-aem-forms-installation}

明智地选择持久性类型。 它可帮助您构建高效且可扩展的AEM Forms环境。

持久性是在物理存储上存储内容的方法。 它定义了实际的数据结构和数据的存储机制。 MicroKernels在AEM Forms中充当持久性管理器。 AEM Forms支持TarMK、MongoMK和RDBMK类型的持久性（微内核）。 您可以根据AEM Forms实例的用途和部署类型（单服务器、场或集群），为AEM Forms选择持久性类型。

>[!NOTE]
>
>LiveCycleES4 SP1使用TarPM持久性存储内容。

下表列出了所有支持的持久性类型以及各种参数，可帮助您为环境选择持久性类型：

<table>
 <tbody>
  <tr>
   <th><strong>安装类型/成本</strong></th>
   <th><strong>TarMK</strong></th>
   <th><strong>MongoMk</strong></th>
   <th><strong>RDBMK</strong></th>
  </tr>
  <tr>
   <th><strong>独立设置</strong></th>
   <td>支持<br /> </td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <th><strong>群集设置</strong></th>
   <td>不支持</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <th><strong>许可证成本</strong></th>
   <td>包含在AEM中 </td>
   <td>需要单独的许可证</td>
   <td>需要单独的许可证</td>
  </tr>
 </tbody>
</table>

TarMK旨在提高性能，而MongoMK和RDBMK旨在实现可扩展性。 Adobe强烈建议将TarMK作为所有AEM Forms部署方案（创作实例和发布实例）的默认持久性技术，但一节中概述的用例除外 [在TarMK上选择Mongo或关系数据库微内核](#p-choosing-mongo-or-a-relational-database-microkernel-over-tarmk-p).

有关受支持的微内核列表，请参见 [AEM Forms on OSGi技术要求](/help/sites-deploying/technical-requirements.md) 或 [AEM Forms on JEE支持的平台组合](/help/forms/using/aem-forms-jee-supported-platforms.md) 文章。

## 在TarMK上选择Mongo或关系数据库微内核 {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk}

可扩展（集群）AEM Forms环境是由两个或多个水平配置的活动创作实例组成的集合。 如果支持所有并发创作活动的单个服务器不再可持续，则可以选择运行多个创作实例。

JEE环境上的可扩展（集群）AEM Forms仅支持MongoMK和RDBMK持久性类型。 服务器的数量或可扩展环境的大小因每次安装而异。 有关注意事项和示例的列表，请参阅 [建议的部署](/help/sites-deploying/recommended-deploys.md) 和/或 [AEM Forms的架构和部署拓扑](/help/forms/using/aem-forms-architecture-deployment.md) 文章。 您还可以联系AEM Forms支持，以获取有关使用RDBMK和TarMK的AEM Forms容量规划的详细信息。
