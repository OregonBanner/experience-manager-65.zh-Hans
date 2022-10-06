---
title: 6.4中的AEM Communities存储库重组
seo-title: Repository Restructuring for AEM Communities in 6.4
description: 了解如何进行必要的更改，以便迁移到AEM 6.4 for Communities中的新存储库结构。
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.4 for Communities.
uuid: d161655f-4074-44a7-8d69-38e80934c58b
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 7383265b-0ed4-4ea7-b741-0a417d187bdd
feature: Upgrading
exl-id: 4d2bdd45-a29a-4936-b8da-f7e011d81e83
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 3%

---

# 6.5中的AEM Communities存储库重组 {#repository-restructuring-for-aem-communities-in}

如父项中所述 [AEM 6.4中的存储库重组](/help/sites-deploying/repository-restructuring.md) 页面，升级到AEM 6.5的客户应使用此页面来评估与影响AEM Communities解决方案的存储库更改相关的工作量。 某些更改需要在AEM 6.5升级过程中完成工作，而其他更改可能会推迟到将来进行升级。

**升级6.5版**

* [电子邮件通知模板](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#e-mail-notification-templates)
* [订阅配置](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#subscription-configurations)

**在将来升级之前**

* [标记配置](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#badging-configurations)
* [经典社区控制台设计](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#classic-communities-console-designs)
* [Facebook Social登录配置](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#facebook-social-login-configurations)
* [语言选项配置](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#language-options-configurations)

* [Pinterest Social登录配置](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#pinterest-social-login-configurations)
* [评分配置](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#scoring-configurations)
* [Twitter Social登录配置](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#twitter-social-login-configurations)
* [杂项](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#misc)

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
   <td><p>如果要在“ ”下移动到新路径，则需要手动迁移<code>/apps/settings</code>" 您可以使用Granite配置管理器执行迁移。</p> <p>您可以通过设置属性来执行迁移 <code>mergeList</code> to <code>true</code> 在“<code>/libs/settings/community/subscriptions</code>“ ”节点并添加 <code>nt:unstructured</code> 子节点。</p> </td>
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
   <td><p>如果要在“ ”下移动到新路径，则需要手动迁移<code>/apps/settings</code>" 您可以使用Granite配置管理器执行迁移。</p> <p>您可以通过设置属性来执行迁移 <code>mergeList</code> to <code>true</code> 在“<code>/libs/settings/community/subscriptions</code>“ ”节点并添加 <code>nt:unstructured</code> 子节点。</p> </td>
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
   <td>延迟迁移任务可用于清理社区配置。<br /> <p>任务将关注词从 <code>/etc/watchwords</code> to <code>/conf/global/settings/community/watchwords</code>.</p> <p>如果自定义的口令存储在SCM中，则应将其部署到 <code>/apps/settings/...</code> 而且你必须确保没有一个 <code>/conf/global/settings/...</code> 优先配置。</p> <p>迁移任务已删除 <code>/etc</code> 位置。</p> </td>
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
   <td><p>需要手动迁移。</p> <p>如果您的实例已自定义标记/评分规则，则无法自动将所有规则放置到存储段下。 需要客户输入要用于您网站的会议存储段（全局或特定于站点）。</p> <p>没有可用于为网站配置标记和评分的UI。</p> <p>要与新的存储库结构保持一致，请执行以下操作：</p>
    <ol>
     <li>使用创建网站上下文存储段 <strong>配置浏览器</strong> 在 <strong>工具</strong></li>
     <li>转到站点根</li>
     <li>已设置 <code>cq:confproperty</code> 到存储所有设置的存储段路径。 也可以通过网站进行设置 <strong>编辑向导 — 设置云配置输入</strong>.</li>
     <li>将相关标记规则和评分规则从 <code>/etc/community/*</code> 到在上一步中创建的站点上下文存储段。</li>
     <li>调整站点根目录上的标记规则和评分规则属性，以使其相对引用新规则位置。
      <ol>
       <li>例如，如果 <code>cq:conf = /conf/we-retail</code>，则 <code>badgingRules [] = community/badging/rules</code> 如果规则现在已移至此新存储段。</li>
      </ol> </li>
     <li>同样，调整标记规则节点中对评分规则的引用，使其具有相对路径。</li>
    </ol> <p> </p> <p>最后，通过删除资源进行清理 <code>/etc/community/badging</code></p> </td>
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

### Facebook Social登录配置 {#facebook-social-login-configurations}

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
       <li>通过AEM创作UI在 <strong>工具&gt;Cloud Services&gt; Facebook Social登录配置</strong>.<br /> 或 <br /> </li>
       <li>将任何新的Facebook云配置从“先前的位置”复制到 <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>通过设置 <code>[cq:Page]/jcr:content@cq:conf</code> 属性到“新建位置”中的绝对路径。</li>
     <li>取消旧版Facebook ConnectCloud Service与任何更新为引用新位置的AEM Communities站点根的关联。</li>
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

### Pinterest Social登录配置 {#pinterest-social-login-configurations}

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
       <li>通过AEM创作UI在 <strong>工具&gt;Cloud Services&gt; Pinterest Social登录配置</strong>.<br /> 或</li>
       <li>将任何新的Pinterest云配置从“先前的位置”复制到 <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>通过将 <code>[cq:Page]/jcr:content@cq:conf</code> 属性到“新建位置”中的绝对路径。</li>
     <li>取消旧版Pinterest ConnectCloud Service与任何更新为引用新位置的AEM Communities站点根的关联。</li>
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
   <td><p>为了与新的存储库结构保持一致，评分规则可以存储在 <code>/apps/settings/</code> 或/<code>conf/.../settings</code></p>
    <ol>
     <li>对于 <code>/apps/settings</code>，这将作为在SCM中管理的全局或默认规则。</li>
    </ol> <p>在中创建上下文感知配置 <code>/conf/</code> 使用CRXDELite:</p>
    <ol>
     <li>在所需的中创建配置 <code>/conf/.../settings</code> 位置<br /> </li>
     <li>社区站点必须具有 <code>cq:conf </code>属性属性集。
      <ol>
       <li>如果否 <code>cq:conf</code> 设置，则将从属性“的给定路径中直接读取评分规则<code>scoringRules</code>“ ”，例如： <code>/content/we-retail/us/en/community/jcr:content</code></li>
      </ol> </li>
    </ol> <p>清理：删除资源 <code>/etc/community/scoring</code></p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### Twitter Social登录配置 {#twitter-social-login-configurations}

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
       <li>通过AEM创作UI在 <strong>工具&gt;Cloud Services&gt; Twitter Social登录配置</strong>.<br /> 或 <br /> </li>
       <li>将任何新的Twitter云配置从“先前的位置”复制到 <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>通过设置 <code>[cq:Page]/jcr:content@cq:conf</code> 属性到“新建位置”中的绝对路径。</li>
     <li>取消旧版Twitter ConnectCloud Service与任何更新为引用新位置的AEM Communities站点根的关联。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 杂项 {#misc}

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
   <td><p>Adobe在以下位置提供了迁移实用程序：</p> <p><a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration">https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration</a></p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>现有的自定义模板将移至 <code>/conf/global/settings/community/template/&lt;groups/sites/functions&gt;</code></td>
  </tr>
 </tbody>
</table>
