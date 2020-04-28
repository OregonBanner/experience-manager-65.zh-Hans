---
title: 服务器端自定义
seo-title: 服务器端自定义
description: 在AEM Communities中自定义服务器端
seo-description: 在AEM Communities中自定义服务器端
uuid: 5e9bc6bf-69dc-414c-a4bd-74a104d7bd8f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: df5416ec-5c63-481b-99ed-9e5a91df2432
translation-type: tm+mt
source-git-commit: 6d425dcec4fab19243be9acb41c25b531a84ea74

---


# 服务器端自定义 {#server-side-customization}

| **[‹功能基本工具](essentials.md)** | **[客户端自定义‡](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers‡](handlebars-helpers.md)** |

## Java API {#java-apis}

>[!NOTE]
>
>从一个主要版本升级到下一个版本时，Communities API的包位置可能会发生更改。


### 社交组件界面 {#socialcomponent-interface}

SocialComponents是POJO，它代表AEM Communities功能的资源。 理想情况下，每个SocialComponent都表示具有公开的GETter的特定resourceType，这些GETter向客户端提供数据，从而准确地表示资源。 所有业务逻辑和视图逻辑都封装在SocialComponent中，如有必要，包括站点访客的会话信息。

该接口定义表示资源所必需的一组基本GETter。 重要的是，该接口规定了Map&lt;String, Object> getAsMap()和String toJSONString()方法，这是渲染Handlebars模板和为资源公开GET JSON端点所必需的。

所有SocialComponent类必须实现该接口 `com.adobe.cq.social.scf.SocialComponent`

### SocialCollection组件界面 {#socialcollectioncomponent-interface}

SocialCollectionComponent界面扩展了SocialComponent界面，以更好地表示作为其他资源集合的资源。

所有SocialCollectionComponent类必须实现接口com.adobe.cq.social.scf.SocialCollectionComponent

### SocialComponentFactory界面 {#socialcomponentfactory-interface}

SocialComponentFactory（工厂）在框架中注册SocialComponent。 工厂提供了一种方法，使框架知道在识别多个SocialComponents时，哪些SocialComponents可用于给定的resourceType及其优先级。

SocialComponentFactory负责创建选定SocialComponent的实例，这样，就可以使用DI惯例从工厂中注入SocialComponent所需的所有依赖项。

SocialComponentFactory是OSGi服务，它可以访问其他OSGi服务，这些服务可以通过构造函数传递到SocialComponent。

所有SocialComponentFactory类必须实现该接口 `com.adobe.cq.social.scf.SocialComponentFactory`

SocialComponentFactory.getPriority()方法的实现应返回最高值，以使工厂用于getResourceType()返回的给定resourceType。

### SocialComponentFactoryManager界面 {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager（管理器）管理在框架中注册的所有SocialComponents，并负责选择SocialComponentFactory以用于给定资源(resourceType)。 如果没有为特定resourceType注册工厂，则经理将返回给定资源具有最接近的超类型的工厂。

SocialComponentFactoryManager是OSGi服务，可访问其他OSGi服务，这些服务可以通过构造函数传递到SocialComponent。

通过调用获得对OSGi服务的处理 `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### HTTP API - POST请求 {#http-api-post-requests}

#### PostOperation类 {#postoperation-class}

HTTP API POST端点是通过实现接口（包）定义的 `SlingPostOperation` PostOperation `org.apache.sling.servlets.post`类。

端 `PostOperation` 点实现将设 `sling.post.operation` 置为操作将响应的值。 将an:operation参数设置为该值的所有POST请求都将被委派给此实现类。

调用 `PostOperation` 执行 `SocialOperation` 操作所需操作的操作。

从 `PostOperation` 客户端接收结果并 `SocialOperation` 将相应的响应返回给客户端。

#### SocialOperation类 {#socialoperation-class}

每个 `SocialOperation` 端点都扩展AbstractSocialOperation类并覆盖该方法 `performOperation()`。 此方法执行完成操作所需的所有操作并返回或抛出 `SocialOperationResult``OperationException`，在这种情况下，将返回包含消息的HTTP错误状态（如果可用），代替正常的JSON响应或成功的HTTP状态代码。

扩展 `AbstractSocialOperation` 使得可以重复使用 `SocialComponents` 来发送JSON响应。

#### SocialOperationResult类 {#socialoperationresult-class}

类 `SocialOperationResult` 作为返回的结果返回， `SocialOperation` 它由HTTP状态 `SocialComponent`代码和HTTP状态消息组成。

表示 `SocialComponent` 受操作影响的资源。

对于创建操作， `SocialComponent` 包含在中的 `SocialOperationResult` 资源表示刚刚创建的资源，对于更新操作，它表示操作更改的资源。 不会 `SocialComponent` 为删除操作返回任何内容。

使用的成功HTTP状态代码包括：

* 2010年创建操作
* 200 for Update operations
* 204用于删除操作

#### OperationException类 {#operationexception-class}

在执 `OperationExcepton` 行操作时，如果请求无效或发生某些其他错误（如内部错误、参数值错误、权限不当等），则可能会引发。 HTTP状 `OperationException` 态代码和错误消息由HTTP状态代码和错误消息组成，这些消息作为对的响应返回给客户端 `PostOperatoin`。

#### OperationService类 {#operationservice-class}

社交组件框架建议，负责执行操作的业务逻辑不在类内实现，而 `SocialOperation` 是委托给OSGi服务。 使用OSGi服务用于业务逻辑， `SocialComponent`允许端点所作用的 `SocialOperation` 与其它代码集成并应用不同的业务逻辑。

所有 `OperationService` 类都扩展 `AbstractOperationService`了，允许附加的扩展，这些扩展可以连接到正在执行的操作中。 服务中的每个操作由类表 `SocialOperation` 示。 在操 `OperationExtensions` 作执行过程中，可通过调用这些方法来调用类

* `performBeforeActions()`

   允许预检／预处理和验证
* `performAfterActions()`

   允许进一步修改资源或调用自定义事件、工作流等

#### OperationExtension类 {#operationextension-class}

`OperationExtension` 类是可以注入到操作中的自定义代码片段，允许自定义操作以满足业务需求。 组件的用户可以动态地以增量方式向组件添加功能。 扩展／挂接模式允许开发人员专门关注扩展本身，并消除复制和覆盖整个操作和组件的需求。

## 示例代码 {#sample-code}

示例代码可在 [Adobe Marketing Cloud GitHub存储库中找到](https://github.com/Adobe-Marketing-Cloud) 。 搜索以或为前缀的 `aem-communities` 项目 `aem-scf`。

## 最佳实践 {#best-practices}

视图编 [码准则部分](code-guide.md) ，了解针对AEM Communities开发人员的各种编码准则和最佳实践。

另请参 [阅存储资源提供商(SRP)](srp.md) (UGC)，了解如何访问用户生成的内容。

| **[‹功能基本工具](essentials.md)** | **[客户端自定义‡](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers‡](handlebars-helpers.md)** |

