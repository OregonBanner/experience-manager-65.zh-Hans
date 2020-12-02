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
translation-type: tm+mt
source-git-commit: 2142df4f7579e052e18879b437fc43911010b475
workflow-type: tm+mt
source-wordcount: '6890'
ht-degree: 0%

---


# AEM{#closed-user-groups-in-aem}中已关闭的用户组

## 简介 {#introduction}

自AEM 6.3起，新的“已关闭的用户组”实施旨在解决现有实施中存在的性能、可扩展性和安全问题。

>[!NOTE]
>
>为了简单起见，本文档中将使用CUG缩写。

新实施的目标是在需要时涵盖现有功能，同时解决旧版本的问题和设计限制。 结果是具有以下特点的新CUG设计：

* 认证和授权元素的清晰分离，可单独或组合使用；
* 专用的授权模型，在配置的CUG树上反映受限读取访问，不会干扰其他访问控制设置和权限要求；
* 在创作实例时通常需要受限读取权限的访问控制设置与发布时通常只需要的权限评估之间进行分离；
* 编辑受限读取访问，而不提升权限；
* 专用节点类型扩展标记认证要求；
* 与身份验证要求关联的可选登录路径。

### 新的自定义用户组实现{#the-new-custom-user-group-implementation}

在AEM的上下文中称为CUG的步骤包括：

* 限制对需要保护的树的读取访问，并且仅允许对包含给定CUG实例的承担者进行读取，或者完全从CUG评估中排除。 这称为&#x200B;**authorization**&#x200B;元素。
* 在给定树上强制进行身份验证，并（可选）为该树指定一个专用登录页，该页随后会被排除。 这称为&#x200B;**authentication**&#x200B;元素。

新的实现设计为在验证和授权元素之间划出一条线。 从AEM 6.3开始，可以在不显式添加身份验证要求的情况下限制读访问。 例如，如果给定实例需要完全身份验证，或者给定树已驻留在需要身份验证的子树中。

同样，给定的树可以用身份验证要求进行标记，而无需更改有效权限设置。 组合和结果列在[组合CUG策略和身份验证要求](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement)部分。

## 概述 {#overview}

### 授权：限制读访问{#authorization-restricting-read-access}

CUG的主要功能是限制内容存储库中给定树上除选定承担者之外的所有人的读取访问权限。 新的实现采用的方法不是即时处理默认访问控制内容，而是定义表示CUG的专用访问控制策略类型。

#### CUG的访问控制策略{#access-control-policy-for-cug}

此新型策略具有以下特点：

* 访问控制org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy（由Apache Jackrabbit API定义）类型的策略；
* PrincipalSetPolicy授予可修改的主体集的权限；
* 授予的权限和策略的范围是实施详细信息。

用于表示CUG的PrincipalSetPolicy的实施还定义了：

* CUG策略仅授予对常规JCR项目的读取权限(例如，访问控制内容被排除);
* 范围由包含CUG策略的访问控制节点定义；
* CUG策略可以嵌套，嵌套的CUG将新CUG开始，而不继承“父”CUG的主体集；
* 如果启用了评估，则策略的效果将继承到整个子树，下一个嵌套CUG。

这些CUG策略通过名为oak-authorization-cug的单独授权模块部署到AEM实例。 本模块附带有自己的访问控制管理和权限评估。 换言之，默认的AEM设置提供一个Oak内容存储库配置，该配置结合了多个授权机制。 有关详细信息，请参阅Apache Oak Documentation](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)上的[此页。

在此复合设置中，新的CUG不会替换附加到访问控制节点的现有目标内容，而是设计为补充，以后也可以删除它而不影响原始访问控制，在AEM中默认情况下，它将是访问控制列表。

与前一实施相比，新的CUG政策始终被承认并视为访问控制内容。 这意味着它们是使用JCR访问控制管理API创建和编辑的。 有关详细信息，请参阅[管理CUG策略](#managing-cug-policies)部分。

#### CUG策略的权限评估{#permission-evaluation-of-cug-policies}

除了CUG的专用访问控制管理，新授权模型还允许有条件地启用其策略的权限评估。 这允许在分阶段环境中设置CUG策略，并且只允许在复制到生产环境后评估有效权限。

CUG策略的权限评估以及与默认或任何附加授权模型的交互遵循Apache Jackrabbit Oak中为多个授权机制设计的模式：如果且仅当所有模型授予访问权限时，才授予给定权限集。 有关详细信息，请参阅[此页](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)。

与用于处理和评估CUG策略的授权模型相关的权限评估适用以下特性：

* 它只处理常规节点和属性的读取权限，而不处理读取访问控制内容
* 它不处理对受保护JCR内容(访问控制、节点类型信息、版本控制、锁定或用户管理等)进行修改所需的写入权限或任何类型的权限；这些权限不受CUG策略影响，并且不会由关联的授权模型评估。 是否授予这些权限取决于在安全设置中配置的其他模型。

单个CUG策略对权限评估的影响可概括如下：

* 除策略中列出的包含被排除的承担者或承担者的主体外，所有人均拒绝读取权限；
* 该策略对包含该策略及其属性的访问控制节点生效；
* 此效果还会在层次结构中继承——即由访问控制节点定义的项目树；
* 但是，它不影响访问控制节点的同级和祖先；
* 给定CUG的继承在嵌套CUG处停止。

#### 最佳实践 {#best-practices}

在通过CUG定义受限读取访问权限时，应考虑以下最佳实践：

* 有意识地决定您对CUG的需求是限制读取访问还是验证要求。 如果是后者，或者如果两者都需要，请查阅最佳实践部分，以了解有关身份验证要求的详细信息
* 为需要保护的数据或内容创建威胁模型，以识别威胁边界并清晰了解数据的敏感性以及与授权访问相关的角色
* 为存储库内容和CUG建立模型，同时要考虑到与一般授权相关的方面和最佳做法：

   * 请记住，仅当给定的CUG和设置授权中部署的其他模块的评估允许给定主体读取给定存储库项目时，才会授予读取权限
   * 避免创建冗余CUG，因为其他授权模块已限制读取访问
   * 对嵌套CUG的过度需求可能会突出内容设计中的问题
   * 对CUG的过度需求（例如，在每个页面上）可能表明需要一个可能更适合满足应用程序和手头内容的特定安全需求的自定义授权模型。

* 将CUG策略支持的路径限制为存储库中的几个树，以便获得优化的性能。 例如，仅允许作为自AEM 6.3以来的默认值发运的/content节点下的CUG。
* CUG策略旨在授予对一小组主体的读取权限。 需要大量原则可能会突出内容或应用程序设计中的问题，并应重新考虑。

### 身份验证：定义身份验证要求{#authentication-defining-the-auth-requirement}

CUG功能的身份验证相关部分允许标记需要身份验证的树，并可选地指定专用登录页。 根据先前版本，新实现允许在内容存储库中标记需要身份验证的树，并有条件地启用与`Sling org.apache.sling.api.auth.Authenticator`的同步，该&lt;a0/>负责最终实施该要求并重定向到登录资源。

通过提供`sling.auth.requirements`注册属性的OSGi服务，向身份验证器注册这些要求。 然后，这些属性用于动态扩展身份验证要求。 有关详细信息，请参阅[Sling文档](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS)。

#### 使用专用混音类型{#defining-the-authentication-requirement-with-a-dedicated-mixin-type}定义身份验证要求

出于安全原因，新实现用名为`granite:AuthenticationRequired`的专用混音类型替换剩余JCR属性的使用，该类型为登录路径`granite:loginPath`定义STRING类型的单个可选属性。 只有与此混合类型相关的内容更改才能更新向Apache Sling Authenticator注册的要求。 在保持任何临时修改时跟踪这些修改，因此需要`javax.jcr.Session.save()`调用才能生效。

`granite:loginPath`属性也是如此。 只有由身份验证要求相关的混音类型定义时，才会尊重它。 在非结构化JCR节点上添加具有此名称的剩余属性将不显示所需效果，负责更新OSGi注册的处理程序将忽略该属性。

>[!NOTE]
>
>设置登录路径属性是可选的，并且仅当需要身份验证的树无法返回到默认登录页面或以其他方式继承的登录页面时才需要。 请参阅下面的[登录路径评估](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path)。

#### 向Sling Authenticator {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}注册身份验证要求和登录路径

由于此类型的身份验证要求应限于某些运行模式以及内容存储库中的一小部分树，因此对要求混合类型和登录路径属性的跟踪是有条件的，并绑定到定义受支持路径的相应配置（请参阅下面的配置选项）。 因此，只有这些受支持路径范围内的更改才会触发OSGi注册的更新，其他位置将忽略mixin类型和属性。

默认的AEM安装程序现在允许在作者运行模式下设置混音，但只有在复制到发布实例后才会生效，从而利用此配置。 有关Sling如何强制执行身份验证要求的详细信息，请参阅[此页](https://sling.apache.org/documentation/the-sling-engine/authentication/authenticationframework.html)。

在已配置的受支持路径中添加`granite:AuthenticationRequired`混音类型将导致更新负责处理程序的OSGi注册，该注册包含具有`sling.auth.requirements`属性的新的附加条目。 如果给定的身份验证要求指定了可选的`granite:loginPath`属性，则该值将附加地注册到验证器中，并带有“-”前缀，以便从身份验证要求中排除。

#### 身份验证要求{#evaluation-and-inheritance-of-the-authentication-requirement}的评估和继承

Apache Sling身份验证要求应通过页面或节点层次结构进行继承。 继承和验证要求评估的详细信息（如顺序和优先级）被视为一个实施详细信息，本文中不予记录。

#### 登录路径{#evaluation-of-login-path}的评估

验证时对登录路径的评估和重定向到相应资源的评估是AdobeGranite登录选择器身份验证处理程序(`com.day.cq.auth.impl.LoginSelectorHandler`)的实现详细信息，该处理程序是默认配置为AEM的Apache Sling AuthenticationHandler。

调用`AuthenticationHandler.requestCredentials`时，此处理函数会尝试确定将用户重定向到的映射登录页。 这包括以下步骤：

* 区分过期密码和需要定期登录作为重定向的原因；
* 如果是定期登录，则测试是否可以按以下顺序获得登录路径：

   * 从新`com.adobe.granite.auth.requirement.impl.RequirementService`实现的LoginPathProvider中，
   * 从旧的、已弃用的CUG实现，
   * 从登录页面映射（如`LoginSelectorHandler`中定义）,
   * 最后，回退到默认登录页，如`LoginSelectorHandler`所定义。

* 一旦通过上述呼叫获得了有效的登录路径，用户的请求将被重定向到该页面。

本文档的目标是对内部`LoginPathProvider`接口所显示登录路径的评估。 自AEM 6.3起发运的实施如下所示：

* 登录路径的注册取决于对过期密码的区别，以及是否需要定期登录作为重定向的原因
* 如果是定期登录，则测试是否可以按以下顺序获得登录路径：

   * 从新`com.adobe.granite.auth.requirement.impl.RequirementService`实现的`LoginPathProvider`,
   * 从旧的、已弃用的CUG实现，
   * 从使用`LoginSelectorHandler`定义的登录页面映射，
   * 最后，回退到使用`LoginSelectorHandler`定义的默认登录页面。

* 一旦通过上述呼叫获得了有效的登录路径，用户的请求将被重定向到该页面。

由Granite中新的身份验证要求支持实现的`LoginPathProvider`显示由`granite:loginPath`属性定义的登录路径，这些属性又由上述的混音类型定义。 保存登录路径和属性值本身的资源路径的映射将保留在内存中，并将被评估为为层次结构中的其他节点找到合适的登录路径。

>[!NOTE]
>
>仅对与配置的支持路径中的资源关联的请求执行评估。 对于任何其他请求，将评估确定登录路径的替代方法。

#### 最佳实践 {#best-practices-1}

在定义身份验证要求时，应考虑以下最佳实践：

* 避免嵌套身份验证要求：在树的开始上放置单个身份验证要求标记应足够，并且继承到由目标节点定义的整个子树。 该树中的其他身份验证要求应被视为冗余，在评估Apache Sling中的身份验证要求时，可能会导致性能问题。 通过将授权和认证相关的CUG区域分开，可以通过CUG或其他类型的策略限制读访问，同时强制对整个树的认证。
* 建模存储库内容，使身份验证要求适用于整个树，无需再次从要求中排除嵌套子树。
* 要避免指定并随后注册冗余登录路径，请执行以下操作：

   * 依赖继承并避免定义嵌套登录路径，
   * 不要将可选登录路径设置为与默认值或继承值对应的值，
   * 应用程序开发人员应确定在与`LoginSelectorHandler`关联的全局登录路径配置（默认和映射）中应配置哪些登录路径。

## 存储库{#representation-in-the-repository}中的表示形式

### 存储库{#cug-policy-representation-in-the-repository}中的CUG策略表示法

Oak文档涵盖新CUG策略在存储库内容中的反映方式。 有关详细信息，请参阅[此页](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository)。

### 存储库{#authentication-requirement-in-the-repository}中的身份验证要求

对单独身份验证要求的需求反映在存储库内容中，并且在目标节点处放置了专用的混合节点类型。 混合类型定义一个可选属性，用于为目标节点定义的树指定专用登录页。

与登录路径关联的页面可能位于该树的内部或外部。 它将被排除在身份验证要求之外。

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## 管理CUG策略和身份验证要求{#managing-cug-policies-and-authentication-requirement}

### 管理CUG策略{#managing-cug-policies}

使用JCR访问控制管理API管理用于限制CUG读访问的新类型访问控制策略，并遵循[JCR 2.0规范](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html)中描述的机制。

#### 设置新的CUG策略{#set-a-new-cug-policy}

在以前没有CUG集的节点应用新CUG策略的代码。 请注意，`getApplicablePolicies`将仅返回以前未设置的新策略。 最后，策略需要写回，并且更改需要保留。

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

#### 编辑现有CUG策略{#edit-an-existing-cug-policy}

编辑现有CUG策略需要以下步骤。 请注意，修改后的策略需要写回，并且需要使用`javax.jcr.Session.save()`保留更改。

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

JCR访问控制管理定义了一种检索在给定路径上生效的策略的最佳方法。 由于CUG策略的评估是有条件的，并且取决于要启用的相应配置，调用`getEffectivePolicies`是验证给定CUG策略是否在给定安装中生效的一种简便方法。

>[!NOTE]
>
>请注意`getEffectivePolicies`与随后的代码示例之间的区别，该示例在层次结构中向上游走，以查找给定路径是否已经是现有CUG的一部分。

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

查找在给定路径中定义的所有嵌套CUG，而不管它们是否生效。 有关详细信息，请参阅[配置选项](/help/sites-administering/closed-user-groups.md#configuration-options)部分。

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

由`JackrabbitAccessControlManager`定义的允许按主体编辑访问控制策略的扩展在CUG访问控制管理中未实现，因为定义中，CUG策略始终影响所有主体：与`PrincipalSetPolicy`一起列出的内容将被授予读取访问权限，而所有其他主体将被阻止读取由目标节点定义的树中的内容。

相应的方法始终返回空策略数组，但不会引发异常。

### 管理身份验证要求{#managing-the-authentication-requirement}

通过改变目标节点的有效节点类型来实现新认证要求的创建、修改或移除。 然后，可以使用常规JCR API编写可选的登录路径属性。

>[!NOTE]
>
>如果`RequirementHandler`已配置，且目标包含在受支持路径定义的树中，则上述对给定目标节点的修改将仅反映在Apache Sling Authenticator上（请参阅配置选项一节）。
>
>有关详细信息，请参阅[分配混合节点类型](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3分配混合节点类型)和[添加节点和设置属性](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4添加节点和设置属性)

#### 添加新的身份验证要求{#adding-a-new-auth-requirement}

创建新身份验证要求的步骤详见下文。 请注意，仅当`RequirementHandler`已为包含目标节点的树配置时，才向Apache Sling Authenticator注册此要求。

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### 使用登录路径{#add-a-new-auth-requirement-with-login-path}添加新的身份验证要求

创建新身份验证要求的步骤，包括登录路径。 请注意，如果`RequirementHandler`已为包含目标节点的树配置，则登录路径的要求和排除将仅向Apache Sling Authenticator注册。

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

删除现有登录路径的步骤。 如果`RequirementHandler`已为包含目标节点的树配置，则登录路径条目将仅从Apache Sling Authenticator中取消注册。 与目标节点关联的身份验证要求不受影响。

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

或者，您可以使用下面的方法来实现相同的目的：

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

删除现有身份验证要求的步骤。 如果`RequirementHandler`已为包含目标节点的树配置，则此要求将仅从Apache Sling Authenticator中取消注册。

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### 检索有效身份验证要求{#retrieve-effective-auth-requirements}

没有专用的公共API来读取向Apache Sling Authenticator注册的所有有效身份验证要求。 但是，列表会显示在系统控制台的“**身份验证要求配置**”部分的`https://<serveraddress>:<serverport>/system/console/slingauth`下。

下图显示了包含演示内容的AEM发布实例的身份验证要求。 社区页的突出显示路径说明了本文档中所述实施所添加的要求如何反映在Apache Sling Authenticator中。

>[!NOTE]
>
>在此示例中，未设置可选登录路径属性。 因此，没有向验证器注册第二项。

![chlimage_1-24](assets/chlimage_1-24.jpeg)

#### 检索有效登录路径{#retrieve-the-effective-login-path}

当前没有公共API可检索登录路径，该路径将在匿名访问需要身份验证的资源时生效。 有关如何检索登录路径的实现详细信息，请参阅登录路径评估部分。

但是，请注意，除了使用此功能定义的登录路径之外，还有其他方法可指定重定向到登录，在设计内容模型和给定AEM安装的身份验证要求时，应考虑这些方法。

#### 检索继承的身份验证要求{#retrieve-the-inherited-auth-requirement}

与登录路径一样，没有公共API可检索内容中定义的继承身份验证要求。 以下示例说明如何列表已使用给定层次结构定义的所有身份验证要求，无论这些要求是否生效。 有关详细信息，请参阅[配置选项](/help/sites-administering/closed-user-groups.md#configuration-options)。

>[!NOTE]
>
>建议使用继承机制满足身份验证要求和登录路径，并避免创建嵌套身份验证要求。
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

### 将CUG策略与身份验证要求{#combining-cug-policies-and-the-authentication-requirement}相结合

下表列表了AEM实例中CUG策略的有效组合和身份验证要求，该实例通过配置同时启用了这两个模块。

| **需要身份验证** | **登录路径** | **受限读取访问** | **预期效果** |
|---|---|---|---|
| 是 | 是 | 是 | 如果有效权限评估授予访问权限，则给定用户只能视图用CUG策略标记的子树。 未通过身份验证的用户将被重定向到指定的登录页面。 |
| 是 | 否 | 是 | 如果有效权限评估授予访问权限，则给定用户只能视图用CUG策略标记的子树。 未通过身份验证的用户将被重定向到继承的默认登录页面。 |
| 是 | 是 | 否 | 未通过身份验证的用户将被重定向到指定的登录页面。 是否允许它视图标记有身份验证要求的树取决于该子树中包含的各个项目的有效权限。 没有专用CUG限制读取访问。 |
| 是 | 否 | 否 | 未通过身份验证的用户将被重定向到继承的默认登录页面。 是否允许它视图带有身份验证要求的树取决于该子树中包含的各个项目的有效权限。 没有专用CUG限制读取访问。 |
| 否 | 否 | 是 | 如果有效的权限评估授予访问权限，则给定的已验证或未验证的用户只能视图用CUG策略标记的子树。 未经身份验证的用户将得到同等对待，不会被重定向到登录。 |

>[!NOTE]
>
>上面未列出“身份验证要求”=“否”和“登录路径”=“是”的组合，因为“登录路径”是与身份验证要求关联的可选属性。 指定不添加定义混音类型而使用该名称的JCR属性将不起作用，并且相应的处理函数将忽略该属性。

## OSGi组件和配置{#osgi-components-and-configuration}

本节概述了OSGi组件以及新CUG实现中引入的各个配置选项。

另请参阅CUG映射文档，以全面映射旧实施和新实施之间的配置选项。

### 授权：设置和配置{#authorization-setup-and-configuration}

新的授权相关部件包含在&#x200B;**Oak CUG授权**&#x200B;捆绑包(`org.apache.jackrabbit.oak-authorization-cug`)中，它是AEM默认安装的一部分。 该绑定定义了一个分离的授权模型，该模型旨在作为管理读访问的一种附加方式进行部署。

#### 设置CUG授权{#setting-up-cug-authorization}

有关设置CUG授权的详细说明，请参阅[相关Apache文档](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)。 默认情况下，AEM在所有运行模式下都部署了CUG授权。 该分步指令还可用于在那些需要不同授权设置的安装中禁用CUG授权。

#### 配置推荐人筛选器{#configuring-the-referrer-filter}

您还需要配置[Sling推荐人过滤器](/help/sites-administering/security-checklist.md#the-sling-referrer-filter)，其中包含可用于访问AEM的所有主机名；例如，通过CDN、负载平衡器等进行。

如果未配置推荐人过滤器，则当用户尝试登录CUG站点时，将看到与以下内容类似的错误：

```shell
31.01.2017 13:49:42.321 *INFO* [qtp1263731568-346] org.apache.sling.security.impl.ReferrerFilter Rejected referrer header for POST request to /libs/granite/core/content/login.html/j_security_check : https://hostname/libs/granite/core/content/login.html?resource=%2Fcontent%2Fgeometrixx%2Fen%2Ftest-site%2Ftest-page.html&$$login$$=%24%24login%24%24&j_reason=unknown&j_reason_code=unknown
```

#### OSGi组件{#characteristics-of-osgi-components}的特性

已引入以下两个OSGi组件来定义身份验证要求和指定专用登录路径：

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
    </ul> <p>另请参阅下面的配置选项一节。</p> </td>
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

主要配置选项有：

* `cugSupportedPaths`:指定可能包含CUG的子树。未设置默认值
* `cugEnabled`:配置选项，以启用对当前CUG策略的权限评估。

有关与CUG授权模块相关的可用配置选项的详细信息，请参阅[Apache Oak文档](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration)。

#### 排除CUG评估{#excluding-principals-from-cug-evaluation}的承担者

在前一个实施中，个人负责人免于进行CUG评估。 新的CUG授权通过一个名为CugExclude的专用接口覆盖此权限。 Apache Jackrabbit Oak 1.4附带默认实现，该实现不包括固定的主体集以及允许配置单个主体名称的扩展实现。 后者是在AEM发布实例中配置的。

自AEM 6.3以来的默认值可防止以下承担者受到CUG策略的影响：

* 管理主体（管理员用户、管理员组）
* 服务用户主体
* 存储库内部系统主体

有关详细信息，请参阅下面[自AEM 6.3](#default-configuration-since-aem)以来的默认配置部分中的表。

在&#x200B;**Apache Jackrabbit Oak CUG排除列表**&#x200B;的配置部分的系统控制台中，可以更改或展开对“管理员”组的排除。

或者，可以提供和部署CugExclude接口的自定义实现，以根据特殊需要调整被排除的承担者集。 有关详细信息和示例实现，请参阅有关[CUG可插件](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)的文档。

### 身份验证：设置和配置{#authentication-setup-and-configuration}

新的与身份验证相关的部分包含在&#x200B;**AdobeGranite身份验证处理程序**&#x200B;包中（`com.adobe.granite.auth.authhandler`版本5.6.48）。 此捆绑包是AEM默认安装的一部分。

为了为已弃用的CUG支持设置身份验证要求替换，在给定的AEM安装中，必须存在某些OSGi组件并且它们处于活动状态。 有关详细信息，请参阅下面的&#x200B;**OSGi组件的特性**。

>[!NOTE]
>
>由于RequirementHandler的强制配置选项，仅当通过指定一组受支持的路径启用了该功能时，验证相关部分才处于活动状态。 在标准AEM安装中，该功能在作者运行模式下处于禁用状态，在发布运行模式下处于/content启用状态。

**OSGi组件的特性**

已引入以下2个OSGi组件来定义身份验证要求并指定专用登录路径：

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
   <td>用于验证要求的专用OSGi服务，该服务向<code>LoginSelectorHandler</code>公开影响验证要求的内容更改（通过<code>granite:AuthenticationRequirement</code>混音类型）和登录路径。 </td>
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
| 描述 | `RequirementHandler` 更新Apache Sling身份验证要求以及相关登录路径的相应排除的实现。 |
| 配置属性 | `supportedPaths` |
| 配置策略 | `ConfigurationPolicy.REQUIRE` |
| 引用 | NA |

#### 配置选项{#configuration-options-1}

CUG重写的身份验证相关部分只附带与AdobeGranite身份验证要求和登录路径处理程序关联的单个配置选项：

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
   <td>此处理程序将遵守身份验证要求的路径。 如果要将<code>granite:AuthenticationRequirement</code>混音类型添加到节点而不强制执行（例如，在创作实例上），请取消设置此配置。 如果缺失，则禁用该功能。 </td>
  </tr>
 </tbody>
</table>

## 自AEM 6.3 {#default-configuration-since-aem}以来的默认配置

默认情况下，新安装的AEM将使用新的实现来进行CUG功能的授权和身份验证相关部分。 旧实现“AdobeGranite已关闭的用户组(CUG)支持”已弃用，默认情况下将在所有AEM安装中禁用。 新实施将改为启用，如下所示：

### 作者实例{#author-instances}

| **&quot;Apache Jackrabbit Oak CUG配置&quot;** | **说明** |
|---|---|
| 支持的路径`/content` | 已启用CUGpolicies的访问控制管理。 |
| 启用CUG评估为FALSE | 权限评估已禁用。 CUG策略无效。 |
| 等级 | 200 | 请参阅Oak文档。 |

>[!NOTE]
>
>默认创作实例中不存在&#x200B;**Apache Jackrabbit Oak CUG排除列表**&#x200B;和&#x200B;**AdobeGranite身份验证要求和登录路径处理程序**&#x200B;的配置。

### 发布实例{#publish-instances}

| **&quot;Apache Jackrabbit Oak CUG配置&quot;** | **说明** |
|---|---|
| 支持的路径`/content` | CUG策略的访问控制管理在配置路径下启用。 |
| 启用CUG评估 | 在配置的路径下启用权限评估。 CUG策略对`Session.save()`生效。 |
| 等级 | 200 | 请参阅Oak文档。 |

| **&quot;Apache Jackrabbit Oak CUG排除列表&quot;** | **说明** |
|---|---|
| 主体名称管理员 | 从CUG评估中不包括管理员主体。 |

| **“AdobeGranite身份验证要求和登录路径处理程序”** | **说明** |
|---|---|
| 支持的路径`/content` | 通过`granite:AuthenticationRequired`混音类型在存储库中定义的身份验证要求在`Session.save()`上生效，具体方式为`/content`以下。 Sling Authenticator将更新。 将忽略在支持的路径之外添加混音类型。 |

## 禁用CUG授权和身份验证要求{#disabling-cug-authorization-and-authentication-requirement}

当给定安装不使用CUG或使用不同的方法进行身份验证和授权时，可以完全禁用新实现。

### 禁用CUG授权{#disable-cug-authorization}

有关如何从复合授权设置中删除CUG授权模型的详细信息，请查阅[CUG可插件](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)文档。

### 禁用身份验证要求{#disable-the-authentication-requirement}

为了禁用`granite.auth.authhandler`模块提供的对身份验证要求的支持，足以删除与&#x200B;**AdobeGranite身份验证要求和登录路径处理程序**&#x200B;关联的配置。

>[!NOTE]
>
>但是，请注意，删除配置不会取消注册混合类型，该类型仍适用于节点而不会生效。

## 与其他模块{#interaction-with-other-modules}的交互

### Apache Jackrabbit API {#apache-jackrabbit-api}

为了反映CUG授权模型使用的新型访问控制策略，扩展了Apache Jackrabbit定义的API。 由于`jackrabbit-api`模块的2.11.0版定义了一个名为`org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`的新接口，该接口从`javax.jcr.security.AccessControlPolicy`扩展。

### Apache Jackrabbit FileVault {#apache-jackrabbit-filevault}

Apache Jackrabbit FileVault的导入机制已调整为处理`PrincipalSetPolicy`类型的访问控制策略。

### Apache Sling内容分发{#apache-sling-content-distribution}

请参阅上面的[Apache Jackrabbit FileVault](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault)部分。

### Adobe花岗岩复制{#adobe-granite-replication}

为了能够在不同AEM实例之间复制CUG策略，复制模块稍作调整：

* `DurboImportConfiguration.isImportAcl()` 是字面解释的，只会影响访问控制政策的实施  `javax.jcr.security.AccessControlList`

* `DurboImportTransformer` 将仅对真正的ACL遵守此配置
* 其他策略（如由CUG授权模型创建的`org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`实例）将始终被复制，并将忽略配置选项`DurboImportConfiguration.isImportAcl`()。

复制CUG策略存在一个限制。 如果在删除相应的混合节点类型`rep:CugMixin,`的情况下删除了给定的CUG策略，则复制时不会反映删除。 已通过始终在删除策略时删除混音来解决此问题。 但是，如果手动添加混音类型，则可能会显示该限制。

### AdobeGranite身份验证处理程序{#adobe-granite-authentication-handler}

随`com.adobe.granite.auth.authhandler`捆绑提供的AdobeGranite HTTP头身份验证处理程序&#x200B;**保存对由同一模块定义的`CugSupport`接口的引用。**&#x200B;它用于在某些情况下计算“领域”，并返回到使用处理函数配置的领域。

已对此进行了调整，使对`CugSupport`的引用成为可选的，以确保在给定设置决定重新启用已弃用的实现时，最大后向兼容性。 使用该实现的安装将不再获取从CUG实现提取的领域，但将始终显示使用&#x200B;**AdobeGranite HTTP头身份验证处理程序**&#x200B;定义的领域。

>[!NOTE]
>
>默认情况下，**AdobeGranite HTTP头身份验证处理程序**&#x200B;仅在发布运行模式下配置，并启用“禁用登录页”(`auth.http.nologin`)选项。

### AEM LiveCopy {#aem-livecopy}

通过添加一个额外节点和一个额外属性，在存储库中表示与LiveCopy一起配置CUG，如下所示：

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

这两个元素都在`cq:Page`下创建。 在当前设计中，MSM只处理`cq:PageContent`(`jcr:content`)节点下的节点和属性。

因此，CUG组无法从Blueprint回滚到Live Copy。 在设置Live Copy时，请相应地计划。

## 对新CUG实现{#changes-with-the-new-cug-implementation}的更改

本节旨在概述对CUG功能所做的更改，以及新旧实施之间的比较。 它列表影响CUG支持配置方式的更改，并描述如何在存储库内容中管理CUG以及由谁管理CUG。

### CUG设置和配置{#differences-in-cug-setup-and-configuration}中的差异

已弃用的OSGi组件&#x200B;**AdobeGranite已关闭的用户组(CUG)支持**(`com.day.cq.auth.impl.cug.CugSupportImpl`)已被新组件替换，以便能够单独处理以前CUG功能的授权和身份验证相关部分。

## 管理存储库内容{#differences-in-managing-cugs-in-the-repository-content}中CUG的差异

以下各节从实施和安全性角度介绍了新旧实施之间的差异。 虽然新实现旨在提供相同的功能，但在使用新CUG时，需要了解一些细微的更改。

### 与授权{#differences-with-regards-to-authorization}的区别

授权方面的主要差异在以下列表中总结：

**CUG专用访问控制内容**

在旧的实现中，默认授权模型用于在发布时操作访问控制列表策略，由CUG授权的设置替换任何现有ACE。 这是由编写常规的、剩余的JCR属性触发的，这些属性在发布时进行解释。

在新的实现中，默认授权模型的访问控制设置不受创建、修改或删除的任何CUG的影响。 而是将名为`PrincipalSetPolicy`的新类型策略作为附加访问控制内容应用于目标节点。 此附加策略将作为目标节点的子项，并且如果存在，将作为默认策略节点的同级。

**在访问控制管理中编辑CUG策略**

从剩余的JCR属性移动到专用访问控制策略会影响创建或修改CUG功能授权部分所需的权限。 由于这被视为对访问控制内容的修改，因此需要`jcr:readAccessControl`和`jcr:modifyAccessControl`权限才能写入存储库。 因此，只有有权修改页面访问控制内容的内容作者才能设置或修改此内容。 这与以前的实施形成鲜明对比，当时编写常规JCR属性的能力已足够，从而导致权限提升。

**目标节点由策略定义**

应在JCR节点创建CUG策略，该节点定义要受受限读取访问的子树。 这可能是AEM页面，以防CUG影响整个树。

请注意，将CUG策略仅放置在给定页面下方的jcr:content节点将仅限访问给定页面的内容s.str，但不会对任何同级或子页面生效。 这可能是一个有效的用例，并且可以通过允许应用细粒度访问内容的存储库编辑器来实现。 但是，它对比了前一个实现，即在jcr:content节点上放置cq:cugEnabled属性是在内部重新映射到页面节点的。 不再执行此映射。

**使用CUG策略的权限评估**

从旧的CUG支持转向其他授权模型，改变评估有效读取权限的方式。 如[Jackrabbit文档](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)中所述，只有在Oak存储库中配置的所有型号的权限评估授予读取访问权限时，才允许给定的视图`CUGcontent`的主体授予读取权限。

换言之，在评估有效权限时，将考虑`CUGPolicy`和默认访问控制条目，并且仅当两种策略都授予对CUG内容的读取访问权时，才授予对CUG内容的读取访问权。 在默认的AEM发布安装中，每个人都有权读取完整`/content`树，CUG策略的效果将与旧实现的效果相同。

**按需评估**

CUG授权模型允许单独开启访问控制管理和权限评估：

* 如果模块具有一个或多个可创建CUG的支持路径，则启用访问控制管理
* 仅当另外选中了选项&#x200B;**已启用CUG评估**&#x200B;时，才启用权限评估。

在新的AEM默认设置CUG策略评估中，它仅启用“发布”运行模式。 有关详细信息，请参阅自AEM 6.3](#default-configuration-since-aem)以来的[默认配置的详细信息。 这可以通过比较给定路径的有效策略与存储在内容中的策略来验证。 只有启用CUG的权限评估后，才会显示有效策略。

如上所述，CUG访问控制策略现在始终存储在内容中，但仅当在Apache Jackrabbit Oak **CUG配置的系统控制台中打开**&#x200B;启用CUG评估&#x200B;**时，才能执行对这些策略产生的有效权限的评估。** 默认情况下，它仅启用“发布”运行模式。

### 与身份验证{#differences-with-regards-to-authentication}的区别

与身份验证相关的差异如下所述。

#### 身份验证要求的专用混合类型{#dedicated-mixin-type-for-authentication-requirement}

在前一个实现中，CUG的授权和身份验证方面都由单个JCR属性(`cq:cugEnabled`)触发。 就身份验证而言，这会导致与Apache Sling Authenticator实现一起存储的身份验证要求的更新列表。 在新的实现中，通过用专用混合类型(`granite:AuthenticationRequired`)标记目标节点而实现相同的结果。

#### 排除登录路径的属性{#property-for-excluding-login-path}

mixin类型定义一个名为`granite:loginPath`的可选属性，该属性基本上与`cq:cugLoginPage`属性相对应。 与以前的实现不同，只有在其声明节点类型为所述混音时，登录路径属性才会受到尊重。 在不设置混音类型的情况下添加具有该名称的属性将不起作用，不会向验证器报告对登录路径的新要求或排除。

#### 身份验证要求的权限{#privilege-for-authentication-requirement}

添加或删除混音类型需要授予`jcr:nodeTypeManagement`权限。 在上一个实现中，`jcr:modifyProperties`权限用于编辑剩余属性。

就`granite:loginPath`而言，添加、修改或删除属性需要相同的权限。

#### 目标节点由Mixin类型{#target-node-defined-by-mixin-type}定义

身份验证要求应在JCR节点创建，该节点定义要受强制登录的子树。 如果CUG预计会影响整个树，则这可能是AEM页面，而新实现的UI将随后在页面节点上添加身份验证要求混合类型。

将CUG策略仅放置在给定页面下方的jcr:content节点上将仅限访问内容，但不会影响页面节点本身或任何子页面。

这可能是有效的方案，并且可以使用允许将混音放置到任何节点的存储库编辑器。 但是，该行为与前一个实现形成了对比，在前一个实现中，将cq:cugEnabled或cq:cugLoginPage属性放置到jcr:content节点上会在内部重新映射到页面节点。 不再执行此映射。

#### 已配置支持的路径{#configured-supported-paths}

`granite:AuthenticationRequired` mixin类型和granite:loginPath属性将仅在&#x200B;**支持的路径**&#x200B;配置选项集定义的范围内进行考虑，这些配置选项与&#x200B;**AdobeGranite身份验证要求和登录路径处理程序**&#x200B;一起提供。 如果未指定路径，则完全禁用身份验证要求功能。 在这种情况下，在添加或设置给定JCR节点时，混合类型或属性将生效。

### JCR内容、OSGi服务和配置的映射{#mapping-of-jcr-content-osgi-services-and-configurations}

以下文档提供了旧实施和新实施之间OSGi服务、配置和存储库内容的全面映射。

自AEM 6.3以来的CUG映射

[获取文件](assets/cug-mapping.pdf)

## 升级CUG {#upgrade-cug}

### 使用已弃用的CUG {#existing-installations-using-the-deprecated-cug}的现有安装

旧的CUG支持实施已弃用，将在将来的版本中删除。 从AEM 6.3以前的版本升级时，建议转到新的实现。

对于升级的AEM安装，确保只启用一个CUG实施非常重要。 新的和已弃用的旧CUG支持的组合未经过测试，可能会导致不期望的行为：

* Sling Authenticator中与身份验证要求的冲突
* 当与旧CUG关联的ACL设置与新CUG策略冲突时，拒绝读取访问。

### 迁移现有CUG内容{#migrating-existing-cug-content}

Adobe为迁移到新CUG实施提供了工具。 要使用它，请执行以下步骤：

1. 转到`https://<serveraddress>:<serverport>/system/console/cug-migration`以访问该工具。
1. 输入要检查CUG的根路径，然后按&#x200B;**执行练习**&#x200B;按钮。 这将扫描选定位置中有资格进行转换的CUG。
1. 查看结果后，按&#x200B;**执行迁移**&#x200B;按钮以迁移到新实现。

>[!NOTE]
>
>如果遇到问题，可以在`com.day.cq.auth.impl.cug`上设置&#x200B;**DEBUG**&#x200B;级别的特定记录器，以获取迁移工具的输出。 有关如何执行此操作的详细信息，请参阅[日志记录](/help/sites-deploying/configure-logging.md)。

