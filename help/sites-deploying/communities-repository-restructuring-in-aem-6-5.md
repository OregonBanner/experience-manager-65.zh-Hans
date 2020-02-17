---
title: 6.4中的AEM Communities存储库重组
seo-title: 6.4中的AEM Communities存储库重组
description: 了解如何进行必要的更改以迁移到AEM 6.4 for Communities中的新存储库结构。
seo-description: 了解如何进行必要的更改以迁移到AEM 6.4 for Communities中的新存储库结构。
uuid: d161655f-4074-44a7-8d69-38e80934c58b
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 7383265b-0ed4-4ea7-b741-0a417d187bdd
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb

---


# 6.5中的AEM Communities存储库重组 {#repository-restructuring-for-aem-communities-in}

如AEM 6.4 [](/help/sites-deploying/repository-restructuring.md) 中的父存储库重组页面中所述，升级到AEM 6.5的客户应使用此页面评估与影响AEM Communities解决方案的存储库更改相关的工作成果。 某些更改需要在AEM 6.5升级过程中进行工作，而其他更改可能会延迟到将来升级。

**升级6.5版**

* [电子邮件通知模板](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#e-mail-notification-templates)
* [订阅配置](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#subscription-configurations)

**在将来升级之前**

* [标记配置](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#badging-configurations)
* [经典社区控制台设计](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#classic-communities-console-designs)
* [Facebook社交登录配置](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#facebook-social-login-configurations)
* [语言选项配置](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#language-options-configurations)

* [Pinterest社交登录配置](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#pinterest-social-login-configurations)
* [评分配置](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#scoring-configurations)
* [Twitter社交登录配置](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#twitter-social-login-configurations)
* [Misc](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#misc)

## 升级6.5版 {#with-upgrade}

### 电子邮件通知模板 {#e-mail-notification-templates}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>如果您要移到“”下的新路径，则需要手动迁<code>/apps/settings</code>移。 您可以使用Granite Configuration manager执行迁移。</p> <p>您可以通过在“”节点上将属 <code>mergeList</code> 性设 <code>true</code> 置为并添加<code>/libs/settings/community/subscriptions</code>子节点来执行迁 <code>nt:unstructured</code> 移。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 订阅配置 {#subscription-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>如果您要移到“”下的新路径，则需要手动迁<code>/apps/settings</code>移。 您可以使用Granite Configuration manager执行迁移。</p> <p>您可以通过在“”节点上将属 <code>mergeList</code> 性设 <code>true</code> 置为并添加<code>/libs/settings/community/subscriptions</code>子节点来执行迁 <code>nt:unstructured</code> 移。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 关注词配置 {#watchwords-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td>/etc/watchwords</td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td>/libs/community/watchwords</td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td>“延迟迁移”任务可用于清除“社区配置”。<br /> <p>“任务”会将关注词从移动 <code>/etc/watchwords</code> 到移动 <code>/conf/global/settings/community/watchwords</code>。</p> <p>如果自定义的口令存储在SCM中，则应将其部署到 <code>/apps/settings/...</code> ，并且您必须确保不存在优先 <code>/conf/global/settings/...</code> 的覆盖配置。</p> <p>迁移任务可删除 <code>/etc</code> 位置。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

## 在将来升级之前 {#prior-to-upgrade}

### 标记配置 {#badging-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/community/badging</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><strong>徽章规则：</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>徽章图像：</strong></p> <p>对于默认图像： <code>/etc/community/badging/images are moved to /libs/community/badging/images</code></p> <p>对于自定义图像： <code>/content/community/badging/images</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>需要手动迁移。</p> <p>如果您的实例已自定义标记／评分规则，则无法自动将所有规则放在存储桶下。 需要客户输入要用于您网站的会议时段（全局或特定于站点）。</p> <p>没有可用于为站点配置标记和评分的UI。</p> <p>要与新存储库结构对齐，请执行以下操作：</p>
    <ol>
     <li>使用“工具”下的“配置浏览器” <strong>创建站点上下文存储</strong> 段 <strong>。</strong></li>
     <li>转到站点根目录</li>
     <li>设置 <code>cq:confproperty</code> 到存储所有设置的存储段路径。 也可以通过站点编辑向导——设 <strong>置云配置输入来设置</strong>。</li>
     <li>将相关标记规则和评分规则从上 <code>/etc/community/*</code> 一步创建的站点上下文存储段移至该存储段。</li>
     <li>调整站点根目录上的标记规则和评分规则属性，以具有对新规则位置的相对引用。
      <ol>
       <li>例如，如果属性为 <code>cq:conf = /conf/we-retail</code>，则 <code>badgingRules [] = community/badging/rules</code> 规则现在已移到此新存储段。</li>
      </ol> </li>
     <li>同样，将标记规则节点中对评分规则的引用调整为具有相对路径。</li>
    </ol> <p> </p> <p>最后，通过删除资源来清理 <code>/etc/community/badging</code></p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 经典社区控制台设计 {#classic-communities-console-designs}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/designs/social/console</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/social/console</code></p> <p><code>/apps/settings/wcm/designs/social/console</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### Facebook Social Login Configurations {#facebook-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/cloudservices/facebookconnect</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/facebookconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/facebookconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>任何新的Facebook云配置都必须迁移到新位置。</p>
    <ol>
     <li>将“上一位置”中的现有配置迁移到“新位置”。
      <ol>
       <li>通过AEM创作UI在“工具”&gt;“云服务”&gt;“Facebook社交登录配置” <strong>中手动重新创建新的Facebook社交登录配置</strong>。<br /> 或 <br /> </li>
       <li>将任何新Facebook云配置从上一位置复制到相应的新位置下 <code>/conf/global or /conf/&lt;tenant&gt;</code>。</li>
      </ol> </li>
     <li>通过将属性设置为“新位置”中的绝对路径，更新任何AEM Communities站点根目录以引用 <code>[cq:Page]/jcr:content@cq:conf</code> 新的Facebook社交登录配置。</li>
     <li>将旧版Facebook Connect cloud服务与任何更新为引用新位置的AEM Communities站点根取消关联。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 语言选项配置 {#language-options-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/social/config/languageOpts</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/social/translation/languageOpts</code></td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td>不适用<br /> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### Pinterest Social Login Configurations {#pinterest-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/cloudservices/pinterestconnect</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/pinterestconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/pinterestconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>任何新的Pinterest云配置都必须迁移到新位置。</p>
    <ol>
     <li>将“上一位置”中的现有配置迁移到“新位置”。
      <ol>
       <li>通过AEM创作UI在“工具”&gt;“云服务”&gt;“Pinterest社交登录配置”中手 <strong>动重新创建新的Pinterest社交登录配置</strong>。<br /> 或</li>
       <li>将任何新的Pinterest云配置从先前位置复制到下相应的新位置 <code>/conf/global or /conf/&lt;tenant&gt;</code>。</li>
      </ol> </li>
     <li>通过将属性设置为“新位置”中的绝对路径，更新任何AEM Communities站点根目录以引用新的Pinterest社交登录配置。 <code>[cq:Page]/jcr:content@cq:conf</code></li>
     <li>将旧版Pinterest Connect云服务与任何更新为引用新位置的AEM Communities站点根取消关联。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 评分配置 {#scoring-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>要与新的存储库结构对齐，评分规则可以存储在或/ <code>/apps/settings/</code> 中<code>conf/.../settings</code></p>
    <ol>
     <li>因 <code>/apps/settings</code>为，这将充当SCM中管理的全局或默认规则。</li>
    </ol> <p>使用CRXDELite在中创建上下 <code>/conf/</code> 文感知型配置：</p>
    <ol>
     <li>在所需位置创建配 <code>/conf/.../settings</code> 置<br /> </li>
     <li>社区站点必须设置 <code>cq:conf </code>属性属性。
      <ol>
       <li>如果未 <code>cq:conf</code> 设置，将从站点根节点的属性“<code>scoringRules</code>”的给定路径直接读取评分规则，例如： <code>/content/we-retail/us/en/community/jcr:content</code></li>
      </ol> </li>
    </ol> <p>清除：删除资源 <code>/etc/community/scoring</code></p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### Twitter Social Login Configurations {#twitter-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/cloudservices/twitterconnect</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/twitterconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/twitterconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>任何新的Twitter云配置都必须迁移到新位置。</p>
    <ol>
     <li>将“上一位置”中的现有配置迁移到“新位置”。
      <ol>
       <li>通过AEM创作UI在“工具”&gt;“云服务”&gt;“Twitter社交登录配置” <strong>中手动重新创建新的Twitter社交登录配置</strong>。<br /> 或 <br /> </li>
       <li>将任何新Twitter云配置从上一位置复制到相应的新位置下 <code>/conf/global or /conf/&lt;tenant&gt;</code>。</li>
      </ol> </li>
     <li>通过将属性设置为“新位置”中的绝对路径，更新任何AEM Communities站点根目录以引 <code>[cq:Page]/jcr:content@cq:conf</code> 用新的Twitter社交登录配置。</li>
     <li>将旧版Twitter Connect cloud服务与任何更新为引用新位置的AEM Communities站点根取消关联。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### Misc {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>Adobe已在以下位置提供了迁移实用程序：</p> <p><a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration">https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration</a></p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>现有的自定义模板将移至 <code>/conf/global/settings/community/template/&lt;groups/sites/functions&gt;</code></td>
  </tr>
 </tbody>
</table>

