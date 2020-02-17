---
title: AEM中已关闭的用户组
seo-title: AEM中已关闭的用户组
description: 了解AEM中已关闭的用户组。
seo-description: 了解AEM中已关闭的用户组。
uuid: 83396163-86ce-406b-b797-2457ed975ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: a2bd7045-970f-4245-ad5d-a272a654df0a
docset: aem65
translation-type: tm+mt
source-git-commit: 2142df4f7579e052e18879b437fc43911010b475

---


# AEM中已关闭的用户组{#closed-user-groups-in-aem}

## 简介 {#introduction}

自AEM 6.3起，新的已关闭用户组实施旨在解决现有实施中存在的性能、可伸缩性和安全问题。

>[!NOTE]
>
>为了简单起见，本文档中将使用CUG缩写。

新实施的目标是在需要时涵盖现有功能，同时解决旧版本的问题和设计限制。 结果是具有以下特点的新CUG设计：

* 身份验证和授权元素的明确分离，可单独或组合使用；
* 专用的授权模型反映配置的CUG树上的受限读访问，不会干扰其他访问控制设置和权限要求；
* 将创作实例时通常需要的受限读访问权限的访问控制设置与发布时通常只需要的权限评估分开；
* 编辑受限读取权限，而不提升权限；
* 专用节点类型扩展标识认证要求；
* 与身份验证要求关联的可选登录路径。

### 新的自定义用户组实现 {#the-new-custom-user-group-implementation}

在AEM上下文中称为CUG的CUG包含以下步骤：

* 限制对需要保护的树的读取访问，并且仅允许对包含给定CUG实例的承担者进行读取，或者完全从CUG评估中排除。 这称为授 **权元** 。
* 对给定树强制执行身份验证，并可选地为随后被排除的树指定专用登录页。 这称为身份验 **证元** 素。

新的实现设计为在身份验证和授权元素之间划出一条线。 从AEM 6.3开始，可以在不显式添加身份验证要求的情况下限制读访问。 例如，如果给定实例需要完全身份验证，或给定树已驻留在需要身份验证的子树中。

同样，给定的树可以用身份验证要求进行标记，而无需更改有效权限设置。 组合和结果列在“组合CUG策 [略”和“身份验证要求](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement) ”部分。

## 概述 {#overview}

### 授权：限制读取访问 {#authorization-restricting-read-access}

CUG的主要功能是限制除选定承担者外，所有人对内容存储库中给定树的读访问权限。 新的实现不会立即操作默认访问控制内容，而是通过定义表示CUG的专用访问控制策略类型来采用不同的方法。

#### CUG的访问控制策略 {#access-control-policy-for-cug}

这种新型政策具有以下特点：

* org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy（由Apache Jackrabbit API定义）类型的访问控制策略；
* PrincipalSetPolicy授予可修改的主体集的权限；
* 授予的权限和策略的范围是一个实施详细信息。

用于表示CUG的PrincipalSetPolicy的实施还定义了：

* CUG策略仅授予对常规JCR项的读取访问权（例如，访问控制内容被排除）;
* 范围由保存CUG策略的接入控制节点定义；
* CUG策略可以嵌套，嵌套的CUG启动新CUG而不继承“父”CUG的主集合；
* 如果启用了评估，则策略的效果将继承到整个子树，下一个嵌套的CUG。

这些CUG策略通过称为oak-authorization-cug的单独授权模块部署到AEM实例。 本模块具有自己的访问控制管理和权限评估功能。 换句话说，默认的AEM设置提供了一个Oak内容存储库配置，该配置结合了多个授权机制。 有关详细信息，请 [参阅Apache Oak文档中的此页](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)。

在此复合设置中，新的CUG不会替换附加到目标节点的现有访问控制内容，而是设计为补充，稍后还可以删除该补充，而不会影响原始访问控制，在AEM中，该补充默认为访问控制列表。

与前一实施不同，新的CUG策略始终被识别和视为访问控制内容。 这意味着它们是使用JCR访问控制管理API创建和编辑的。 有关详细信息，请参阅 [管理CUG策略部分](#managing-cug-policies) 。

#### CUG策略的权限评估 {#permission-evaluation-of-cug-policies}

除了CUG的专用访问控制管理之外，新授权模型还允许有条件地启用其策略的权限评估。 这允许在分阶段环境中设置CUG策略，并且只允许在复制到生产环境后评估有效权限。

CUG策略的权限评估以及与默认或任何其他授权模型的交互遵循为Apache Jackrabbit Oak中的多个授权机制设计的模式：如果且仅当所有模型授予访问权限时，才授予给定的权限集。 有关 [更多详细信息](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html) ，请参阅此页。

与用于处理和评估CUG策略的授权模型相关的权限评估具有以下特点：

* 它只处理常规节点和属性的读取权限，但不处理读取访问控制内容
* 它不处理对受保护JCR内容（访问控制、节点类型信息、版本控制、锁定或用户管理等）的修改所需的写入权限或任何类型的权限；这些权限不受CUG策略的影响，并且不会由关联的授权模型评估。 是否授予这些权限取决于在安全设置中配置的其他模型。

单个CUG策略对权限评估的影响可概括如下：

* 除政策中列出的包含被排除的承担者或承担者的主体外，所有人均拒绝读取权限；
* 该策略对包含该策略及其属性的接入控制节点生效；
* 效果还会在层次结构中继承，即由访问控制节点定义的项目树；
* 但是，它不影响访问控制节点的同级和祖先；
* 给定CUG的继承会在嵌套的CUG处停止。

#### 最佳实践 {#best-practices}

在通过CUG定义受限读访问权限时，应考虑以下最佳做法：

* 对CUG的需求是限制读访问还是验证要求做出有意识的决定。 如果是后者，或者如果需要两者，请查阅最佳实践部分，以了解有关身份验证要求的详细信息
* 为需要保护的数据或内容创建威胁模型，以识别威胁边界并清晰了解数据的敏感性以及与授权访问相关的角色
* 为存储库内容和CUG建模，同时要牢记一般授权相关方面和最佳做法：

   * 请记住，只有当给定CUG和设置授权中部署的其他模块的评估允许给定主体读取给定存储库项目时，才会授予读取权限
   * 避免创建冗余CUG，因为其他授权模块已限制读访问
   * 对嵌套CUG的过度需求可能会突出内容设计中的问题
   * 对CUG的过度需求（例如，在每个页面上）可能表明需要一个可能更适合满足应用程序和手头内容的特定安全需求的自定义授权模型。

* 将CUG策略支持的路径限制在存储库中的几个树中，以便获得优化的性能。 例如，仅允许作为自AEM 6.3以来的默认值发售的/content节点下的CUG。
* CUG策略旨在授予对一小组主体的读取权限。 对大量原则的需要可能会突出内容或应用程序设计中的问题，并应重新考虑。

### 身份验证：定义身份验证要求 {#authentication-defining-the-auth-requirement}

CUG功能的认证相关部分允许标记需要认证的树，并可选地指定专用登录页。 根据先前版本，新实现允许在内容存储库中标记需要认证的树，并有条件地允许与负责最终强制要求和重定向到登录资源的 `Sling org.apache.sling.api.auth.Authenticator`负责的同步。

这些要求通过提供注册属性的OSGi服务向身份验证器 `sling.auth.requirements` 注册。 然后，这些属性用于动态扩展身份验证要求。 有关更多详细信息，请查阅 [Sling文档](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS)。

#### 使用专用混音类型定义身份验证要求 {#defining-the-authentication-requirement-with-a-dedicated-mixin-type}

出于安全原因，新实现将剩余JCR属性的使用替换为名为的专用混音类型 `granite:AuthenticationRequired`，该混音类型为登录路径定义STRING类型的单个可选属性 `granite:loginPath`。 只有与此混音类型相关的内容更改才能更新向Apache Sling Authenticator注册的要求。 在保持任何临时修改时跟踪这些修改，因此需要调 `javax.jcr.Session.save()` 用才能生效。

这同样适用于该属 `granite:loginPath` 性。 只有在由身份验证要求相关的混音类型定义时，才会考虑该问题。 在非结构化JCR节点上添加具有此名称的剩余属性将不显示所需效果，并且负责更新OSGi注册的处理函数将忽略该属性。

>[!NOTE]
>
>设置登录路径属性是可选的，并且仅当需要身份验证的树无法返回到默认登录页面或以其他方式继承的登录页面时才需要。 请参阅以 [下登录路径评估](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path) 。

#### 向Sling Authenticator注册身份验证要求和登录路径 {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}

由于此类型的身份验证要求预计仅限于某些运行模式和内容存储库中的一小部分树，因此跟踪要求混合类型和登录路径属性是有条件的，并绑定到定义支持路径的相应配置（请参阅下面的配置选项）。 因此，只有这些受支持路径范围内的更改才会触发OSGi注册的更新，在其他位置，mixin类型和属性都将被忽略。

默认AEM设置现在允许在创作运行模式中设置混音，以利用此配置，但仅在复制到发布实例后才会生效。 有关 [Sling如何实施身份验证要求的详细信息](https://sling.apache.org/documentation/the-sling-engine/authentication/authenticationframework.html) ，请参阅本页。

在配置 `granite:AuthenticationRequired` 的受支持路径中添加混音类型将导致更新负责处理函数的OSGi注册，该注册包含带有该属性的新附加条 `sling.auth.requirements` 目。 如果给定的认证要求指定了可选属性，则该值附加地向认证器注册具有“-”前缀，以便从认证要求中排除。 `granite:loginPath`

#### 认证要求的评估与继承 {#evaluation-and-inheritance-of-the-authentication-requirement}

Apache Sling身份验证要求应通过页面或节点层次结构继承。 继承和验证要求评估的详细信息（如顺序和优先级）被视为一个实施详细信息，本文中不予记录。

#### 登录路径评估 {#evaluation-of-login-path}

在身份验证时评估登录路径并重定向到相应资源当前是Adobe Granite登录选择器身份验证处理程序( `com.day.cq.auth.impl.LoginSelectorHandler`)的实施详细信息，该处理程序是默认配置有AEM的Apache Sling AuthenticationHandler。

调用此 `AuthenticationHandler.requestCredentials` 处理函数时，会尝试确定将用户重定向到的映射登录页。 这包括以下步骤：

* 区分过期密码和需要定期登录作为重定向原因；
* 如果是常规登录，则测试是否可以按以下顺序获得登录路径：

   * 从LoginPathProvider(由新 `com.adobe.granite.auth.requirement.impl.RequirementService`
   * 从旧的、已弃用的CUG实现，
   * 从登录页面映射(如 `LoginSelectorHandler`,
   * 最后，回退到默认登录页面，如中所定义 `LoginSelectorHandler`。

* 一旦通过上面列出的调用获得了有效的登录路径，用户的请求将被重定向到该页面。

本文档的目标是评估内部界面显示的登录路径 `LoginPathProvider` 。 自AEM 6.3起发售的实施如下所示：

* 登录路径的注册取决于对过期密码的区分，以及是否需要定期登录作为重定向的原因
* 如果是常规登录，则测试是否可以按以下顺序获得登录路径：

   * 从新 `LoginPathProvider``com.adobe.granite.auth.requirement.impl.RequirementService`的，新的，
   * 从旧的、已弃用的CUG实现，
   * 从登录页面映射(如 `LoginSelectorHandler`,
   * 最后，按照使用定义的方式回退到默认登录页面 `LoginSelectorHandler`。

* 一旦通过上面列出的调用获得了有效的登录路径，用户的请求将被重定向到该页面。

由Granite `LoginPathProvider` 中新的身份验证要求支持实现的登录路径由属性定义，而属性又由上述混合类型定义 `granite:loginPath` 。 保存登录路径和属性值本身的资源路径的映射被保存在内存中，并将被评估以为层次中的其他节点找到合适的登录路径。

>[!NOTE]
>
>仅对与配置的支持路径中的资源相关联的请求执行评估。 对于任何其他请求，将评估确定登录路径的替代方法。

#### 最佳实践 {#best-practices-1}

定义身份验证要求时应考虑以下最佳做法：

* 避免嵌套身份验证要求：在树的开始处放置一个身份验证要求标记应足够，并且继承到目标节点定义的整个子树。 该树中的其他身份验证要求应被视为冗余，在评估Apache Sling中的身份验证要求时，可能会导致性能问题。 通过将授权和认证相关CUG区域分开，可以通过CUG或其他类型的策略限制读访问，同时强制对整个树的认证。
* 模型库内容，使得身份验证要求适用于整个树，而无需再次从要求中排除嵌套子树。
* 要避免指定，并随后注册冗余登录路径：

   * 依赖继承并避免定义嵌套登录路径，
   * 不要将可选登录路径设置为与默认值或继承值相对应的值，
   * 应用程序开发人员应确定在与关联的全局登录路径配置（默认和映射）中应配置哪些登录路径 `LoginSelectorHandler`。

## 存储库中的表示形式 {#representation-in-the-repository}

### 存储库中的CUG策略表示 {#cug-policy-representation-in-the-repository}

Oak文档涵盖新CUG策略在存储库内容中的反映方式。 有关详细信息，请 [参阅本页](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository)。

### 存储库中的身份验证要求 {#authentication-requirement-in-the-repository}

对单独认证要求的需求反映在位于目标节点的专用混合节点类型的存储库内容中。 混音类型定义一个可选属性，以指定目标节点定义的树的专用登录页。

与登录路径关联的页面可能位于该树的内部或外部。 它将被排除在身份验证要求之外。

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## 管理CUG策略和身份验证要求 {#managing-cug-policies-and-authentication-requirement}

### 管理CUG策略 {#managing-cug-policies}

使用JCR访问控制管理API管理用于限制CUG读访问的新型访问控制策略，并遵循 [JCR 2.0规范中描述的机制](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html)。

#### 设置新的CUG策略 {#set-a-new-cug-policy}

在之前没有CUG集的节点应用新CUG策略的代码。 请注意， `getApplicablePolicies` 将仅返回之前未设置的新策略。 最后，需要回写策略，并且需要保留更改。

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

#### 编辑现有CUG策略 {#edit-an-existing-cug-policy}

编辑现有CUG策略需要执行以下步骤。 请注意，修改后的策略需要写回，并且更改需要使用保留 `javax.jcr.Session.save()`。

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

JCR访问控制管理定义了一种检索在给定路径上生效的策略的最佳方法。 由于CUG策略的评估是有条件的并且取决于要启用的相应配置，调用是验证给定CUG策略是否在给定安装中生效的一种简便方法。 `getEffectivePolicies`

>[!NOTE]
>
>请注意与随后的代 `getEffectivePolicies` 码示例之间的差异，该示例在层次结构中向上遍历以查找给定路径是否已包含在现有CUG中。

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

查找在给定路径中定义的所有嵌套CUG，而不管它们是否生效。 有关详细信息，请参阅“配 [置选项](/help/sites-administering/closed-user-groups.md#configuration-options) ”部分。

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

#### 按Pincipal管理CUG策略 {#managing-cug-policies-by-pincipal}

由允许按主体编 `JackrabbitAccessControlManager` 辑访问控制策略定义的扩展不会通过CUG访问控制管理实现，因为根据定义，CUG策略始终影响所有主体：将授予与列出 `PrincipalSetPolicy` 的内容一起读取的访问权限，而将阻止所有其他承担者读取目标节点定义的树中的内容。

相应的方法始终返回空策略数组，但不会引发异常。

### 管理身份验证要求 {#managing-the-authentication-requirement}

通过改变目标节点的有效节点类型来实现新认证要求的创建、修改或移除。 然后，可以使用常规JCR API编写可选的登录路径属性。

>[!NOTE]
>
>对上述给定目标节点的修改仅会在Apache Sling Authenticator上反映（如果已配置目标，且目标包含在受支持路径定义的树中）（请参阅“配置选项”一节）。 `RequirementHandler`
>
>有关详细信息，请参 [阅指定混合节点类型](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3指定混合节点类型)和 [添加节点和设置属性](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4添加节点和设置属性)

#### 添加新的身份验证要求 {#adding-a-new-auth-requirement}

创建新身份验证要求的步骤如下所述。 请注意，仅当为包含目标节点的树配置了Apache Sling Authenticator时， `RequirementHandler` 才会向Apache Sling Authenticator注册此要求。

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### 使用登录路径添加新的身份验证要求 {#add-a-new-auth-requirement-with-login-path}

创建新身份验证要求的步骤，包括登录路径。 请注意，只有在为包含目标节点的树配置了登录路径的要求和排除 `RequirementHandler` 内容后，才会向Apache Sling Authenticator注册。

```java
Node targetNode = [...]
String loginPath = [...] // STRING property

Node targetNode = session.getNode(path);
targetNode.addMixin("granite:AuthenticationRequired");

targetNode.setProperty("granite:loginPath", loginPath);
session.save();
```

#### 修改现有登录路径 {#modify-an-existing-login-path}

更改现有登录路径的步骤详见下文。 只有为包含目标节点的树配置了Apache Sling Authenticator, `RequirementHandler` 才会向Apache Sling Authenticator注册修改。 将从注册中删除以前的登录路径值。 与目标节点关联的身份验证要求不受此修改的影响。

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

删除现有登录路径的步骤。 如果已为包含目标节点的树配置登录路径条目， `RequirementHandler` 则登录路径条目将仅从Apache Sling Authenticator中注册。 与目标节点关联的身份验证要求不受影响。

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

或者，您可以使用以下方法来实现相同的目的：

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

删除现有身份验证要求的步骤。 如果为包含目标节点的树配置了Apache Sling Authenticator, `RequirementHandler` 则此要求将仅从Apache Sling Authenticator中取消注册。

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### 检索有效的身份验证要求 {#retrieve-effective-auth-requirements}

没有专用的公共API可读取向Apache Sling Authenticator注册的所有有效身份验证要求。 但是，该列表会在系统控制台的“身份验 `https://<serveraddress>:<serverport>/system/console/slingauth` 证要求配&#x200B;**置”部分下显示**。

下图显示了包含演示内容的AEM发布实例的身份验证要求。 社区页面的突出显示路径说明了Apache Sling Authenticator中如何反映本文档中所述的实施所添加的要求。

>[!NOTE]
>
>在此示例中，未设置可选登录路径属性。 因此，没有向认证者注册第二项。

![chlimage_1-24](assets/chlimage_1-24.jpeg)

#### 检索有效登录路径 {#retrieve-the-effective-login-path}

当前没有公共API可检索登录路径，该路径将在匿名访问需要身份验证的资源时生效。 有关如何检索登录路径的实现详细信息，请参阅登录路径评估一节。

但是，除了使用此功能定义的登录路径之外，还有其他方法可指定指向登录的重定向，在设计内容模型和给定AEM安装的身份验证要求时，应考虑这些方法。

#### 检索继承的身份验证要求 {#retrieve-the-inherited-auth-requirement}

与登录路径一样，没有公共API可检索内容中定义的继承身份验证要求。 以下示例说明了如何列出使用给定层次结构定义的所有身份验证要求，而不管这些要求是否生效。 有关详细信息，请参阅 [配置选项](/help/sites-administering/closed-user-groups.md#configuration-options)。

>[!NOTE]
>
>建议将继承机制用于身份验证要求和登录路径，并避免创建嵌套的身份验证要求。
>
>有关详细信息，请 [参阅评估和继承身份验证要求](#evaluation-and-inheritance-of-the-authentication-requirement)、 [评估登录路径](#evaluation-of-login-path) 和最佳 [实践](#best-practices)。

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

### 结合CUG策略和身份验证要求 {#combining-cug-policies-and-the-authentication-requirement}

下表列出了CUG策略的有效组合以及通过配置同时启用两个模块的AEM实例中的身份验证要求。

| **需要身份验证** | **登录路径** | **受限读取访问** | **预期效果** |
|---|---|---|---|
| 是 | 是 | 是 | 只有在有效权限评估授予访问权限时，给定用户才能查看使用CUG策略标记的子树。 未通过身份验证的用户将被重定向到指定的登录页面。 |
| 是 | 否 | 是 | 只有在有效权限评估授予访问权限时，给定用户才能查看使用CUG策略标记的子树。 未通过身份验证的用户将被重定向到继承的默认登录页面。 |
| 是 | 是 | 否 | 未通过身份验证的用户将被重定向到指定的登录页面。 是否允许它查看使用身份验证要求标记的树取决于该子树中包含的各个项目的有效权限。 没有专用的CUG限制就地读取访问。 |
| 是 | 否 | 否 | 未通过身份验证的用户将被重定向到继承的默认登录页面。 是否允许它查看使用身份验证要求标记的树取决于该子树中包含的各个项目的有效权限。 没有专用的CUG限制就地读取访问。 |
| 否 | 否 | 是 | 如果授予有效权限评估授予访问权限，则给定的已验证或未验证的用户只能查看使用CUG策略标记的子树。 未经身份验证的用户将得到同等对待，不会被重定向到登录。 |

>[!NOTE]
>
>“身份验证要求”=“否”和“登录路径”=“是”的组合未在上面列出，因为“登录路径”是与身份验证要求关联的可选属性。 指定具有该名称的JCR属性而不添加定义混音类型将不起作用，并且相应的处理函数将忽略该属性。

## OSGi组件和配置 {#osgi-components-and-configuration}

本节概述了OSGi组件以及新CUG实施中引入的各个配置选项。

另请参阅CUG映射文档，以全面映射旧实施和新实施之间的配置选项。

### 授权：设置和配置 {#authorization-setup-and-configuration}

新的授权相关部件包含在 **Oak CUG授权包** ( `org.apache.jackrabbit.oak-authorization-cug`)中，它是AEM默认安装的一部分。 该包定义了分开的授权模型，该模型旨在作为管理读访问的另一种方式部署。

#### 设置CUG授权 {#setting-up-cug-authorization}

相关Apache文档中详细介绍了设置CUG [授权](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)。 默认情况下，AEM在所有运行模式下都部署了CUG授权。 该分步指令还可用于在那些需要不同授权设置的安装中禁用CUG授权。

#### 配置引用过滤器 {#configuring-the-referrer-filter}

您还需要配置 [Sling引用过滤器](/help/sites-administering/security-checklist.md#the-sling-referrer-filter) ，以及可能用于访问AEM的所有主机名；例如，通过CDN、负载平衡器和任何其他方式。

如果未配置引用过滤器，则当用户尝试登录CUG站点时，会看到与以下内容类似的错误：

```shell
31.01.2017 13:49:42.321 *INFO* [qtp1263731568-346] org.apache.sling.security.impl.ReferrerFilter Rejected referrer header for POST request to /libs/granite/core/content/login.html/j_security_check : https://hostname/libs/granite/core/content/login.html?resource=%2Fcontent%2Fgeometrixx%2Fen%2Ftest-site%2Ftest-page.html&$$login$$=%24%24login%24%24&j_reason=unknown&j_reason_code=unknown
```

#### OSGi组件的特性 {#characteristics-of-osgi-components}

已引入以下两个OSGi组件来定义身份验证要求并指定专用的登录路径：

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
    </ul> <p>另请参阅下 <a href="#configuration-options">面的配置选</a> 项。</p> </td>
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

**org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugImpl**

<table>
 <tbody>
  <tr>
   <td>标签</td>
   <td>Apache Jackrabbit Oak CUG排除列表</td>
  </tr>
  <tr>
   <td>描述</td>
   <td>允许从CUG评估中排除配置了名称的主体。</td>
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

#### Configuration Options {#configuration-options}

主要配置选项包括：

* `cugSupportedPaths`:指定可能包含CUG的子树。 未设置默认值
* `cugEnabled`:配置选项以启用对当前CUG策略的权限评估。

与CUG授权模块相关的可用配置选项在 [Apache Oak文档中列出并有更详细的说明](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration)。

#### 从CUG评估中排除承担者 {#excluding-principals-from-cug-evaluation}

对个人负责人免予CUG评估，前者不予执行。 新的CUG授权通过一个名为CugExclude的专用接口覆盖此功能。 Apache Jackrabbit Oak 1.4附带一个默认实现，该实现不包括一组固定的承担者，以及一个允许配置单个承担者名称的扩展实现。 后者在AEM发布实例中配置。

自AEM 6.3以来的默认值会阻止以下承担者受到CUG策略的影响：

* 管理主管（管理员用户、管理员组）
* 服务用户主管
* 存储库内部系统主体

有关详细信息，请参阅下面“自AEM 6.3 [以来的默认配置”部分中的表](#default-configuration-since-aem) 。

在 **Apache Jackrabbit Oak CUG排除列表的配置部分的系统控制台中，可以更改或展开“管理员”组的排除**。

或者，可以提供和部署CugExclude接口的自定义实现，以根据特殊需要调整被排除的承担者集。 有关详细信 [息和示例实施](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) ，请参阅有关CUG可插件的文档。

### 身份验证：设置和配置 {#authentication-setup-and-configuration}

与身份验证相关的新部分包含在 **Adobe Granite Authentication Handler** bundle( `com.adobe.granite.auth.authhandler` 版本5.6.48)中。 此捆绑包是AEM默认安装的一部分。

为了为已弃用的CUG支持设置身份验证要求替换，某些OSGi组件必须在给定AEM安装中存在并处于活动状态。 有关详细信息，请参 **阅以下OSGi组件的特性** 。

>[!NOTE]
>
>由于RequirementHandler的强制配置选项，仅当通过指定一组支持的路径启用了该功能时，验证相关部分才处于活动状态。 在标准AEM安装中，该功能在创作运行模式下处于禁用状态，在发布运行模式下为/content启用。

**OSGi组件的特性**

已引入以下2个OSGi组件以定义身份验证要求并指定专用登录路径：

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
   <td>用于验证要求的专用OSGi服务，该服务将观察器注册到影响验证要求的内容变化（通过混合类型）和登录路径 <code>granite:AuthenticationRequirement</code><code>LoginSelectorHandler</code>。 </td>
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
| 描述 | `RequirementHandler` 更新Apache Sling身份验证要求和相关登录路径的相应排除的实现。 |
| 配置属性 | `supportedPaths` |
| 配置策略 | `ConfigurationPolicy.REQUIRE` |
| 引用 | NA |

#### Configuration Options {#configuration-options-1}

CUG重写的身份验证相关部分只附带与Adobe Granite身份验证要求和登录路径处理程序关联的单个配置选项：

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
   <td>Set&lt;String&gt;</td>
   <td>-</td>
   <td>此处理函数将遵循身份验证要求的路径。 如果要向节点添加混音类型而不强制 <code>granite:AuthenticationRequirement</code> 执行（例如，在创作实例上），请取消设置此配置。 如果缺失，则禁用该功能。 </td>
  </tr>
 </tbody>
</table>

## 自AEM 6.3以来的默认配置 {#default-configuration-since-aem}

默认情况下，AEM的新安装将将新实施用于CUG功能的授权和身份验证相关部分。 旧实施“Adobe Granite Closed User Group(CUG)Support”已弃用，默认情况下将在所有AEM安装中禁用。 新实施将改为启用，如下所示：

### 作者实例 {#author-instances}

| **“Apache Jackrabbit Oak CUG配置”** | **说明** |
|---|---|
| 支持的路径 `/content` | 已启用CUGpolicies的访问控制管理。 |
| 启用CUG评估FALSE | 权限评估已禁用。 CUG策略不起作用。 |
| 等级 | 200 | 请参阅Oak文档。 |

>[!NOTE]
>
>默认创作实 **例中不提供Apache Jackrabbit Oak CUG Exclude List** 、 **** Adobe Granite Authentication Requirement和Login Path Handler的配置。

### 发布实例 {#publish-instances}

| **“Apache Jackrabbit Oak CUG配置”** | **说明** |
|---|---|
| 支持的路径 `/content` | CUG策略的访问控制管理在配置的路径下启用。 |
| 启用CUG评估 | 在配置的路径下启用权限评估。 CUG政策生效 `Session.save()`。 |
| 等级 | 200 | 请参阅Oak文档。 |

| **“Apache Jackrabbit Oak CUG排除列表”** | **说明** |
|---|---|
| 主体名称管理员 | 从CUG评估中不包括管理员主体。 |

| **“Adobe Granite身份验证要求和登录路径处理程序”** | **说明** |
|---|---|
| 支持的路径 `/content` | 通过混合类型在存储库中定义的身份验证要 `granite:AuthenticationRequired` 求在下面生 `/content` 效 `Session.save()`。 Sling Authenticator将更新。 将忽略在支持路径之外添加混音类型。 |

## 禁用CUG授权和身份验证要求 {#disabling-cug-authorization-and-authentication-requirement}

如果给定安装不使用CUG或使用不同的验证和授权手段，则可以完全禁用新实施。

### 禁用CUG授权 {#disable-cug-authorization}

有关如何 [](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) 从复合授权设置中删除CUG授权模型的详细信息，请查阅CUG可插件文档。

### 禁用身份验证要求 {#disable-the-authentication-requirement}

为了禁用对模块提供的身份验证要求的支持， `granite.auth.authhandler` 请删除与 **Adobe Granite身份验证要求和登录路径处理程序相关的配置就足够了**。

>[!NOTE]
>
>但是，请注意，删除配置不会取消注册mixin类型，该类型仍适用于节点而不起作用。

## 与其他模块的交互 {#interaction-with-other-modules}

### Apache Jackrabbit API {#apache-jackrabbit-api}

为了反映CUG授权模型所使用的新型访问控制策略，扩展了Apache Jackrabbit定义的API。 由于模块的版本2.11.0定义 `jackrabbit-api` 了一个名为的新界面 `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`，该界面从扩展 `javax.jcr.security.AccessControlPolicy`。

### Apache Jackrabbit FileVault {#apache-jackrabbit-filevault}

Apache Jackrabbit FileVault的导入机制已调整为处理类型的访问控制策略 `PrincipalSetPolicy`。

### Apache Sling内容分发 {#apache-sling-content-distribution}

请参阅上 [述Apache Jackrabbit fileVault部分](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault) 。

### Adobe Granite复制 {#adobe-granite-replication}

为了能够在不同AEM实例之间复制CUG策略，复制模块已稍作调整：

* `DurboImportConfiguration.isImportAcl()` 以字面形式解释，只会影响访问控制策略的实施 `javax.jcr.security.AccessControlList`

* `DurboImportTransformer` 将仅遵循此配置，以用于真正的ACL
* 其他策略(如 `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy` 由CUG授权模型创建的实例)将始终被复制，并且将忽 `DurboImportConfiguration.isImportAcl`略配置选项()。

复制CUG策略有一个限制。 如果在不删除相应的混合节点类型的情况下删除了给定的CUG策 `rep:CugMixin,` 略，则复制时不会反映删除。 通过始终在删除策略时删除混音来解决此问题。 但是，如果手动添加混音类型，则可能会显示该限制。

### Adobe Granite身份验证处理程序 {#adobe-granite-authentication-handler}

捆绑包附带的 **身份验证处理程序Adobe Granite HTTP Header Authentication Handler**`com.adobe.granite.auth.authhandler` 包含对同一模块定义 `CugSupport` 的接口的引用。 它用于在某些情况下计算“领域”，并返回到使用处理函数配置的领域。

这已经调整，以使引用为可选，以确保在给定设置决定重新启用已弃用的实现时，最大向后兼容性。 `CugSupport` 使用该实现的安装将不再获取从CUG实现提取的领域，但始终会按 **Adobe Granite HTTP Header Authentication Handler定义显示该领域**。

>[!NOTE]
>
>默认情况下， **Adobe Granite HTTP头身份验证处理程序仅在发布运行模式下配置** ，并启用“禁用登录页面”( `auth.http.nologin`)选项。

### AEM LiveCopy {#aem-livecopy}

配置CUG和LiveCopy时，在存储库中添加一个额外的节点和一个额外的属性，如下所示：

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

这两个元素都在下面创建 `cq:Page`。 在当前设计中，MSM仅处理()节点下的节 `cq:PageContent` 点和`jcr:content`属性。

因此，CUG组无法从Blueprint回滚到Live Copy。 在设置Live copy时，请相应地制定计划。

## 新CUG实施中的更改 {#changes-with-the-new-cug-implementation}

本节旨在概述对CUG功能所做的更改，以及新旧实施的比较。 它列出了影响CUG支持配置方式的更改，并描述了在存储库内容中管理CUG的方式和方式。

### CUG设置和配置中的差异 {#differences-in-cug-setup-and-configuration}

已弃用的OSGi组件 **Adobe Granite Closed User Group(CUG)Support** ( `com.day.cq.auth.impl.cug.CugSupportImpl`)已替换为新组件，以便能够单独处理以前CUG功能的授权和身份验证相关部分。

## 在管理存储库内容中的CUG方面的差异 {#differences-in-managing-cugs-in-the-repository-content}

以下各节从实施和安全性角度描述了新旧实施之间的差异。 虽然新实现旨在提供相同的功能，但在使用新CUG时，需要了解的细微更改很重要。

### 与授权的区别 {#differences-with-regards-to-authorization}

从授权角度来看，主要区别在于：

**CUG的专用访问控制内容**

在旧的实现中，默认授权模型用于控制发布时的访问控制列表策略，由CUG授权的设置替换任何现有ACE。 这是由编写常规的、剩余的JCR属性触发的，这些属性在发布时进行了解释。

在新实施中，默认授权模型的访问控制设置不受创建、修改或删除的任何CUG的影响。 而是会将名为的新类型的策 `PrincipalSetPolicy` 略作为附加访问控制内容应用到目标节点。 此附加策略将作为目标节点的子级进行定位，并且如果存在，将作为默认策略节点的同级。

**在访问控制管理中编辑CUG策略**

从剩余的JCR属性移动到专用访问控制策略会影响创建或修改CUG功能的授权部分所需的权限。 由于这被视为对访问控制内容的修改，因此它 `jcr:readAccessControl` 需要 `jcr:modifyAccessControl` 和权限才能写入存储库。 因此，只有有权修改页面访问控制内容的内容作者才能设置或修改此内容。 这与旧实施不同，旧实施中编写常规JCR属性的能力足够，从而导致权限提升。

**策略定义的目标节点**

CUG策略应在JCR节点创建，该节点定义要受受限读访问的子树。 这可能是AEM页面，以防CUG影响整个树。

请注意，将CUG策略仅放在给定页面下方的jcr:content节点上将仅限制对给定页面内容s.str的访问，但不会对任何同级或子页面生效。 这可能是一个有效的用例，并且可以使用允许应用精细访问内容的存储库编辑器来实现。 但是，它与前一个实现形成了对比，在前一个实现中，将cq:cugEnabled属性放在jcr:content节点上是在内部重新映射到页面节点的。 不再执行此映射。

**使用CUG策略的权限评估**

从旧的CUG支持转向其他授权模型，改变了评估有效读取权限的方式。 如 [Jackrabbit文档中所述](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)`CUGcontent` ，只有在Oak存储库中配置的所有型号的权限评估授予读访问权限时，才允许查看该模型的给定主体授予读访问权限。

换句话说，为了评估有效权限，将同时考虑CUG内容和默认访问控制条目，并且只有当CUG内容被两种策略授予时，才会授予对CUG内容的读访问权限。 `CUGPolicy` 在默认AEM发布安装中，将为每个人授予对完整树的读访问权限， `/content` CUG策略的效果将与旧实施的效果相同。

**按需评估**

CUG授权模型允许单独开启访问控制管理和权限评估：

* 如果模块具有一个或多个可创建CUG的支持路径，则启用访问控制管理
* 仅当另外选中了“启用CUG评估”选项时，才 **会启用权限评估** 。

在CUG策略的新AEM默认设置评估中，仅启用“发布”运行模式。 有关更多详细信 [息，请参阅自AEM 6.3以来默认配置的详细信息](#default-configuration-since-aem) 。 这可以通过比较给定路径的有效策略与存储在内容中的策略来验证。 只有在启用了CUG权限评估时，才会显示有效策略。

如上所述，CUG访问控制策略现在始终存储在内容中，但只有在Apache Jackrabbit Oak **CUG Configuration的系统控制台中打开** CUG Evaluation Enabled **，才能执行对这些策略产生的有效权限的评估。** 默认情况下，它仅启用“发布”运行模式。

### 与身份验证的区别 {#differences-with-regards-to-authentication}

与身份验证相关的差异如下所述。

#### 用于验证要求的专用混音类型 {#dedicated-mixin-type-for-authentication-requirement}

在前一个实现中，CUG的授权和认证都由单个JCR属性( `cq:cugEnabled`)触发。 就身份验证而言，这会生成与Apache Sling Authenticator实现一起存储的身份验证要求的更新列表。 在新的实现中，通过用专用混音类型( `granite:AuthenticationRequired`)标记目标节点来实现相同的结果。

#### 排除登录路径的属性 {#property-for-excluding-login-path}

mixin类型定义一个名为的可选属性，该属 `granite:loginPath`性基本上与该属性相 `cq:cugLoginPage` 对应。 与之前的实现不同，只有在其声明的节点类型是所述的mixin时，登录路径属性才会得到尊重。 在不设置mixin类型的情况下添加具有该名称的属性将不起作用，并且不会向身份验证器报告对登录路径的新要求或排除。

#### 身份验证要求的权限 {#privilege-for-authentication-requirement}

添加或删除混音类型需要授 `jcr:nodeTypeManagement` 予权限。 在上一个实现中，权 `jcr:modifyProperties` 限用于编辑剩余属性。

就某些方面而 `granite:loginPath` 言，添加、修改或删除属性需要相同的权限。

#### 由混合类型定义的目标节点 {#target-node-defined-by-mixin-type}

JCR节点应创建身份验证要求，该节点定义要受强制登录影响的子树。 如果CUG预期会影响整个树，则这很可能是AEM页面，而新实现的UI将随后在页面节点上添加身份验证要求混合类型。

将CUG策略仅放在位于给定页面下方的jcr:content节点将仅限制对内容的访问，但不会影响页面节点本身或任何子页面。

这可能是一个有效的方案，在允许将混音放在任何节点的存储库编辑器中是可能的。 但是，这种行为与前一个实现形成了对比，其中在jcr:content节点上放置cq:cugEnabled或cq:cugLoginPage属性最终在内部重新映射到页面节点。 不再执行此映射。

#### 已配置支持的路径 {#configured-supported-paths}

mixin类 `granite:AuthenticationRequired` 型和granite:loginPath属性将仅在 **Adobe Granite Authentication Requirement和Login Path handler附带的一组“支持的路径”配置选项所定义的范围内得到遵守******。 如果未指定路径，则完全禁用身份验证要求功能。 在这种情况下，混音类型和属性在添加或设置到给定JCR节点时生效。

### JCR内容、OSGi服务和配置的映射 {#mapping-of-jcr-content-osgi-services-and-configurations}

以下文档提供了旧实施和新实施之间OSGi服务、配置和存储库内容的全面映射。

自AEM 6.3以来的CUG映射

[获取文件](assets/cug-mapping.pdf)

## 升级CUG {#upgrade-cug}

### 使用已弃用CUG的现有安装 {#existing-installations-using-the-deprecated-cug}

旧版CUG支持实施已弃用，将在将来版本中删除。 当从AEM 6.3以前的版本升级时，建议移至新实施。

对于升级的AEM安装，务必确保仅启用一个CUG实施。 新的和已弃用的旧CUG支持的组合不会进行测试，并且可能导致不期望的行为：

* Sling Authenticator中与身份验证要求的冲突
* 当与旧CUG关联的ACL设置与新CUG策略冲突时，拒绝读访问。

### 迁移现有CUG内容 {#migrating-existing-cug-content}

Adobe为迁移到新的CUG实施提供了一个工具。 要使用它，请执行以下步骤：

1. 转到 `https://<serveraddress>:<serverport>/system/console/cug-migration` 访问该工具。
1. 输入要检查CUG的根路径，然后按“ **Perform dry run** ”按钮。 这将扫描选定位置中有资格进行转换的CUG。
1. 查看结果后，按“ **Perform migration** （执行迁移）”按钮迁移到新实施。

>[!NOTE]
>
>如果遇到问题，则可以在上的 **DEBUG** 级别设置特定记录器 `com.day.cq.auth.impl.cug` ，以获得迁移工具的输出。 有关 [如何执行](/help/sites-deploying/configure-logging.md) ，请参阅记录。

