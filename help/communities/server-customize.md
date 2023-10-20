---
title: 服务器端自定义
description: 了解如何在Adobe Experience Manager Communities中进行服务器端自定义。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 190735bc-1909-4b92-ba4f-a221c0cd5be7
source-git-commit: f03d0ab9d0f491441378e16e1590d33651f064b5
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---

# 服务器端自定义 {#server-side-customization}

| **[⇐功能要点](essentials.md)** | **[客户端自定义⇒](client-customize.md)** |
|---|---|
|   | **[SCF Handlebars Helpers ⇒](handlebars-helpers.md)** |

## Java™ API {#java-apis}

>[!NOTE]
>
>从一个主要版本升级到下一个主要版本时，Communities API的包位置可能会发生更改。

### 社交组件界面 {#socialcomponent-interface}

SocialComponents是POJO，表示AEM Communities功能的资源。 理想情况下，每个SocialComponent都表示一个特定的resourceType，其中包含公开的GETter，用于向客户端提供数据，以便准确表示资源。 所有业务和视图逻辑都封装在SocialComponent中，包括站点访客的会话信息（如有必要）。

该接口定义了表示资源所必需的一组GETter。 重要的是，界面中指定了&lt;string object=&quot;&quot;> getAsMap()和String toJSONString()方法，它们是呈现Handlebars模板和公开资源的GETJSON端点所必需的。

所有SocialComponent类都必须实现接口 `com.adobe.cq.social.scf.SocialComponent`

### SocialCollectionComponent接口 {#socialcollectioncomponent-interface}

SocialCollectionComponent接口扩展了SocialComponent接口，以更好地表示作为其他资源集合的资源。

所有SocialCollectionComponent类都必须实现接口com.adobe.cq.social.scf.SocialCollectionComponent

### SocialComponentFactory接口 {#socialcomponentfactory-interface}

SocialComponentFactory（工厂）向框架注册SocialComponent。 工厂提供了一种方法，让框架知道对于给定的resourceType有哪些SocialComponents可用，以及在标识了多个SocialComponents时它们的优先级排名。

SocialComponentFactory负责创建所选SocialComponent的实例，以便能够使用DI实践从工厂注入SocialComponent所需的所有依赖项。

SocialComponentFactory是一种OSGi服务，有权访问可通过构造函数传递给SocialComponent的其他OSGi服务。

所有SocialComponentFactory类都必须实现接口 `com.adobe.cq.social.scf.SocialComponentFactory`

SocialComponentFactory.getPriority()方法的实现应返回由getResourceType()返回的用于给定resourceType的工厂的最大值。

### SocialComponentFactoryManager接口 {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager（管理器）管理在框架中注册的所有SocialComponents，并负责选择要用于给定资源(resourceType)的SocialComponentFactory。 如果没有为特定的resourceType注册工厂，则经理将返回给定资源具有最接近超级类型的工厂。

SocialComponentFactoryManager是一种OSGi服务，具有其他OSGi服务的访问权限，这些服务可以通过构造函数传递给SocialComponent。

通过调用OSGi服务的句柄 `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### HTTP API -POST请求 {#http-api-post-requests}

#### Postoperation类 {#postoperation-class}

HTTP APIPOST端点是通过实现 `SlingPostOperation` 界面（包） `org.apache.sling.servlets.post`)。

此 `PostOperation` 端点实施集 `sling.post.operation` 操作响应的值。 所有将：operation参数设置为该值的POST请求都委托给此实现类。

此 `PostOperation` 调用 `SocialOperation` 执行操作所需的操作。

此 `PostOperation` 接收来自 `SocialOperation` 并将相应的响应返回给客户端。

#### SocialOperation类 {#socialoperation-class}

每个 `SocialOperation` 端点扩展AbstractSocialOperation类并覆盖方法 `performOperation()`. 此方法执行完成操作所需的所有操作并返回 `SocialOperationResult` 或者抛出 `OperationException`. 在这种情况下，会返回带有消息的HTTP错误状态（如果可用），以代替常规JSON响应或成功HTTP状态代码。

扩展 `AbstractSocialOperation` 使得重复使用 `SocialComponents` 以发送JSON响应。

#### SocialOperationResult类 {#socialoperationresult-class}

此 `SocialOperationResult` 类作为 `SocialOperation` 并且由 `SocialComponent`、HTTP状态代码和HTTP状态消息。

此 `SocialComponent` 表示受该操作影响的资源。

对于“创建”操作， `SocialComponent` 包含在 `SocialOperationResult` 表示创建的资源，对于“更新”操作，它表示该操作更改的资源。 否 `SocialComponent` 为删除操作返回。

使用的成功HTTP状态代码包括：

* 201用于创建操作
* 200表示更新操作
* 204用于删除操作

#### Operationexception类 {#operationexception-class}

An `OperationExcepton` 如果请求无效或发生其他错误，则执行操作时会引发。 例如，内部错误、参数值错误或权限错误。 An `OperationException` 由HTTP状态代码和错误消息组成，这些代码和消息将作为对 `PostOperatoin`.

#### 操作服务类 {#operationservice-class}

社交组件框架建议不要在内实施负责执行操作的业务逻辑 `SocialOperation` 类，而是委派给OSGi服务。 将OSGi服务用于业务逻辑允许 `SocialComponent`，由 `SocialOperation` 端点，与其他代码集成并应用不同的业务逻辑。

全部 `OperationService` 类扩展 `AbstractOperationService`，允许附加的扩展挂接到正在执行的操作。 服务中的每项操作均由 `SocialOperation` 类。 此 `OperationExtensions` 可以通过调用方法在执行操作期间调用类

* `performBeforeActions()`

  允许预先检查/预处理和验证
* `performAfterActions()`

  允许进一步编辑资源或调用自定义事件、工作流等。

#### Operationextension类 {#operationextension-class}

此 `OperationExtension` 类是可插入到操作的自定义代码段，允许根据业务需求自定义操作。 组件的使用者可以动态和增量地向组件添加功能。 扩展/挂接模式允许开发人员专门关注扩展本身，并且消除复制和覆盖整个操作和组件的需要。

## 示例代码 {#sample-code}

示例代码位于 [Adobe Experience Cloud GitHub](https://github.com/Adobe-Marketing-Cloud) 存储库。 搜索带有以下前缀的项目： `aem-communities` 或 `aem-scf`.

## 最佳实践 {#best-practices}

查看 [编码准则](code-guide.md) 部分，了解面向AEM Communities开发人员的各种编码准则和最佳实践。

另请参阅 [适用于UGC的存储资源提供程序(SRP)](srp.md) 了解有关访问用户生成的内容的信息。

| **[⇐功能要点](essentials.md)** | **[客户端自定义⇒](client-customize.md)** |
|---|---|
|   | **[SCF Handlebars Helpers ⇒](handlebars-helpers.md)** |
