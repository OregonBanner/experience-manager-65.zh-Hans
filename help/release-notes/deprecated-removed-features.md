---
title: 已弃用和已删除的功能
description: 以下发行说明特定于 Adobe Experience Manager 6.5 中已弃用和已删除功能。
uuid: 81d9a064-e712-4eff-bd3b-6e15513a5435
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: e8e2e01b-0117-48c3-86d8-609d29a147be
docset: aem65
translation-type: tm+mt
source-git-commit: 4be5286858b255a30983b5987ac54c4e71dd4f2f

---


# 已弃用和已删除的功能 {#deprecated-and-removed-features}

Adobe 不断评估产品功能，以便随着时间的推移，使用更现代的替代方案重塑或替换旧功能，从而提高整体客户价值，此过程中将始终谨慎考虑功能的向后兼容性。

为了传达即将删除/替换 AEM 功能，以下规则适用：

1. 首先宣布弃用。虽然已弃用，但功能仍然可用，但不会进一步增强。
1. 最早将在以下主要发行版中删除已弃用的功能。将宣布实际删除目标的日期。

在实际删除之前，此过程将为客户提供至少一个发行周期时间，使其实施适应已弃用功能的新版本或后续版本。

## 已弃用功能 {#deprecated-features}

本部分列出了 AEM 6.5 中已标记为弃用的特性和功能。通常，计划在未来发行版中删除的特性将首先设置为弃用，并提供备用方案。

建议客户检查其当前部署中是否使用了此类特性/功能，然后制定相应的计划以将其实施更改为使用提供的备选方案。

<table>
 <tbody>
  <tr>
   <td><b>区域</b></td>
   <td><b>功能</b></td>
   <td><b>替换</b></td>
  </tr>
  <tr>
   <td>Creative Cloud 集成</td>
   <td><p><a href="/help/assets/aem-cc-folder-sharing-best-practices.md">AEM 6.2中引入了“AEM到Creative Cloud文件夹共享</a> ”功能，旨在让创意用户能够从AEM访问资产，以便在CC应用程序中打开资产并上传新文件或将更改保存到AEM。 在 Creative Cloud 应用程序中发布的新功能“Adobe 资产链接”提供了更佳的用户体验，能够直接从 Photoshop、InDesign 和 Illustrator 中轻松访问 AEM 资产。</p> <p>Adobe 不打算进一步增强“AEM 到 Creative Cloud Folder Sharing”集成。虽然该功能包含在 AEM 中，但强烈建议客户使用替换解决方案。</p> </td>
   <td>建议客户切换到新的Creative Cloud集成功能，包括Adobe Asset Link或AEM桌面应用程序。 有关更多详细信息，请查看 <a href="/help/assets/aem-cc-integration-best-practices.md">AEM 和 Creative Cloud 集成最佳实践</a>。</td>
  </tr>
  <tr>
   <td>资产</td>
   <td>
    <ol>
     <li>默认情况下，对发布实例禁用 AssetDownloadServlet。有关更多详细信息，请参阅 <a href="/help/sites-administering/security-checklist.md">AEM 安全核对清单</a>。</li>
     <li>如果用户对 /content/dam/collections 没有足够的（读写）权限，则用户无法创建收藏集。</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/sites-administering/security-checklist.md">AEM 安全核对清单</a>中描述的配置。</li>
     <li>遵循用户的访问控制设置并确保具有适当的权限。<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Adobe Search &amp; Promote</td>
   <td><p>已弃用与Adobe Search &amp; Promote的集成。</p> <p>Adobe 不打算进一步增强 Search &amp; Promote 集成。请注意，Search &amp; Promote 集成在弃用期间仍完全受支持。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>DTM 标记管理器</td>
   <td>已弃用与 DTM (Dynamic Tag Manager) 的集成。</td>
   <td>切换为使用 Adobe Experience Platform Launch 作为标记管理器</td>
  </tr>
  <tr>
   <td>Adobe Target</td>
   <td>为 AEM 新增了一项功能，可以在 AEM 6.5 中通过基于 Adobe I/O 的 Adobe Target Standard API (Rest API) 连接到 Adobe Target 服务，与此同时，弃用 Target Classic API (XML) 方法。</td>
   <td><a href="https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html">重新配置集成以使用新的 API</a></td>
  </tr>
  <tr>
   <td>Adobe Target</td>
   <td>已在 AEM 中弃用基于 mbox.js 的 Adobe Target 集成。</td>
   <td>切换为使用 at.js 1.x</td>
  </tr>
  <tr>
   <td>商务</td>
   <td><p><a href="https://github.com/adobe/commerce-cif-api" target="_blank">CIF REST</a> 2018年作为一组微型服务提供，用于实现AEM与商务引擎之间的集成。</p> <p>在Adobe于2018年年中收购Magento后，Adobe决定更改其方法，原因有二： </p> <p><strong>1.</strong> Magento有其自己的一组Commerce API（REST和GraphQL），维护两组API不是很好的做法 </p> <p><strong>2.</strong> 市场趋势表明，客户正在转向GraphQL，因为它是一种更高效的数据查询方式。 2019年，Adobe发布了新的商务集成框架，使用Magento的GraphQL API作为真相的来源。</p> <p>Adobe不打算在CIF REST中进一步投资。 强烈建议客户使用更换解决方案。</p> </td>
   <td><p>对于AEM-Magento集成，切换到 <a href="https://github.com/adobe/aem-cif-project-archetype" target="_blank">AEM CIF Archetype</a>，和 <a href="https://github.com/adobe/aem-core-cif-components" target="_blank">AEM CIF核心组件</a></p> <p>有关详细信 <a href="https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md" target="_blank">息，请查看使用Commerce Integration Framework的AEM和Magento Integration</a> 。</p> <p>我们的产品路线图支持与新方法进行第三方（Magento除外）集成。</p> </td>
  </tr>
  <tr>
   <td>组件 (AEM Sites)</td>
   <td><p>Adobe 计划不再进一步提升 /libs/foundation/components 中存储的大多数基础组件的功能。</p> <p>在组件文件夹中查找 <strong>cq:deprecated</strong> 和 <strong>cq:deprecatedReason</strong> 属性。</p> <p>AEM 6.5包含基础组件，从早期版本升级的客户可以按原样继续使用它们。 此外，在弃用时，基础组件仍完全受支持。 </p> </td>
   <td>建议客户在未来的项目中使用核心组件。Existing sites can remain as is or use the <a href="https://github.com/adobe/aem-modernize-tools">AEM Modernize Tools Suite</a> to refactor the site to use Core Components.</td>
  </tr>
  <tr>
   <td>组件 (AEM Sites)</td>
   <td>从 AEM 6.5 开始，/libs/wcm/designimporter/components 中的设计导入程序组件已标记为弃用组件，Adobe 计划不再进一步增强该设计导入程序的实施。</td>
   <td>Adobe 计划在未来的发行版本中提供替代的用例实施。</td>
  </tr>
  <tr>
   <td>组件 (AEM Forms)</td>
   <td><p>签名步骤允许用户验证和签署自适应表单。 在以前的版本中，签名步骤可以将Adobe Sign和Scribble Signature组件用作签名字段。 在AEM 6.5表单中，已弃用“签名步骤”的基于Scribble Signature的签名体验。</p> </td>
   <td>
    <ul>
     <li>如果您已执行全新安装：
      <ul>
       <li>在自适应表单的签名步骤中使用基于Adobe Sign的签名体验。</li>
       <li>在自适应表单、交互式通信和HTML5表单中使用独立的Scribble Signature组件。</li>
      </ul> </li>
     <li>如果您已从先前版本升级到AEM 6.5 Forms:<br />
      <ul>
       <li>在已使用该功能的表单中继续使用基于Scribble签名的签名步骤签名体验。<br /> </li>
       <li>在创建新表单时，在签名步骤中使用独立的Scribble Signature组件或基于Adobe Sign的签名体验。 </li>
      </ul> </li>
    </ul> <p> </p> <p> </p> </td>
  </tr>
  <tr>
   <td>Foundation</td>
   <td><p>Granite 卸载框架</p> <p>Adobe 不打算进一步增强 5.6.1 中引入的用于外部化资产处理的卸载框架。 </p> </td>
   <td>Adobe 正在开发下一代云本机卸载框架。</td>
  </tr>
  <tr>
   <td>开发人员</td>
   <td><p>Hobbes.js</p> <p>Adobe不计划对hobbes.js用户界面测试框架进行进一步增强。</p> </td>
   <td>Adobe建议客户使用Selenium自动化。</td>
  </tr>
  <tr>
   <td>开发人员</td>
   <td><p>jQuery UI 客户端库</p> <p>Adobe 不打算进一步维护和更新作为分发版（快速入门）的一部分提供的 jQuery UI 客户端库</p> </td>
   <td>Adobe建议仍需jQuery UI才能生成代码的客户将其添加到其项目代码库中。</td>
  </tr>
  <tr>
   <td>开发人员</td>
   <td><p>jQuery Animation客户端库(granite.jquery.animation)</p> <p>Adobe 不打算进一步维护和更新作为分发版（快速入门）的一部分提供的 jQuery Animation 客户端库</p> </td>
   <td>Adobe建议仍需jQuery Animations作为其代码的客户将其添加到项目代码库中。</td>
  </tr>
  <tr>
   <td>开发人员</td>
   <td><p>Handlebars 客户端库</p> <p>Adobe 不打算进一步维护和更新作为分发版（快速入门）的一部分提供的 Handlebar 客户端库</p> </td>
   <td>Adobe建议仍需要Handlebars代码的客户将其添加到其项目代码库中。</td>
  </tr>
  <tr>
   <td>开发人员</td>
   <td><p>Lawnchair 客户端库</p> <p>Adobe 不打算进一步维护和更新作为分发版（快速入门）的一部分提供的 Lawnchair 客户端库</p> </td>
   <td>Adobe建议仍需Lawnchair编写代码的客户将其添加到其项目代码库中。</td>
  </tr>
  <tr>
   <td>开发人员</td>
   <td><p>Granite.Sling.js 客户端库</p> <p>Adobe 不打算进一步增强作为分发版（快速入门）的一部分提供的 Granite.Sling.js 客户端库</p> </td>
   <td>Adobe建议依赖库功能的客户重新调整其代码以不再使用它。</td>
  </tr>
  <tr>
   <td>开发人员</td>
   <td>使用 YUI 压缩/缩小 JavaScript 客户端库。Adobe 不打算进一步更新 YUI 库。在AEM 6.4之前，YUI默认为使用切换到Google Closure Compiler(GCC)的选项缩小JavaScript。 从 AEM 6.5 开始，默认使用 GCC。</td>
   <td>Adobe建议升级到AEM 6.5的客户切换到GCC进行实施</td>
  </tr>
  <tr>
   <td>开发人员</td>
   <td><p>CRXDE lite 中的 Classic UI Dialog Editor</p> <p>Adobe 不打算进一步增强作为分发版（快速入门）的一部分提供的 Classic UI Dialog Editor</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>表单</td>
   <td><p>已弃用AEM Forms与AEM Mobile集成&lt; </p> </td>
   <td>无替换项 </td>
  </tr>
 </tbody>
</table>

## 已删除功能 {#removed-features}

本节列表了已从AEM 6.5中删除的特性和功能。先前版本的这些功能标记为已弃用。

| 区域 | 功能 | 替换 |
|--- |--- |--- |
| 分析活动图 | AEM中包含的活动图版本。 | 由于 Adobe Analytics API 中的安全性更改，因此无法再使用 AEM 中包含的 Activity Map 版本。使用Adobe [Analytics提供的ActivityMap插件](https://docs.adobe.com/content/help/zh-Hans/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html)。 |
| 集成 | ExactTarget集成已从默认分发（快速启动）中删除，并且不再可用。 | 无替换项 |
| 集成 | Salesforce Force API 集成已从默认分发版（快速入门）中删除，现在是一个额外的包，可从 PackageShare 安装。 | 功能仍然可用。 |
| Forms | 由于不再支持 Adobe Central 产品，删除了对 Adobe Central Migration Bridge 服务的支持。 | 无替换项 |
| 表单 | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | 无替换项 |
| 表单 | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | 无替换项 |
| 表单 | 在JEE上从LiveCycle ES4 SP1到AEM 6.5 Forms的单跳升级不可用 | 请参 [阅AEM Forms升级文档](../forms/using/upgrade.md) 中的可用升级路径。 |
| 开发人员 | Firebug Lite 已从默认分发版（快速入门）中删除 | 使用浏览器内置的开发人员控制台 |
| 开发人员 | Remove `customJavaScriptPath` support in HTML Client Library Manager. | 无替换项 |
| 资产 | 在AEM 6.5中，资产卸载功能已被删除 | 无替换项 |
| 缓存 | `system/console/slingjsp` is removed is no lenable in AEM 6.5. | 类和轻缓存存储在Apache Sling Commons FileSystem ClassLoader包下。 您可以在AEM Web Console中检查捆绑编号，并直接从文件系统(`crx-quickstart/launchpad/felix/bundle<ID>`)中删除缓存文件夹。 |

## 针对下一个发行版的预先宣布 {#pre-announcement-for-next-release}

此部分用于预先宣布未来发行版中的更改，这些更改未弃用，但会影响客户。以下内容为规划目的而提供。

| 区域 | 功能 | 公告 |
|--- |--- |--- |
| Foundation | UI 框架 | Adobe 计划在 2019 年弃用 Coral UI 2 组件。Coral UI 3 是随 AEM 6.2 引入的，而 AEM 6.5 完全基于 Coral 3。Adobe 建议使用 Coral 2 构建自定义 UI 的客户和合作伙伴将它们重构为使用 Coral 3。Adobe 将提供将 Coral 2 对话框转换为 Coral 3 的工具 - [阅读更多](/help/sites-developing/dialog-conversion.md)。 |
