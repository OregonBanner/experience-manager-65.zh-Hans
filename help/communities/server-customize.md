---
title: 服务器端自定义
seo-title: Server-side Customization
description: 在AEM Communities中自定义服务器端
seo-description: Customizing server-side in AEM Communities
uuid: 5e9bc6bf-69dc-414c-a4bd-74a104d7bd8f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: df5416ec-5c63-481b-99ed-9e5a91df2432
exl-id: 190735bc-1909-4b92-ba4f-a221c0cd5be7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---

# 服务器端自定义 {#server-side-customization}

| **[⇐ Feature Essentials](essentials.md)** | **[客户端自定义⇒](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers ⇒](handlebars-helpers.md)** |

## Java API {#java-apis}

>[!NOTE]
>
>从一个主要版本升级到下一个主要版本时，Communities API的包位置可能会发生更改。

### SocialComponent界面 {#socialcomponent-interface}

SocialComponents是POJO，表示AEM Communities功能的资源。 理想情况下，每个SocialComponent都表示一个特定的resourceType，其中公开的GETter向客户端提供数据，以便准确表示资源。 所有业务逻辑和视图逻辑都封装在SocialComponent中，包括网站访客的会话信息（如有必要）。

该接口定义了表示资源所需的基本GETter集。 重要的是，界面中指定了&lt;string object=&quot;&quot;> 呈现Handlebars模板和公开资源的GETJSON端点所必需的getAsMap()和String toJSONString()方法。

所有SocialComponent类都必须实现接口 `com.adobe.cq.social.scf.SocialComponent`

### SocialCollectionComponent接口 {#socialcollectioncomponent-interface}

SocialCollectionComponent接口扩展了SocialComponent接口，以更好地表示作为其他资源集合的资源。

所有SocialCollectionComponent类都必须实现接口com.adobe.cq.social.scf.SocialCollectionComponent

### SocialComponentFactory接口 {#socialcomponentfactory-interface}

SocialComponentFactory（工厂）在框架中注册SocialComponent。 工厂提供了一种方法，让框架知道哪些SocialComponents可用于给定resourceType，以及标识多个SocialComponents时它们的优先级等级。

SocialComponentFactory负责创建所选SocialComponent的实例，从而可以使用DI实践从工厂注入SocialComponent所需的所有依赖项。

SocialComponentFactory是一种OSGi服务，有权访问可通过构造函数传递到SocialComponent的其他OSGi服务。

所有SocialComponentFactory类都必须实现接口 `com.adobe.cq.social.scf.SocialComponentFactory`

SocialComponentFactory.getPriority()方法的实现应返回最高值，以便工厂能够用于getResourceType()返回的给定resourceType。

### SocialComponentFactoryManager接口 {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager（经理）管理在框架中注册的所有SocialComponent，并负责选择要用于给定资源(resourceType)的SocialComponentFactory。 如果没有为特定resourceType注册工厂，经理将返回给定资源具有最近超级类型的工厂。

SocialComponentFactoryManager是一种OSGi服务，有权访问可通过构造函数传递到SocialComponent的其他OSGi服务。

通过调用OSGi服务获取句柄 `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### HTTP API -POST请求 {#http-api-post-requests}

#### Postoperation类 {#postoperation-class}

HTTP APIPOST端点是通过实现 `SlingPostOperation` 界面（包） `org.apache.sling.servlets.post`)。

此 `PostOperation` 端点实现集 `sling.post.operation` 操作将响应的值。 所有POST请求的：operation参数均设置为该值，都将委派给此实现类。

此 `PostOperation` 调用 `SocialOperation` 执行操作所需的操作。

此 `PostOperation` 从接收结果 `SocialOperation` 并将相应的响应返回给客户端。

#### SocialOperation类 {#socialoperation-class}

每个 `SocialOperation` 端点扩展AbstractSocialOperation类并覆盖方法 `performOperation()`. 此方法执行完成操作所需的所有操作并返回 `SocialOperationResult` 否则会掷回 `OperationException`在这种情况下，将返回包含消息（如果可用）的HTTP错误状态，以代替常规JSON响应或成功HTTP状态代码。

扩展 `AbstractSocialOperation` 使重复使用 `SocialComponents` 以发送JSON响应。

#### SocialOperationResult类 {#socialoperationresult-class}

此 `SocialOperationResult` 类作为 `SocialOperation` 并且由 `SocialComponent`、HTTP状态代码和HTTP状态消息。

此 `SocialComponent` 表示受该操作影响的资源。

对于“创建”操作， `SocialComponent` 包含在 `SocialOperationResult` 表示刚刚创建的资源，对于“更新”操作，它表示该操作更改的资源。 否 `SocialComponent` 为删除操作返回。

使用的成功HTTP状态代码包括：

* 201用于创建操作
* 200（更新操作）
* 204（删除操作）

#### Operationexception类 {#operationexception-class}

An `OperationExcepton` 如果请求无效或发生其他错误（例如内部错误、参数值错误、权限不正确等），则在执行操作时可能会抛出。 An `OperationException` 由HTTP状态代码和错误消息组成，将作为对 `PostOperatoin`.

#### 操作服务类 {#operationservice-class}

社交组件框架建议不要在内实施负责执行操作的业务逻辑。 `SocialOperation` 类，而是委托给OSGi服务。 将OSGi服务用于业务逻辑允许 `SocialComponent`，由 `SocialOperation` 端点，与其他代码集成并应用不同的业务逻辑。

全部 `OperationService` 类扩展 `AbstractOperationService`，从而允许附加扩展，这些扩展可以挂接到正在执行的操作。 服务中的每个操作都由 `SocialOperation` 类。 此 `OperationExtensions` 可以通过调用方法在执行操作期间调用类

* `performBeforeActions()`

   允许预先检查/预处理和验证
* `performAfterActions()`

   允许进一步修改资源或调用自定义事件、工作流等

#### 操作扩展类 {#operationextension-class}

`OperationExtension` 类是可以插入到操作的自定义代码段，允许根据业务需求自定义操作。 组件的使用者可以动态地增量向组件添加功能。 扩展/挂接模式允许开发人员专门关注扩展本身，并且消除复制和覆盖整个操作和组件的需要。

## 示例代码 {#sample-code}

示例代码位于 [Adobe Marketing Cloud GitHub](https://github.com/Adobe-Marketing-Cloud) 存储库。 搜索带有以下前缀的项目： `aem-communities` 或 `aem-scf`.

## 最佳实践 {#best-practices}

查看 [编码准则](code-guide.md) 部分，了解面向AEM Communities开发人员的各种编码准则和最佳实践。

另请参阅 [适用于UGC的存储资源提供程序(SRP)](srp.md) 了解有关访问用户生成的内容的信息。

| **[⇐ Feature Essentials](essentials.md)** | **[客户端自定义⇒](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers ⇒](handlebars-helpers.md)** |
