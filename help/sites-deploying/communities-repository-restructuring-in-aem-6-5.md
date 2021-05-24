---
title: 6.4中的AEM Communities存储库重组
seo-title: 6.4中的AEM Communities存储库重组
description: 了解如何进行必要的更改，以便迁移到AEM 6.4 for Communities中的新存储库结构。
seo-description: 了解如何进行必要的更改，以便迁移到AEM 6.4 for Communities中的新存储库结构。
uuid: d161655f-4074-44a7-8d69-38e80934c58b
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 7383265b-0ed4-4ea7-b741-0a417d187bdd
feature: 升级
exl-id: 4d2bdd45-a29a-4936-b8da-f7e011d81e83
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 3%

---

# 6.5 {#repository-restructuring-for-aem-communities-in}中的AEM Communities存储库重组

如AEM 6.4](/help/sites-deploying/repository-restructuring.md)中的父[存储库重组页面中所述，升级到AEM 6.5的客户应使用此页面评估与影响AEM Communities解决方案的存储库更改相关的工作量。 某些更改需要在AEM 6.5升级过程中完成工作，而其他更改可能会推迟到将来进行升级。

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

## 使用6.5升级{#with-upgrade}

### 电子邮件通知模板{#e-mail-notification-templates}

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
   <td><p>如果要移动到“<code>/apps/settings</code>”下的新路径，需要手动迁移。 您可以使用Granite配置管理器执行迁移。</p> <p>您可以通过在“<code>/libs/settings/community/subscriptions</code>”节点上将属性<code>mergeList</code>设置为<code>true</code>并添加一个<code>nt:unstructured</code>子节点来执行迁移。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 订阅配置{#subscription-configurations}

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
   <td><p>如果要移动到“<code>/apps/settings</code>”下的新路径，需要手动迁移。 您可以使用Granite配置管理器执行迁移。</p> <p>您可以通过在“<code>/libs/settings/community/subscriptions</code>”节点上将属性<code>mergeList</code>设置为<code>true</code>并添加一个<code>nt:unstructured</code>子节点来执行迁移。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 关注词配置{#watchwords-configurations}

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
   <td>延迟迁移任务可用于清理社区配置。<br /> <p>任务将关注词从<code>/etc/watchwords</code>移动到<code>/conf/global/settings/community/watchwords</code>。</p> <p>如果自定义的关注词存储在SCM中，则应将其部署到<code>/apps/settings/...</code>，并且您必须确保没有优先覆盖的<code>/conf/global/settings/...</code>配置。</p> <p>迁移任务将删除<code>/etc</code>位置。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

## 在将来升级之前{#prior-to-upgrade}

### 标记配置{#badging-configurations}

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
     <li>使用<strong>Tools</strong>下的<strong>Configuration Browser</strong>创建站点上下文存储段</li>
     <li>转到站点根</li>
     <li>将<code>cq:confproperty</code>设置为要存储所有设置的存储段路径。 也可以通过站点<strong>编辑向导 — 设置云配置输入</strong>来设置。</li>
     <li>将相关标记规则和评分规则从<code>/etc/community/*</code>移至上一步中创建的网站上下文存储段。</li>
     <li>调整站点根目录上的标记规则和评分规则属性，以使其相对引用新规则位置。
      <ol>
       <li>例如，如果<code>cq:conf = /conf/we-retail</code>的属性，则<code>badgingRules [] = community/badging/rules</code>（如果规则现在已移至此新存储段）。</li>
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

### 经典社区控制台设计{#classic-communities-console-designs}

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

### Facebook Social登录配置{#facebook-social-login-configurations}

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
       <li>通过位于<strong>工具&gt;Cloud Services&gt; Facebook Social登录配置</strong>的AEM创作UI，手动重新创建新的Facebook Social登录配置。<br /> 或 <br /> </li>
       <li>将任何新的Facebook云配置从“上一位置”复制到<code>/conf/global or /conf/&lt;tenant&gt;</code>下的相应新位置。</li>
      </ol> </li>
     <li>通过将<code>[cq:Page]/jcr:content@cq:conf</code>属性设置为“新位置”中的绝对路径，更新任何AEM Communities站点根目录以引用新的Facebook社交登录配置。</li>
     <li>取消旧版Facebook ConnectCloud Service与任何更新为引用新位置的AEM Communities站点根的关联。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 语言选项配置{#language-options-configurations}

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

### Pinterest Social登录配置{#pinterest-social-login-configurations}

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
       <li>通过位于<strong>工具&gt;Cloud Services&gt; Pinterest Social登录配置</strong>的AEM创作UI，手动重新创建新的Pinterest Social登录配置。<br /> 或</li>
       <li>将任何新的Pinterest云配置从“上一位置”复制到<code>/conf/global or /conf/&lt;tenant&gt;</code>下的相应新位置。</li>
      </ol> </li>
     <li>通过将<code>[cq:Page]/jcr:content@cq:conf</code>属性设置为“新位置”中的绝对路径，更新任何AEM Communities站点根目录以引用新的Pinterest社交登录配置。</li>
     <li>取消旧版Pinterest ConnectCloud Service与任何更新为引用新位置的AEM Communities站点根的关联。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 评分配置{#scoring-configurations}

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
   <td><p>为了与新的存储库结构保持一致，评分规则可以存储在<code>/apps/settings/</code>或/中<code>conf/.../settings</code></p>
    <ol>
     <li>对于<code>/apps/settings</code>，此规则将充当在SCM中管理的全局或默认规则。</li>
    </ol> <p>使用CRXDELite在<code>/conf/</code>中创建上下文感知配置：</p>
    <ol>
     <li>在所需的<code>/conf/.../settings</code>位置<br />中创建配置 </li>
     <li>社区站点必须设置<code>cq:conf </code>属性属性。
      <ol>
       <li>如果未设置<code>cq:conf</code>，则将从站点根节点的属性“<code>scoringRules</code>”的给定路径中直接读取评分规则，例如： <code>/content/we-retail/us/en/community/jcr:content</code></li>
      </ol> </li>
    </ol> <p>清理：删除资源 <code>/etc/community/scoring</code></p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### Twitter Social登录配置{#twitter-social-login-configurations}

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
       <li>通过位于<strong>工具&gt;Cloud Services&gt; Twitter Social登录配置</strong>的AEM创作UI，手动重新创建新的Twitter Social登录配置。<br /> 或 <br /> </li>
       <li>将任何新的Twitter云配置从“上一位置”复制到<code>/conf/global or /conf/&lt;tenant&gt;</code>下的相应新位置。</li>
      </ol> </li>
     <li>通过将<code>[cq:Page]/jcr:content@cq:conf</code>属性设置为“新位置”中的绝对路径，更新任何AEM Communities站点根目录以引用新的Twitter社交登录配置。</li>
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
