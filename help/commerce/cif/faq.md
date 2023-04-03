---
title: AEM — 使用商务集成框架的商务集成常见问题解答
description: AEM — 使用商务集成框架的商务集成常见问题解答
exl-id: d541607f-c4c9-4dd5-aadf-64d4cb5f9f2a
source-git-commit: 9defa6d1843007e9375d839f72f6993c691a37c0
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 0%

---

# AEM — 使用商务集成框架的商务集成常见问题解答

## 1. CIF GraphQL是仅用于商务，还是可用于查询在AEM. JCR上创作的内容？

Adobe已采用Adobe Commerce的GraphQL API作为其官方商务API，用于所有与商务相关的数据。 因此，AEM使用GraphQL与Adobe Commerce以及通过I/O运行时与任何商务引擎交换商务数据。 此GraphQL API独立于AEM GraphQL API，可用于访问内容片段。

## 2.能否通过Adobe Commerce管理员从AEM中存储和引用产品资产（图像）？ 如何使用Dynamic Media中的资产？

没有官方的AEM Assets - Adobe Commerce集成可用。 在 [市场](https://marketplace.magento.com/partner/bounteous_ecomm).

或者，作为解决方法，您可以在AEM Assets中存储产品资产（图像），但必须在Adobe Commerce中手动存储资产URL。 Dynamic Media是AEM Assets的一部分，工作方式相同。

## 3.在何处部署商务解决方案是否重要？ （内部或云中）

不，商务解决方案的部署位置并不重要。 CIF和AEM店面无论部署模型如何都能正常工作。 但是，如果该解决方案与建议的E2E参考体系结构一起部署，则E2E测试可能会针对代表典型企业客户配置文件的性能KPI运行。 此过程提供了可用作基准的其他信息。

## 4.如何在AEM中创建目录页面或产品页面？ 它们如何在AEM中持续？

目录页面和产品页面是根据通用目录和产品页面模板在AEM中动态创建和缓存的。 不会在AEM中导入和存储任何产品或目录数据。

## 5.在商务解决方案中更新产品数据时，是否是实时推送到AEM? 还是批量处理？

与AEM一起使用的CIF附加组件允许数据从商务解决方案流向AEM按需。 因此，当您的商务解决方案中存在更新时，此工作流不是实时推送或批量流程。

## 6. CIF支持的AEM目录大小是多少？

目录大小支持取决于您必须考虑的其他几个方面。 目录数据和页面的缓存比率是多少？ 在高峰时段，您预计会有多少个并发请求？ 您的商务解决方案的API有多大的可扩展性？

## 7. PIM在这个框架中如何发挥作用？

PIM数据通过GraphQL请求公开给AEM和客户端。 Adobe的建议是将PIM与商务引擎(Adobe Commerce或其他)集成，以便随后可以从商务引擎中检索PIM数据。

## 8.您是否还通过Dispatcher缓存定价和其他数据。 这是否会经常引发缓存失效问题？

不会在Dispatcher中缓存价格或库存等动态数据。 动态数据是通过Web组件直接通过GraphQL API在客户端获取的。 只有静态数据（如产品或类别数据）会缓存在Dispatcher中。 如果产品数据发生更改，则需要缓存失效。

## 9. AEM Dispatcher的缓存失效如何与AEM和商务一起使用？

Adobe建议为Dispatcher上缓存的页面设置基于TTL的缓存失效。 对于价格或库存等动态信息，Adobe建议渲染客户端日期。 有关基于TTL的缓存失效的更多信息，请参阅 [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17458.html?lang=zh-Hans)

## 10.是否建议使用商务在AEM内容中进行统一搜索？

提供了产品搜索参考实施，但没有对内容进行统一搜索。 此功能是特定于客户的，在特定于项目的级别上得到更好的解决。

## 11.如何使用CIF在AEM和商务中使用搜索？

CIF提供搜索栏和搜索结果组件。 搜索栏组件会向商务解决方案发送包含搜索词的GraphQL请求，该解决方案随后会返回包含产品名称、价格、SLUG等的产品列表。 然后，搜索结果组件在在AEM中创建的搜索结果页面的库视图中显示搜索结果。 搜索支持基本的全文搜索。 使用SLUG/url键构建对PDP的引用。

## 12.如何在MSM或翻译中使用产品数据？

产品数据已在PIM或Adobe Commerce中翻译。 AEM - Adobe Commerce集成支持与多个Adobe Commerce商店和商店视图的连接。 在MSM设置中，通常有一个AEM站点链接到一个Adobe Commerce存储视图。

## 13.是否有办法用商业文本增强产品数据？ 如果是，它在哪里完成？ 在AEM中还是在商务解决方案中？

Adobe建议在AEM中管理与营销相关的数据和内容。 使用使用内容片段的其他属性装饰您的商务解决方案中的产品数据，或创建非结构化内容的体验片段并将其与您的产品关联。

## 14.在整个表示层使用AEM时，公司如何确保PCI合规性？

Adobe建议使用抽象的付款方法。 这样，浏览器客户端便与支付网关提供商直接通信，使Adobe不会持有或通过持卡人日期，也不会通过商务解决方案。 这种方法只需要3级PCI合规性。 但是，还有一些其他事项需要考虑完全符合PCI标准，例如员工如何与系统和数据交互。 有关Adobe Commerce PCI合规性的详细信息，请参阅 [PCI合规性](https://business.adobe.com/products/magento/pci-compliance.html)

## 15.如果我使用AEM和Adobe Commerce云版本，此联合解决方案是否符合PCI标准？

是的，可应要求提供自我评估调查表D和合规性证明。

## 16.如何请求I/O运行时试用许可证？

您可以请求试用许可证以使用I/O运行时 [此处](https://adobeio.typeform.com/to/obqgRm).
