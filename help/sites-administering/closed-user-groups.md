---
title: AEM中的已关闭用户组
seo-title: AEM中的已关闭用户组
description: 了解AEM中的已关闭用户组。
seo-description: 了解AEM中的已关闭用户组。
uuid: 83396163-86ce-406b-b797-2457ed975ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: a2bd7045-970f-4245-ad5d-a272a654df0a
docset: aem65
exl-id: 39e35a07-140f-4853-8f0d-8275bce27a65
feature: 安全
source-git-commit: cb4b0cb60b8709beea3da70495a15edc8c4831b8
workflow-type: tm+mt
source-wordcount: '6886'
ht-degree: 0%

---

# AEM{#closed-user-groups-in-aem}中的已关闭用户组

## 简介 {#introduction}

自AEM 6.3起，新的封闭用户组实施旨在解决现有实施存在的性能、可伸缩性和安全问题。

>[!NOTE]
>
>为了简单起见，本文档中将使用CUG缩写。

新实施的目标是在需要时覆盖现有功能，同时解决旧版本中的问题和设计限制。 其结果是新的CUG设计，具有以下特点：

* 验证和授权元素的明确分离，可单独或组合使用；
* 专用授权模型，在配置的CUG树上反映受限读取访问，而不干扰其他访问控制设置和权限要求；
* 将创作实例通常需要的受限读取访问权限的访问控制设置与发布时通常只需要的权限评估分开；
* 编辑受限读取访问，而不提升权限；
* 专用节点类型扩展标记认证要求；
* 与身份验证要求关联的可选登录路径。

### 新的自定义用户组实施{#the-new-custom-user-group-implementation}

在AEM上下文中称为CUG的步骤如下：

* 在需要保护的树上限制读取访问，并且仅允许读取与给定CUG实例一起列出或完全从CUG评估中排除的承担者。 这称为&#x200B;**authorization**&#x200B;元素。
* 对给定树强制进行身份验证，并（可选）为该树指定随后被排除的专用登录页。 这称为&#x200B;**authentication**&#x200B;元素。

新实施旨在在身份验证和授权元素之间划出一条线。 从AEM 6.3开始，可以在不显式添加身份验证要求的情况下限制读取访问。 例如，如果给定实例完全需要身份验证，或者给定树已驻留在需要身份验证的子树中。

同样，给定的树可以用验证要求进行标记，而无需更改有效的许可设置。 这些组合和结果列在[Combining CUG Policies and the Authentication Requirement](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement)部分。

## 概述 {#overview}

### 授权：限制读取访问{#authorization-restricting-read-access}

CUG的主要功能是限制内容存储库中除选定承担者之外的所有人对给定树的读取访问权限。 新实施不会即时处理默认的访问控制内容，而是采用不同的方法来定义代表CUG的专用类型的访问控制策略。

#### CUG {#access-control-policy-for-cug}的访问控制策略

这种新型策略具有以下特征：

* org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy类型的访问控制策略（由Apache Jackrabbit API定义）；
* PrincipalSetPolicy授予可修改的一组主体的权限；
* 授予的权限和策略的范围是实施详细信息。

此外，用于表示CUG的PrincipalSetPolicy的实施还定义了：

* CUG策略仅授予对常规JCR项的读取权限（例如，排除访问控制内容）；
* 该范围由包含CUG策略的访问控制节点定义；
* 可以嵌套CUG策略，嵌套的CUG启动新CUG，而不继承“父”CUG的主集；
* 如果启用了评估，则策略的效果会继承到下一个嵌套CUG的整个子树。

这些CUG策略通过名为oak-authorization-cug的单独授权模块部署到AEM实例。 本模块提供了自己的访问控制管理和权限评估。 换句话说，默认的AEM设置提供了Oak内容存储库配置，该配置结合了多种授权机制。 有关更多信息，请参阅Apache Oak文档](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)上的[此页面。

在此复合设置中，新的CUG不会替换附加到目标节点的现有访问控制内容，而是设计为补充内容，此补充内容也可在以后删除，而不会影响原始访问控制，在AEM中默认为访问控制列表。

与以前的实施不同，新的CUG策略始终被识别并视为访问控制内容。 这意味着它们是使用JCR访问控制管理API创建和编辑的。 有关更多信息，请参阅[管理CUG策略](#managing-cug-policies)一节。

#### CUG策略的权限评估{#permission-evaluation-of-cug-policies}

除了针对CUG的专用访问控制管理之外，新授权模型还允许有条件地启用对其策略的许可评估。 这允许在暂存环境中设置CUG策略，并且仅在复制到生产环境后才允许评估有效权限。

CUG策略的权限评估以及与默认或任何其他授权模型的交互遵循为Apache Jackrabbit Oak中的多个授权机制设计的模式：仅当且仅当所有模型授予访问权限时，才会授予给定的一组权限。 有关更多详细信息，请参阅[此页面](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)。

以下特征适用于与用于处理和评估CUG策略的授权模型相关的权限评估：

* 它仅处理常规节点和属性的读取权限，而不处理访问控制内容
* 它不处理修改受保护的JCR内容（访问控制、节点类型信息、版本控制、锁定或用户管理等）所需的写入权限或任何类型的权限；这些权限不受CUG策略的影响，并且不会由关联的授权模型来评估。 是否授予这些权限取决于在安全设置中配置的其他模型。

单个CUG策略对权限评估的影响可概括如下：

* 除了包含策略中列出的被排除的主体或主体的主体之外，所有人都被拒绝读取；
* 该策略对包含该策略的接入控制节点及其属性生效；
* 此效果在层级结构下被继承，即由访问控制节点定义的项目树；
* 但是，它不影响访问控制节点的同级或祖先；
* 给定CUG的继承将在嵌套CUG处停止。

#### 最佳实践 {#best-practices}

在定义通过CUG的受限读取访问时，应考虑以下最佳实践：

* 有意识地决定您对CUG的需求是关于限制读取访问还是验证要求。 如果是后者，或者如果需要两者，请查阅“最佳实践”一节，以了解有关身份验证要求的详细信息
* 为需要保护的数据或内容创建威胁模型，以确定威胁边界并清楚了解数据的敏感性以及与授权访问相关的角色
* 为存储库内容和CUG建模时，应牢记一般授权相关方面和最佳实践：

   * 请记住，仅当给定CUG和对设置授予中部署的其他模块的评估允许给定主体读取给定存储库项目时，才会授予读取权限
   * 避免创建冗余CUG，在这些CUG中，读取访问已被其他授权模块限制
   * 对嵌套CUG的过度需求可能会突出显示内容设计中的问题
   * 对CUG的过度需求（例如，在每个单页上）可能表明需要一个自定义授权模型，这种模型可能更适合满足应用程序和手头内容的特定安全需求。

* 将CUG策略支持的路径限制为存储库中的几个树，以便优化性能。 例如，仅允许在/content节点下的CUG作为自AEM 6.3以来的默认值提供。
* CUG策略旨在授予对一组小主体的读取权限。 需要大量原则可能会突出内容或应用程序设计中的问题，应重新考虑。

### 身份验证：定义身份验证要求{#authentication-defining-the-auth-requirement}

CUG功能的与身份验证相关的部分允许标记需要身份验证的树并可选地指定专用登录页面。 根据以前的版本，新实施允许标记需要在内容存储库中进行身份验证的树，并有条件地启用与`Sling org.apache.sling.api.auth.Authenticator`的同步，该负责最终实施该要求并重定向到登录资源。

这些要求通过提供`sling.auth.requirements`注册属性的OSGi服务在验证器中注册。 然后，这些属性用于动态扩展身份验证要求。 有关更多详细信息，请参阅[Sling文档](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS)。

#### 使用专用混合类型{#defining-the-authentication-requirement-with-a-dedicated-mixin-type}定义身份验证要求

出于安全原因，新实施将使用名为`granite:AuthenticationRequired`的专用混合类型替换剩余JCR属性，该混合类型为登录路径`granite:loginPath`定义STRING类型的单个可选属性。 只有与此混合类型相关的内容更改才会导致更新向Apache Sling Authenticator注册的要求。 在保留任何临时修改时会跟踪这些修改，因此需要`javax.jcr.Session.save()`调用才能生效。

`granite:loginPath`属性也是如此。 仅当它由与身份验证相关的mixin类型定义时，才会遵守该规则。 在非结构化JCR节点中添加具有此名称的剩余属性将不会显示所需的效果，该属性将被负责更新OSGi注册的处理程序忽略。

>[!NOTE]
>
>设置登录路径属性是可选的，并且仅当需要身份验证的树无法回退到默认登录页面或继承的登录页面时才需要此属性。 请参阅下面的[登录路径评估](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path)。

#### 向Sling Authenticator {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}注册身份验证要求和登录路径

由于此类身份验证要求预计仅限于某些运行模式和内容存储库中树的一小部分，因此对要求混合类型和登录路径属性的跟踪是有条件的，并绑定到定义受支持路径的相应配置（请参阅下面的配置选项）。 因此，只有这些受支持路径范围内的更改才会触发OSGi注册的更新，在mixin类型和属性的其他位置都会被忽略。

默认的AEM设置现在允许在创作运行模式下设置mixin，以便利用此配置，但只有在复制到发布实例时才会生效。 有关Sling如何实施身份验证要求的详细信息，请参阅[此页面](https://sling.apache.org/documentation/the-sling-engine/authentication/authenticationframework.html)。

在配置的受支持路径中添加`granite:AuthenticationRequired` mixin类型将导致更新负责处理程序的OSGi注册，该注册包含一个具有`sling.auth.requirements`属性的新附加条目。 如果给定的身份验证要求指定了可选的`granite:loginPath`属性，则该值会附加地向验证器注册“ — ”前缀，以便从身份验证要求中排除。

#### 认证要求{#evaluation-and-inheritance-of-the-authentication-requirement}的评估与继承

Apache Sling身份验证要求应通过页面或节点层次结构进行继承。 继承和验证要求（如顺序和优先顺序）评估的详细信息被视为实施详细信息，本文不会对此进行记录。

#### 登录路径{#evaluation-of-login-path}的评估

当前，AdobeGranite登录选择器身份验证处理程序(`com.day.cq.auth.impl.LoginSelectorHandler`)的实施详细信息(默认情况下是使用AEM配置的Apache Sling AuthenticationHandler)将评估登录路径并重定向到相应的资源。

在调用`AuthenticationHandler.requestCredentials`时，此处理程序会尝试确定用户将被重定向到的映射登录页面。 这包括以下步骤：

* 区分密码过期和需要定期登录作为重定向原因；
* 如果是定期登录，则会测试是否可以按以下顺序获取登录路径：

   * 从新`com.adobe.granite.auth.requirement.impl.RequirementService`实施的LoginPathProvider中，
   * 从已弃用的旧CUG实施中，
   * 从登录页面映射（如`LoginSelectorHandler`中定义）
   * 最后，回退到默认登录页面，如`LoginSelectorHandler`所定义。

* 一旦通过上述调用获得了有效的登录路径，用户的请求就会被重定向到该页面。

本文档的目标是评估内部`LoginPathProvider`界面所显示的登录路径。 自AEM 6.3起提供的实施如下所示：

* 登录路径的注册取决于是否区分过期的密码以及是否因重定向而需要定期登录
* 如果是定期登录，则会测试是否可以按以下顺序获取登录路径：

   * 从新`com.adobe.granite.auth.requirement.impl.RequirementService`实施的`LoginPathProvider`中，
   * 从已弃用的旧CUG实施中，
   * 从使用`LoginSelectorHandler`定义的登录页面映射中，
   * 最后，回退到使用`LoginSelectorHandler`定义的默认登录页面。

* 一旦通过上述调用获得了有效的登录路径，用户的请求就会被重定向到该页面。

由Granite中新的auth-requerience支持实施的`LoginPathProvider`会公开由`granite:loginPath`属性定义的登录路径，这些属性又由如上所述的mixin类型定义。 保存登录路径的资源路径和属性值本身的映射被保存在内存中，并且将被评估以为层次结构中的其他节点找到合适的登录路径。

>[!NOTE]
>
>仅对与配置的支持路径中的资源相关联的请求执行评估。 对于任何其他请求，将评估确定登录路径的替代方法。

#### 最佳实践 {#best-practices-1}

定义身份验证要求时应考虑以下最佳实践：

* 避免嵌套身份验证要求：在树的开头放置单个身份验证要求标记应该足够，并且可以继承到目标节点定义的整个子树。 该树中的其他身份验证要求应视为冗余要求，在评估Apache Sling中的身份验证要求时，这可能会导致性能问题。 通过将授权和认证相关的CUG区域分离，可以通过CUG或其他类型的策略来限制读取访问，同时强制整个树的认证。
* 为存储库内容建模，以便验证要求适用于整个树，而无需再次从要求中排除嵌套的子树。
* 要避免指定并随后注册冗余登录路径，请执行以下操作：

   * 依赖继承并避免定义嵌套的登录路径，
   * 请勿将可选登录路径设置为与默认值或继承值对应的值，
   * 应用程序开发人员应当确定在与`LoginSelectorHandler`关联的全局登录路径配置（默认和映射）中应配置哪些登录路径。

## 存储库{#representation-in-the-repository}中的表示形式

### 存储库{#cug-policy-representation-in-the-repository}中的CUG策略表示

Oak文档介绍了新CUG策略在存储库内容中的反映方式。 有关详细信息，请参阅[此页面](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository)。

### 存储库{#authentication-requirement-in-the-repository}中的身份验证要求

对单独身份验证要求的需求反映在存储库内容中，并且目标节点处放置专用的混合节点类型。 mixin类型定义一个可选属性，用于为目标节点定义的树指定专用登录页。

与登录路径关联的页面可以位于该树内部或外部。 它将被排除在身份验证要求之外。

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## 管理CUG策略和身份验证要求{#managing-cug-policies-and-authentication-requirement}

### 管理CUG策略{#managing-cug-policies}

使用JCR访问控制管理API管理用于限制CUG读访问的新类型的访问控制策略，并遵循[JCR 2.0规范](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html)中描述的机制。

#### 设置新的CUG策略{#set-a-new-cug-policy}

用于在之前没有设置CUG的节点应用新CUG策略的代码。 请注意，`getApplicablePolicies`将只返回以前未设置的新策略。 最后，需要回写策略，并且需要保留更改。

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
   log.debug("no applicable policy"); // path not supported or no applicable policy (e.g.
                                                   // the policy was set before)
   return;
}

cugPolicy.addPrincipals(toAdd1, toAdd2);
cugPolicy.removePrincipals(toRemove));

acMgr.setPolicy(path, cugPolicy); // as of this step the policy can be edited/removed
session.save();
```

#### 编辑现有的CUG策略{#edit-an-existing-cug-policy}

编辑现有CUG策略需要执行以下步骤。 请注意，修改后的策略需要回写，并且需要使用`javax.jcr.Session.save()`保留更改。

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

### 检索有效的CUG策略{#retrieve-effective-cug-policies}

JCR访问控制管理定义了一种检索在给定路径生效的策略的最佳方法。 由于评估CUG策略是有条件的，并且取决于要启用的相应配置，因此调用`getEffectivePolicies`是验证给定CUG策略是否在给定安装中生效的一种简便方法。

>[!NOTE]
>
>请注意`getEffectivePolicies`与后续代码示例之间的区别，该示例将逐级向上查找给定路径是否已包含在现有CUG中。

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

#### 检索继承的CUG策略{#retrieve-inherited-cug-policies}

查找在给定路径上定义的所有嵌套CUG，而不管它们是否生效。 有关更多信息，请参阅[配置选项](/help/sites-administering/closed-user-groups.md#configuration-options)部分。

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

#### 按Pincipal {#managing-cug-policies-by-pincipal}管理CUG策略

`JackrabbitAccessControlManager`定义的允许按主体编辑访问控制策略的扩展未通过CUG访问控制管理实施，因为根据定义，CUG策略始终影响所有主体：与`PrincipalSetPolicy`一起列出的主体将被授予读取访问权限，而所有其他主体将被阻止读取目标节点定义的树中的内容。

相应的方法始终返回空策略数组，但不会引发异常。

### 管理身份验证要求{#managing-the-authentication-requirement}

通过改变目标节点的有效节点类型来实现新的认证要求的创建、修改或移除。 然后，可以使用常规JCR API写入可选的登录路径属性。

>[!NOTE]
>
>只有配置了`RequirementHandler`并且目标包含在由支持的路径定义的树中时，对上述给定目标节点所做的修改才会反映在Apache Sling Authenticator中（请参阅配置选项一节）。
>
>有关更多信息，请参阅[分配混合节点类型](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3分配混合节点类型)和[添加节点和设置属性](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4添加节点和设置属性)

#### 添加新的身份验证要求{#adding-a-new-auth-requirement}

创建新身份验证要求的步骤详见下文。 请注意，仅当为包含目标节点的树配置了`RequirementHandler`时，才向Apache Sling Authenticator注册此要求。

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### 使用登录路径{#add-a-new-auth-requirement-with-login-path}添加新的身份验证要求

创建新身份验证要求（包括登录路径）的步骤。 请注意，仅当为包含目标节点的树配置了`RequirementHandler`时，才向Apache Sling Authenticator注册登录路径的要求和排除项。

```java
Node targetNode = [...]
String loginPath = [...] // STRING property

Node targetNode = session.getNode(path);
targetNode.addMixin("granite:AuthenticationRequired");

targetNode.setProperty("granite:loginPath", loginPath);
session.save();
```

#### 修改现有登录路径{#modify-an-existing-login-path}

更改现有登录路径的步骤详见下文。 仅当为包含目标节点的树配置了`RequirementHandler`时，才会向Apache Sling Authenticator注册该修改。 将从注册中删除之前的登录路径值。 与目标节点关联的身份验证要求不受此修改的影响。

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

#### 删除现有登录路径{#remove-an-existing-login-path}

删除现有登录路径的步骤。 仅当为包含目标节点的树配置了`RequirementHandler`时，才会从Apache Sling Authenticator中取消注册登录路径条目。 与目标节点关联的身份验证要求不受影响。

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

或者，您也可以使用以下方法实现相同目的：

```java
String path = [...] // absolute path to target node

String propertyPath = PathUtils.concat(path, "granite:loginPath");
if (session.propertyExists(propertyPath)) {
    session.getProperty(propertyPath).remove();
    // or: session.removeItem(propertyPath);
    session.save();
}
```

#### 删除验证要求{#remove-an-auth-requirement}

删除现有身份验证要求的步骤。 仅当为包含目标节点的树配置了`RequirementHandler`时，才会从Apache Sling Authenticator中取消注册该要求。

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### 检索有效的身份验证要求{#retrieve-effective-auth-requirements}

没有专用的公共API来读取在Apache Sling Authenticator中注册的所有有效身份验证要求。 但是，该列表会显示在位于`https://<serveraddress>:<serverport>/system/console/slingauth`的系统控制台中“**身份验证要求配置**”部分下。

下图显示了包含演示内容的AEM发布实例的身份验证要求。 社区页面突出显示的路径说明了Apache Sling Authenticator如何反映本文档中所述实施添加的要求。

>[!NOTE]
>
>在此示例中，未设置可选的登录路径属性。 因此，没有向鉴定人登记第二项。

![chlimage_1-24](assets/chlimage_1-24.jpeg)

#### 检索有效登录路径{#retrieve-the-effective-login-path}

当前没有公共API来检索在匿名访问需要身份验证的资源时生效的登录路径。 有关如何检索登录路径的实施详细信息，请参阅登录路径评估一节。

但请注意，除了使用此功能定义的登录路径之外，还有其他方法可指定到登录的重定向，在设计内容模型和给定AEM安装的身份验证要求时，应考虑这些方法。

#### 检索继承的身份验证要求{#retrieve-the-inherited-auth-requirement}

与登录路径一样，没有用于检索内容中定义的继承身份验证要求的公共API。 以下示例说明了如何列出已使用给定层次结构定义的所有身份验证要求，而不管这些要求是否生效。 有关更多信息，请参阅[配置选项](/help/sites-administering/closed-user-groups.md#configuration-options)。

>[!NOTE]
>
>建议在身份验证要求和登录路径上都使用继承机制，并避免创建嵌套的身份验证要求。
>
>有关更多信息，请参阅[身份验证要求的评估和继承](#evaluation-and-inheritance-of-the-authentication-requirement)、[登录路径评估](#evaluation-of-login-path)和[最佳实践](#best-practices)。

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

### 将CUG策略与身份验证要求{#combining-cug-policies-and-the-authentication-requirement}结合使用

下表列出了AEM实例中CUG策略的有效组合和身份验证要求，该实例通过配置启用了两个模块。

| **需要身份验证** | **登录路径** | **受限读取访问** | **预期效果** |
|---|---|---|---|
| 是 | 是 | 是 | 只有在有效权限评估授予访问权限时，给定用户才能查看使用CUG策略标记的子树。 未经身份验证的用户将被重定向到指定的登录页面。 |
| 是 | 否 | 是 | 只有在有效权限评估授予访问权限时，给定用户才能查看使用CUG策略标记的子树。 未经身份验证的用户将被重定向到继承的默认登录页面。 |
| 是 | 是 | 否 | 未经身份验证的用户将被重定向到指定的登录页面。 是否允许查看标记有身份验证要求的树取决于该子树中包含的各个项目的有效权限。 没有专用CUG限制读取访问。 |
| 是 | 否 | 否 | 未经身份验证的用户将被重定向到继承的默认登录页面。 是否允许查看带有身份验证要求标记的树取决于该子树中包含的各个项目的有效权限。 没有专用CUG限制读取访问。 |
| 否 | 否 | 是 | 只有当有效的权限评估授予访问权限时，给定的已验证或未验证的用户才能查看使用CUG策略标记的子树。 未经身份验证的用户将得到同等的对待，并且不会被重定向到登录。 |

>[!NOTE]
>
>上面未列出“身份验证要求”=“否”和“登录路径”=“是”的组合，因为“登录路径”是与身份验证要求关联的可选属性。 在不添加定义mixin类型的情况下指定具有该名称的JCR属性将不起作用，并且将被相应的处理程序忽略。

## OSGi组件和配置{#osgi-components-and-configuration}

本节概述了OSGi组件以及新CUG实施中引入的各个配置选项。

另请参阅CUG映射文档，以了解旧实施和新实施之间配置选项的全面映射。

### 授权：安装和配置{#authorization-setup-and-configuration}

新的授权相关部件包含在&#x200B;**Oak CUG授权**&#x200B;包(`org.apache.jackrabbit.oak-authorization-cug`)中，该包是AEM默认安装的一部分。 该包定义了一个分离的授权模型，该授权模型旨在作为管理读取访问的另一种方式进行部署。

#### 设置CUG授权{#setting-up-cug-authorization}

[相关Apache文档](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)中对设置CUG授权进行了详细描述。 默认情况下，AEM在所有运行模式下都部署了CUG授权。 在那些需要不同授权设置的安装中，也可以使用分步指令来禁用CUG授权。

#### 配置反向链接过滤器{#configuring-the-referrer-filter}

您还需要配置[Sling反向链接过滤器](/help/sites-administering/security-checklist.md#the-sling-referrer-filter)，以包含可用于访问AEM的所有主机名；例如，通过CDN、负载平衡器和其他任何方式。

如果未配置反向链接过滤器，则用户尝试登录CUG网站时会看到与以下类似的错误：

```shell
31.01.2017 13:49:42.321 *INFO* [qtp1263731568-346] org.apache.sling.security.impl.ReferrerFilter Rejected referrer header for POST request to /libs/granite/core/content/login.html/j_security_check : https://hostname/libs/granite/core/content/login.html?resource=%2Fcontent%2Fgeometrixx%2Fen%2Ftest-site%2Ftest-page.html&$$login$$=%24%24login%24%24&j_reason=unknown&j_reason_code=unknown
```

#### OSGi元件{#characteristics-of-osgi-components}的特性

引入了以下两个OSGi组件来定义身份验证要求并指定专用的登录路径：

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
   <td>专用于设置和评估CUG权限的授权配置。</td>
  </tr>
  <tr>
   <td>配置属性</td>
   <td>
    <ul>
     <li><code>cugSupportedPaths</code></li>
     <li><code>cugEnabled</code></li>
     <li><code>configurationRanking</code></li>
    </ul> <p>另请参阅下面的<a href="#configuration-options">配置选项</a>。</p> </td>
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
   <td>允许从CUG评估中排除具有配置名称的主体。</td>
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

#### 配置选项{#configuration-options}

关键配置选项包括：

* `cugSupportedPaths`:指定可能包含CUG的子树。未设置默认值
* `cugEnabled`:配置选项，以启用对当前CUG策略的权限评估。

[Apache Oak Documentation](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration)中列出了与CUG授权模块关联的可用配置选项，并对其进行了更详细的描述。

#### 从CUG评估中排除承担者{#excluding-principals-from-cug-evaluation}

对个人负责人免予进行国别评价，原执行情况除外。 新的CUG授权通过名为CugExclude的专用接口来覆盖此功能。 Apache Jackrabbit Oak 1.4附带一个默认实施，该实施不包括一组固定的承担者，还提供了一个扩展实施，该实施允许配置各个承担者名称。 后者在AEM发布实例中配置。

自AEM 6.3以来的默认设置可防止以下主体受到CUG策略的影响：

* 管理主体（管理员用户、管理员组）
* 服务用户主体
* 存储库内部系统主体

有关更多信息，请参阅下面“自AEM 6.3](#default-configuration-since-aem)以来的默认配置”部分中的表。[

在系统控制台的&#x200B;**Apache Jackrabbit Oak CUG Exclude List**&#x200B;的配置部分中，可以更改或扩展“管理员”组的排除。

或者，也可以提供和部署CugExclude界面的自定义实施，以在特殊需要时调整排除的承担者集。 有关详细信息和示例实施，请参阅[CUG插件](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)上的文档。

### 身份验证：安装和配置{#authentication-setup-and-configuration}

与身份验证相关的新部分包含在&#x200B;**AdobeGranite身份验证处理程序**&#x200B;包（`com.adobe.granite.auth.authhandler`版本5.6.48）中。 此包是AEM默认安装的一部分。

要设置已弃用CUG支持的身份验证要求替换，某些OSGi组件必须在给定的AEM安装中存在且处于活动状态。 有关更多详细信息，请参阅下面的&#x200B;**OSGi组件的特性** 。

>[!NOTE]
>
>由于RequirementHandler的强制配置选项，只有通过指定一组受支持的路径来启用该功能时，验证相关部分才会处于活动状态。 在标准AEM安装中，该功能在创作运行模式下处于禁用状态，并在发布运行模式下为/content启用。

**OSGi元件的特性**

引入了以下2个OSGi组件来定义身份验证要求并指定专用的登录路径：

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
   <td>用于验证要求的专用OSGi服务，该服务为影响验证要求的内容更改（通过<code>granite:AuthenticationRequirement</code> mixin类型）的观察者注册，以及与的登录路径将暴露在<code>LoginSelectorHandler</code>中。 </td>
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
| 描述 | `RequirementHandler` 可更新Apache Sling身份验证要求以及相关登录路径的相应排除项的实施。 |
| 配置属性 | `supportedPaths` |
| 配置策略 | `ConfigurationPolicy.REQUIRE` |
| 引用 | NA |

#### 配置选项{#configuration-options-1}

CUG重写的与身份验证相关的部分只附带与AdobeGranite身份验证要求和登录路径处理程序关联的单个配置选项：

**&quot;身份验证要求和登录路径处理程序&quot;**

<table>
 <tbody>
  <tr>
   <td>属性</td>
   <td>类型</td>
   <td>默认值</td>
   <td>描述</td>
  </tr>
  <tr>
   <td><p>标签=支持的路径</p> <p>Name = 'supportedPaths'</p> </td>
   <td>Set&lt;String&gt;</td>
   <td>-</td>
   <td>此处理程序将遵循身份验证要求的路径。 如果要将<code>granite:AuthenticationRequirement</code> mixin类型添加到节点而不强制执行它们（例如，在创作实例上），请保持未设置此配置。 如果缺失，则禁用该功能。 </td>
  </tr>
 </tbody>
</table>

## 自AEM 6.3 {#default-configuration-since-aem}以来的默认配置

默认情况下，新安装的AEM将使用新实施来进行CUG功能的授权和身份验证相关部分。 旧的“AdobeGranite封闭用户组(CUG)支持”实施已弃用，默认情况下将在所有AEM安装中禁用。 新实施将改为启用，如下所示：

### 创作实例{#author-instances}

| **&quot;Apache Jackrabbit Oak CUG配置&quot;** | **说明** |
|---|---|
| 支持的路径`/content` | 已启用CUGpolicies的访问控制管理。 |
| CUG评估已启用FALSE | 权限评估被禁用。 CUG政策不起作用。 |
| 等级 | 200 | 请参阅Oak文档。 |

>[!NOTE]
>
>默认创作实例中不存在&#x200B;**Apache Jackrabbit Oak CUG Exclude List**&#x200B;和&#x200B;**AdobeGranite身份验证要求和登录路径处理程序**&#x200B;的配置。

### 发布实例{#publish-instances}

| **&quot;Apache Jackrabbit Oak CUG配置&quot;** | **说明** |
|---|---|
| 支持的路径`/content` | CUG策略的访问控制管理在配置的路径下启用。 |
| CUG评估已启用TRUE | 权限评估在配置的路径下启用。 CUG策略对`Session.save()`生效。 |
| 等级 | 200 | 请参阅Oak文档。 |

| **&quot;Apache Jackrabbit Oak CUG排除列表&quot;** | **说明** |
|---|---|
| 主体名称管理员 | 不包括CUG评估中的管理员主体。 |

| **“AdobeGranite身份验证要求和登录路径处理程序”** | **说明** |
|---|---|
| 支持的路径`/content` | `granite:AuthenticationRequired` mixin类型在存储库中定义的身份验证要求在`Session.save()`后在`/content`下生效。 Sling Authenticator已更新。 将忽略在支持的路径之外添加混合类型。 |

## 禁用CUG授权和身份验证要求{#disabling-cug-authorization-and-authentication-requirement}

如果给定的安装没有使用CUG或使用不同的方法进行身份验证和授权，则可以完全禁用新实施。

### 禁用CUG授权{#disable-cug-authorization}

有关如何从复合授权设置中删除CUG授权模型的详细信息，请参阅[CUG插件](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)文档。

### 禁用身份验证要求{#disable-the-authentication-requirement}

为了禁用对`granite.auth.authhandler`模块提供的身份验证要求的支持，就足以删除与&#x200B;**AdobeGranite身份验证要求和登录路径处理程序**&#x200B;关联的配置。

>[!NOTE]
>
>但请注意，删除配置将不会取消注册mixin类型，该类型仍适用于节点，且不会产生任何影响。

## 与其他模块{#interaction-with-other-modules}的交互

### Apache Jackrabbit API {#apache-jackrabbit-api}

为了引用CUG授权模型使用的新类型访问控制策略，扩展了Apache Jackrabbit定义的API。 自`jackrabbit-api`模块版本2.11.0起，定义了一个名为`org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`的新接口，该接口从`javax.jcr.security.AccessControlPolicy`扩展。

### Apache Jackrabbit FileVault {#apache-jackrabbit-filevault}

已调整Apache Jackrabbit FileVault的导入机制，以处理`PrincipalSetPolicy`类型的访问控制策略。

### Apache Sling内容分发{#apache-sling-content-distribution}

请参阅上面的[Apache Jackrabbit FileVault](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault)部分。

### AdobeGranite复制{#adobe-granite-replication}

为了能够在不同AEM实例之间复制CUG策略，复制模块已进行了稍微调整：

* `DurboImportConfiguration.isImportAcl()` 将以字面形式解释，并且只会影响访问控制策略的实施  `javax.jcr.security.AccessControlList`

* `DurboImportTransformer` 将仅遵守此配置，才能获得真正的ACL
* 其他策略（如由CUG授权模型创建的`org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`实例）将始终被复制，并且配置选项`DurboImportConfiguration.isImportAcl`()将被忽略。

复制CUG策略存在一个限制。 如果在删除相应的混合节点类型`rep:CugMixin,`的情况下删除了给定的CUG策略，则复制时不会反映该删除。 已通过始终在删除策略时删除mixin来解决此问题。 但是，如果手动添加混合类型，则可能会显示该限制。

### AdobeGranite身份验证处理程序{#adobe-granite-authentication-handler}

验证处理程序&#x200B;**AdobeGranite HTTP标头验证处理程序**&#x200B;随`com.adobe.granite.auth.authhandler`包一起提供，它包含对由同一模块定义的`CugSupport`接口的引用。 它用于在某些情况下计算“领域”，并回退到使用处理程序配置的领域。

已对此进行了调整，使对`CugSupport`的引用成为可选的引用，以确保在给定设置决定重新启用已弃用的实施时最大的向后兼容性。 使用该实施的安装将不再获取从CUG实施提取的领域，但将始终按照&#x200B;**AdobeGranite HTTP标头身份验证处理程序**&#x200B;定义的领域显示。

>[!NOTE]
>
>默认情况下，**AdobeGranite HTTP标头身份验证处理程序**&#x200B;仅在发布运行模式下配置，并启用“禁用登录页面”(`auth.http.nologin`)选项。

### AEM LiveCopy {#aem-livecopy}

配置CUG与LiveCopy一起使用时，会添加一个额外节点和一个额外属性，如下所示：

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

这两个元素都在`cq:Page`下创建。 使用当前设计时，MSM仅处理`cq:PageContent`(`jcr:content`)节点下的节点和属性。

因此，无法从Blueprint将CUG组转出到Live Copy。 请在配置Live Copy时针对此进行规划。

## 对新CUG实施{#changes-with-the-new-cug-implementation}的更改

本节旨在概述对CUG功能所做的更改，以及旧实施和新实施的比较。 它列出了影响CUG支持配置方式的更改，并描述了如何以及由谁在存储库内容中管理CUG。

### CUG设置和配置中的差异{#differences-in-cug-setup-and-configuration}

已弃用的OSGi组件&#x200B;**AdobeGranite封闭用户组(CUG)支持**(`com.day.cq.auth.impl.cug.CugSupportImpl`)已被新组件替换，以便能够单独处理前CUG功能中与授权和身份验证相关的部分。

## 在管理存储库内容中的CUG方面的差异{#differences-in-managing-cugs-in-the-repository-content}

以下各节从实施和安全角度介绍了旧实施与新实施之间的差异。 虽然新实施旨在提供相同的功能，但在使用新CUG时，需要了解一些细微的更改。

### 与授权{#differences-with-regards-to-authorization}有关的差异

从授权角度来看，主要区别如下：

**CUG的专用访问控制内容**

在旧实施中，默认授权模型用于处理发布时的访问控制列表策略，通过CUG授权的设置替换任何现有ACE。 这是由编写常规的剩余JCR属性触发的，这些属性会在发布时进行解释。

在新实施中，默认授权模型的访问控制设置不受任何正在创建、修改或删除的CUG的影响。 而是将名为`PrincipalSetPolicy`的新策略类型作为附加访问控制内容应用到目标节点。 此附加策略将作为目标节点的子项找到，并且如果存在，则将作为默认策略节点的同级。

**在访问控制管理中编辑CUG策略**

从剩余的JCR属性移动到专用的访问控制策略会影响创建或修改CUG功能的授权部分所需的权限。 由于这被视为访问控制内容的修改，因此需要`jcr:readAccessControl`和`jcr:modifyAccessControl`权限才能写入存储库。 因此，只有有权修改页面访问控制内容的内容作者才能设置或修改此内容。 这与旧实施形成了对比，旧实施中写入常规JCR属性的功能已足够，从而导致权限提升。

**策略定义的目标节点**

CUG策略应在JCR节点创建，该节点定义要受限制读取访问的子树。 如果CUG应影响整个树，则该页面可能是AEM页面。

请注意，将CUG策略仅放置在位于给定页面下方的jcr:content节点上，将仅限制对给定页面内容s.str的访问，但不会对任何同级或子页面生效。 这可能是一个有效的用例，并且可以使用允许应用细粒度访问内容的存储库编辑器来实现。 但是，它与之前的实施形成了对比，在之前的实施中，将cq:cugEnabled属性放置到jcr:content节点后，会在内部将该属性重新映射到页面节点。 不再执行此映射。

**使用CUG策略进行权限评估**

从旧的CUG支持转移到其他授权模型，更改了评估有效读取权限的方式。 如[Jackrabbit文档](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)中所述，仅当Oak存储库中配置的所有模型的权限评估授予读取访问权限时，才会授予允许查看`CUGcontent`的给定主体读取权限。

换言之，在评估有效权限时，将考虑`CUGPolicy`和默认访问控制条目，并且仅当两种策略都授予CUG内容读取权限时，才授予对CUG内容的读取权限。 在默认的AEM发布安装中，为每个人授予对完整`/content`树的读取访问权限，CUG策略的效果将与旧实施的效果相同。

**按需评估**

CUG授权模型允许单独开启访问控制管理和权限评估：

* 如果模块具有一个或多个可创建CUG的支持路径，则会启用访问控制管理
* 仅当另外选中选项&#x200B;**已启用CUG评估**&#x200B;时，才启用权限评估。

在新的AEM默认设置CUG策略评估中，仅通过“发布”运行模式启用该设置。 有关更多详细信息，请参阅自AEM 6.3](#default-configuration-since-aem)以来的[默认配置的详细信息。 可通过将给定路径的有效策略与存储在内容中的策略进行比较来验证这一点。 只有在启用CUG的权限评估时，才会显示有效策略。

如上所述，CUG访问控制策略现在始终存储在内容中，但只有在Apache Jackrabbit Oak **CUG配置的系统控制台中打开**&#x200B;启用CUG评估&#x200B;**时，才会强制评估这些策略产生的有效权限。** 默认情况下，仅通过“发布”运行模式启用此功能。

### 与身份验证{#differences-with-regards-to-authentication}有关的差异

与身份验证有关的差异如下所述。

#### 用于验证要求{#dedicated-mixin-type-for-authentication-requirement}的专用混合类型

在前一个实现中，CUG的授权和身份验证方面都由单个JCR属性(`cq:cugEnabled`)触发。 就身份验证而言，这会生成与Apache Sling Authenticator实施一起存储的身份验证要求的更新列表。 在新的实施中，通过用专用混合类型(`granite:AuthenticationRequired`)标记目标节点来实现相同的结果。

#### 用于排除登录路径{#property-for-excluding-login-path}的属性

mixin类型定义一个名为`granite:loginPath`的可选属性，该属性基本上与`cq:cugLoginPage`属性相对应。 与之前的实施相反，仅当其声明节点类型为所述mixin时，才会遵守登录路径属性。 在不设置mixin类型的情况下添加具有该名称的属性将不起作用，并且不会向验证器报告对登录路径的新要求或排除项。

#### 身份验证要求的权限{#privilege-for-authentication-requirement}

添加或删除混合类型需要授予`jcr:nodeTypeManagement`权限。 在上一个实施中，使用`jcr:modifyProperties`权限来编辑剩余属性。

就`granite:loginPath`而言，添加、修改或删除资产时需要相同的权限。

#### 由混合类型{#target-node-defined-by-mixin-type}定义的目标节点

应在JCR节点创建身份验证要求，该节点定义要强制登录的子树。 如果CUG预期会影响整个树，且用于新实施的UI随后会在页面节点上添加身份验证要求mixin类型，则这可能是AEM页面。

将CUG策略仅放置在位于给定页面下方的jcr:content节点将仅限访问内容，但不会影响页面节点本身或任何子页面。

这可能是一种有效的方案，在允许将混合内容放置到任意节点的存储库编辑器中，也可能是这种情况。 但是，这种行为与之前的实施形成了对比，在之前的实施中，将cq:cugEnabled或cq:cugLoginPage属性放置到jcr:content节点后，最终会将其内部重新映射到页面节点。 不再执行此映射。

#### 已配置支持的路径{#configured-supported-paths}

`granite:AuthenticationRequired` mixin类型和granite:loginPath属性将仅在&#x200B;**支持的路径**&#x200B;配置选项集定义的范围内得到遵守，该选项集与&#x200B;**Adobe的Granite身份验证要求和登录路径处理程序**&#x200B;一起提供。 如果未指定路径，则完全禁用身份验证要求功能。 在这种情况下，将mixin类型或属性添加到给定的JCR节点或将其设置为该节点时，将会生效。

### JCR内容、OSGi服务和配置的映射{#mapping-of-jcr-content-osgi-services-and-configurations}

以下文档提供了旧实施和新实施之间OSGi服务、配置和存储库内容的全面映射。

自AEM 6.3以来的CUG映射

[获取文件](assets/cug-mapping.pdf)

## 升级CUG {#upgrade-cug}

### 使用已弃用的CUG {#existing-installations-using-the-deprecated-cug}的现有安装

旧的CUG支持实施已弃用，将在将来的版本中删除。 从AEM 6.3以前的版本升级时，建议移至新实施。

对于已升级的AEM安装，请务必确保只启用一个CUG实施。 不会测试已弃用的新CUG和旧CUG支持的组合，这可能会导致不希望的行为：

* Sling Authenticator中与身份验证要求有关的冲突
* 当与旧CUG关联的ACL设置与新CUG策略冲突时，拒绝读取访问。

### 迁移现有CUG内容{#migrating-existing-cug-content}

Adobe提供了迁移到新CUG实施的工具。 要使用该插件，请执行以下步骤：

1. 转到`https://<serveraddress>:<serverport>/system/console/cug-migration`以访问该工具。
1. 输入要检查CUG的根路径，然后按&#x200B;**Perform dry run**&#x200B;按钮。 这将扫描选定位置中符合转化条件的CUG。
1. 查看结果后，按&#x200B;**Perform migration**&#x200B;按钮以迁移到新实施。

>[!NOTE]
>
>如果遇到问题，可以在`com.day.cq.auth.impl.cug`的&#x200B;**DEBUG**&#x200B;级别设置特定的日志记录器，以获取迁移工具的输出。 有关如何执行此操作的详细信息，请参阅[日志记录](/help/sites-deploying/configure-logging.md)。
