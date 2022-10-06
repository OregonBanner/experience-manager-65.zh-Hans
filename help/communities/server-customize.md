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

| **[⇐功能要点](essentials.md)** | **[客户端自定义⇒](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers ⇒](handlebars-helpers.md)** |

## Java API {#java-apis}

>[!NOTE]
>
>从一个主要版本升级到下一个版本时，Communities API的包位置可能会发生更改。

### SocialComponent界面 {#socialcomponent-interface}

SocialComponents是POJO，表示AEM Communities功能的资源。 理想情况下，每个SocialComponent都表示一个具有公开GETter的特定resourceType，该GETter向客户端提供数据，以便准确表示资源。 所有业务逻辑和视图逻辑都封装在SocialComponent中，包括网站访客的会话信息（如有必要）。

该界面定义了表示资源所需的一组基本GETter。 重要的是，界面规定了&lt;string object=&quot;&quot;> getAsMap()和String toJSONString()方法，这是渲染Handlebars模板和为资源公开GETJSON端点所必需的。

所有SocialComponent类必须实现该接口 `com.adobe.cq.social.scf.SocialComponent`

### SocialCollectionComponent界面 {#socialcollectioncomponent-interface}

SocialCollectionComponent界面扩展了SocialComponent界面，以更好地表示其他资源集合的资源。

所有SocialCollectionComponent类必须实现接口com.adobe.cq.social.scf.SocialCollectionComponent

### SocialComponentFactory界面 {#socialcomponentfactory-interface}

SocialComponentFactory（工厂）在框架中注册SocialComponent。 工厂提供了一种方法，让框架知道哪些SocialComponent可用于给定的resourceType，以及在确定多个SocialComponent时它们的优先级排名。

SocialComponentFactory负责创建所选SocialComponent的实例，以便能够使用DI惯例从工厂中注入SocialComponent所需的所有依赖项。

SocialComponentFactory是OSGi服务，可以访问其他OSGi服务，这些服务可以通过构造函数传递到SocialComponent。

所有SocialComponentFactory类必须实施该接口 `com.adobe.cq.social.scf.SocialComponentFactory`

SocialComponentFactory.getPriority()方法的实现应返回最高值，以便工厂用于getResourceType()返回的给定resourceType。

### SocialComponentFactoryManager界面 {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager（经理）管理在框架中注册的所有SocialComponents，并负责选择SocialComponentFactory以用于给定资源(resourceType)。 如果没有为特定resourceType注册工厂，则管理器将返回具有给定资源最接近超级类型的工厂。

SocialComponentFactoryManager是OSGi服务，可以访问其他OSGi服务，这些服务可以通过构造函数传递到SocialComponent。

通过调用获取对OSGi服务的句柄 `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### HTTP API -POST请求 {#http-api-post-requests}

#### 操作后类 {#postoperation-class}

HTTP APIPOST端点是通过实施 `SlingPostOperation` 界面（包） `org.apache.sling.servlets.post`)。

的 `PostOperation` endpont实施集 `sling.post.operation` 到操作将响应的值。 将an:operation参数设置为该值的所有POST请求都将委派给此实现类。

的 `PostOperation` 调用 `SocialOperation` 执行操作所需的操作。

的 `PostOperation` 从 `SocialOperation` 和会向客户端返回相应的响应。

#### SocialOperation类 {#socialoperation-class}

每个 `SocialOperation` 端点扩展AbstractSocialOperation类并覆盖方法 `performOperation()`. 此方法将执行完成操作所需的所有操作并返回 `SocialOperationResult` 否则 `OperationException`，在这种情况下，会返回带有消息的HTTP错误状态（如果可用），而不是正常的JSON响应或成功的HTTP状态代码。

扩展 `AbstractSocialOperation` 使得 `SocialComponents` 以发送JSON响应。

#### SocialOperationResult类 {#socialoperationresult-class}

的 `SocialOperationResult` 类作为 `SocialOperation` 由 `SocialComponent`、 HTTP状态代码和HTTP状态消息。

的 `SocialComponent` 表示受操作影响的资源。

对于创建操作， `SocialComponent` 包含在 `SocialOperationResult` 表示刚刚创建的资源，并表示更新操作更改的资源。 否 `SocialComponent` 为删除操作返回。

使用的成功HTTP状态代码包括：

* 201，用于创建操作
* 200 for Update operations
* 204 for Delete操作

#### 操作例外类 {#operationexception-class}

安 `OperationExcepton` 如果请求无效或发生其他错误（如内部错误、参数值错误、权限不当等），则在执行操作时可能会引发。 安 `OperationException` 由HTTP状态代码和错误消息组成，该消息将作为对 `PostOperatoin`.

#### 操作服务类 {#operationservice-class}

社交组件框架建议，不要在 `SocialOperation` 类，而是委派给OSGi服务。 对业务逻辑使用OSGi服务允许 `SocialComponent`，由 `SocialOperation` 端点，与其他代码集成，并应用不同的业务逻辑。

全部 `OperationService` 类扩展 `AbstractOperationService`，允许可挂接到正在执行的操作的其他扩展。 服务中的每个操作由 `SocialOperation` 类。 的 `OperationExtensions` 在操作执行期间，可通过调用方法来调用类

* `performBeforeActions()`

   允许进行预检查/预处理和验证
* `performAfterActions()`

   允许进一步修改资源或调用自定义事件、工作流等

#### OperationExtension类 {#operationextension-class}

`OperationExtension` 类是自定义的代码段，可以插入到操作中，以允许自定义操作以满足业务需求。 组件的使用者可以动态地和递增地向组件添加功能。 扩展/挂接模式允许开发人员仅专注于扩展本身，而无需复制和覆盖整个操作和组件。

## 示例代码 {#sample-code}

示例代码在 [Adobe Marketing Cloud GitHub](https://github.com/Adobe-Marketing-Cloud) 存储库。 搜索带有以下项的项目 `aem-communities` 或 `aem-scf`.

## 最佳实践 {#best-practices}

查看 [编码准则](code-guide.md) 部分，以了解面向AEM Communities开发人员的各种编码准则和最佳实践。

另请参阅 [UGC的存储资源提供程序(SRP)](srp.md) 以了解如何访问用户生成的内容。

| **[⇐功能要点](essentials.md)** | **[客户端自定义⇒](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers ⇒](handlebars-helpers.md)** |
