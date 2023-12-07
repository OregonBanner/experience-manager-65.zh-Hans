---
title: AEM 6.5中的自定义用户组映射
description: 了解自定义用户组映射在Adobe Experience Manager中的工作方式。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 661602eb-a117-454d-93d3-a079584f7a5d
feature: Security
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# AEM 6.5中的自定义用户组映射 {#custom-user-group-mapping-in-aem}

## 与CUG（自定义用户组）相关的JCR内容比较 {#comparison-of-jcr-content-related-to-cug}

<table>
 <tbody>
  <tr>
   <td><strong>较旧的AEM版本</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td><p>属性：cq：cugEnabled</p> <p>声明节点类型： N/A，剩余属性</p> </td>
   <td><p>授权：</p> <p>节点：节点类型rep：CugPolicy的rep：cugPolicy</p> <p>声明节点类型：rep：CugMixin</p> <p> </p> <p> </p> <p> </p> 身份验证：</p> <p>Mixin类型： granite：AuthenticationRequired</p> </td>
   <td><p>为了限制读取访问，将专用CUG策略应用于目标节点。</p> <p>注意：策略只能在配置的受支持路径上应用。</p> <p>名为rep：cugPolicy且类型为rep：CugPolicy的节点受到保护，无法使用常规JCR API调用进行写入；请改用JCR访问控制管理。</p> <p>请参阅 <a href="https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html">此页面</a> 以了解更多信息。</p> <p>要在节点上强制实施身份验证要求，只需添加mixin类型granite：AuthenticationRequired即可。</p> <p>注意：仅遵循所配置的受支持路径下方。</p> </td>
  </tr>
  <tr>
   <td><p>属性：cq：cugPrincipals</p> <p>声明节点类型： NA，剩余属性</p> </td>
   <td><p>属性： rep：principalNames</p> <p>声明节点类型：rep：CugPolicy</p> </td>
   <td><p>属性包含允许读取受限CUG下内容的主体的名称，该属性受到保护，不能使用常规JCR API调用写入，请改用JCR访问控制管理。</p> <p>请参阅 <a href="https://jackrabbit.apache.org/api/2.12/org/apache/jackrabbit/api/security/authorization/PrincipalSetPolicy.html">此页面</a> 以了解关于实施的更多详细信息。</p> </td>
  </tr>
  <tr>
   <td><p>属性：cq：cugLoginPage</p> <p>声明节点类型： NA，剩余属性</p> </td>
   <td><p>属性：granite：loginPath（可选）</p> <p>声明节点类型： granite：AuthenticationRequired</p> </td>
   <td><p>如果定义了mixin类型granite：AuthenticationRequired ，则JCR节点可以选择定义替代登录路径。</p> <p>注意：仅遵循所配置的受支持路径下方。</p> </td>
  </tr>
  <tr>
   <td><p>属性：cq：cugRealm</p> <p>声明节点类型： NA，剩余属性</p> </td>
   <td>NA</td>
   <td>新的实施不再支持。</td>
  </tr>
 </tbody>
</table>

## OSGi服务的比较 {#comparison-of-osgi-services}

**较旧的AEM版本**

标签：AdobeGranite封闭用户组(CUG)支持

名称：com.day.cq.auth.impl.CugSupportImpl

**AEM 6.5**

* 标签：Apache Jackrabbit Oak CUG配置

  名称：org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration

  ConfigurationPolicy =必需

* 标签：Apache Jackrabbit Oak CUG排除列表

  名称：org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl

  ConfigurationPolicy =必需

* 名称：com.adobe.granite.auth.requirement.impl.RequirementService
* 标签：AdobeGranite身份验证要求和登录路径处理程序

  名称：com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler

  ConfigurationPolicy =必需

**评论**

* 配置CUG授权并启用/禁用评估。
用于配置不受CUG授权影响的主体排除列表的服务。

  >[!NOTE]
  > 
  >如果 `CugExcludeImpl` 未配置， `CugConfiguration` 回退到默认值。

  如果有特殊需求，可以插入自定义CugExclude实施。

* 实施LoginPathProvider的OSGi组件公开与LoginSelectorHandler匹配的登录路径。 它具有对RequirementHandler的强制引用，用于注册观察者，该观察者通过granite：AuthenticationRequired mixin类型侦听内容中存储的已更改身份验证要求。
* 实施RequirementHandler的OSGi组件将authenticator更改通知给SlingAuthenticator。

  由于此组件的配置策略是REQUIRE，因此只有在指定了一组受支持的路径时才激活它。

  启用服务将启动RequirementService。

<!-- nested tables not supported - text above is the table>
<table>
 <tbody>
  <tr>
   <td><strong>Older AEM Versions</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>Comments</strong></td>
  </tr>
  <tr>
   <td><p>Label: Adobe Granite Closed User Group (CUG) Support</p> <p>Name: com.day.cq.auth.impl.CugSupportImpl</p> </td>
   <td><p>Label: Apache Jackrabbit Oak CUG Configuration</p> <p>Name: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration</p> <p>ConfigurationPolicy = REQUIRED</p> </td>
    <td><p>Label: Apache Jackrabbit Oak CUG Exclude List</p> <p>Name: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl</p> <p>ConfigurationPolicy = REQUIRED</p> <p> </p> <p> </p> <p> </p> <p> </p> </td>
      </tr>
      <tr>
       <td>Name: com.adobe.granite.auth.requirement.impl.RequirementService</td>
      </tr>
      <tr>
       <td><p>Label: Adobe Granite Authentication Requirement and Login Path Handler</p> <p>Name: com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler</p> <p>ConfigurationPolicy = REQUIRED</p> </td>
      </tr>
     </tbody>
    </table> </td>
   <td>
     <tbody>
      <tr>
       <td>Configuration of the CUG authorization and enable/disable the evaluation.</td>
      </tr>
      <tr>
       <td><p>Service to configure exclusion list of principals which should not be affected by the CUG authorization.</p> <p>NOTE: If the CugExcludeImpl is not configured, the CugConfiguration will fall back to the default.</p> <p>It is possible to plug a custom CugExclude implementation if there are special needs.</p> </td>
      </tr>
      <tr>
       <td>OSGi component implementing LoginPathProvider that exposes a matching login path to the LoginSelectorHandler. It has a mandatory reference to a RequirementHandler which is used to register the observer that listens to changed auth requirements stored in the content by the means of the granite:AuthenticationRequired mixin type. </td>
      </tr>
      <tr>
       <td><p>OSGi component implementing RequirementHandler that notifies the SlingAuthenticator about changes to authrequirements.</p> <p>As configuration policy for this component is REQUIRE it will only be activated if a set of supported paths is specified.</p> <p>Enabling the service will launch the RequirementService.</p> </td>
      </tr>
     </tbody>
     </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->
