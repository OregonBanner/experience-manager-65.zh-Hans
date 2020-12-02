---
title: 服务器端自定义
seo-title: 服务器端自定义
description: 在AEM Communities自定义服务器端
seo-description: 在AEM Communities自定义服务器端
uuid: 5e9bc6bf-69dc-414c-a4bd-74a104d7bd8f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: df5416ec-5c63-481b-99ed-9e5a91df2432
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---


# 服务器端自定义{#server-side-customization}

| **[‹功能基本工具](essentials.md)** | **[客户端自定义](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars帮助器](handlebars-helpers.md)** |

## Java API {#java-apis}

>[!NOTE]
>
>从一个主要版本升级到下一个版本时，Communities API的包位置可能会发生更改。

### SocialComponent接口{#socialcomponent-interface}

SocialComponents是POJO，它代表AEM Communities功能的资源。 理想情况下，每个SocialComponent都表示具有公开的GETter的特定resourceType，这些GETter向客户端提供数据，从而准确地表示资源。 所有业务逻辑和视图逻辑都封装在SocialComponent中，如有必要，包括站点访客的会话信息。

该接口定义表示资源所必需的基本GETter集。 重要的是，该接口规定了Map&lt;String, Object> getAsMap()和String toJSONString()方法，这是渲染Handlebars模板和为资源公开GETJSON端点所必需的。

所有SocialComponent类必须实现接口`com.adobe.cq.social.scf.SocialComponent`

### SocialCollectionComponent接口{#socialcollectioncomponent-interface}

SocialCollectionComponent界面扩展了SocialComponent界面，以更好地表示作为其他资源集合的资源。

所有SocialCollectionComponent类必须实现接口com.adobe.cq.social.scf.SocialCollectionComponent

### SocialComponentFactory接口{#socialcomponentfactory-interface}

SocialComponentFactory（工厂）在框架中注册SocialComponent。 工厂提供了一种方法，让框架知道在确定多个SocialComponent时，哪些SocialComponents可用于给定的resourceType及其优先级等级。

SocialComponentFactory负责创建所选SocialComponent的实例，使得能够使用DI惯例从工厂中注入SocialComponent所需的所有依赖项。

SocialComponentFactory是OSGi服务，可访问其他OSGi服务，这些服务可以通过构造函数传递到SocialComponent。

所有SocialComponentFactory类必须实现接口`com.adobe.cq.social.scf.SocialComponentFactory`

SocialComponentFactory.getPriority()方法的实现应返回最高值，以使工厂用于getResourceType()返回的给定resourceType。

### SocialComponentFactoryManager接口{#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager（管理者）管理在框架中注册的所有SocialComponents，并负责选择SocialComponentFactory以用于给定资源(resourceType)。 如果没有为特定resourceType注册工厂，则经理将返回给定资源具有最接近超级类型的工厂。

SocialComponentFactoryManager是OSGi服务，可访问其他OSGi服务，这些服务可以通过构造函数传递到SocialComponent。

通过调用`com.adobe.cq.social.scf.SocialComponentFactoryManager`获取OSGi服务的句柄

### HTTP API -POST请求{#http-api-post-requests}

#### PostOperation类{#postoperation-class}

HTTP APIPOST端点是通过实现`SlingPostOperation`接口（包`org.apache.sling.servlets.post`）定义的PostOperation类。

`PostOperation`端点实现将`sling.post.operation`设置为操作将响应的值。 将an:operation参数设置为该值的所有POST请求都将委派给此实现类。

`PostOperation`调用`SocialOperation`，它执行操作所需的操作。

`PostOperation`从`SocialOperation`接收结果，并将相应的响应返回给客户端。

#### SocialOperation类{#socialoperation-class}

每个`SocialOperation`端点扩展AbstractSocialOperation类并覆盖方法`performOperation()`。 此方法执行完成操作并返回`SocialOperationResult`或引发`OperationException`所需的所有操作，在这种情况下，将返回包含消息的HTTP错误状态（如果可用），而不返回正常JSON响应或成功HTTP状态代码。

通过扩展`AbstractSocialOperation`，可重用`SocialComponents`来发送JSON响应。

#### SocialOperationResult类{#socialoperationresult-class}

`SocialOperationResult`类作为`SocialOperation`的结果返回，由`SocialComponent`、HTTP状态代码和HTTP状态消息组成。

`SocialComponent`表示受操作影响的资源。

对于“创建”操作，`SocialOperationResult`中包含的`SocialComponent`表示刚创建的资源，对于“更新”操作，它表示操作更改的资源。 Delete操作不返回`SocialComponent`。

使用的成功HTTP状态代码为：

* 201 for Create operations
* 200用于更新操作
* 204 for Delete operations

#### OperationException类{#operationexception-class}

如果请求无效或出现某些其他错误，例如内部错误、参数值错误、权限不当等，则执行操作时可能引发`OperationExcepton`。 `OperationException`由HTTP状态代码和错误消息组成，这些消息作为对`PostOperatoin`的响应返回给客户端。

#### OperationService类{#operationservice-class}

社交组件框架建议不在`SocialOperation`类中实现负责执行操作的业务逻辑，而是将其委派给OSGi服务。 使用业务逻辑的OSGi服务允许由`SocialOperation`端点所作用的`SocialComponent`与其它代码集成，并应用不同的业务逻辑。

所有`OperationService`类都扩展`AbstractOperationService`，允许附加扩展，这些扩展可以连接到正在执行的操作中。 服务中的每个操作都由`SocialOperation`类表示。 在操作执行过程中，可通过调用方法调用`OperationExtensions`类

* `performBeforeActions()`

   允许预检／预处理和验证
* `performAfterActions()`

   允许进一步修改资源或调用自定义事件、工作流等

#### OperationExtension类{#operationextension-class}

`OperationExtension` 类是可注入到操作中的自定义代码片段，允许定制操作以满足业务需求。组件的使用者可以动态地以增量方式向组件添加功能。 扩展／挂接模式使开发人员能专门专注于扩展本身，并消除复制和覆盖整个操作和组件的需求。

## 示例代码{#sample-code}

示例代码位于[Adobe Marketing CloudGitHub](https://github.com/Adobe-Marketing-Cloud)存储库中。 搜索以`aem-communities`或`aem-scf`为前缀的项目。

## 最佳实践 {#best-practices}

视图[编码准则](code-guide.md)部分，了解针对AEM Communities开发人员的各种编码准则和最佳实践。

另请参阅UGC](srp.md)的[存储资源提供程序(SRP)，以了解如何访问用户生成的内容。

| **[‹功能基本工具](essentials.md)** | **[客户端自定义](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars帮助器](handlebars-helpers.md)** |

