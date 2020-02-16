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
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# AEM中的服务用户{#service-users-in-aem}

## 概述 {#overview}

在AEM中获取管理会话或资源解析程序的主要方法是使用Sling提供 `SlingRepository.loginAdministrative()` 的 `ResourceResolverFactory.getAdministrativeResourceResolver()` 和方法。

但是，这两种方法都没有围绕最少权限原则进行设计 [](https://en.wikipedia.org/wiki/Principle_of_least_privilege) ，而且开发者很容易在早期就不为其内容规划适当的结构和相应的访问控制级别(ACL)。 如果此类服务中存在漏洞，则通常会导致权限提升到用户，即使代码本身不需要管理权限也能正常工作。 `admin`

## 如何逐步退出管理会话 {#how-to-phase-out-admin-sessions}

### 优先级0:该功能是否处于活动状态／需要／废弃？ {#priority-is-the-feature-active-needed-derelict}

有时可能不使用管理员会话，或者完全禁用该功能。 如果您的实施存在这种情况，请确保完全删除该功能或将其与 [NOP代码配合](https://en.wikipedia.org/wiki/NOP)。

### 优先级1:使用请求会话 {#priority-use-the-request-session}

尽可能重新构建您的功能，以便给定的、经过身份验证的请求会话可用于读取或写入内容。 如果这不可行，则通常可以通过应用以下优先事项来实现。

### 优先级2:重构内容 {#priority-restructure-content}

许多问题可以通过重组内容来解决。 进行重组时，请牢记以下简单的规则：

* **更改访问控制**

   * 确保真正需要访问的用户或用户组实际具有访问权限；

* **调整内容结构**

   * 将其移至其他位置，例如访问控制与可用的请求会话相匹配；
   * 更改内容粒度；

* **重新调整代码，使其成为正确的服务**

   * 将业务逻辑从JSP代码移到服务。 这允许不同的内容建模。

此外，请确保您开发的任何新功能都符合以下原则：

* **安全要求应驱动内容结构**

   * 管理访问控制应该感觉很自然
   * 访问控制必须由存储库而非应用程序来实施

* **利用节点类型**

   * 限制可设置的属性集

* **遵守隐私设置**

   * 对于私有配置文件，一个示例是不公开在专用节点上找到的配置文件图片、电子邮件或全 `/profile` 名。

## 严格的访问控制 {#strict-access-control}

无论您是在重组内容时应用访问控制还是在为新服务用户应用访问控制时，都必须应用尽可能严格的ACL。 使用所有可能的访问控制设施：

* 例如，不应在上应 `jcr:read` 用 `/apps`它，只应用于 `/apps/*/components/*/analytics`

* Use [restrictions](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)

* 为节点类型应用ACL
* 限制权限

   * 例如，仅需编写属性时，不要授予权 `jcr:write` 限；请改 `jcr:modifyProperties` 用

## 服务用户和映射 {#service-users-and-mappings}

如果上述方法失败，Sling 7提供服务用户映射服务，该服务允许配置捆绑到用户的映射和两个相应的API方法：并 ` [SlingRepository.loginService()](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)`` [ResourceResolverFactory.getServiceResourceResolver()](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)` 且只返回具有已配置用户权限的会话／资源解析程序。 这些方法具有以下特点：

* 它们允许将服务映射到用户
* 它们使得定义子服务用户成为可能
* 中心配置点是： `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl`
* `service-id` = `service-name`[ &quot;:&quot; subservice-name ] 

* `service-id` 映射到资源解析程序和／或JCR存储库用户ID以进行身份验证
* `service-name` 是提供服务的捆绑包的符号名称

## 其他建议 {#other-recommendations}

### 用服务用户替换管理会话 {#replacing-the-admin-session-with-a-service-user}

服务用户是JCR用户，没有密码设置和执行特定任务所需的最少权限集。 未设置密码意味着无法与服务用户登录。

停用管理会话的一种方法是将其替换为服务用户会话。 如果需要，还可以用多个子服务用户替换它。

要将管理员会话替换为服务用户，应执行以下步骤：

1. 确定服务的必要权限，并记住最少权限的原则。
1. 检查是否已有用户具有您所需的权限设置。 如果没有现有用户满足您的需求，则创建新的系统服务用户。 需要RTC来创建新的服务用户。 有时，创建多个子服务用户（例如，一个用于编写，一个用于阅读）来划分更多访问是有意义的。
1. 为用户设置和测试ACE。
1. 为您的 `service-user` 服务和 `user/sub-users`

1. 使服务用户Sling功能可用于您的捆绑包：更新到的最新版本 `org.apache.sling.api`。

1. 将代 `admin-session` 码中的代码替换为 `loginService` 或 `getServiceResourceResolver` API。

## 创建新服务用户 {#creating-a-new-service-user}

在您确认AEM服务用户列表中的任何用户均不适用于您的使用案例，且相应的RTC问题已获得批准后，您可以继续将新用户添加到默认内容。

建议的方法是创建一个服务用户以使用位于https://&lt;server>:&lt;port>/crx/explorer/index.jsp的存储库资源管理器 **

其目标是获取有效的属 `jcr:uuid` 性，该属性是必需的，以便通过内容包安装创建用户。

您可以通过以下方式创建服务用户：

1. 转到位于https://&lt;server>:&lt; *port>/crx/explorer/index.jsp的存储库资源管理器*
1. 通过按屏幕左上角 **的“登录** ”链接以管理员身份登录。
1. 然后，创建并命名系统用户。 要将用户创建为系统用户，请将中间路径设置为，并根据需 `system` 要添加可选子文件夹：

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. 验证系统用户节点的外观如下：

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >请注意，不存在与服务用户关联的混音类型。 这意味着系统用户将不存在访问控制策略。

在将相应的。content.xml添加到捆绑的内容时，请确保已设置并且 `rep:authorizableId` 主类型是 `rep:SystemUser`。 它应该如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## 向ServiceUserMapper配置添加配置修改 {#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}

要从服务向相应的系统用户添加映射，您需要为服务创建出厂配 ` [ServiceUserMapper](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html)` 置。 为了保持这种模块化，可以使用 [Sling修正机制提供这种配置](https://issues.apache.org/jira/browse/SLING-3578)。 使用Sling初始内容加载来安装此类配置的建议方 [式是](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html):

1. 在捆绑包的src/main/resources文件夹下创建子文件夹SLING-INF/content
1. 在此文件夹中，创建一个名为org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.reminded-&lt;您的工厂配置的唯一名称>.xml的文件，其中包含您的工厂配置的内容（包括所有子服务用户映射）。 示例:

1. 在捆绑 `SLING-INF/content` 包的文件夹下 `src/main/resources` 创建一个文件夹；
1. 在此文件夹中，创建一个 `named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml` 包含工厂配置内容（包括所有子服务用户映射）的文件。

   为便于说明，请使用名为 `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml`:

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

1. 在捆绑包中的配置中引 `maven-bundle-plugin` 用Sling `pom.xml` 初始内容。 示例:

   ```xml
   <Sling-Initial-Content>
      SLING-INF/content;path:=/libs/system/config;overwrite:=true;
   </Sling-Initial-Content>
   ```

1. 安装您的捆绑套件，并确保已安装出厂配置。 您可以通过以下方式执行此操作：

   * 转到Web控制台，网址为 *https://serverhost:serveraddress/system/console/configMgr*
   * 搜索 **Apache Sling Service User Mapper Service Amper Amper Action**
   * 单击链接以查看是否有正确的配置。

## 处理服务中的共享会话 {#dealing-with-shared-sessions-in-services}

呼叫通 `loginAdministrative()` 常与共享会话一起显示。 这些会话在服务激活时获取，并且仅在服务停止后注销。 尽管这是常见的做法，但它导致了两个问题：

* **** 安全性：此类管理员会话用于缓存和返回绑定到共享会话的资源或其他对象。 在调用堆栈的稍后部分，这些对象可以适应具有提升权限的会话或资源解析程序，而且通常，调用者不清楚它们是否使用管理员会话。
* **** 性能：在Oak共享会话中，可能会导致性能问题，目前不建议使用这些会话。

解决安全风险的最显而易见的解决方案是简单地将调 `loginAdministrative()` 用替换为权限 `loginService()` 受限的用户呼叫。 但是，这不会对任何潜在的性能降级产生任何影响。 减轻这种情况的一种可能性是将所有请求的信息包含在与会话没有关联的对象中。 然后，按需创建（或销毁）会话。

建议的方法是重新构建服务的API，以便让调用者控制会话的创建／破坏。

## JSP中的管理会话 {#administrative-sessions-in-jsps}

JSP无法使 `loginService()`用，因为没有关联的服务。 但是，JSP中的管理会话通常是违反MVC范例的迹象。

可以通过两种方式来修复此问题：

1. 以允许与用户会话一起操作内容的方式重组内容；
1. 将逻辑提取到提供API的服务，然后JSP可以使用该API。

第一种方法是优选的。

## 处理事件、复制预处理器和作业 {#processing-events-replication-preprocessors-and-jobs}

在处理事件或作业时，在某些情况下，工作流通常会丢失触发该事件的相应会话。 这会导致事件句柄和作业处理程序经常使用管理会话来完成其工作。 解决这一问题的方法可能各不相同，但各有其优势和劣势：

1. 在事件 `user-id` 有效负荷中传递并使用模拟。

   **** 优势：易于使用。

   **** 缺点：仍在使用 `loginAdministrative()`。 它重新验证已通过身份验证的请求。

1. 创建或重用有权访问数据的服务用户。

   **** 优势：与当前设计一致。 需要最小的更改。

   **** 缺点：需要非常强大的服务用户才能灵活，这很容易导致权限提升。 避开安全模型。

1. 在事件有效负 `Subject` 荷中传递序列化，并基于该主 `ResourceResolver` 题创建一个。 一个示例是在中使 `doAsPrivileged` 用JAAS `ResourceResolverFactory`。

   **** 优势：从安全角度清晰地实施。 它避免了重新认证，并且它以原始权限运行。 安全相关代码对事件的消费者是透明的。

   **** 缺点：需要重构。 安全相关代码对事件的消费者透明这一事实也可能导致问题。

第三种方法目前是首选的处理技术。

## 工作流程 {#workflow-processes}

在工作流进程实现中，触发工作流的相应用户会话通常会丢失。 这会导致工作流程经常使用管理会话来执行其工作。

为了解决这些问题，建议使用处理事件、复制预处理器和作 [业中提到的相同方法](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs) 。

## Sling POST处理器和已删除的页面 {#sling-post-processors-and-deleted-pages}

在sling POST处理器实现中使用了几个管理会话。 通常，管理会话用于访问正在处理的POST中待删除的节点。 因此，它们不再通过请求会话可用。 可以访问节点待删除以披露元数据，否则不应访问该元数据。
