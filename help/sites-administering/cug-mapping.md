---
title: AEM 6.5中的自訂使用者群組對應
seo-title: Custom User Group Mapping in AEM 6.5
description: 瞭解自訂使用者群組對應在AEM中的運作方式。
seo-description: Lear how Custom User Group Mapping works in AEM.
uuid: 7520351a-ab71-4661-b214-a0ef012c0c93
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 13085dd3-d283-4354-874b-cd837a9db9f9
docset: aem65
exl-id: 661602eb-a117-454d-93d3-a079584f7a5d
feature: Security
source-git-commit: 2981f11565db957fac323f81014af83cab2c0a12
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# AEM 6.5中的自訂使用者群組對應 {#custom-user-group-mapping-in-aem}

## 與CUG （自訂使用者群組）相關的JCR內容比較 {#comparison-of-jcr-content-related-to-cug}

<table>
 <tbody>
  <tr>
   <td><strong>舊版AEM</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td><p>屬性：cq：cugEnabled</p> <p>宣告節點型別： N/A、剩餘屬性</p> </td>
   <td><p>授权:</p> <p>節點：rep：cugPolicy，節點型別rep：CugPolicy</p> <p>宣告節點型別： rep：CugMixin</p> <p> </p> <p> </p> <p> </p> 身份验证:</p> <p>Mixin型別： granite：AuthenticationRequired</p> </td>
   <td><p>為了限制讀取存取權，會將專用的CUG原則套用至目標節點。</p> <p>注意：原則只能套用至已設定的支援路徑。</p> <p>名稱為rep：cugPolicy和型別rep：CugPolicy的節點受到保護，且不能使用一般JCR API呼叫寫入；請改用JCR存取控制管理。</p> <p>另請參閱 <a href="https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html">此頁面</a> 以取得更多資訊。</p> <p>若要在節點上強制執行驗證需求，只需新增mixin型別granite：AuthenticationRequired即可。</p> <p>注意：僅遵循設定的支援路徑下方。</p> </td>
  </tr>
  <tr>
   <td><p>屬性：cq：cugPrincipals</p> <p>宣告節點型別： NA，剩餘屬性</p> </td>
   <td><p>屬性： rep：principalNames</p> <p>宣告節點型別： rep：CugPolicy</p> </td>
   <td><p>包含允許讀取受限制CUG下方內容之主體名稱的屬性受到保護，且無法使用一般JCR API呼叫進行寫入，請改用JCR存取控制管理。</p> <p>另請參閱 <a href="https://jackrabbit.apache.org/api/2.12/org/apache/jackrabbit/api/security/authorization/PrincipalSetPolicy.html">此頁面</a> 以取得實作的詳細資訊。</p> </td>
  </tr>
  <tr>
   <td><p>屬性：cq：cugLoginPage</p> <p>宣告節點型別： NA，剩餘屬性</p> </td>
   <td><p>屬性： granite：loginPath （選用）</p> <p>宣告節點型別： granite：AuthenticationRequired</p> </td>
   <td><p>已定義mixin型別granite：AuthenticationRequired的JCR節點可選擇定義替代登入路徑。</p> <p>注意：僅遵循設定的支援路徑下方。</p> </td>
  </tr>
  <tr>
   <td><p>屬性：cq：cugRealm</p> <p>宣告節點型別： NA，剩餘屬性</p> </td>
   <td>NA</td>
   <td>不再支援新的實作。</td>
  </tr>
 </tbody>
</table>

## OSGi服務的比較 {#comparison-of-osgi-services}

**舊版AEM**

標籤：AdobeGranite封閉式使用者群組(CUG)支援

名稱： com.day.cq.auth.impl.CugSupportImpl

**AEM 6.5**

* 標籤： Apache Jackrabbit Oak CUG設定

   名稱： org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration

   ConfigurationPolicy =必要

* 標籤： Apache Jackrabbit Oak CUG排除清單

   名稱： org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl

   ConfigurationPolicy =必要

* 名稱： com.adobe.granite.auth.requirement.impl.RequirementService
* 標籤：AdobeGranite驗證需求和登入路徑處理常式

   名稱： com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler

   ConfigurationPolicy =必要

**评论**

* 設定CUG授權及啟用/停用評估。
此服務可設定不受CUG授權影響的主參與者排除清單。

   >[!NOTE]
   > 
   >如果 `CugExcludeImpl` 未設定，則 `CugConfiguration` 會回覆為預設值。

   如有特殊需求，可插入自訂CugExclude實作。

* 實作LoginPathProvider的OSGi元件會公開與LoginSelectorHandler相符的登入路徑。 它具有對RequirementHandler的強制參考，用於註冊觀察者，該觀察者會偵聽透過granite：AuthenticationRequired mixin型別儲存在內容中的已變更驗證要求。
* 實作RequirementHandler的OSGi元件會通知SlingAuthenticator授權需求的變更。

   由於此元件的設定原則為REQUIRE，因此只有在指定一組支援的路徑時，才會啟動它。

   啟用服務會啟動RequirementService。

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
