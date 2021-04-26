---
title: AEM - Commerce Integration using Commerce Integration Framework常见问题解答
description: AEM - Commerce Integration using Commerce Integration Framework常见问题解答
exl-id: 0a946d98-22c7-445d-984a-9e09c306ce45,aece1190-9530-4060-9b08-022da7068987
translation-type: tm+mt
source-git-commit: d92a635d41cf1b14e109c316bd7264cf7d45a9fe
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---

# AEM - Commerce Integration using Commerce Integration Framework常见问题解答

## 1. CIF GraphQL是否仅用于商务，或者它是否可用于查询在AEM. JCR上创作的内容？

Adobe已采用Magento的GraphQL API作为其所有商务相关数据的官方商务API。 因此，AEM使用GraphQL与Magento以及通过I/O Runtime与任何商务引擎交换商务数据。 此GraphQL API独立于AEM GraphQL API以访问内容片段。

## 2.产品资产（图像）是否可以通过Adobe Commerce(Magento)admin从AEM存储和引用？ 如何使用Dynamic Media中的资产？

没有正式的AEM Assets -Magento集成可用。 [marketplace](https://marketplace.magento.com/bounteous-dam.html)上有一个可用的合作伙伴连接器。

或者，您也可以将产品资产（图像）存储在AEM Assets中，但您必须在Magento中手动存储资产URL。 Dynamic Media现在是AEM Assets的一部分，将以同样的方式工作。

## 3.商务解决方案部署在何处是否重要？ （在云中或在云中）

不，商务解决方案的部署位置并不重要。 CIF和AEM店无论部署模式如何，都能正常工作。 但是，如果将解决方案与建议的E2E参考体系结构一起部署，则E2E测试可以针对代表典型企业客户用户档案的性能KPI运行。 这将提供可用作基准的其他信息。

## 4.如何在AEM中创建目录页面或产品页面？ 他们如何在AEM中坚持？

目录页面和产品页面是根据通用目录和产品页面模板在AEM中动态创建和缓存的。 没有产品或目录数据导入并存储在AEM中。

## 5.在您的商务解决方案中更新产品数据时，这是否是实时推送到AEM? 还是说，这是批量流程？

与AEM一起使用的CIF加载项使数据能够从商务解决方案流到AEM点播。 因此，当您的商务解决方案中存在更新时，这不是实时推送或批处理。

## 6.AEM支持哪些目录大小？

这取决于您需要考虑的其他几个方面。 目录数据和页面的缓存比率是多少？ 在高峰时段，您预计有多少个并发请求？ 您的商务解决方案的API有多大的可扩展性？

## 7. PIM如何融入这个框架？

PIM数据通过GraphQL请求暴露给AEM和客户端。 我们的推荐是将PIM与商务引擎(Magento或其他)集成，以便PIM数据随后可从商务引擎中检索。

## 8.您是否也通过Dispatcher缓存定价和其他数据。 这是否会引发频繁的缓存失效挑战？

不会在调度程序上缓存价格或库存等动态数据。 动态数据通过GraphQL API直接通过Web组件在客户端获取。 只有静态数据(如产品或类别数据)才会缓存在Dispatcher上。 如果产品数据发生更改，则需要缓存失效。

## 9. AEM Dispatcher的缓存失效如何与AEM和商务一起使用？

我们建议为在调度程序上缓存的页面设置基于TTL的缓存失效。 对于价格或库存等动态信息，我们建议呈现日期客户端。 有关基于TTL的缓存失效的详细信息，请参阅[AEM Dispatcher](https://helpx.adobe.com/experience-manager/kb/optimizing-the-dispatcher-cache.html)

## 10.是否建议使用商务跨AEM内容进行统一搜索？

提供了产品搜索参考实施，但没有对内容进行统一搜索。 此功能通常非常针对客户，并且在项目特定级别得到更好的解决。

## 11.搜索如何使用CIF与AEM和商务协作？

CIF提供搜索栏和搜索结果组件。 搜索栏组件会向商务解决方案发送包含搜索词的GraphQL请求，该解决方案随后会返回包含产品名称、价格、辅助信息域等的产品列表。 然后，搜索结果组件会在AEM中创建的搜索结果页面的库视图中显示搜索结果。 “搜索”支持基本的全文搜索。 我们使用SLUG/url键来构建对PDP的引用。

## 12.如何在MSM或翻译中使用产品数据？

产品数据通常已在PIM或Magento中翻译。 AEM - Magento集成支持连接到多个Magento商店和商店视图。 在MSM设置中，通常有一个AEM站点链接到一个Magento存储视图。

## 13.是否有办法用商业文本增强产品数据？ 你从哪儿做的？ 在AEM中还是在商务解决方案中？

我们建议在AEM中管理与营销相关的数据和内容。 使用内容片段的其他属性装饰您的商务解决方案中的产品数据，或为不结构化的内容创建体验片段并将其与您的产品链接。

## 14.如何确保整个表示层使用AEM时的PCI兼容性？

建议采用抽象的支付方式。 这使得浏览器客户端与支付网关提供商直接通信，以便Adobe或商务解决方案都不持有或传递持卡人数据。 此方法只需要3级PCI兼容性。 但是，还有其他一些事项需要考虑完全符合PCI规范，例如员工如何与系统和数据交互。 有关MagentoPCI兼容性的详细信息，请参阅<https://magento.com/pci-compliance>

## 15.如果我使用AEM和Magento云版本，此联合解决方案是否符合PCI标准？

是，可应要求提供自我评估调查表D和合规性证明。

## 16.如何申请I/O Runtime试用许可？

您可以在此处](https://adobeio.typeform.com/to/obqgRm)申请试用许可证以使用I/O Runtime [。
