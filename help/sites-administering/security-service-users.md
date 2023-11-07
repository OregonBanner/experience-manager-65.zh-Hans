---
title: Adobe Experience Manager中的服务用户
description: 了解Adobe Experience Manager中的服务用户。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: ccd8577b-3bbf-40ba-9696-474545f07b84
feature: Security
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1797'
ht-degree: 0%

---


# Adobe Experience Manager (AEM)中的“服务用户” {#service-users-in-aem}

## 概述 {#overview}

在AEM中获取管理会话或资源解析程序的主要方法是使用 `SlingRepository.loginAdministrative()` 和 `ResourceResolverFactory.getAdministrativeResourceResolver()` 方法由Sling提供。

但是，这两种方法都不是围绕 [最小特权原则](https://en.wikipedia.org/wiki/Principle_of_least_privilege) 并且让开发人员很容易不去为内容规划适当的结构和相应的访问控制级别(ACL)。 如果此类服务中存在漏洞，则它通常会导致将权限提升到 `admin` 用户，即使代码本身不需要管理权限即可工作。

## 如何逐步停用管理员会话 {#how-to-phase-out-admin-sessions}

### 优先级0：功能是否处于活动状态/需要/已弃用？ {#priority-is-the-feature-active-needed-derelict}

在某些情况下，可能未使用管理员会话，或者该功能被完全禁用。 如果您的实施就是这种情况，请确保完全移除该功能或适合该功能 [NOP代码](https://en.wikipedia.org/wiki/NOP).

### 优先级1：使用请求会话 {#priority-use-the-request-session}

只要有可能，您都可以重构功能，以便可以使用经过身份验证的给定请求会话来读取或写入内容。 如果不可行，则通常可以通过遵循以下优先顺序来达到此目的。

### 优先级2：重构内容 {#priority-restructure-content}

许多问题可以通过重组内容来解决。 在进行重组时，请牢记以下简单规则：

* **更改访问控制**

   * 确保真正需要访问的用户或组实际拥有访问权限；

* **优化内容结构**

   * 将其移动到其他位置，例如，访问控制与可用的请求会话相匹配；
   * 更改内容粒度；

* **重构代码以使其成为适当的服务**

   * 将业务逻辑从JSP代码移动到服务。 这允许进行不同的内容建模。

此外，请确保您开发的任何新功能都遵守以下原则：

* **安全要求应驱动内容结构**

   * 管理访问控制应该感觉很自然
   * 访问控制必须由存储库而非应用程序实施

* **使用节点类型**

   * 限制可设置的属性集

* **尊重隐私设置**

   * 如果存在个人资料，则一个示例就是不公开个人资料图片、电子邮件或个人资料中的全名 `/profile` 节点。

## 严格访问控制 {#strict-access-control}

无论是在重构内容时应用访问控制，还是在为新服务用户应用访问控制时，都必须尽可能应用最严格的ACL。 使用所有可能的访问控制工具：

* 例如，不要应用 `jcr:read` 日期 `/apps`，仅将其应用于 `/apps/*/components/*/analytics`

* 使用 [限制](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)

* 为节点类型应用ACL
* 限制权限

   * 例如，当只需要编写属性时，不要将 `jcr:write` 权限；使用 `jcr:modifyProperties` 相反

## 服务用户和映射 {#service-users-and-mappings}

如果上述操作失败，Sling 7会提供服务用户映射服务，该服务允许配置捆绑包到用户的映射和两种相应的API方法：

* [`SlingRepository.loginService()`](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)
* [`ResourceResolverFactory.getServiceResourceResolver()`](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)

这些方法仅返回具有已配置用户权限的会话/资源解析程序。 这些方法具有以下特点：

* 它们允许将服务映射到用户
* 它们使得定义子服务用户成为可能
* 中心配置点为： `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl`
* `service-id` = `service-name` [“：”子服务名称]

* `service-id` 映射到资源解析程序和/或JCR存储库用户ID以进行身份验证
* `service-name` 是提供服务的包的符号名称

## 其他Recommendations {#other-recommendations}

### 将管理会话替换为服务用户 {#replacing-the-admin-session-with-a-service-user}

服务用户是不设置密码的JCR用户，是执行特定任务所需的最小权限集。 未设置密码意味着无法使用服务用户登录。

弃用管理会话的一种方法是将其替换为服务用户会话。 如果需要，还可以由多个子服务用户替换。

要将管理会话替换为服务用户，您应该执行以下步骤：

1. 确定服务的必要权限，并牢记最小权限原则。
1. 检查是否已有一个用户可以使用所需的确切权限设置。 如果没有现有用户符合您的需求，请创建系统服务用户。 创建服务用户需要RTC。 有时，创建多个子服务用户（例如，一个用于写入，一个用于读取）以进一步划分访问是明智的。
1. 为用户设置和测试ACE。
1. 添加 `service-user` 服务与的映射 `user/sub-users`

1. 使服务用户sling功能可用于您的捆绑包：更新到最新版本的 `org.apache.sling.api`.

1. 替换 `admin-session` 在代码中使用 `loginService` 或 `getServiceResourceResolver` API。

## 创建服务用户 {#creating-a-new-service-user}

在您验证AEM服务用户列表中没有任何用户适用于您的用例并且相应的RTC问题已被批准后，您可以继续并将新用户添加到默认内容。

建议的方法是创建服务用户以使用位于的存储库资源管理器 *https://&lt;server>：&lt;port>/crx/explorer/index.jsp*

目标是获得有效的 `jcr:uuid` 属性，通过内容包安装创建用户时必须使用此属性。

您可以通过以下方式创建服务用户：

1. 转到存储库资源管理器： *https://&lt;server>：&lt;port>/crx/explorer/index.jsp*
1. 以管理员身份登录，按 **登录** 屏幕左上角的链接。
1. 接下来，创建您的系统用户并为其命名。 要将用户创建为系统用户，请将中间路径设置为 `system` 并添加可选的子文件夹（具体取决于您的需要）：

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. 验证您的系统用户节点是否如下所示：

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >没有与服务用户关联的mixin类型。 这意味着系统用户将没有访问控制策略。

将相应的.content.xml添加到捆绑包的内容时，请确保已设置 `rep:authorizableId` 主要类型是 `rep:SystemUser`. 它应如下所示：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## 正在向ServiceUserMapper配置添加配置修正 {#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}

要添加从服务到相应系统用户的映射，请为创建工厂配置 [`ServiceUserMapper`](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html) 服务。 要保持此模块化，可以使用 [Sling修正机构](https://issues.apache.org/jira/browse/SLING-3578). 建议在捆绑包中安装此类配置的方法是，使用 [Sling初始内容加载](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html)：

1. 在包的src/main/resources文件夹下创建子文件夹SLING-INF/content
1. 在此文件夹中，创建一个名为org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.modified-&lt;some unique=&quot;&quot; name=&quot;&quot; for=&quot;&quot; your=&quot;&quot; factory=&quot;&quot; configuration=&quot;&quot;>.xml，其中包含工厂配置的内容（包括所有子服务用户映射）。 示例：

1. 创建 `SLING-INF/content` 下的文件夹 `src/main/resources` 文件夹的位置；
1. 在此文件夹中创建文件 `named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml` 包含工厂配置的内容，包括所有子服务用户映射。

   为了便于说明，请获取名为 `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml`：

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

1. 在的配置中引用Sling初始内容 `maven-bundle-plugin` 在 `pom.xml` 您的捆绑包中。 示例：

   ```xml
   <Sling-Initial-Content>
      SLING-INF/content;path:=/libs/system/config;overwrite:=true;
   </Sling-Initial-Content>
   ```

1. 安装捆绑包，并确保已安装工厂配置。 您可以执行以下操作来实现此目标：

   * 转到位于的Web控制台 *https://serverhost:serveraddress/system/console/configMgr*
   * 搜索 **Apache Sling服务用户映射器服务修正**
   * 单击链接以查看是否已正确配置。

## 在服务中处理共享会话 {#dealing-with-shared-sessions-in-services}

调用对象 `loginAdministrative()` 通常与共享会话一起出现。 这些会话是在服务激活时获取的，仅在服务停止后注销。 虽然这是常见的做法，但会导致两个问题：

* **安全性：** 此类管理会话用于缓存和返回绑定到共享会话的资源或其他对象。 稍后在调用栈栈中，这些对象可能会适应具有提升权限的会话或资源解析器，通常调用者并不清楚它们正在与哪个管理会话一起操作。
* **性能：** 在Oak中，共享会话可能会导致性能问题，建议您不要使用它们。

对于安全风险，最显而易见的解决方案是直接更换 `loginAdministrative()` 通过调用 `loginService()` 一对一的权限受限的用户。 但是，这不会对任何潜在的性能下降产生任何影响。 一种缓解方法是，将所有请求的信息封装在与会话无关联的对象中。 然后，根据需要创建（或销毁）会话。

建议的方法是重构服务的API，以便让调用方能够控制会话的创建/销毁。

## JSP中的管理会话 {#administrative-sessions-in-jsps}

JSP无法使用 `loginService()`，因为没有关联的服务。 但是，JSP中的管理会话通常是违反MVC范例的标志。

可通过两种方式修复此问题：

1. 以允许用户会话操作的方式重组内容；
1. 将逻辑提取到提供随后可供JSP使用的API的服务。

第一种方法是首选方法。

## 处理事件、复制预处理程序和作业 {#processing-events-replication-preprocessors-and-jobs}

在处理事件或作业（有时是工作流）时，触发事件的相应会话将丢失。 这会导致事件处理者和作业处理者经常使用管理会话来完成其工作。 解决这一问题有各种可行的方法，每种方法各有其优缺点：

1. 传递 `user-id` 在事件有效负载中，并使用模拟。

   **优点：** 易于使用。

   **缺点：** 仍使用 `loginAdministrative()`. 它会对已经过身份验证的请求进行重新身份验证。

1. 创建或重用有权访问数据的服务用户。

   **优点：** 与当前设计一致。 只需极少的更改。

   **缺点：** 需要强大的服务用户灵活使用，这很容易导致权限提升。 绕过安全模式。

1. 传递序列化 `Subject` 在事件有效负载中，并创建 `ResourceResolver` 基于这个主题。 例如，使用JAAS `doAsPrivileged` 在 `ResourceResolverFactory`.

   **优点：** 从安全角度出发清理实施。 它可避免重新身份验证，并以原始权限操作。 安全相关代码对事件的使用者是透明的。

   **缺点：** 需要重构。 安全相关代码对事件的消费者透明这一事实也可能导致问题。

第三种方法是首选的处理技术。

## 工作流进程 {#workflow-processes}

在工作流进程实施中，触发工作流的相应用户会话将丢失。 这会导致工作流进程经常使用管理会话来执行其工作。

要解决这些问题，建议使用中提到的相同方法 [处理事件、复制预处理程序和作业](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs) 使用。

## SlingPOST处理器和删除的页面 {#sling-post-processors-and-deleted-pages}

SlingPOST处理器实施中使用了一些管理会话。 通常，管理会话用于访问正在处理的POST内挂起的删除节点。 因此，无法再通过请求会话访问它们。 可以访问待删除的节点来公开在其他情况下不应访问的元数据。
