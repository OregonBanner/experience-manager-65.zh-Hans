---
title: AEM 6.5中的自定义用户组映射
seo-title: AEM 6.5中的自定义用户组映射
description: 了解自定义用户群组映射在AEM中的工作方式。
seo-description: 了解自定义用户群组映射在AEM中的工作方式。
uuid: 7520351a-ab71-4661-b214-a0ef012c0c93
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 13085dd3-d283-4354-874b-cd837a9db9f9
docset: aem65
exl-id: 661602eb-a117-454d-93d3-a079584f7a5d
feature: 安全
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 1%

---

# AEM 6.5 {#custom-user-group-mapping-in-aem}中的自定义用户组映射

## CUG{#comparison-of-jcr-content-related-to-cug}相关JCR含量比较

<table>
 <tbody>
  <tr>
   <td><strong>旧版AEM</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td><p>属性：cq:cugEnabled</p> <p>声明节点类型：N/A，剩余财产</p> </td>
   <td><p>授权:</p> <p>节点：节点类型rep:CugPolicy的rep:cugPolicy</p> <p>声明节点类型：rep:CugMixin</p> <p> </p> <p> </p> <p> </p> 身份验证:</p> <p>混合类型：granite:AuthenticationRequired</p> </td>
   <td><p>为了限制读取访问，专用CUG策略被应用到目标节点。</p> <p>注意：策略只能应用于已配置的受支持路径。</p> <p>名为rep:cugPolicy和type rep:CugPolicy的节点受保护，无法使用常规JCR API调用写入；请改用JCR访问控制管理。</p> <p>有关更多信息，请参阅<a href="https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html">此页面</a>。</p> <p>为了对节点强制执行身份验证要求，只需添加mixin类型granite:AuthenticationRequired即可。</p> <p>注意：仅在配置的受支持路径下遵循。</p> </td>
  </tr>
  <tr>
   <td><p>属性：cq:cugPrincipals</p> <p>声明节点类型：NA，剩余财产</p> </td>
   <td><p>属性：rep:principalNames</p> <p>声明节点类型：rep:CugPolicy</p> </td>
   <td><p>包含允许读取受限CUG下内容的主体名称的属性受保护，无法使用常规JCR API调用写入；请改用JCR访问控制管理。</p> <p>有关实施的更多详细信息，请参阅<a href="https://svn.apache.org/repos/asf/jackrabbit/trunk/jackrabbitapi/src/main/java/org/apache/jackrabbit/api/security/authorization/PrincipalSetPolicy.java">此页面</a>。</p> </td>
  </tr>
  <tr>
   <td><p>属性：cq:cugLoginPage</p> <p>声明节点类型：NA，剩余财产</p> </td>
   <td><p>属性：granite:loginPath（可选）</p> <p>声明节点类型：granite:AuthenticationRequired</p> </td>
   <td><p>定义了mixin类型granite:AuthenticationRequired的JCR节点可以选择定义替代登录路径。</p> <p>注意：仅在配置的受支持路径下遵循。</p> </td>
  </tr>
  <tr>
   <td><p>属性：cq:cugRealm</p> <p>声明节点类型：NA，剩余财产</p> </td>
   <td>NA</td>
   <td>新实施不再支持。</td>
  </tr>
 </tbody>
</table>

## OSGi服务{#comparison-of-osgi-services}的比较

**旧版AEM**

标签：AdobeGranite封闭用户组(CUG)支持

名称：com.day.cq.auth.impl.CugSupportImpl

**AEM 6.5**

* 标签：Apache Jackrabbit Oak CUG配置

   名称：org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration

   ConfigurationPolicy = REQUIRED

* 标签：Apache Jackrabbit Oak CUG排除列表

   名称：org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl

   ConfigurationPolicy = REQUIRED

* 名称：com.adobe.granite.auth.requirement.impl.RequirementService
* 标签：AdobeGranite身份验证要求和登录路径处理程序

   名称：com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler

   ConfigurationPolicy = REQUIRED

**评论**

* 配置CUG授权并启用/禁用评估。
用于配置不应受CUG授权影响的主体排除列表的服务。

   >[!NOTE]
   > 
   >如果未配置`CugExcludeImpl`，则`CugConfiguration`将回退到默认值。

   如有特殊需要，可以插入自定义CugExclude实施。

* 实施LoginPathProvider的OSGi组件，该组件会向LoginSelectorHandler公开匹配的登录路径。 它对RequirementHandler有强制引用，该RequirementHandler用于通过granite:AuthenticationRequired mixin类型注册侦听内容中存储的更改身份验证要求的观察者。
* 实施RequirementHandler的OSGi组件，该组件会通知SlingAuthenticator有关对创作要求的更改。

   由于此组件的配置策略是REQUIRE，因此只有在指定一组受支持的路径时才会激活它。

   启用该服务将启动RequirementService。

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
       <td><p>Service to configure exclusion list of principals which should not be affected by the CUG authorization.</p> <p>NOTE: If the CugExcludeImpl is not configured, the CugConfiguration will fall back to the default.</p> <p>It is possible to plug a custom CugExclude implementation in case of special needs.</p> </td>
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
