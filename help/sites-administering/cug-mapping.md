---
title: AEM 6.5中的自定义用户组映射
seo-title: AEM 6.5中的自定义用户组映射
description: 了解自定义用户组映射在AEM中的工作方式。
seo-description: 了解自定义用户组映射在AEM中的工作方式。
uuid: 7520351a-ab71-4661-b214-a0ef012c0c93
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 13085dd3-d283-4354-874b-cd837a9db9f9
docset: aem65
translation-type: tm+mt
source-git-commit: c2937a1989c6cfe33cc3f56f89c307cb5fb8d272
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 1%

---


# AEM 6.5中的自定义用户组映射 {#custom-user-group-mapping-in-aem}

## 与CUG相关的JCR内容比较 {#comparison-of-jcr-content-related-to-cug}

<table>
 <tbody>
  <tr>
   <td><strong>旧版AEM</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td><p>属性： cq:cugEnabled</p> <p>声明节点类型： N/A，剩余属性</p> </td>
   <td><p>授权:</p> <p>节点： rep:cugPolicy of node type rep:CugPolicy</p> <p>声明节点类型： rep:CugMixin</p> <p> </p> <p> </p> <p> </p> 身份验证:</p> <p>混合类型： granite：需要身份验证</p> </td>
   <td><p>为了限制读访问，专用CUG策略被应用到目标节点。</p> <p>注意： 策略只能应用于已配置的支持路径。</p> <p>名为rep:cugPolicy和type rep:CugPolicy的节点受保护，不能使用常规JCR API调用编写； 请改用JCR访问控制管理。</p> <p>有关 <a href="https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html">更多信息</a> ，请参阅此页。</p> <p>为了对节点强制实施身份验证要求，添加混合类型granite:AuthenticationRequired已足够。</p> <p>注意： 仅在已配置的受支持路径下受尊重。</p> </td>
  </tr>
  <tr>
   <td><p>属性： cq:cugPrincipals</p> <p>声明节点类型： NA，剩余财产</p> </td>
   <td><p>属性： rep:principalNames</p> <p>声明节点类型： rep:CugPolicy</p> </td>
   <td><p>包含允许读取受限CUG下内容的那些承担者名称的属性受保护，不能使用常规JCR API调用进行写入； 请改用JCR访问控制管理。</p> <p>有关 <a href="https://svn.apache.org/repos/asf/jackrabbit/trunk/jackrabbitapi/src/main/java/org/apache/jackrabbit/api/security/authorization/PrincipalSetPolicy.java">实施的更</a> 多详细信息，请参阅本页。</p> </td>
  </tr>
  <tr>
   <td><p>属性： cq:cugLoginPage</p> <p>声明节点类型： NA，剩余财产</p> </td>
   <td><p>属性： granite:loginPath（可选）</p> <p>声明节点类型： granite：需要身份验证</p> </td>
   <td><p>定义混合类型granite:AuthenticationRequired的JCR节点可以选择地定义替代登录路径。</p> <p>注意： 仅在已配置的受支持路径下受尊重。</p> </td>
  </tr>
  <tr>
   <td><p>属性： cq:cugRealm</p> <p>声明节点类型： NA，剩余财产</p> </td>
   <td>NA</td>
   <td>不再支持新实施。</td>
  </tr>
 </tbody>
</table>

## OSGi服务比较 {#comparison-of-osgi-services}

**旧版AEM**

标签： AdobeGranite封闭用户组(CUG)支持

名称： com.day.cq.auth.impl.CugSupportImpl

**AEM 6.5**

* 标签： Apache Jackrabbit Oak CUG配置

   名称： org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration

   ConfigurationPolicy = REQUIRED

* 标签： Apache Jackrabbit Oak CUG排除列表

   名称： org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl

   ConfigurationPolicy = REQUIRED

* 名称： com.adobe.granite.auth.requirement.impl.RequirementService
* 标签： AdobeGranite身份验证要求和登录路径处理程序

   名称： com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler

   ConfigurationPolicy = REQUIRED

**评论**

* 配置CUG授权并启用／禁用评估。
用于配置不应受CUG授权影响的承担者的排除列表的服务。

   >[!NOTE]
   > 
   >如果未 `CugExcludeImpl` 配置，则 `CugConfiguration` 将返回默认值。

   根据特殊需要，可以插入自定义CugExclude实现。

* 实现LoginPathProvider的OSGi组件，它向LoginSelectorHandler公开匹配的登录路径。 它对RequirementHandler有强制引用，它用于注册观察者，该观察者通过granite:AuthenticationRequired混音类型监听存储在内容中的更改的身份验证要求。
* 实现RequirementHandler的OSGi组件，该组件会通知SlingAuthenticator有关对身份验证要求的更改。

   由于此组件的配置策略为REQUIRE，因此只有在指定了一组受支持的路径时，才会激活它。

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

