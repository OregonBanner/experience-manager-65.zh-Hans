---
title: AEM 中的封闭用户组
description: 了解封闭用户组及其为AEM中的可扩展性和安全性带来的好处。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 39e35a07-140f-4853-8f0d-8275bce27a65
feature: Security
source-git-commit: e54c1d422f2bf676e8a7b0f50a101e495c869c96
workflow-type: tm+mt
source-wordcount: '6854'
ht-degree: 1%

---

# AEM 中的封闭用户组{#closed-user-groups-in-aem}

## 简介 {#introduction}

自AEM 6.3起，出现了一个新的封闭用户组实施，旨在解决现有实施中存在的性能、可扩展性和安全问题。

>[!NOTE]
>
>为了简单起见，本文档中将使用CUG缩写。

新实施的目标是在需要时涵盖现有功能，同时解决旧版本的问题和设计限制。 最终得到一种具有以下特征的新CUG设计：

* 身份验证和授权要素的明确分离，可以单独使用，也可以结合使用；
* 专用授权模型反映所配置的CUG树上的受限读取访问，而不干扰其它访问控制设置和权限要求；
* 将编写实例时通常需要的受限读取访问权限的访问控制设置与通常只需要在发布时进行的权限评估分开；
* 编辑受限读取访问而不提升权限；
* 专用节点类型扩展标记认证要求；
* 与身份验证要求关联的可选登录路径。

### 新的自定义用户组实施 {#the-new-custom-user-group-implementation}

在AEM上下文中称为CUG，它包含以下步骤：

* 限制对树中需要保护的读取权限，并且仅允许对随给定CUG实例列出或完全从CUG评估中排除的主体进行读取。 这称为 **授权** 元素。
* 在给定树上强制进行身份验证，并（可选）为该树指定随后被排除的专用登录页面。 这称为 **身份验证** 元素。

新实施的设计旨在使身份验证和授权元素之间划出一条界线。 从AEM 6.3开始，可以限制读取访问，而无需明确添加身份验证要求。 例如，如果给定实例完全要求身份验证，或者给定树已驻留在要求身份验证的子树中。

同样，可以在给定树上标记身份验证要求，而无需更改有效权限设置。 合并及结果列于 [将CUG策略和身份验证要求相结合](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement) 部分。

## 概述 {#overview}

### 授权：限制读取访问 {#authorization-restricting-read-access}

CUG的关键功能是限制内容存储库中给定树上除选定承担者外的所有人员的读取权限。 新实施通过定义代表CUG的专用类型的访问控制策略而采用不同的方法，而不是快速操作默认访问控制内容。

#### CUG的访问控制策略 {#access-control-policy-for-cug}

这种新类型的策略具有以下特性：

* org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy类型的访问控制策略（由Apache Jackrabbit API定义）；
* PrincipalSetPolicy将权限授予一组可修改的主体；
* 授予的权限和策略的范围是实施详细信息。

用于表示CUG的PrincipalSetPolicy的实施还定义了：

* CUG策略仅向常规JCR项目授予读访问权限（例如，排除访问控制内容）；
* 范围由拥有CUG策略的接入控制节点定义；
* 可以嵌套CUG策略，嵌套CUG不继承“父”CUG的主体集，启动新的CUG；
* 如果启用了评估，则策略的效果将继承到整个子树直至下一个嵌套CUG。

这些CUG策略通过名为oak-authorization-cug的单独授权模块部署到AEM实例。 此模块带有自己的访问控制管理和权限评估。 换言之，默认的AEM设置会提供一个结合了多个授权机制的Oak内容存储库配置。 有关更多信息，请参阅 [此页面位于Apache Oak文档中](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html).

在此复合设置中，新的CUG不会替换附加到目标节点的现有访问控制内容，而是被设计为补充内容，以后还可以在不影响原始访问控制的情况下将其删除，默认情况下，AEM中的访问控制列表是访问控制列表。

与以前的实施不同，新的CUG策略总是被识别并视为访问控制内容。 这意味着使用JCR访问控制管理API创建和编辑它们。 欲了解更多信息，请参见 [管理CUG策略](#managing-cug-policies) 部分。

#### CUG策略的权限评估 {#permission-evaluation-of-cug-policies}

除了为CUG提供专门的访问控制管理外，新的授权模型还允许您有条件地为其策略启用权限评估。 这样，您便可以在暂存环境中设置CUG策略，并且仅在复制到生产环境后才能启用有效权限评估。

对CUG策略的权限评估以及与默认授权模型或任何其他授权模型的交互遵循为Apache Jackrabbit Oak中的多个授权机制设计的模式：当且仅当所有模型都授予访问权限时，才授予给定权限集。 请参阅 [此页面](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html) 以了解更多详细信息。

以下特征适用于与旨在处理和评估CUG策略的授权模型相关联的权限评估：

* 它仅处理常规节点和属性的读取权限，而不处理读取访问控制内容
* 它不处理修改受保护的JCR内容所需的写权限或任何类型的权限（访问控制、节点类型信息、版本控制、锁定或用户管理等）；这些权限不受CUG策略的影响，并且不会被关联的授权模型评估。 是否授予这些权限取决于安全设置中配置的其他模型。

单个CUG策略对权限评估的影响可概括如下：

* 拒绝每个人的读取权限，但策略中列出的排除主体或主体除外；
* 该策略对保存该策略及其属性的访问控制节点生效；
* 该效果还会沿层级向下继承 — 即由访问控制节点定义的项目树；
* 但是，它不影响访问控制节点的同级或祖先；
* 给定CUG的继承在嵌套CUG处停止。

#### 最佳实践 {#best-practices}

在通过CUG定义受限读取访问时，应考虑以下最佳实践：

* 慎重决定您对CUG的需求是限制读访问还是身份验证要求。 如果是后者，或者同时需要这两者，请查阅最佳实践部分，了解有关身份验证要求的详细信息
* 为需要保护的数据或内容创建威胁模型，以便确定威胁边界，并清楚地了解数据的敏感性和与授权访问相关的角色
* 为存储库内容和CUG建模，以遵循与授权相关的一般方面和最佳实践：

   * 请记住，仅当给定CUG和设置授权中部署的其他模块评估允许给定主题读取给定存储库项目时，才会授予读取权限
   * 避免创建读取访问已被其他授权模块限制的冗余CUG
   * 对嵌套CUG的过度需求可能会突显内容设计中的问题
   * 对CUG的过度需求（例如，在每个页面上）可能表明需要一种自定义授权模型，该模型可能更适合匹配现有应用程序和内容的特定安全需求。

* 将CUG策略支持的路径限制为存储库中的几棵树，以便优化性能。 例如，自AEM 6.3起，仅允许将/content节点下的CUG作为默认值提供。
* CUG策略旨在向一小部分主体授予读取权限。 对大量主体的需求可能会突出显示内容或应用程序设计中的问题，应当重新考虑。

### 身份验证：定义身份验证要求 {#authentication-defining-the-auth-requirement}

CUG功能的与身份验证相关的部分允许您标记需要身份验证的树，并可以选择指定专用登录页面。 根据以前的版本，新的实施允许您在内容存储库中标记需要身份验证的树，并有条件地启用与的同步 `Sling org.apache.sling.api.auth.Authenticator`负责最终强制实施该要求并重定向到登录资源。

这些要求通过OSGi服务向验证者注册，该服务提供 `sling.auth.requirements` 注册属性。 然后，使用这些属性来动态扩展身份验证要求。 欲知更多详情，请参见 [Sling文档](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS).

#### 使用专用Mixin类型定义身份验证要求 {#defining-the-authentication-requirement-with-a-dedicated-mixin-type}

出于安全原因，新的实施将替换为称为的专用mixin类型对剩余JCR属性的使用 `granite:AuthenticationRequired`，为登录路径定义一个类型为STRING的可选属性 `granite:loginPath`. 只有与此mixin类型相关的内容更改才会导致更新在Apache Sling Authenticator中注册的要求。 在保留任何临时修改时会跟踪这些修改，因此需要 `javax.jcr.Session.save()` 号召变得有效。

这同样适用于 `granite:loginPath` 属性。 只有当它由与身份验证要求相关的mixin类型定义时，才会遵守它。 在非结构化JCR节点中添加具有此名称的剩余属性将不会显示所需的效果，并且负责更新OSGi注册的处理程序将忽略该属性。

>[!NOTE]
>
>设置登录路径属性是可选的，并且仅当需要身份验证的树无法回退到默认登录页或继承的登录页时才需要设置。 请参阅 [登录路径评估](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path) 下。

#### 向Sling身份验证器注册身份验证要求和登录路径 {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}

由于此类身份验证要求应仅限于某些运行模式以及内容存储库中的一小部分树，因此跟踪要求mixin类型和登录路径属性是有条件的，并绑定到定义受支持路径的相应配置（请参阅下面的配置选项）。 因此，只有在这些受支持的路径范围内的更改才会触发OSGi注册的更新，而其他地方mixin类型和属性都将被忽略。

默认AEM安装程序现在通过允许以创作运行模式设置mixin来使用此配置，但只有在复制到发布实例时才会生效。 请参阅 [此页面](https://sling.apache.org/documentation/the-sling-engine/authentication/authenticationframework.html) 有关Sling如何实施身份验证要求的详细信息。

添加 `granite:AuthenticationRequired` 配置的支持路径中的mixin类型将导致更新负责处理程序的OSGi注册，其中包含新的、额外的条目 `sling.auth.requirements` 属性。 如果给定的身份验证要求指定了可选 `granite:loginPath` 属性，该值另外会向身份验证器注册一个“ — ”前缀，以便从身份验证要求中排除。

#### 身份验证要求的评估和继承 {#evaluation-and-inheritance-of-the-authentication-requirement}

应通过页面或节点层次结构继承Apache Sling身份验证要求。 继承和身份验证要求评估的详细信息（如顺序和优先级）被视为实施详细信息，本文中不会记录这些详细信息。

#### 登录路径评估 {#evaluation-of-login-path}

评估登录路径并在验证时重定向到相应的资源当前是AdobeGranite登录选择器身份验证处理程序( `com.day.cq.auth.impl.LoginSelectorHandler`)，默认情况下是使用AEM配置的Apache Sling AuthenticationHandler。

调用时 `AuthenticationHandler.requestCredentials` 此处理程序尝试确定用户将被重定向到的映射登录页面。 这包括以下步骤：

* 区分过期密码和需要定期登录作为重定向的原因；
* 如果是常规登录，测试是否可以按照以下顺序获取登录路径：

   * 从由新实施的LoginPathProvider `com.adobe.granite.auth.requirement.impl.RequirementService`，
   * 旧的、已弃用的CUG实施中的
   * 从登录页映射，如与一起定义的 `LoginSelectorHandler`，
   * 最后，回退到默认登录页面，如 `LoginSelectorHandler`.

* 通过以上列出的调用获得有效的登录路径后，用户的请求就会被重定向到该页面。

本文档的目标是对内部公开的登录路径进行评估 `LoginPathProvider` 界面。 自AEM 6.3以来发布的实施具有以下行为：

* 登录路径的注册取决于区分过期密码和需要定期登录才能进行重定向
* 如果定期登录，则测试是否可以按照以下顺序获取登录路径：

   * 从 `LoginPathProvider` 由新版实施 `com.adobe.granite.auth.requirement.impl.RequirementService`，
   * 旧的、已弃用的CUG实施中的
   * 从登录页面映射，如使用 `LoginSelectorHandler`，
   * 最后，回退到与一起定义的默认登录页面。 `LoginSelectorHandler`.

* 通过以上列出的调用获得有效的登录路径后，用户的请求就会被重定向到该页面。

此 `LoginPathProvider` 由Granite中新的身份验证要求支持实施的操作会公开由定义的登录路径 `granite:loginPath` 属性，这些属性又由mixin类型定义，如上所述。 保存登录路径的资源路径与属性值本身的映射将保存在内存中，并将进行评估，以便为层次结构中的其他节点找到合适的登录路径。

>[!NOTE]
>
>评估仅针对与位于所配置的支持路径中的资源相关联的请求执行。 对于任何其他请求，将评估确定登录路径的替代方法。

#### 最佳实践 {#best-practices-1}

定义身份验证要求时，应考虑以下最佳实践：

* 避免嵌套身份验证要求：在树的开头放置单个身份验证要求标记应该就足够了，并且会继承到目标节点定义的整个子树。 应将该树中的其他身份验证要求视为冗余，这可能会导致在评估Apache Sling中的身份验证要求时出现性能问题。 通过分离授权和与验证相关的CUG区域，可以利用CUG或其它类型的策略限制读取访问，同时实施整个树的验证。
* 对存储库内容进行建模，以便身份验证要求适用于整个树，而无需再次从要求中排除嵌套的子树。
* 要避免指定并随后注册冗余登录路径，请执行以下操作：

   * 依赖继承并避免定义嵌套登录路径，
   * 不要将可选登录路径设置为与默认值或继承值对应的值，
   * 应用程序开发人员应确定在与关联的全局登录路径配置（默认和映射）中应配置哪些登录路径。 `LoginSelectorHandler`.

## 存储库中的表示方式 {#representation-in-the-repository}

### 存储库中的CUG策略表示 {#cug-policy-representation-in-the-repository}

Oak文档涵盖了新的CUG策略在存储库内容中的反映方式。 有关更多信息，请参阅 [此页面](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository).

### 存储库中的身份验证要求 {#authentication-requirement-in-the-repository}

将专用mixin节点类型放置在目标节点处的存储库内容中，反映了单独的身份验证要求。 mixin类型定义了一个可选属性，用于为目标节点定义的树指定专用登录页面。

与登录路径关联的页面可以位于该树的内部或外部。 它将被排除在身份验证要求之外。

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## 管理CUG策略和身份验证要求 {#managing-cug-policies-and-authentication-requirement}

### 管理CUG策略 {#managing-cug-policies}

使用JCR访问控制管理API管理用于限制CUG读取访问的新类型访问控制策略，并遵循中所述的机制。 [JCR 2.0规范](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html).

#### 设置新的CUG策略 {#set-a-new-cug-policy}

此代码用于在之前未设置CUG的节点上应用新的CUG策略。 请注意 `getApplicablePolicies` 将仅返回以前未设置的新策略。 最后，策略需要回写，更改需要保留。

```java
String path = [...] // needs to be a supported, absolute path

Principal toAdd1 = [...]
Principal toAdd2 = [...]
Principal toRemove = [...]

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

AccessControlPolicyIterator it = acMgr.getApplicablePolicies(path);
while (it.hasNext()) {
        AccessControlPolicy policy = it.nextAccessControlPolicy();
        if (policy instanceof PrincipalSetPolicy) {
           cugPolicy = (PrincipalSetPolicy) policy;
           break;
        }
}

if (cugPolicy == null) {
   log.debug("no applicable policy"); // path not supported or no applicable policy (for example,
                                                   // the policy was set before)
   return;
}

cugPolicy.addPrincipals(toAdd1, toAdd2);
cugPolicy.removePrincipals(toRemove));

acMgr.setPolicy(path, cugPolicy); // as of this step the policy can be edited/removed
session.save();
```

#### 编辑现有CUG策略 {#edit-an-existing-cug-policy}

编辑现有CUG策略需要执行以下步骤。 请注意，修改后的策略需要回写，并且更改需要通过使用保留 `javax.jcr.Session.save()`.

```java
String path = [...] // needs to be a supported, absolute path

Principal toAdd1 = [...]
Principal toAdd2 = [...]
Principal toRemove = [...]

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

for (AccessControlPolicy policy : acMgr.getPolicies(path)) {
     if (policy instanceof PrincipalSetPolicy) {
        cugPolicy = (PrincipalSetPolicy) policy;
        break;
     }
}

if (cugPolicy == null) {
   log.debug("no policy to edit"); // path not supported or policy not set before
   return;
}

if (cugPolicy.addPrincipals(toAdd1, toAdd2) || cugPolicy.removePrincipals(toRemove)) {
   acMgr.setPolicy(path, cugPolicy);
   session.save();
} else {
     log.debug("cug policy not modified");
}
```

### 检索有效的CUG策略 {#retrieve-effective-cug-policies}

JCR访问控制管理定义了一种尽力而为的方法，用于检索在给定路径上生效的策略。 由于评估CUG策略是有条件的，并且取决于要启用的相应配置，因此，调用 `getEffectivePolicies` 是一种验证给定CUG策略是否在给定安装中生效的简便方法。

>[!NOTE]
>
>请注意以下两者之间的区别 `getEffectivePolicies` 以及后续代码示例，该示例向上遍历层级以查找给定路径是否已是现有CUG的一部分。

```java
String path = [...] // needs to be a supported, absolute path

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

// log an debug message of all CUG policies that take effect at the given path
// there could be zero, one or many (creating nested CUGs is possible)
for (AccessControlPolicy policy : acMgr.getEffectivePolicies(path) {
     if (policy instanceof PrincipalSetPolicy) {
        String policyPath = "-";
        if (policy instanceof JackrabbitAccessControlPolicy) {
           policyPath = ((JackrabbitAccessControlPolicy) policy).getPath();
        }
        log.debug("Found effective CUG for path '{}' at '{}', path, policyPath);
     }
}
```

#### 检索继承的CUG策略 {#retrieve-inherited-cug-policies}

查找已在给定路径定义的所有嵌套CUG，无论它们是否生效。 欲了解更多信息，请参见 [配置选项](/help/sites-administering/closed-user-groups.md#configuration-options) 部分。

```java
String path = [...]

List<AccessControlPolicy> cugPolicies = new ArrayList<AccessControlPolicy>();
while (isSupportedPath(path)) {
     for (AccessControlPolicy policy : acMgr.getPolicies(path)) {
         if (policy instanceof PrincipalSetPolicy) {
            cugPolicies.add(policy);
         }
      }
      path = (PathUtils.denotesRoot(path)) ? null : PathUtils.getAncestorPath(path, 1);
}
```

#### 按主体管理CUG策略 {#managing-cug-policies-by-pincipal}

由定义的扩展 `JackrabbitAccessControlManager` 允许按主体编辑访问控制策略的策略未使用CUG访问控制管理实现，因为根据定义，CUG策略始终影响所有主体：以 `PrincipalSetPolicy` 将被授予读取权限，而所有其他主体将阻止读取目标节点定义的树中的内容。

相应方法始终返回空策略数组，但不会引发异常。

### 管理身份验证要求 {#managing-the-authentication-requirement}

通过更改目标节点的有效节点类型来实现新身份验证要求的创建、修改或移除。 然后，可以使用常规JCR API写入可选的登录路径属性。

>[!NOTE]
>
>对于上述给定目标节点的修改，如果 `RequirementHandler` 已配置，并且目标包含在由支持的路径定义的树中（请参阅配置选项部分）。
>
>有关更多信息，请参阅 [分配Mixin节点类型](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3分配Mixin节点类型)和 [添加节点并设置属性](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4添加节点并设置属性)

#### 添加新的身份验证要求 {#adding-a-new-auth-requirement}

下面详细说明了创建新身份验证要求的步骤。 请注意，只有在满足以下条件时，才会向Apache Sling Authenticator注册该要求： `RequirementHandler` 已为包含目标节点的树进行了配置。

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### 使用登录路径添加新身份验证要求 {#add-a-new-auth-requirement-with-login-path}

创建新的身份验证要求（包括登录路径）的步骤。 请注意，只有在符合以下条件时，才会向Apache Sling身份验证器注册登录路径的要求和排除项： `RequirementHandler` 已为包含目标节点的树进行了配置。

```java
Node targetNode = [...]
String loginPath = [...] // STRING property

Node targetNode = session.getNode(path);
targetNode.addMixin("granite:AuthenticationRequired");

targetNode.setProperty("granite:loginPath", loginPath);
session.save();
```

#### 修改现有登录路径 {#modify-an-existing-login-path}

下面详细说明了更改现有登录路径的步骤。 仅当出现以下情况时，该修改才会注册到Apache Sling身份验证器： `RequirementHandler` 已为包含目标节点的树进行了配置。 上一个登录路径值将从注册中删除。 此修改不会影响与目标节点关联的身份验证要求。

```java
Node targetNode = [...]
String newLoginPath = [...] // STRING property

if (targetNode.isNodeType("granite:AuthenticationRequired")) {
   targetNode.setProperty("granite:loginPath", newLoginPath);
   session.save();
} else {
     log.debug("cannot modify login path property; mixin type missing");
}
```

#### 删除现有登录路径 {#remove-an-existing-login-path}

删除现有登录路径的步骤。 仅当满足以下条件时，登录路径条目才会从Apache Sling身份验证器中注销： `RequirementHandler` 已为包含目标节点的树进行了配置。 不影响与目标节点关联的身份验证要求。

```java
Node targetNode = [...]

if (targetNode.hasProperty("granite:loginPath") &&
   targetNode.isNodeType("granite:AuthenticationRequired")) {
   targetNode.setProperty("granite:loginPath", null);
   session.save();
} else {
     log.debug("cannot remove login path property; mixin type missing");
}
```

或者，您也可以使用以下方法来达到相同目的：

```java
String path = [...] // absolute path to target node

String propertyPath = PathUtils.concat(path, "granite:loginPath");
if (session.propertyExists(propertyPath)) {
    session.getProperty(propertyPath).remove();
    // or: session.removeItem(propertyPath);
    session.save();
}
```

#### 删除身份验证要求 {#remove-an-auth-requirement}

删除现有身份验证要求的步骤。 仅当满足以下条件时，才会从Apache Sling Authenticator取消注册该要求： `RequirementHandler` 已为包含目标节点的树进行了配置。

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### 检索有效的身份验证要求 {#retrieve-effective-auth-requirements}

没有专用公共API来读取在Apache Sling Authenticator中注册的所有有效身份验证要求。 但是，该列表会显示在位于的系统控制台中 `https://<serveraddress>:<serverport>/system/console/slingauth` 在&quot;**身份验证要求配置**“ ”部分。

下图显示了包含演示内容的AEM发布实例的身份验证要求。 社区页面中突出显示的路径说明了本文档中描述的实施添加的要求如何反映在Apache Sling身份验证程序中。

>[!NOTE]
>
>在此示例中，未设置可选的登录路径属性。 因此，没有向验证者登记第二项。

![chlimage_1-24](assets/chlimage_1-24.jpeg)

#### 检索有效登录路径 {#retrieve-the-effective-login-path}

目前没有公共API来检索匿名访问需要身份验证的资源时将生效的登录路径。 有关如何检索登录路径的实施详细信息，请参阅登录路径评估部分。

但是，请注意，除了使用此功能定义的登录路径之外，还有其他方法可以指定到登录的重定向，在设计内容模型和给定AEM安装的身份验证要求时，应当考虑这些方法。

#### 检索继承的身份验证要求 {#retrieve-the-inherited-auth-requirement}

与登录路径一样，没有公共API来检索内容中定义的继承身份验证要求。 以下示例说明如何列出使用给定层次结构定义的所有身份验证要求，而不管它们是否生效。 有关更多信息，请参阅 [配置选项](/help/sites-administering/closed-user-groups.md#configuration-options).

>[!NOTE]
>
>建议依赖继承机制来满足身份验证要求和登录路径，并避免创建嵌套身份验证要求。
>
>有关详细信息，请参阅 [身份验证要求的评估和继承](#evaluation-and-inheritance-of-the-authentication-requirement)， [登录路径评估](#evaluation-of-login-path) 和 [最佳实践](#best-practices).

```java
String path = [...]
Node node = session.getNode(path);

Map<String, String> authRequirements = new ArrayList<String, String>();
while (isSupported(node)) {
     if (node.isNodeType("granite:AuthenticationRequired")) {
         String loginPath = (node.hasProperty("granite:loginPath") ?
                                     node.getProperty("granite:loginPath").getString() :
                                     "";
        authRequirements.put(node.getPath(), loginPath);
        node = node.getParent();
     }
}
```

### 将CUG策略和身份验证要求相结合 {#combining-cug-policies-and-the-authentication-requirement}

下表列出了AEM实例中CUG策略的有效组合以及身份验证要求，该实例通过配置启用了这两个模块。

| **需要身份验证** | **登录路径** | **受限的读取访问** | **预期效果** |
|---|---|---|---|
| 是 | 是 | 是 | 如果有效的权限评估授予访问权限，给定用户将只能查看标记为CUG策略的子树。 未经身份验证的用户将被重定向到指定的登录页面。 |
| 是 | 否 | 是 | 如果有效的权限评估授予访问权限，给定用户将只能查看标记为CUG策略的子树。 未经身份验证的用户将被重定向到继承的默认登录页面。 |
| 是 | 是 | 否 | 未经身份验证的用户将被重定向到指定的登录页面。 是否允许查看标有身份验证要求的树取决于该子树中包含的个别项的有效权限。 没有专用的CUG限制读取访问。 |
| 是 | 否 | 否 | 未经身份验证的用户将被重定向到继承的默认登录页面。 是否允许查看标记有身份验证要求的树，取决于该子树中包含的个别项的有效权限。 没有专用的CUG限制读取访问。 |
| 否 | 否 | 是 | 如果有效的权限评估授予访问权限，则给定的经过身份验证或未经过身份验证的用户将只能查看标记有CUG策略的子树。 未经身份验证的用户将被同等对待，并且不会被重定向到登录。 |

>[!NOTE]
>
>“Authentication Requirement”=“No”和“Login Path”=“Yes”的组合未列出，因为“Login Path”是与Auth-Requirement关联的可选属性。 在不添加定义mixin类型的情况下指定具有该名称的JCR属性将没有效果，并且将被相应的处理程序忽略。

## OSGi组件和配置 {#osgi-components-and-configuration}

本节概述了OSGi组件以及新的CUG实施中引入的各个配置选项。

另请参阅CUG映射文档，以全面映射旧实施和新实施之间的配置选项。

### 授权：设置和配置 {#authorization-setup-and-configuration}

新的授权相关部分包含在 **Oak CUG授权** 捆绑( `org.apache.jackrabbit.oak-authorization-cug`)，它是AEM默认安装的一部分。 该捆绑包定义了一个单独的授权模型，旨在作为管理读取访问权限的附加方式部署。

#### 设置CUG授权 {#setting-up-cug-authorization}

有关设置CUG授权的详细说明，请参见 [相关Apache文档](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability). 默认情况下，AEM在所有运行模式下都部署了CUG授权。 分步说明还可用于在那些需要不同的授权设置的安装中禁用CUG授权。

#### 配置反向链接过滤器 {#configuring-the-referrer-filter}

您还需要配置 [Sling引用过滤器](/help/sites-administering/security-checklist.md#the-sling-referrer-filter) 所有可用于访问AEM的主机名；例如，通过CDN、负载平衡器和任何其他。

如果未配置反向链接筛选条件，则当用户尝试登录CUG网站时，会看到与以下内容类似的错误：

```shell
31.01.2017 13:49:42.321 *INFO* [qtp1263731568-346] org.apache.sling.security.impl.ReferrerFilter Rejected referrer header for POST request to /libs/granite/core/content/login.html/j_security_check : https://hostname/libs/granite/core/content/login.html?resource=%2Fcontent%2Fgeometrixx%2Fen%2Ftest-site%2Ftest-page.html&$$login$$=%24%24login%24%24&j_reason=unknown&j_reason_code=unknown
```

#### OSGi组件的特性 {#characteristics-of-osgi-components}

引入了以下两个OSGi组件来定义身份验证要求并指定专用登录路径：

* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration`
* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl`

**org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration**

<table>
 <tbody>
  <tr>
   <td>标签</td>
   <td>Apache Jackrabbit Oak CUG配置</td>
  </tr>
  <tr>
   <td>描述</td>
   <td>专门用于设置和评估CUG权限的授权配置。</td>
  </tr>
  <tr>
   <td>配置属性</td>
   <td>
    <ul>
     <li><code>cugSupportedPaths</code></li>
     <li><code>cugEnabled</code></li>
     <li><code>configurationRanking</code></li>
    </ul> <p>另请参阅 <a href="#configuration-options">配置选项</a> 下。</p> </td>
  </tr>
  <tr>
   <td>配置策略</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>引用</td>
   <td><code>CugExclude (ReferenceCardinality.OPTIONAL_UNARY)</code></td>
  </tr>
 </tbody>
</table>

**org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl**

<table>
 <tbody>
  <tr>
   <td>标签</td>
   <td>Apache Jackrabbit Oak CUG排除列表</td>
  </tr>
  <tr>
   <td>描述</td>
   <td>允许您从CUG评估中排除具有已配置名称的主体。</td>
  </tr>
  <tr>
   <td>配置属性</td>
   <td>
    <ul>
     <li><code>principalNames</code></li>
    </ul> <p>另请参阅下面的配置选项部分。</p> </td>
  </tr>
  <tr>
   <td>配置策略</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>引用</td>
   <td>NA</td>
  </tr>
 </tbody>
</table>

#### 配置选项 {#configuration-options}

关键配置选项包括：

* `cugSupportedPaths`：指定可能包含CUG的子树。 未设置默认值
* `cugEnabled`：配置选项，用于启用当前CUG策略的权限评估。

与CUG-authorization模块相关的可用配置选项在下列位置列出并详细说明： [Apache Oak文档](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration).

#### 从CUG评估中排除承担者 {#excluding-principals-from-cug-evaluation}

在前一实施中，已采用免除个人主参与者的CUG评估。 新的CUG授权通过名为CugExclude的专用接口覆盖这一点。 Apache Jackrabbit Oak 1.4附带默认实施，该实施不包括固定主体集以及允许配置单个主体名称的扩展实施。 后者在AEM发布实例中配置。

自AEM 6.3起的默认设置可防止以下主体受CUG策略的影响：

* 管理主体（管理员用户、管理员组）
* 服务用户主体
* 存储库内部系统主体

有关详细信息，请参见 [自AEM 6.3以来的默认配置](#default-configuration-since-aem) 部分。

可以在system console的configuration部分更改或扩展“administrators”组的排除 **Apache Jackrabbit Oak CUG排除列表**.

或者，可以提供并部署CugExclude接口的自定义实现，以调整排除的承担者集以满足特殊需求。 请参阅相关文档 [CUG可插拔性](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) 详细信息和实施示例。

### 身份验证：设置和配置 {#authentication-setup-and-configuration}

新的身份验证相关部分包含在 **AdobeGranite身份验证处理程序** 捆绑( `com.adobe.granite.auth.authhandler` 版本5.6.48)。 此捆绑包是AEM默认安装的一部分。

要设置身份验证要求以取代已弃用的CUG支持，某些OSGi组件必须在给定AEM安装中存在并处于活动状态。 有关更多详细信息，请参阅 **OSGi组件的特性** 下。

>[!NOTE]
>
>由于RequirementHandler具有强制配置选项，因此，仅当通过指定一组受支持的路径来启用该功能时，与身份验证相关的部分才会处于活动状态。 在标准AEM安装中，该功能在创作运行模式下禁用，在发布运行模式下为/content启用。

**OSGi组件的特性**

引入了以下两个OSGi组件来定义身份验证要求并指定专用登录路径：

* `com.adobe.granite.auth.requirement.impl.RequirementService`
* `com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler`

**com.adobe.granite.auth.requirement.impl.RequirementService**

<table>
 <tbody>
  <tr>
   <td>标签</td>
   <td>-</td>
  </tr>
  <tr>
   <td>描述</td>
   <td>用于身份验证要求的专用OSGi服务，为影响身份验证要求的内容更改注册观察者(通过 <code>granite:AuthenticationRequirement</code> mixin type)和的登录路径会向 <code>LoginSelectorHandler</code>. </td>
  </tr>
  <tr>
   <td>配置属性</td>
   <td>-</td>
  </tr>
  <tr>
   <td>配置策略</td>
   <td><code>ConfigurationPolicy.OPTIONAL</code></td>
  </tr>
  <tr>
   <td>引用</td>
   <td>
    <ul>
     <li><code>RequirementHandler (ReferenceCardinality.MANDATORY_UNARY)</code></li>
     <li><code>Executor (ReferenceCardinality.MANDATORY_UNARY)</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

**com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler**

| 标签 | AdobeGranite身份验证要求和登录路径处理程序 |
|---|---|
| 描述 | `RequirementHandler` 实施更新Apache Sling身份验证要求以及关联登录路径的相应排除项。 |
| 配置属性 | `supportedPaths` |
| 配置策略 | `ConfigurationPolicy.REQUIRE` |
| 引用 | NA |

#### 配置选项 {#configuration-options-1}

CUG重写的身份验证相关部分只附带一个与AdobeGranite身份验证要求和登录路径处理程序关联的配置选项：

**“身份验证要求和登录路径处理程序”**

<table>
 <tbody>
  <tr>
   <td>属性</td>
   <td>类型</td>
   <td>默认值</td>
   <td>描述</td>
  </tr>
  <tr>
   <td><p>标签=支持的路径</p> <p>名称= 'supportedPaths'</p> </td>
   <td>设置&lt;string&gt;</td>
   <td>-</td>
   <td>此处理程序将遵循身份验证要求的路径。 如果要添加 <code>granite:AuthenticationRequirement</code> mixin类型到节点而无需强制执行这些操作（例如，在创作实例上）。 如果缺少，则禁用该功能。 </td>
  </tr>
 </tbody>
</table>

## 自AEM 6.3以来的默认配置 {#default-configuration-since-aem}

默认情况下，新安装的AEM将新实施用于CUG功能的授权和与身份验证相关的部分。 旧实施“AdobeGranite封闭用户组(CUG)支持”已被弃用，并将在所有AEM安装中默认禁用。 新的实施将改为按以下方式启用：

### 创作实例 {#author-instances}

| **“Apache Jackrabbit Oak CUG配置”** | **解释** |
|---|---|
| 支持的路径 `/content` | 已启用CUGpolicies的访问控制管理。 |
| CUG评估启用FALSE | 已禁用权限评估。 CUG政策不起作用。 |
| 等级 | 200 | 请参阅Oak文档。 |

>[!NOTE]
>
>没有配置 **Apache Jackrabbit Oak CUG排除列表** 和 **AdobeGranite身份验证要求和登录路径处理程序** 在默认创作实例中存在。

### 发布实例 {#publish-instances}

| **“Apache Jackrabbit Oak CUG配置”** | **解释** |
|---|---|
| 支持的路径 `/content` | 在配置的路径下启用了CUG策略的访问控制管理。 |
| CUG评估已启用TRUE | 在配置的路径下启用了权限评估。 CUG政策生效日期 `Session.save()`. |
| 等级 | 200 | 请参阅Oak文档。 |

| **“Apache Jackrabbit Oak CUG排除列表”** | **解释** |
|---|---|
| 主体名称管理员 | 不包括CUG评估中的管理员主体。 |

| **“AdobeGranite身份验证要求和登录路径处理程序”** | **解释** |
|---|---|
| 支持的路径  `/content` | 在存储库中定义的身份验证要求，通过 `granite:AuthenticationRequired` mixin类型在下方生效 `/content` 于 `Session.save()`. Sling身份验证器已更新。 在支持的路径之外添加mixin类型会被忽略。 |

## 禁用CUG授权和身份验证要求 {#disabling-cug-authorization-and-authentication-requirement}

如果给定的安装不使用CUG或使用不同的身份验证和授权方式，则可以完全禁用新实施。

### 禁用CUG授权 {#disable-cug-authorization}

请参阅 [CUG可插拔性](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) 有关如何从复合授权设置中删除CUG授权模型的详细信息，请参阅文档。

### 禁用身份验证要求 {#disable-the-authentication-requirement}

为了禁用对身份验证要求的支持， `granite.auth.authhandler` 模块足以删除与关联的配置 **AdobeGranite身份验证要求和登录路径处理程序**.

>[!NOTE]
>
>但请注意，删除配置将不会取消注册mixin类型，该类型仍适用于未生效的节点。

## 与其他模块的交互 {#interaction-with-other-modules}

### Apache Jackrabbit API {#apache-jackrabbit-api}

为了反映CUG授权模型使用的新类型的访问控制策略，对Apache Jackrabbit定义的API进行了扩展。 从版本2.11.0开始的 `jackrabbit-api` 模块定义一个名为的新接口 `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`，扩展自 `javax.jcr.security.AccessControlPolicy`.

### Apache Jackrabbit FileVault {#apache-jackrabbit-filevault}

为处理类型的访问控制策略，对Apache Jackrabbit FileVault的导入机制进行了调整 `PrincipalSetPolicy`.

### Apache Sling内容分发 {#apache-sling-content-distribution}

请参阅上文 [Apache Jackrabbit FileVault](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault) 部分。

### AdobeGranite复制 {#adobe-granite-replication}

为了能够在不同的AEM实例之间复制CUG策略，稍微调整了复制模块：

* `DurboImportConfiguration.isImportAcl()` 将按字面解释，并且只影响实施的访问控制策略 `javax.jcr.security.AccessControlList`

* `DurboImportTransformer` 只对真正的ACL遵守此配置
* 其他政策，例如 `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy` 将始终复制由CUG授权模型创建的实例，并且配置选项 `DurboImportConfiguration.isImportAcl`()将被忽略。

复制CUG策略有一个限制。 如果删除了给定的CUG策略而没有删除相应的mixin节点类型 `rep:CugMixin,` 复制时将不会反映删除。 通过在删除策略时始终删除mixin解决了此问题。 但是，如果手动添加mixin类型，则可能会显示此限制。

### AdobeGranite身份验证处理程序 {#adobe-granite-authentication-handler}

身份验证处理程序 **AdobeGranite HTTP标头身份验证处理程序** 随附的 `com.adobe.granite.auth.authhandler` 束保存对 `CugSupport` 由同一模块定义的接口。 它用于在特定情况下计算“领域”，回退到使用处理程序配置的领域。

该名称已调整，以引用 `CugSupport` 可选，以确保在给定设置决定重新启用已弃用的实施时实现最大向后兼容性。 使用该实施的安装将不再从CUG实施中提取领域，而是始终显示定义的领域 **AdobeGranite HTTP标头身份验证处理程序**.

>[!NOTE]
>
>默认情况下， **AdobeGranite HTTP标头身份验证处理程序** 仅在发布运行模式下使用“禁用登录页面”( `auth.http.nologin`)选项已启用。

### AEM LiveCopy {#aem-livecopy}

在存储库中配置CUG与LiveCopy时，会添加一个额外的节点和一个额外的属性，如下所示：

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

这两个元素均创建于 `cq:Page`. 对于当前设计，MSM仅处理 `cq:PageContent` (`jcr:content`)节点。

因此，CUG组无法从Blueprint转出到Live Copies。 请在配置 Live Copy 时对此进行规划。

## 对新的CUG实施进行的更改 {#changes-with-the-new-cug-implementation}

本节旨在概述对CUG功能所做的更改，并比较新旧实施。 其中列出了影响CUG支持配置方式的更改，并描述了在存储库内容中如何以及谁管理CUG。

### CUG设置和配置的差异 {#differences-in-cug-setup-and-configuration}

已弃用的OSGi组件 **AdobeGranite封闭用户组(CUG)支持** ( `com.day.cq.auth.impl.cug.CugSupportImpl`)已被新组件取代，以便能够单独处理以前CUG功能的授权和身份验证相关部分。

## 管理存储库内容中的CUG的区别 {#differences-in-managing-cugs-in-the-repository-content}

以下各节从实施和安全角度介绍了新旧实施之间的差异。 虽然新实施旨在提供相同的功能，但在使用新CUG时，务必要了解一些细微的变化。

### 与授权有关的差异 {#differences-with-regards-to-authorization}

授权方面的主要区别概述于以下列表：

**CUG的专用访问控制内容**

在旧实施中，默认授权模型用于处理发布时的访问控制列表策略，按照CUG要求的设置替换任何现有的ACE。 触发此问题的方法是，编写在发布时解释的常规、剩余JCR属性。

在新实施中，默认授权模型的访问控制设置不受任何正在创建、修改或删除的CUG的影响。 而是使用一种名为的新策略类型 `PrincipalSetPolicy` 作为目标节点的附加访问控制内容应用。 此附加策略将被定位为目标节点的子节点，并且如果存在，将成为默认策略节点的同级。

**在访问控制管理中编辑CUG策略**

从剩余的JCR属性迁移到专用的访问控制策略会影响创建或修改CUG功能的授权部分所需的权限。 由于这被视为对访问控制内容的修改，因此它需要 `jcr:readAccessControl` 和 `jcr:modifyAccessControl` 权限以写入存储库。 因此，只有有权修改页面的访问控制内容的内容作者才能设置或修改此内容。 这与旧实施形成对比，旧实施写入常规JCR属性的能力已经足够，从而导致权限提升。

**策略定义的目标节点**

CUG策略应在JCR节点创建，以定义子树接受受限的读取访问。 如果预计CUG会影响整个树，则这可能是一个AEM页面。

请注意，仅将CUG策略放置在给定页面下方的jcr：content节点上，将只会限制对给定页面内容s.str的访问，而不会对任何同级页面或子页面生效。 这可能是有效的用例，并且可以使用允许应用细粒度访问内容的存储库编辑器实现。 但是，它与以前的实施形成了对比，以前的实施是在jcr：content节点上放置cq：cugEnabled属性时，将内部重新映射到页面节点。 不再执行此映射。

**使用CUG策略进行权限评估**

从旧的CUG支持迁移到额外的授权模型，改变了评估有效读取权限的方式。 如 [Jackrabbit文档](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)，允许给定主体查看 `CUGcontent` 只有当Oak存储库中配置的所有模型的权限评估授予读取权限时，才会授予读取权限。

换言之，对于有效权限的评估，既有 `CUGPolicy` 默认访问控制条目将被考虑在内，只有在这两种策略都授予了CUG内容的情况下，才会授予对该内容的读取权限。 在默认AEM发布安装中，对完整版的读取权限 `/content` 树被授予每个人，CUG政策的效果将与旧实施相同。

**按需评估**

CUG授权模型允许单独打开访问控制管理和权限评估：

* 如果模块具有一个或多个支持创建CUG的路径，则会启用访问控制管理
* 仅当选项为时才启用权限评估 **CUG评估已启用** 另外还被选中。

在对CUG策略进行的新的AEM默认设置评估中，仅在“发布”运行模式下启用它。 欲知详情，请参见 [自AEM 6.3以来的默认配置](#default-configuration-since-aem) 以了解更多详细信息。 这可以通过比较给定路径的有效策略与内容中存储的策略来验证。 只有启用CUG的权限评估后，才会显示有效的策略。

如上所述，CUG访问控制策略现在始终存储在内容中，但只有在以下情况下，才会强制评估由这些策略产生的有效权限 **CUG评估已启用** 在Apache Jackrabbit Oak的系统控制台中打开 **cug配置。** 默认情况下，它仅在“发布”运行模式下启用。

### 与身份验证有关的差异 {#differences-with-regards-to-authentication}

与身份验证有关的区别如下所述。

#### 身份验证要求的专用Mixin类型 {#dedicated-mixin-type-for-authentication-requirement}

在以前的实现中，CUG的授权和身份验证两个层面都是由一个JCR属性( `cq:cugEnabled`)。 就身份验证而言，这导致更新了随Apache Sling Authenticator实施一起存储的身份验证要求列表。 在新实施中，通过用专用的mixin类型( `granite:AuthenticationRequired`)。

#### 用于排除登录路径的属性 {#property-for-excluding-login-path}

mixin类型定义一个名为的可选属性 `granite:loginPath`，基本上对应于 `cq:cugLoginPage` 属性。 与以前的实现不同，登录路径属性仅在其声明节点类型是上面提到的mixin时才被考虑。 添加具有此名称的属性而不设置mixin类型不会产生任何效果，并且不会向身份验证程序报告对登录路径的新要求或排除项。

#### 身份验证要求的权限 {#privilege-for-authentication-requirement}

添加或删除mixin类型需要 `jcr:nodeTypeManagement` 正在授予权限。 在上一个实施中， `jcr:modifyProperties` 权限用于编辑剩余属性。

至此 `granite:loginPath` 关注添加、修改或删除属性需要相同的权限。

#### 由Mixin类型定义的目标节点 {#target-node-defined-by-mixin-type}

身份验证要求应在JCR节点创建，该节点定义要强制登录的子树。 如果预计CUG会影响整个树，则这可能是AEM页面，并且新实现的UI随后将在页面节点上添加身份验证要求mixin类型。

仅将CUG策略放在给定页面下方的jcr：content节点上，将只会限制对内容的访问，而不会影响页面节点本身或任何子页面。

这可能是有效的方案，并且可以在允许将mixin放置在任何节点的存储库编辑器中实现。 但是，该行为与以前的实施相反，在前一种实施中，对jcr：content节点放置cq：cugEnabled或cq：cugLoginPage属性最终会在内部重新映射到页面节点。 不再执行此映射。

#### 已配置支持的路径 {#configured-supported-paths}

两者都是 `granite:AuthenticationRequired` mixin类型和granite：loginPath属性将只遵循以下规则集定义的范围： **支持的路径** 配置选项与 **AdobeGranite身份验证要求和登录路径处理程序**. 如果未指定路径，则身份验证要求功能将完全禁用。 在这种情况下，将mixin类型nor属性添加到给定JCR节点或对其进行设置时，它们将生效。

### JCR内容、OSGi服务和配置的映射 {#mapping-of-jcr-content-osgi-services-and-configurations}

以下文档提供了旧实施与新实施之间的OSGi服务、配置和存储库内容的全面映射。

AEM 6.3之后的CUG映射

[获取文件](assets/cug-mapping.pdf)

## 升级CUG {#upgrade-cug}

### 使用已弃用CUG的现有安装 {#existing-installations-using-the-deprecated-cug}

旧的CUG支持实施已弃用，并将在未来版本中删除。 从AEM 6.3之前的版本升级时，建议迁移到新实施。

对于升级后的AEM安装，请务必确保仅启用一个CUG实施。 新旧弃用的CUG支持组合未经测试，并且可能会导致意外行为：

* Sling身份验证程序中与身份验证要求相关的冲突
* 当与旧CUG关联的ACL设置与新CUG策略冲突时，拒绝读取访问。

### 迁移现有CUG内容 {#migrating-existing-cug-content}

Adobe提供了迁移到新的CUG实施的工具。 要使用它，请执行以下步骤：

1. 转到 `https://<serveraddress>:<serverport>/system/console/cug-migration` 以访问该工具。
1. 输入要检查CUG的根路径，然后按 **执行试运行** 按钮。 这将扫描选定位置中符合转换条件的CUG。
1. 查看结果后，按 **执行迁移** 按钮以迁移到新实施。

>[!NOTE]
>
>如果您遇到问题，可以在以下位置设置特定记录器： **调试** 级别 `com.day.cq.auth.impl.cug` 以获取迁移工具的输出。 请参阅 [记录](/help/sites-deploying/configure-logging.md) 以了解有关如何执行此操作的更多信息。
