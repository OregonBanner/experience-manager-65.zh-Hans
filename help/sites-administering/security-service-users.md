---
title: AEM中的服务用户
seo-title: AEM中的服务用户
description: 了解AEM中的服务用户。
seo-description: 了解AEM中的服务用户。
uuid: 4efab5fb-ba11-4922-bd68-43ccde4eb355
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 9cfe5f11-8a0e-4a27-9681-a8d50835c864
exl-id: ccd8577b-3bbf-40ba-9696-474545f07b84
feature: Security
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '1789'
ht-degree: 0%

---

# AEM{#service-users-in-aem}中的服务用户

## 概述 {#overview}

在AEM中获取管理会话或资源解析程序的主要方法是使用Sling提供的`SlingRepository.loginAdministrative()`和`ResourceResolverFactory.getAdministrativeResourceResolver()`方法。

但是，这两种方法都没有围绕[最小权限](https://en.wikipedia.org/wiki/Principle_of_least_privilege)原则进行设计，因此开发者很容易不为其内容早期规划适当的结构和相应的访问控制级别(ACL)。 如果此类服务中存在漏洞，则通常会导致权限提升到`admin`用户，即使代码本身不需要管理权限才能正常工作。

## 如何逐步退出管理会话{#how-to-phase-out-admin-sessions}

### 优先级0:该功能是否处于活动状态/需要/废弃？{#priority-is-the-feature-active-needed-derelict}

可能未使用管理会话，或完全禁用该功能。 如果您的实现存在这种情况，请确保完全删除该功能或将其与[NOP代码](https://en.wikipedia.org/wiki/NOP)配合。

### 优先级1:使用请求会话{#priority-use-the-request-session}

尽可能重新调整功能，以便使用给定的、经过身份验证的请求会话来读取或写入内容。 如果这样做不可行，则通常可以通过采用下列优先事项来实现。

### 优先级2:重构内容{#priority-restructure-content}

重组内容可以解决许多问题。 进行重组时，请牢记以下简单规则：

* **更改访问控制**

   * 确保真正需要访问的用户或用户组实际具有访问权限；

* **优化内容结构**

   * 将其移至其他位置，例如访问控制与可用的请求会话相匹配；
   * 更改内容粒度；

* **重新调整代码，使其成为正确的服务**

   * 将业务逻辑从JSP代码移动到服务。 这允许不同的内容建模。

另外，请确保您开发的任何新功能都遵循以下原则：

* **安全要求应推动内容结构**

   * 管理访问控制应该感觉自然
   * 访问控制必须由存储库而非应用程序强制执行

* **利用节点类型**

   * 限制可设置的属性集

* **遵守隐私设置**

   * 对于私有用户档案，一个示例是不公开在私有`/profile`节点上找到的用户档案图片、电子邮件或全名。

## 严格访问控制{#strict-access-control}

无论您是在重组内容时应用访问控制，还是在为新服务用户应用时，都必须尽可能应用最严格的ACL。 使用所有可能的访问控制设施：

* 例如，不应在`/apps`上应用`jcr:read`，而只应用到`/apps/*/components/*/analytics`

* 使用[restrictions](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)

* 对节点类型应用ACL
* 限制权限

   * 例如，当仅需要写入属性时，不要授予`jcr:write`权限；请改用`jcr:modifyProperties`

## 服务用户和映射{#service-users-and-mappings}

如果上述方法失败，Sling 7将优惠服务用户映射服务，该服务允许配置捆绑到用户映射和两个相应的API方法：` [SlingRepository.loginService()](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)`和` [ResourceResolverFactory.getServiceResourceResolver()](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)`，它们返回的会话/资源解析程序仅具有已配置用户的权限。 这些方法具有以下特点：

* 它们允许将服务映射到用户
* 它们使得定义子服务用户成为可能
* 中心配置点是：`org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl`
* `service-id` =  `service-name` [ &quot;:&quot; subservice-name  ] 

* `service-id` 映射到资源解析器和/或JCR存储库用户ID以进行身份验证
* `service-name` 是提供服务的捆绑包的符号名

## 其他Recommendations {#other-recommendations}

### 用服务用户{#replacing-the-admin-session-with-a-service-user}替换admin-session

服务用户是没有密码集和执行特定任务所需的最少权限集的JCR用户。 未设置密码意味着无法与服务用户登录。

停用管理会话的一种方法是将其替换为服务用户会话。 如果需要，还可以用多个子服务用户替换。

要将管理会话替换为服务用户，您应执行以下步骤：

1. 确定您的服务的必要权限，同时要牢记最少的权限原则。
1. 检查是否已有具有您需要的权限设置的用户。 如果没有符合您需求的现有用户，请创建新的系统服务用户。 需要RTC来创建新的服务用户。 有时，创建多个子服务用户（例如，一个用于写入，一个用于阅读）来划分更多的访问权限是有道理的。
1. 为用户设置和测试ACE。
1. 为服务和`user/sub-users`添加`service-user`映射

1. 为您的捆绑包提供服务用户sling功能：更新至`org.apache.sling.api`的最新版本。

1. 将代码中的`admin-session`替换为`loginService`或`getServiceResourceResolver` API。

## 创建新服务用户{#creating-a-new-service-user}

在您验证AEM服务列表的任何用户均不适用于您的用例且相应的RTC问题已获得批准后，您可以继续将新用户添加到默认内容。

建议的方法是创建一个服务用户以使用位于&#x200B;*https://&lt;server>:&lt;port>/crx/explorer/index.jsp*&#x200B;的存储库资源管理器

其目标是获取有效的`jcr:uuid`属性，这是通过内容包安装创建用户所必需的。

可以通过以下方式创建服务用户：

1. 转到位于&#x200B;*https://&lt;server>:&lt;port>/crx/explorer/index.jsp*&#x200B;的存储库资源管理器
1. 按屏幕左上角的&#x200B;**登录**&#x200B;链接，以管理员身份登录。
1. 然后，创建并命名系统用户。 要将用户创建为系统用户，请将中间路径设置为`system`并根据您的需要添加可选子文件夹：

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. 验证您的系统用户节点是否如下所示：

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >请注意，没有与服务用户关联的混合类型。 这意味着系统用户将没有访问控制策略。

在将相应的.content.xml添加到捆绑包的内容时，请确保已设置`rep:authorizableId`，且主类型为`rep:SystemUser`。 它应该如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## 正在向ServiceUserMapper配置{#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}添加配置修正

要将服务中的映射添加到相应的系统用户，您需要为` [ServiceUserMapper](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html)`服务创建出厂配置。 为了保持这种模块化，可以使用[Sling修正机构](https://issues.apache.org/jira/browse/SLING-3578)提供这种配置。 与捆绑包一起安装此类配置的建议方法是使用[Sling初始内容加载](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html):

1. 在捆绑包的src/main/resources文件夹下创建子文件夹SLING-INF/content
1. 在此文件夹中，创建一个名为org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.revined-&lt;您的工厂配置的唯一名称>.xml，其中包含您的工厂配置的内容（包括所有子服务用户映射）。 示例:

1. 在捆绑包的`src/main/resources`文件夹下创建一个`SLING-INF/content`文件夹；
1. 在此文件夹中，创建一个文件`named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml`，其中包含您的工厂配置的内容，包括所有子服务用户映射。

   为便于说明，请取一个名为`org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml`的文件：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <node>
       <primaryNodeType>sling:OsgiConfig</primaryNodeType>
       <property>
           <name>user.default</name>
           <value></value>
       </property>
       <property>
           <name>user.mapping</name>
           <values>
               <value>com.adobe.granite.auth.saml=authentication-service</value>
           </values>
       </property>
   </node>
   ```

1. 在捆绑包`pom.xml`的`maven-bundle-plugin`配置中引用Sling初始内容。 示例:

   ```xml
   <Sling-Initial-Content>
      SLING-INF/content;path:=/libs/system/config;overwrite:=true;
   </Sling-Initial-Content>
   ```

1. 安装您的捆绑包，并确保已安装出厂配置。 您可以通过以下方式执行此操作：

   * 转到位于&#x200B;*https://serverhost:serveraddress/system/console/configMgr*&#x200B;的Web控制台
   * 搜索&#x200B;**Apache Sling Service用户映射器服务修正**
   * 单击链接以查看是否有正确的配置。

## 处理服务{#dealing-with-shared-sessions-in-services}中的共享会话

对`loginAdministrative()`的调用通常与共享会话一起显示。 这些会话在服务激活上获取，并且仅在服务停止后才注销。 尽管这是常见的做法，但它导致了两个问题：

* **安全性：** 此类管理会话用于缓存和返回资源或绑定到共享会话的其他对象。在调用堆栈的稍后部分，这些对象可以适应具有提升权限的会话或资源解析器，而且调用者通常不清楚它是他们正在操作的管理会话。
* **性能：** 在Oak共享会话中，可能会导致性能问题，目前不建议使用。

针对安全风险的最明显解决方案是简单地将`loginAdministrative()`调用替换为具有受限权限的用户的`loginService()`调用。 但是，这不会对任何潜在性能降级产生任何影响。 减轻这种情况的一种可能性是将所有请求的信息包含在与会话没有关联的对象中。 然后，按需创建（或销毁）会话。

建议的方法是重新构建服务的API，以便让调用者控制会话的创建/破坏。

## JSP {#administrative-sessions-in-jsps}中的管理会话

JSP无法使用`loginService()`，因为没有关联的服务。 但是，JSP中的管理会话通常是违反MVC模式的一个迹象。

可通过两种方式解决此问题：

1. 以允许与用户会话一起操作内容的方式重组内容；
1. 将逻辑提取到提供API的服务，JSP随后可以使用该API。

第一种方法是首选方法。

## 处理事件、复制预处理器和作业{#processing-events-replication-preprocessors-and-jobs}

处理事件或作业时，在某些情况下，触发事件的对应会话通常会丢失。 这导致事件处理程序和作业处理程序经常使用管理会话来完成工作。 可以想象到的解决这一问题的方法各不相同，每种方法都有其优势和劣势：

1. 在事件负载中传递`user-id`并使用模拟。

   **优势：** 易于使用。

   **缺点：** 仍使用 `loginAdministrative()`。它重新对已通过身份验证的请求进行身份验证。

1. 创建或重复使用有权访问数据的服务用户。

   **优势：** 与当前设计一致。需要最小的更改。

   **缺点：需** 要非常强大的服务用户灵活，这很容易导致权限提升。规避安全模型。

1. 在事件负载中传递`Subject`的序列化，并基于该主题创建`ResourceResolver`。 一个示例是使用`ResourceResolverFactory`中的JAAS `doAsPrivileged`。

   **优势：** 从安全角度清晰实施。它避免了重认证，并且以原始权限运行。 安全相关代码对事件的消费者是透明的。

   **缺点：** 需要重构。安全相关代码对事件的消费者透明这一事实也可能导致问题。

第三种方法目前是首选的处理技术。

## 工作流进程{#workflow-processes}

在工作流进程实现中，触发工作流的相应用户会话通常会丢失。 这会导致工作流进程经常使用管理会话来执行其工作。

为了解决这些问题，建议使用[处理事件、复制预处理器和作业](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs)中提到的相同方法。

## SlingPOST处理器和已删除页{#sling-post-processors-and-deleted-pages}

在sling POST处理器实施中使用了几个管理会话。 通常，管理会话用于访问正在处理的POST中处于待删除状态的节点。 因此，它们不再通过请求会话可用。 可以访问节点待删除以披露元数据，否则不应访问元数据。
