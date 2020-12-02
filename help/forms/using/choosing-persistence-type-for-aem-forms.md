---
title: 为AEM Forms安装选择持久性类型
seo-title: 为AEM Forms安装选择持久性类型
description: 明智地选择持久性类型。 它可以帮助您构建一个高效、可扩展的AEM Forms环境。
seo-description: 明智地选择持久性类型。 它可以帮助您构建一个高效、可扩展的AEM Forms环境。
uuid: 1c692502-5039-4757-9358-1772772b3904
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: a972fb35-38a7-4b83-99bd-6a6dddf8043b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 1%

---


# 为AEM Forms安装选择持久性类型{#choosing-a-persistence-type-for-an-aem-forms-installation}

明智地选择持久性类型。 它可以帮助您构建一个高效、可扩展的AEM Forms环境。

持久性是在物理存储上存储内容的方法。 它定义了数据的实际数据结构和存储机制。 MicroKernel在AEM Forms充当持久性管理器。 AEM Forms支持TarMK、MongoMK和RDBMK类型的持久性(MicroKernals)。 您可以根据AEM Forms实例的用途和部署类型（单服务器、场或群集）为AEM Forms选择持久性类型。

>[!NOTE]
>
>LiveCycleES4 SP1使用TarPM持久性存储内容。

下表列表了所有支持的持久性类型以及各种参数，以帮助您为环境选择持久性类型：

<table>
 <tbody>
  <tr>
   <th><strong>安装类型／成本</strong></th>
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
   <th><strong>许可费用</strong></th>
   <td>随AEM提供 </td>
   <td>需要单独的许可证</td>
   <td>需要单独的许可证</td>
  </tr>
 </tbody>
</table>

TarMK设计为性能，而MongoMK和RDBMK设计为可伸缩性。 Adobe强烈建议将TarMK作为所有AEM Forms部署方案（对于作者实例和Publish实例）的默认持久性技术，但在[选择Mongo或关系数据库微内核（对于TarMK](#p-choosing-mongo-or-a-relational-database-microkernel-over-tarmk-p)）一节中概述的使用案例除外。

有关受支持微内核的列表，请参见OSGi技术要求](/help/sites-deploying/technical-requirements.md)上的[AEM Forms或JEE支持的平台组合](/help/forms/using/aem-forms-jee-supported-platforms.md)文章上的[AEM Forms。

## 选择Mongo或关系数据库微内核，而不是TarMK {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk}

可缩放（群集）AEM Forms环境是由两个或多个水平配置的活动作者实例组成的集。 如果支持所有并发创作活动的单个服务器不再可持续，则可以选择运行多个作者实例。

JEE环境上的可伸缩（群集）AEM Forms仅支持MongoMK和RDBMK持久性类型。 每个安装的服务器数或可扩展环境的大小都不同。 有关注意事项和示例的列表，请参阅[推荐部署](/help/sites-deploying/recommended-deploys.md)和[AEM Forms的架构和部署拓扑文章](/help/forms/using/aem-forms-architecture-deployment.md)。 您还可以联系AEM Forms支持部门，了解有关使用RDBMK和TarMK为AEM Forms进行容量规划的详细信息。
