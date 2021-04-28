---
title: AEM中已关闭的用户组
seo-title: AEM中已关闭的用户组
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
translation-type: tm+mt
source-git-commit: cb4b0cb60b8709beea3da70495a15edc8c4831b8
workflow-type: tm+mt
source-wordcount: '6886'
ht-degree: 0%

---

# AEM{#closed-user-groups-in-aem}中已关闭的用户组

## 简介 {#introduction}

自AEM 6.3以来，新的“已关闭的用户组”实施旨在解决现有实施中存在的性能、可扩展性和安全问题。

>[!NOTE]
>
>为了简单起见，本文档中将使用CUG缩写。

新实施的目标是在需要时覆盖现有功能，同时解决旧版本的问题和设计限制。 结果为CUG设计提供了新的特点：

* 明确区分可单独或组合使用的身份验证和授权元素；
* 专用的授权模型，在配置的CUG树上反映受限的读取访问，而不会干扰其他访问控制设置和权限要求；
* 将创作实例时通常需要的受限读取权限的访问控制设置与发布时通常只需要的权限评估分开；
* 编辑受限读取访问，而无权限提升；
* 专用节点类型扩展标识认证要求；
* 与身份验证要求关联的可选登录路径。

### 新的自定义用户组实现{#the-new-custom-user-group-implementation}

在AEM上下文中称为CUG的步骤如下：

* 在树上限制需要保护的读取访问，并且仅允许读取包含给定CUG实例或完全从CUG评估中排除的承担者。 这称为&#x200B;**authorization**&#x200B;元素。
* 在给定树上强制执行身份验证，并（可选）为随后被排除的树指定专用登录页。 这称为&#x200B;**authentication**&#x200B;元素。

新的实施设计为在身份验证和授权元素之间划出一条线。 从AEM 6.3开始，无需显式添加身份验证要求即可限制读访问。 例如，如果给定实例需要完全身份验证，或者给定树已驻留在需要身份验证的子树中。

同样，给定的树可以用身份验证要求进行标记，而无需更改有效权限设置。 组合和结果列在[组合CUG策略和身份验证要求](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement)部分。

## 概述 {#overview}

### 授权：限制读访问{#authorization-restricting-read-access}

CUG的主要功能是限制除所选主体之外的所有用户对内容存储库中给定树的读取访问。 新的实现不是实时操作默认访问控制内容，而是通过定义表示CUG的专用访问控制策略类型来采用不同的方法。

#### CUG {#access-control-policy-for-cug}的访问控制策略

此新类型的策略具有以下特点：

* org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy（由Apache Jackrabbit API定义）类型的访问控制策略；
* PrincipalSetPolicy授予可修改的主体集的权限；
* 授予的权限和策略的范围是实施细节。

用于表示CUG的PrincipalSetPolicy的实现还定义：

* CUG策略仅授予对常规JCR项的读取权限(例如，排除访问控制内容);
* 该范围由持有CUG策略的接入控制节点定义；
* CUG策略可以嵌套，嵌套的CUG开始新的CUG，而不继承“父”CUG的主体集；
* 如果启用了评估，则策略的效果将继承到整个子树，下一个嵌套的CUG。

这些CUG策略通过称为oak-authorization-cug的单独授权模块部署到AEM实例。 本模块附带有自己的访问控制管理和权限评估。 换句话说，默认的AEM设置会发布Oak内容存储库配置，该配置结合了多个授权机制。 有关详细信息，请参阅Apache Oak Documentation](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)上的[此页。

在此复合设置中，新的CUG不会替换附加到访问控制节点的现有目标内容，而是设计为补充，稍后还可以删除它而不影响原始访问控制，在AEM中默认情况下，它将是访问控制列表。

与以前的实施不同，新的CUG策略始终被认可和视为访问控制内容。 这意味着它们是使用JCR访问控制管理API创建和编辑的。 有关详细信息，请参阅[管理CUG策略](#managing-cug-policies)部分。

#### CUG策略的权限评估{#permission-evaluation-of-cug-policies}

除了CUG的专用访问控制管理，新授权模型允许有条件地启用其策略的许可评估。 这允许在暂存环境中设置CUG策略，并且只允许在将有效权限复制到生产环境后对有效权限进行评估。

CUG策略的权限评估以及与默认或任何其他授权模型的交互遵循Apache Jackrabbit Oak中为多个授权机制设计的模式：当且仅当所有模型授予访问权限时，才授予给定的权限集。 有关详细信息，请参阅[此页](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)。

与用于处理和评估CUG策略的授权模型相关的权限评估适用以下特征：

* 它只处理常规节点和属性的读取权限，而不会读取访问控制内容
* 它不处理写权限或修改受保护的JCR内容(访问控制、节点类型信息、版本控制、锁定或用户管理等)所需的任何类型的权限；这些权限不受CUG策略影响，并且不会由关联的授权模型评估。 是否授予这些权限取决于在安全设置中配置的其他模型。

单个CUG策略对权限评估的影响可以概括如下：

* 除政策中列出的包含被排除的承担者或承担者的主体之外，所有人都拒绝读取权限；
* 该策略对包含该策略及其属性的访问控制节点生效；
* 此效果在层次结构中被额外继承，即由访问控制节点定义的项目树；
* 但是，它不影响接入控制节点的同级和祖先；
* 给定CUG的继承会在嵌套CUG处停止。

#### 最佳实践 {#best-practices}

在通过CUG定义受限读取访问时，应考虑以下最佳做法：

* 有意识地决定您对CUG的需求是限制读访问还是身份验证要求。 如果是后者或需要两者，请查阅最佳实践部分，了解有关身份验证要求的详细信息
* 为需要保护的数据或内容创建威胁模型，以便识别威胁边界并清晰了解数据的敏感性以及与授权访问相关的角色
* 为存储库内容和CUG建模，同时要牢记一般授权相关方面和最佳做法：

   * 请记住，只有在给定CUG和设置授权中部署的其他模块的评估允许给定主体读取给定存储库项目时，才会授予读取权限
   * 避免创建冗余CUG，因为其他授权模块已限制读取访问
   * 过度需要嵌套CUG可能会突出内容设计中的问题
   * 对CUG的过度需求（例如，在每一页上）可能表明需要一个可能更适合满足应用程序和手头内容的特定安全需求的自定义授权模型。

* 将CUG策略支持的路径限制在存储库中的几个树中，以便获得优化的性能。 例如，仅允许作为自AEM 6.3以来的默认值发运的/content节点下的CUG。
* CUG策略旨在授予对一小组主体的读取权限。 需要大量原则可能会突出内容或应用程序设计中的问题，应重新考虑。

### 身份验证：定义身份验证要求{#authentication-defining-the-auth-requirement}

CUG功能的身份验证相关部分允许标记需要身份验证的树，并可选地指定专用登录页。 根据先前版本，新实现允许在内容存储库中标记需要身份验证的树，并有条件地启用与`Sling org.apache.sling.api.auth.Authenticator`的同步，该负责最终实施该要求并重定向到登录资源。

通过提供`sling.auth.requirements`注册属性的OSGi服务向验证器注册这些要求。 然后，这些属性用于动态扩展身份验证要求。 有关详细信息，请参阅[Sling文档](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS)。

#### 使用专用混音类型{#defining-the-authentication-requirement-with-a-dedicated-mixin-type}定义身份验证要求

出于安全原因，新实现将剩余JCR属性的使用替换为名为`granite:AuthenticationRequired`的专用混音类型，该类型为登录路径`granite:loginPath`定义了STRING类型的单个可选属性。 只有与此混音类型相关的内容更改才能更新向Apache Sling Authenticator注册的要求。 在保持任何临时修改时跟踪这些修改，因此需要`javax.jcr.Session.save()`调用才能生效。

`granite:loginPath`属性也是如此。 只有由身份验证要求相关的混音类型定义时，才会尊重它。 在非结构化JCR节点上添加具有此名称的剩余属性将不会显示所需效果，而负责更新OSGi注册的处理函数将忽略该属性。

>[!NOTE]
>
>设置登录路径属性是可选的，并且仅当需要身份验证的树无法回退到默认登录页或以其他方式继承的登录页时才需要。 请参阅下面的[登录路径评估](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path)。

#### 向Sling Authenticator {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}注册身份验证要求和登录路径

由于此类身份验证要求预计将限于某些运行模式和内容存储库中的一小部分树，因此对要求混合类型和登录路径属性的跟踪是有条件的，并绑定到定义受支持路径的相应配置（请参阅下面的配置选项）。 因此，只有这些支持路径范围内的更改才会触发OSGi注册的更新，而其他位置的mixin类型和属性都将被忽略。

默认AEM设置现在允许在作者运行模式下设置mixin，但仅在复制到发布实例后才会生效，从而利用此配置。 有关Sling如何强制执行身份验证要求的详细信息，请参阅[此页](https://sling.apache.org/documentation/the-sling-engine/authentication/authenticationframework.html)。

在配置的受支持路径中添加`granite:AuthenticationRequired`混音类型将导致更新负责处理函数的OSGi注册，该注册包含具有`sling.auth.requirements`属性的新的附加条目。 如果给定的身份验证要求指定了可选的`granite:loginPath`属性，则该值会附加地向身份验证器注册一个“ — ”前缀，以便从身份验证要求中排除。

#### 认证要求{#evaluation-and-inheritance-of-the-authentication-requirement}的评估与继承

Apache Sling身份验证要求应通过页面或节点层次结构继承。 继承和验证要求评估的详细信息（如顺序和优先级）被视为实施细节，本文中不予记录。

#### 登录路径{#evaluation-of-login-path}的评估

验证时对登录路径的评估和重定向到相应的资源当前是Adobe Granite登录选择器身份验证处理程序(`com.day.cq.auth.impl.LoginSelectorHandler`)的实现详细信息，该处理程序是默认配置为AEM的Apache Sling AuthenticationHandler。

在调用`AuthenticationHandler.requestCredentials`时，此处理函数会尝试确定将用户重定向到的映射登录页。 这包括以下步骤：

* 区分过期密码和需要定期登录作为重定向原因；
* 如果是定期登录，则测试是否可以按以下顺序获得登录路径：

   * 从新`com.adobe.granite.auth.requirement.impl.RequirementService`实现的LoginPathProvider中，
   * 从旧的、已弃用的CUG实现，
   * 从登录页面映射，如`LoginSelectorHandler`中定义，
   * 最后，回退到“默认登录页面”，如`LoginSelectorHandler`中所定义。

* 一旦通过上述呼叫获得有效的登录路径，用户的请求将被重定向到该页面。

本文档的目标是对内部`LoginPathProvider`接口所公开的登录路径的评估。 自AEM 6.3起发运的实施如下所示：

* 登录路径的注册取决于对过期密码的区分，以及是否需要定期登录作为重定向的原因
* 如果是定期登录，则测试是否可以按以下顺序获得登录路径：

   * 从新`com.adobe.granite.auth.requirement.impl.RequirementService`实现的`LoginPathProvider`,
   * 从旧的、已弃用的CUG实现，
   * 从使用`LoginSelectorHandler`定义的登录页面映射，
   * 最后，回退到使用`LoginSelectorHandler`定义的“默认登录页面”。

* 一旦通过上述呼叫获得有效的登录路径，用户的请求将被重定向到该页面。

由Granite中新的auth-requirement支持实现的`LoginPathProvider`公开由`granite:loginPath`属性定义的登录路径，而这些属性又由上述的mixin类型定义。 保存登录路径和属性值本身的资源路径的映射保留在内存中，并将进行评估，以为层次结构中的其他节点找到合适的登录路径。

>[!NOTE]
>
>仅对与配置的支持路径中的资源相关联的请求执行评估。 对于任何其他请求，将评估确定登录路径的替代方法。

#### 最佳实践 {#best-practices-1}

定义身份验证要求时应考虑以下最佳做法：

* 避免嵌套身份验证要求：在树的开始放置单个身份验证要求标记应足够，并继承到由目标节点定义的整个子树。 该树中的其他身份验证要求应被视为冗余，在评估Apache Sling中的身份验证要求时，这可能会导致性能问题。 通过将授权和认证相关的CUG区分开，可以通过CUG或其他类型的策略限制读访问，同时强制对整个树的认证。
* 建模存储库内容，使身份验证要求适用于整个树，而无需再次将嵌套子树排除在需求之外。
* 要避免指定，并随后注册多余的登录路径：

   * 依赖继承并避免定义嵌套登录路径，
   * 不要将可选登录路径设置为与默认值或继承值相对应的值，
   * 应用程序开发人员应确定在与`LoginSelectorHandler`关联的全局登录路径配置（默认和映射）中应配置哪些登录路径。

## 存储库{#representation-in-the-repository}中的表示形式

### 存储库{#cug-policy-representation-in-the-repository}中的CUG策略表示

Oak文档介绍了新CUG策略在存储库内容中的反映方式。 有关详细信息，请查阅[此页](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository)。

### 存储库{#authentication-requirement-in-the-repository}中的身份验证要求

在存储库内容中反映了对单独身份验证要求的需要，而将专用的混合节点类型放置在目标节点。 混合类型定义一个可选属性，以指定由目标节点定义的树的专用登录页。

与登录路径关联的页面可以位于该树的内部或外部。 它将被排除在身份验证要求之外。

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## 管理CUG策略和身份验证要求{#managing-cug-policies-and-authentication-requirement}

### 管理CUG策略{#managing-cug-policies}

用于限制CUG读访问的新类型访问控制策略是使用JCR访问控制管理API管理的，并遵循[JCR 2.0规范](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html)中描述的机制。

#### 设置新的CUG策略{#set-a-new-cug-policy}

在以前没有设置CUG的节点上应用新CUG策略的代码。 请注意，`getApplicablePolicies`将仅返回以前未设置的新策略。 最后，策略需要回写，并且需要保留更改。

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

编辑现有CUG策略需要执行以下步骤。 请注意，修改后的策略需要写回，并且需要使用`javax.jcr.Session.save()`保留更改。

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

JCR访问控制管理定义了一种检索在给定路径上生效的策略的最佳方法。 由于评估CUG策略的条件性且取决于要启用的相应配置，调用`getEffectivePolicies`是验证给定CUG策略是否在给定安装中生效的一种简便方法。

>[!NOTE]
>
>请注意`getEffectivePolicies`与随后代码示例之间的差异，该示例将向上遍历层次结构以查找给定路径是否已是现有CUG的一部分。

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

查找在给定路径中定义的所有嵌套CUG，而不管这些CUG是否生效。 有关详细信息，请参阅[配置选项](/help/sites-administering/closed-user-groups.md#configuration-options)部分。

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

`JackrabbitAccessControlManager`定义的允许按主体编辑访问控制策略的扩展未通过CUG访问控制管理实现，因为根据定义，CUG策略始终影响所有主体：与`PrincipalSetPolicy`一起列出的内容将被授予读访问权限，而所有其他主体将被阻止读取由目标节点定义的树中的内容。

相应的方法始终返回空策略数组，但不会引发异常。

### 管理身份验证要求{#managing-the-authentication-requirement}

通过改变目标节点的有效节点类型来实现新认证要求的创建、修改或移除。 然后，可以使用常规JCR API编写可选的登录路径属性。

>[!NOTE]
>
>如果`RequirementHandler`已配置，且目标包含在受支持路径定义的树中，则上述对给定目标节点的修改仅会反映在Apache Sling Authenticator上（请参阅配置选项一节）。
>
>有关详细信息，请参阅[分配混合节点类型](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3分配混合节点类型)和[添加节点和设置属性](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4添加节点和设置属性)

#### 添加新的身份验证要求{#adding-a-new-auth-requirement}

创建新身份验证要求的步骤详述如下。 请注意，仅当`RequirementHandler`已为包含目标节点的树配置时，才向Apache Sling Authenticator注册此要求。

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### 使用登录路径{#add-a-new-auth-requirement-with-login-path}添加新的身份验证要求

创建新身份验证要求的步骤，包括登录路径。 请注意，仅当`RequirementHandler`已为包含目标节点的树配置时，才向Apache Sling Authenticator注册登录路径的要求和排除。

```java
Node targetNode = [...]
String loginPath = [...] // STRING property

Node targetNode = session.getNode(path);
targetNode.addMixin("granite:AuthenticationRequired");

targetNode.setProperty("granite:loginPath", loginPath);
session.save();
```

#### 修改现有登录路径{#modify-an-existing-login-path}

更改现有登录路径的步骤详见下文。 如果`RequirementHandler`已为包含目标节点的树配置，则只有向Apache Sling Authenticator注册修改。 之前的登录路径值将从注册中删除。 与目标节点关联的身份验证要求不受此修改的影响。

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

删除现有登录路径的步骤。 如果`RequirementHandler`已为包含目标节点的树配置，则登录路径条目将仅从Apache Sling Authenticator中注册。 与目标节点关联的身份验证要求不受影响。

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

或者，您可以使用以下方法来实现相同目的：

```java
String path = [...] // absolute path to target node

String propertyPath = PathUtils.concat(path, "granite:loginPath");
if (session.propertyExists(propertyPath)) {
    session.getProperty(propertyPath).remove();
    // or: session.removeItem(propertyPath);
    session.save();
}
```

#### 删除身份验证要求{#remove-an-auth-requirement}

删除现有身份验证要求的步骤。 如果`RequirementHandler`已为包含目标节点的树配置，则只能从Apache Sling Authenticator中取消注册此要求。

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### 检索有效身份验证要求{#retrieve-effective-auth-requirements}

没有专用的公共API来读取向Apache Sling Authenticator注册的所有有效身份验证要求。 但是，列表会在系统控制台的“**身份验证要求配置**”部分下的`https://<serveraddress>:<serverport>/system/console/slingauth`中显示。

下图显示了包含演示内容的AEM发布实例的身份验证要求。 社区页面的突出显示路径说明了本文档中描述的实施所添加的要求在Apache Sling Authenticator中的反映情况。

>[!NOTE]
>
>在此示例中，未设置可选登录路径属性。 因此，没有向验证者注册第二项。

![chlimage_1-24](assets/chlimage_1-24.jpeg)

#### 检索有效登录路径{#retrieve-the-effective-login-path}

当前没有公共API可检索登录路径，该路径将在匿名访问需要身份验证的资源时生效。 有关如何检索登录路径的实施详细信息，请参阅登录路径的评估部分。

但是，请注意，除了使用此功能定义的登录路径之外，还有其他方法可指定指向登录的重定向，在设计内容模型和给定AEM安装的身份验证要求时，应考虑这些方法。

#### 检索继承的身份验证要求{#retrieve-the-inherited-auth-requirement}

与登录路径一样，没有公共API可检索内容中定义的继承身份验证要求。 以下示例说明如何列表使用给定层次结构定义的所有身份验证要求，而不管这些要求是否生效。 有关详细信息，请参阅[配置选项](/help/sites-administering/closed-user-groups.md#configuration-options)。

>[!NOTE]
>
>建议将继承机制用于身份验证要求和登录路径，并避免创建嵌套身份验证要求。
>
>有关详细信息，请参阅[验证要求的评估和继承](#evaluation-and-inheritance-of-the-authentication-requirement)、[登录路径评估](#evaluation-of-login-path)和[最佳实践](#best-practices)。

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

### 将CUG策略与身份验证要求{#combining-cug-policies-and-the-authentication-requirement}组合

下表列表了AEM实例中CUG策略的有效组合和身份验证要求，该实例通过配置启用了这两个模块。

| **需要身份验证** | **登录路径** | **受限读取访问** | **预期效果** |
|---|---|---|---|
| 是 | 是 | 是 | 如果有效权限评估授予访问权限，则给定用户只能视图用CUG策略标记的子树。 未通过身份验证的用户将被重定向到指定的登录页面。 |
| 是 | 否 | 是 | 如果有效权限评估授予访问权限，则给定用户只能视图用CUG策略标记的子树。 未通过身份验证的用户将被重定向到继承的默认登录页面。 |
| 是 | 是 | 否 | 未通过身份验证的用户将被重定向到指定的登录页面。 是否允许视图带有身份验证要求的树取决于子树中包含的各个项目的有效权限。 没有专用的CUG限制读取访问。 |
| 是 | 否 | 否 | 未通过身份验证的用户将被重定向到继承的默认登录页面。 是否允许视图带有身份验证要求的树取决于子树中包含的各个项目的有效权限。 没有专用的CUG限制读取访问。 |
| 否 | 否 | 是 | 如果有效权限评估授予访问权限，则给定已验证或未验证的用户只能视图用CUG策略标记的子树。 未通过身份验证的用户将得到同等对待，不会被重定向到登录。 |

>[!NOTE]
>
>“身份验证要求”=“否”和“登录路径”=“是”的组合未在上面列出，因为“登录路径”是与身份验证要求关联的可选属性。 指定不添加定义混音类型而使用该名称的JCR属性将不起作用，并且将被相应的处理程序忽略。

## OSGi组件和配置{#osgi-components-and-configuration}

本节概述了OSGi组件以及新CUG实施引入的各个配置选项。

另请参阅CUG映射文档，以全面映射旧实施和新实施之间的配置选项。

### 授权：设置和配置{#authorization-setup-and-configuration}

新的授权相关部件包含在AEM默认安装的&#x200B;**Oak CUG授权**&#x200B;包(`org.apache.jackrabbit.oak-authorization-cug`)中。 该绑定定义了一个分离的授权模型，该模型旨在作为管理读访问的另一种方式进行部署。

#### 设置CUG授权{#setting-up-cug-authorization}

有关设置CUG授权的详细说明，请参阅[相关Apache文档](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)。 默认情况下，AEM在所有运行模式下都部署了CUG授权。 该分步指令也可用于在那些需要不同授权设置的安装中禁用CUG授权。

#### 配置推荐人筛选器{#configuring-the-referrer-filter}

您还需要配置[Sling推荐人过滤器](/help/sites-administering/security-checklist.md#the-sling-referrer-filter)，其中包含可用于访问AEM的所有主机名；例如，通过CDN、负载平衡器和任何其他方式。

如果未配置推荐人过滤器，则当用户尝试登录CUG站点时，将看到与以下内容类似的错误：

```shell
31.01.2017 13:49:42.321 *INFO* [qtp1263731568-346] org.apache.sling.security.impl.ReferrerFilter Rejected referrer header for POST request to /libs/granite/core/content/login.html/j_security_check : https://hostname/libs/granite/core/content/login.html?resource=%2Fcontent%2Fgeometrixx%2Fen%2Ftest-site%2Ftest-page.html&$$login$$=%24%24login%24%24&j_reason=unknown&j_reason_code=unknown
```

#### OSGi组件{#characteristics-of-osgi-components}的特性

已引入以下两个OSGi组件来定义身份验证要求并指定专用登录路径：

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
   <td>允许从CUG评估中排除配置名称的主体。</td>
  </tr>
  <tr>
   <td>配置属性</td>
   <td>
    <ul>
     <li><code>principalNames</code></li>
    </ul> <p>另请参见下面的配置选项部分。</p> </td>
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

在[Apache Oak Documentation](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration)中列出并详细描述了与CUG授权模块相关的可用配置选项。

#### 排除CUG评估{#excluding-principals-from-cug-evaluation}中的承担者

已采取将个人负责人免于进行国别小组评价的办法。 新的CUG授权通过一个名为CugExclude的专用接口覆盖此权限。 Apache Jackrabbit Oak 1.4附带默认实现，该实现不包括固定的主体集以及允许配置单个主体名称的扩展实现。 后者是在AEM发布实例中配置的。

自AEM 6.3以来的默认值可防止以下承担者受到CUG策略的影响：

* 管理主体（管理员用户、管理员组）
* 服务用户主体
* 存储库内部系统主

有关详细信息，请参阅下面[自AEM 6.3](#default-configuration-since-aem)以来的默认配置部分中的表。

在系统控制台中，可以在&#x200B;**Apache Jackrabbit Oak CUG Exclude列表**&#x200B;的配置部分更改或展开“administrators”组的排除。

或者，可以提供和部署CugExclude接口的自定义实现，以在特殊需要时调整被排除的承担者集。 有关详细信息和示例实现，请参阅[CUG可插件](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)上的文档。

### 身份验证：设置和配置{#authentication-setup-and-configuration}

新的、与身份验证相关的部件包含在&#x200B;**AdobeGranite身份验证处理程序**&#x200B;包（`com.adobe.granite.auth.authhandler`版本5.6.48）中。 此捆绑包是AEM默认安装的一部分。

为了为已弃用的CUG支持设置身份验证要求替换，在给定的AEM安装中，必须存在某些OSGi组件并且它们处于活动状态。 有关详细信息，请参阅下面的&#x200B;**OSGi组件的特性**。

>[!NOTE]
>
>由于RequirementHandler具有强制配置选项，因此仅当通过指定一组受支持的路径启用了该功能时，验证相关部分才会处于活动状态。 在标准AEM安装中，该功能在作者运行模式下处于禁用状态，在发布运行模式下为/content启用。

**OSGi组件的特性**

已引入以下2个OSGi组件来定义身份验证要求并指定专用登录路径：

* `com.adobe.granite.auth.requirement.impl.RequirementService`
* `com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler`

**com.adobe.granite.auth.requirement.impl.RequiredService**

<table>
 <tbody>
  <tr>
   <td>标签</td>
   <td>-</td>
  </tr>
  <tr>
   <td>描述</td>
   <td>用于验证要求的专用OSGi服务，该服务将观察器注册到影响验证要求的内容更改（通过<code>granite:AuthenticationRequirement</code>混合类型）和登录路径暴露到<code>LoginSelectorHandler</code>。 </td>
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

| 标签 | Adobe Granite身份验证要求和登录路径处理程序 |
|---|---|
| 描述 | `RequirementHandler` 更新Apache Sling身份验证要求以及相关登录路径的相应排除的实现。 |
| 配置属性 | `supportedPaths` |
| 配置策略 | `ConfigurationPolicy.REQUIRE` |
| 引用 | NA |

#### 配置选项{#configuration-options-1}

CUG重写的身份验证相关部分只附带与Adobe Granite身份验证要求和登录路径处理程序关联的单个配置选项：

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
   <td><p>标签=支持的路径</p> <p>名称= 'supportedPaths'</p> </td>
   <td>Set&lt;String&gt;</td>
   <td>-</td>
   <td>此处理函数将遵守身份验证要求的路径。 如果要将<code>granite:AuthenticationRequirement</code>混音类型添加到节点而不强制执行（例如，在创作实例中），请取消设置此配置。 如果缺少，则禁用该功能。 </td>
  </tr>
 </tbody>
</table>

## 自AEM 6.3 {#default-configuration-since-aem}以来的默认配置

默认情况下，新安装的AEM将使用新的实现来进行CUG功能的授权和身份验证相关部分。 旧实现“Adobe Granite Closed User Group(CUG)Support”已弃用，默认情况下将在所有AEM安装中禁用。 新实施将改为启用，如下所示：

### 作者实例{#author-instances}

| **&quot;Apache Jackrabbit Oak CUG配置&quot;** | **解释** |
|---|---|
| 支持的路径`/content` | 已启用CUGpolicies的访问控制管理。 |
| 已启用CUG评估FALSE | 权限评估已禁用。 CUG策略不起作用。 |
| 等级 | 200 | 请参阅Oak文档。 |

>[!NOTE]
>
>默认创作实例中不存在&#x200B;**Apache Jackrabbit Oak CUG Exclude 列表**&#x200B;和&#x200B;**AdobeGranite身份验证要求和登录路径处理程序**&#x200B;的配置。

### 发布实例{#publish-instances}

| **&quot;Apache Jackrabbit Oak CUG配置&quot;** | **解释** |
|---|---|
| 支持的路径`/content` | 在配置的路径下启用了CUG策略的访问控制管理。 |
| 已启用CUG评估 | 在已配置路径下启用权限评估。 CUG策略对`Session.save()`生效。 |
| 等级 | 200 | 请参阅Oak文档。 |

| **&quot;Apache Jackrabbit Oak CUG排除列表&quot;** | **解释** |
|---|---|
| 主体名称管理员 | 从CUG评估中排除管理员主体。 |

| **“Adobe Granite身份验证要求和登录路径处理程序”** | **解释** |
|---|---|
| 支持的路径`/content` | 通过`granite:AuthenticationRequired`混合类型在存储库中定义的身份验证要求在`Session.save()`后生效。 `/content`Sling Authenticator会更新。 将忽略在支持的路径之外添加混音类型。 |

## 禁用CUG授权和身份验证要求{#disabling-cug-authorization-and-authentication-requirement}

如果给定安装不使用CUG或使用不同的身份验证和授权手段，则可以完全禁用新实现。

### 禁用CUG授权{#disable-cug-authorization}

有关如何从复合授权设置中删除CUG授权模型的详细信息，请参阅[CUG可插件](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)文档。

### 禁用身份验证要求{#disable-the-authentication-requirement}

为了禁用对`granite.auth.authhandler`模块提供的身份验证要求的支持，足以删除与&#x200B;**AdobeGranite身份验证要求和登录路径处理程序**&#x200B;关联的配置。

>[!NOTE]
>
>但请注意，删除配置不会取消注册混合类型，该类型仍适用于节点，但不会产生任何影响。

## 与其他模块{#interaction-with-other-modules}的交互

### Apache Jackrabbit API {#apache-jackrabbit-api}

为了反映CUG授权模型使用的新类型的访问控制策略，扩展了Apache Jackrabbit定义的API。 由于`jackrabbit-api`模块的版本2.11.0定义了一个名为`org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`的新接口，该接口从`javax.jcr.security.AccessControlPolicy`扩展。

### Apache Jackrabbit FileVault {#apache-jackrabbit-filevault}

Apache Jackrabbit FileVault的导入机制已调整为处理`PrincipalSetPolicy`类型的访问控制策略。

### Apache Sling内容分发{#apache-sling-content-distribution}

请参阅上面的[Apache Jackrabbit FileVault](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault)部分。

### Adobe Granite复制{#adobe-granite-replication}

为了能够在不同AEM实例之间复制CUG策略，已对复制模块进行了稍微调整：

* `DurboImportConfiguration.isImportAcl()` 是字面解释的，只会影响访问控制政策的实施  `javax.jcr.security.AccessControlList`

* `DurboImportTransformer` 将仅对真实ACL遵守此配置
* 其他策略（如由CUG授权模型创建的`org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`实例）将始终被复制，并将忽略配置选项`DurboImportConfiguration.isImportAcl`()。

复制CUG策略存在一个限制。 如果在删除相应的混合节点类型`rep:CugMixin,`的情况下删除了给定的CUG策略，则复制时不会反映删除。 通过始终在删除策略时删除混音来解决此问题。 但是，如果手动添加混合类型，则可能会显示限制。

### Adobe Granite身份验证处理程序{#adobe-granite-authentication-handler}

随`com.adobe.granite.auth.authhandler`包一起提供的AdobeGranite HTTP头身份验证处理程序&#x200B;**包含对由同一模块定义的`CugSupport`接口的引用。**&#x200B;它用于在某些情况下计算“领域”，并回退到使用处理程序配置的领域。

已对此进行了调整，使对`CugSupport`的引用成为可选的，以确保在给定设置决定重新启用已弃用的实现时最大的向后兼容性。 使用该实现的安装将不再获取从CUG实现提取的领域，但将始终显示使用&#x200B;**Adobe Granite HTTP头身份验证处理程序**&#x200B;定义的领域。

>[!NOTE]
>
>默认情况下，**AdobeGranite HTTP头身份验证处理程序**&#x200B;仅在发布运行模式下配置，并启用“禁用登录页面”(`auth.http.nologin`)选项。

### AEM LiveCopy {#aem-livecopy}

通过添加一个额外节点和一个额外属性，在存储库中表示配置与LiveCopy相关的CUG，如下所示：

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

这两个元素均在`cq:Page`下创建。 在当前设计中，MSM仅处理位于`cq:PageContent`(`jcr:content`)节点下的节点和属性。

因此，无法从Blueprint中将CUG组转出到Live Copy。 请在配置Live Copy时针对此进行规划。

## 使用新CUG实施{#changes-with-the-new-cug-implementation}进行更改

本节旨在概述对CUG功能所做的更改，并比较旧实施和新实施。 它列表了影响配置CUG支持方式的更改，并描述了如何在存储库内容中管理CUG以及由谁管理CUG。

### CUG设置和配置{#differences-in-cug-setup-and-configuration}中的差异

已弃用的OSGi组件&#x200B;**Adobe Granite Closed User Group(CUG)Support**(`com.day.cq.auth.impl.cug.CugSupportImpl`)已被新组件替换，以便能够单独处理以前CUG功能的授权和身份验证相关部分。

## 在管理存储库内容{#differences-in-managing-cugs-in-the-repository-content}中的CUG方面的差异

以下几节从实施和安全角度描述了新旧实施之间的差异。 虽然新实施旨在提供相同的功能，但在使用新CUG时，需要了解的细微更改非常重要。

### 与授权的差异{#differences-with-regards-to-authorization}

以下列表概述了授权方面的主要差异：

**CUG专用访问控制内容**

在旧的实现中，默认授权模型用于在发布时操作访问控制列表策略，由CUG授权的设置替换任何现有ACE。 这是由编写常规的、剩余的JCR属性触发的，这些属性在发布时进行了解释。

在新的实现中，默认授权模型的访问控制设置不受任何正在创建、修改或删除的CUG的影响。 而是将名为`PrincipalSetPolicy`的新策略类型作为附加访问控制内容应用到目标节点。 此附加策略将作为目标节点的子级，并且如果存在，将作为默认策略节点的同级。

**在访问控制管理中编辑CUG策略**

从剩余JCR属性移动到专用访问控制策略会影响创建或修改CUG功能授权部分所需的权限。 由于这被视为对访问控制内容的修改，因此需要`jcr:readAccessControl`和`jcr:modifyAccessControl`权限才能写入存储库。 因此，只有有权修改页面访问控制内容的内容作者才能设置或修改此内容。 这与旧实施相反，旧实施中编写常规JCR属性的能力足够，导致权限提升。

**目标节点由策略定义**

应在JCR节点创建CUG策略，该节点定义要受受限读取访问约束的子树。 这可能是AEM页面，以防CUG影响整个树。

请注意，将CUG策略仅放置在给定页面下方的jcr:content节点上将仅限访问给定页面的内容s.str，但不会对任何同级或子页面生效。 这可能是一个有效的用例，并且可以通过允许应用细粒度访问内容的存储库编辑器来实现。 但是，它与前一个实现形成了对比，在前一个实现中，将cq:cugEnabled属性放在jcr:content节点上是在内部重新映射到页面节点的。 不再执行此映射。

**使用CUG策略的权限评估**

从旧的CUG支持转向其他授权模型，改变了评估有效读取权限的方式。 如[Jackrabbit文档](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)中所述，只有在对Oak存储库中配置的所有型号进行权限评估时，才能授予允许视图`CUGcontent`的给定主体读取权限。

换句话说，在评估有效权限时，将考虑`CUGPolicy`和默认访问控制条目，并且只有在两种策略都授予对CUG内容的读取访问权时，才授予对CUG内容的读取访问权。 在默认AEM发布安装中，每个人都有权读取完整`/content`树，CUG策略的效果将与旧实施相同。

**按需评估**

CUG授权模型允许单独开启访问控制管理和权限评估：

* 如果模块有一个或多个可创建CUG的支持路径，则会启用访问控制管理
* 仅当另外选中选项&#x200B;**已启用CUG评估**&#x200B;时，才启用权限评估。

在新的AEM默认设置CUG策略评估中，它仅启用“发布”运行模式。 有关详细信息，请参阅自AEM 6.3](#default-configuration-since-aem)以来的[默认配置的详细信息。 可以通过比较给定路径的有效策略与存储在内容中的策略来验证这一点。 只有在启用CUG的权限评估时，才会显示有效策略。

如上所述，CUG访问控制策略现在始终存储在内容中，但仅当在Apache Jackrabbit Oak **CUG配置的系统控制台中打开**&#x200B;启用&#x200B;**CUG评估后，才会强制执行对这些策略产生的有效权限的评估。** 默认情况下，它仅以“发布”运行模式启用。

### 与身份验证{#differences-with-regards-to-authentication}的区别

与身份验证有关的差异如下所述。

#### 用于身份验证要求的专用混合类型{#dedicated-mixin-type-for-authentication-requirement}

在前一个实现中，CUG的授权和身份验证方面都由单个JCR属性(`cq:cugEnabled`)触发。 就身份验证而言，这导致对与Apache Sling Authenticator实现一起存储的身份验证要求进行更新列表。 在新实施中，通过用专用混合类型(`granite:AuthenticationRequired`)标记目标节点实现相同结果。

#### 排除登录路径{#property-for-excluding-login-path}的属性

mixin类型定义一个名为`granite:loginPath`的可选属性，该属性基本上与`cq:cugLoginPage`属性相对应。 与之前的实现不同，只有在其声明节点类型为所述混合时，登录路径属性才会得到尊重。 在不设置mixin类型的情况下添加具有该名称的属性将不起作用，不会向验证器报告新要求或对登录路径的排除。

#### 身份验证要求的权限{#privilege-for-authentication-requirement}

添加或删除混音类型需要授予`jcr:nodeTypeManagement`权限。 在上一个实现中，`jcr:modifyProperties`权限用于编辑剩余属性。

就`granite:loginPath`而言，添加、修改或删除属性时需要相同的权限。

#### 目标节点由混合类型{#target-node-defined-by-mixin-type}定义

应在JCR节点创建身份验证要求，该节点定义要受强制登录影响的子树。 如果CUG预期会影响整个树，则这可能是AEM页面，而新实施的UI将随后在页面节点上添加身份验证要求混合类型。

将CUG策略仅放置在给定页面下方的jcr:content节点上将仅限访问内容，但不会影响页面节点本身或任何子页面。

这可能是一个有效的方案，并且可以使用允许将混音放置在任何节点的存储库编辑器。 但是，此行为与前一个实现形成了对比，在前一个实现中，将cq:cugEnabled或cq:cugLoginPage属性放置到jcr:content节点上会在内部重新映射到页面节点。 不再执行此映射。

#### 已配置支持的路径{#configured-supported-paths}

`granite:AuthenticationRequired` mixin类型和granite:loginPath属性将仅在&#x200B;**AdobeGranite身份验证要求和登录路径处理程序**&#x200B;中提供的&#x200B;**支持的路径**&#x200B;配置选项集所定义的范围内得到遵守。 如果未指定任何路径，则完全禁用身份验证要求功能。 在这种情况下，在添加或设置给定JCR节点时，mixin类型或属性生效。

### JCR内容、OSGi服务和配置的映射{#mapping-of-jcr-content-osgi-services-and-configurations}

以下文档提供了旧实施和新实施之间OSGi服务、配置和存储库内容的全面映射。

自AEM 6.3以来的CUG映射

[获取文件](assets/cug-mapping.pdf)

## 升级CUG {#upgrade-cug}

### 使用已弃用的CUG {#existing-installations-using-the-deprecated-cug}的现有安装

旧的CUG支持实施已弃用，将在将来的版本中删除。 从AEM 6.3以前的版本升级时，建议移到新实施。

对于升级的AEM安装，务必确保只启用一个CUG实施。 新的和旧的、已弃用的CUG支持的组合未经测试，并可能导致不希望的行为：

* Sling Authenticator中与身份验证要求的冲突
* 当与旧CUG关联的ACL设置与新CUG策略冲突时，拒绝读取访问。

### 迁移现有CUG内容{#migrating-existing-cug-content}

Adobe为迁移到新的CUG实施提供了工具。 要使用它，请执行以下步骤：

1. 转到`https://<serveraddress>:<serverport>/system/console/cug-migration`以访问该工具。
1. 输入要检查CUG的根路径，然后按&#x200B;**执行练习**&#x200B;按钮。 这将扫描在所选位置中有资格进行转换的CUG。
1. 查看结果后，按&#x200B;**执行迁移**&#x200B;按钮可迁移到新实现。

>[!NOTE]
>
>如果遇到问题，可以在`com.day.cq.auth.impl.cug`上设置&#x200B;**DEBUG**&#x200B;级别的特定记录器，以获取迁移工具的输出。 有关如何执行此操作的详细信息，请参阅[日志记录](/help/sites-deploying/configure-logging.md)。
