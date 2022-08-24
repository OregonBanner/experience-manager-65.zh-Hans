---
title: AEM中的服务用户
seo-title: Service Users in AEM
description: 了解AEM中的服务用户。
seo-description: Learn about Service Users in AEM.
uuid: 4efab5fb-ba11-4922-bd68-43ccde4eb355
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 9cfe5f11-8a0e-4a27-9681-a8d50835c864
exl-id: ccd8577b-3bbf-40ba-9696-474545f07b84
feature: Security
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1778'
ht-degree: 0%

---

# AEM中的服务用户{#service-users-in-aem}

## 概述 {#overview}

在AEM中获取管理会话或资源解析程序的主要方法是使用 `SlingRepository.loginAdministrative()` 和 `ResourceResolverFactory.getAdministrativeResourceResolver()` 方法。

但是，这两种方法均未围绕 [最小特权原则](https://en.wikipedia.org/wiki/Principle_of_least_privilege) 而且，开发人员很容易就无法为其内容尽早规划适当的结构和相应的访问控制级别(ACL)。 如果此类服务中存在漏洞，则通常会导致权限升级到 `admin` 用户，即使代码本身不需要管理权限也可正常工作。

## 如何逐步停用管理会话 {#how-to-phase-out-admin-sessions}

### 优先级0:该功能是否处于活动状态/需要/废弃？ {#priority-is-the-feature-active-needed-derelict}

有时可能未使用管理员会话，或者完全禁用该功能。 如果您的实施存在这种情况，请确保完全删除该功能或将其与之配合 [NOP代码](https://en.wikipedia.org/wiki/NOP).

### 优先级1:使用请求会话 {#priority-use-the-request-session}

尽可能重新构建您的功能，以便使用经过身份验证的给定请求会话来读取或写入内容。 如果这不可行，则通常可以通过采用下列优先事项来实现。

### 优先级2:重构内容 {#priority-restructure-content}

许多问题可以通过重组内容来解决。 在进行重构时，请牢记以下简单的规则：

* **更改访问控制**

   * 确保真正需要访问权限的用户或组实际拥有访问权限；

* **优化内容结构**

   * 将其移动到其他位置，例如，在访问控制与可用请求会话匹配的位置；
   * 更改内容粒度；

* **重新构建代码以提供适当的服务**

   * 将业务逻辑从JSP代码移动到服务。 这允许进行不同的内容建模。

此外，请确保您开发的任何新功能都遵循以下原则：

* **安全要求应驱动内容结构**

   * 管理访问控制应该感觉很自然
   * 访问控制必须由存储库（而非应用程序）强制执行

* **使用节点类型**

   * 限制可设置的属性集

* **遵守隐私设置**

   * 对于私人用户档案，一个示例是不显示在私人用户档案上找到的用户档案图片、电子邮件或全名 `/profile` 节点。

## 严格访问控制 {#strict-access-control}

无论您是在重组内容时应用访问控制，还是在为新服务用户应用访问控制时，都必须尽可能应用最严格的ACL。 使用所有可能的访问控制设施：

* 例如，不应用 `jcr:read` on `/apps`，则仅将其应用于 `/apps/*/components/*/analytics`

* 使用 [限制](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)

* 对节点类型应用ACL
* 限制权限

   * 例如，当只需要写入属性时，不要为 `jcr:write` 许可；use `jcr:modifyProperties` 改为

## 服务用户和映射 {#service-users-and-mappings}

如果上述方法失败，Sling 7提供了服务用户映射服务，该服务允许配置包到用户的映射以及两个相应的API方法： ` [SlingRepository.loginService()](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)` 和 ` [ResourceResolverFactory.getServiceResourceResolver()](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)` 仅返回具有已配置用户权限的会话/资源解析程序。 这些方法具有以下特征：

* 它们允许将服务映射到用户
* 它们使用户能够定义子服务用户
* 中心配置点是： `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl`
* `service-id` = `service-name` [ &quot;:&quot; subservice-name ] 

* `service-id` 映射到资源解析程序和/或JCR存储库用户ID以进行身份验证
* `service-name` 是提供服务的包的符号名称

## 其他Recommendations {#other-recommendations}

### 将管理员会话替换为服务用户 {#replacing-the-admin-session-with-a-service-user}

服务用户是JCR用户，没有设置密码，并且拥有执行特定任务所需的最少权限集。 未设置密码意味着无法与服务用户登录。

一种弃用管理会话的方法是，将其替换为服务用户会话。 如果需要，也可以由多个子服务用户替换。

要将管理员会话替换为服务用户，您应执行以下步骤：

1. 确定服务的必要权限，并牢记最少权限的原则。
1. 检查是否已经有一个用户可用，且该用户完全符合您所需的权限设置。 如果现有用户与您的需求不匹配，请创建新的系统服务用户。 需要RTC来创建新的服务用户。 有时，创建多个子服务用户（例如，一个用于写入，一个用于阅读）以划分更多访问权限是有意义的。
1. 为用户设置和测试ACE。
1. 添加 `service-user` 为您的服务和 `user/sub-users`

1. 使服务用户sling功能可用于您的包：更新至 `org.apache.sling.api`.

1. 替换 `admin-session` 的 `loginService` 或 `getServiceResourceResolver` API。

## 创建新服务用户 {#creating-a-new-service-user}

在您确认AEM服务用户列表中的任何用户均不适用于您的用例，且相应的RTC问题已获得批准后，您可以继续将新用户添加到默认内容中。

建议创建一个服务用户，以便在 *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*

目标是获得有效 `jcr:uuid` 属性，要通过内容包安装创建用户，此属性是必需的。

您可以通过以下方式创建服务用户：

1. 转到位于 *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*
1. 通过按 **登录** 链接。
1. 接下来，创建并命名您的系统用户。 要将用户创建为系统用户，请将中间路径设置为 `system` 并根据您的需要，添加可选子文件夹：

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. 验证您的系统用户节点是否如下所示：

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >请注意，没有与服务用户关联的混合类型。 这意味着系统用户将没有访问控制策略。

将相应的.content.xml添加到包的内容时，请确保已设置 `rep:authorizableId` 主要类型是 `rep:SystemUser`. 它应该如下所示：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## 向ServiceUserMapper配置添加配置修正 {#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}

要将服务中的映射添加到相应的系统用户，您需要为 ` [ServiceUserMapper](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html)` 服务。 为保持此模块化，可使用 [Sling修正机制](https://issues.apache.org/jira/browse/SLING-3578). 使用包安装此类配置的建议方法是： [Sling初始内容加载](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html):

1. 在包的src/main/resources文件夹下创建子文件夹SLING-INF/content
1. 在此文件夹中，创建一个名为org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.revined-&lt;some unique=&quot;&quot; name=&quot;&quot; for=&quot;&quot; your=&quot;&quot; factory=&quot;&quot; configuration=&quot;&quot;>.xml ，其中包含工厂配置的内容（包括所有子服务用户映射）。 示例:

1. 创建 `SLING-INF/content` 文件夹 `src/main/resources` 包文件夹；
1. 在此文件夹中，创建一个文件 `named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml` ，包括所有子服务用户映射。

   为了提供说明，请获取名为 `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml`:

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

1. 在的配置中引用Sling初始内容 `maven-bundle-plugin` 在 `pom.xml` 你的包。 示例:

   ```xml
   <Sling-Initial-Content>
      SLING-INF/content;path:=/libs/system/config;overwrite:=true;
   </Sling-Initial-Content>
   ```

1. 安装包并确保已安装出厂配置。 您可以执行以下操作来实现此目标：

   * 转到Web控制台(位于 *https://serverhost:serveraddress/system/console/configMgr*
   * 搜索 **《Apache Sling服务用户映射器服务修正》**
   * 单击该链接可查看是否配置正确。

## 处理服务中的共享会话 {#dealing-with-shared-sessions-in-services}

调用 `loginAdministrative()` 通常与共享的会话一起显示。 这些会话在服务激活时获取，并且仅在服务停止后注销。 尽管这是常见的做法，但它导致了两个问题：

* **安全性：** 此类管理员会话用于缓存并返回绑定到共享会话的资源或其他对象。 在调用堆栈的后面，这些对象可能会以提升的权限适应会话或资源解析器，而且调用者通常不清楚这是他们正在使用的管理员会话。
* **性能：** 在Oak共享会话中，可能会导致性能问题，目前不建议使用这些会话。

对于安全风险，最明显的解决方案是 `loginAdministrative()` 使用 `loginService()` 一个用户拥有受限权限。 但是，这不会对任何潜在的性能下降产生任何影响。 缓解这种情况的一种方法是，将所有请求的信息包含在与会话没有关联的对象中。 然后，根据需要创建（或销毁）会话。

推荐的方法是重构服务的API，以便让调用方控制会话的创建/销毁。

## JSP中的管理会话 {#administrative-sessions-in-jsps}

JSP无法使用 `loginService()`，因为没有关联的服务。 但是，JSP中的管理会话通常是违反MVC模式的一个标志。

可以通过以下两种方式解决此问题：

1. 以允许在用户会话中处理内容的方式重组内容；
1. 将逻辑提取到提供API的服务，该API随后可供JSP使用。

第一种方法是首选方法。

## 处理事件、复制预处理器和作业 {#processing-events-replication-preprocessors-and-jobs}

在处理事件或作业（在某些情况下是工作流）时，触发该事件的相应会话通常会丢失。 这会导致事件处理程序和作业处理程序经常使用管理会话来完成其工作。 可以想象的解决这个问题的方法各不相同，每种方法都有其优势和劣势：

1. 传递 `user-id` 并使用模拟。

   **优点：** 易于使用。

   **缺点：** 仍使用 `loginAdministrative()`. 它会重新验证已通过身份验证的请求。

1. 创建或重复使用有权访问数据的服务用户。

   **优点：** 与当前设计一致。 需要最少的更改。

   **缺点：** 需要功能非常强大的服务用户才能灵活，这很容易导致权限提升。 规避安全模型。

1. 传递序列化 `Subject` 在事件有效负载中，并创建 `ResourceResolver` 基于那个主题。 例如，使用JAAS `doAsPrivileged` 在 `ResourceResolverFactory`.

   **优点：** 从安全角度清理实施。 它避免了重新认证，并且以原始权限运行。 安全相关代码对事件的消费者是透明的。

   **缺点：** 需要重构。 安全相关代码对事件的消费者是透明的，这一事实也可能导致问题。

第三种方法目前是首选的处理技术。

## 工作流流程 {#workflow-processes}

在工作流流程实施中，触发工作流的相应用户会话通常会丢失。 这会导致通常使用管理会话来执行其工作的工作流进程。

为了解决这些问题，建议在 [处理事件、复制预处理器和作业](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs) 。

## SlingPOST处理器和删除的页面 {#sling-post-processors-and-deleted-pages}

slingPOST处理器实施中使用了几个管理会话。 通常，管理会话用于访问正在处理的POST中处于待删除状态的节点。 因此，它们将不再通过请求会话可用。 可以访问节点挂起的删除以公开其他不应访问的元数据。
