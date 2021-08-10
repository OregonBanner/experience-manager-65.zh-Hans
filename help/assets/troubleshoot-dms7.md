---
title: Dynamic Media - Scene7模式故障诊断
description: 对Dynamic Media在Scene7模式下运行时进行故障诊断。
uuid: 77e04ccf-33dc-4d2f-8950-318d4b008f74
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 0d48c031-d3ee-4143-b739-a79ba28fd63a
docset: aem65
role: User, Admin
exl-id: d4507059-a54d-4dc9-a263-e55dfa27eeb1
feature: 疑难解答
source-git-commit: 77687a0674b939460bd34011ee1b94bd4db50ba4
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 1%

---

# Dynamic Media - Scene7模式故障诊断{#troubleshooting-dynamic-media-scene-mode}

以下文档介绍了运行&#x200B;**dynamicmedia_scene7**&#x200B;运行模式的Dynamic Media的故障排除。

## 设置和配置 {#setup-and-configuration}

通过执行以下操作，确保已正确设置Dynamic Media:

* 启动命令包含`-r dynamicmedia_scene7`运行模式参数。
* 任何Adobe Experience Manager 6.4累积修补程序包(CFP)均先于&#x200B;**&#x200B;任何可用的Dynamic Media功能包安装。
* 已安装可选功能包18912。

   此可选功能包适用于FTP支持，或者如果您要将资产从Dynamic Media Classic迁移到Dynamic Media。

* 导航到Cloud Services用户界面，并确认已配置的帐户显示在&#x200B;**[!UICONTROL 可用配置]**&#x200B;下。
* 确保已启用`Dynamic Media Asset Activation (scene7)`复制代理。

   此复制代理位于“创作代理”下。

## 常规（所有资产） {#general-all-assets}

以下是所有资产的一些常规提示和技巧。

### 资产同步状态属性 {#asset-synchronization-status-properties}

可以在CRXDE Lite中审核以下资产属性，以确认资产是否已成功从Experience Manager同步到Dynamic Media:

| **属性** | **示例** | **描述** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a|364266`** | 节点已链接到Dynamic Media的常规指示符。 |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **** PublishCompleteor错误文本 | 资产上传到Dynamic Media的状态。 |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | 必须填充才能生成指向Dynamic Media远程资产的URL。 |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **** 后继 **者失败：`<error text>`** | 集（旋转集、图像集等）、图像预设、查看器预设、资产的图像映射更新或已编辑图像的同步状态。 |

### 同步日志记录 {#synchronization-logging}

同步错误和问题记录在`error.log`(Experience Manager服务器目录`/crx-quickstart/logs/`)中。 有足够的日志记录来确定大多数问题的根本原因，但是您可以通过Sling控制台([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog))将日志记录增加到`com.adobe.cq.dam.ips`包上的DEBUG，以收集更多信息。

### 移动、复制、删除 {#move-copy-delete}

在执行移动、复制或删除操作之前，请执行以下操作：

* 对于图像和视频，在执行移动、复制或删除操作之前，请确认存在`<object_node>/jcr:content/metadata/dam:scene7ID`值。
* 对于图像预设和查看器预设，在执行移动、复制或删除操作之前，请确认存在`https://<server>/crx/de/index.jsp#/etc/dam/presets/viewer/testpreset/jcr%3Acontent/metadata`值。
* 如果缺少上述元数据值，则必须在执行移动、复制或删除操作之前重新上传资产。

### 版本控制 {#version-control}

替换现有Dynamic Media资产（名称和位置相同）时，您可以保留两个资产或替换/创建版本：

* 同时保留这两个属性，会为已发布的资产URL创建一个具有唯一名称的资产。 例如，`image.jpg`是原始资产，`image1.jpg`是新上传的资产。

* Dynamic Media - Scene7模式交付不支持创建版本。 新版本会替换交付中的现有资产。

## 图像和集 {#images-and-sets}

如果您在图像和集合方面遇到问题，请参阅以下疑难解答指南。

<table>
 <tbody>
  <tr>
   <td><strong>带有 OS 剪贴板</strong></td>
   <td><strong>如何调试</strong></td>
   <td><strong>解决方案</strong></td>
  </tr>
  <tr>
   <td>无法在资产详细信息视图中访问复制URL/嵌入按钮</td>
   <td>
    <ol>
     <li><p>转到CRX/DE:</p>
      <ul>
       <li>检查JCR <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code>中是否定义了预设。 如果您从Experience Manager6.x升级到6.4并选择退出迁移，则此位置适用。 否则，位置为<code>/conf/global/settings/dam/dm/presets/viewer</code>。</li>
       <li>检查以确保JCR中的资产在元数据下具有<code>dam:scene7FileStatus</code><strong> </strong>，并显示为<code>PublishComplete</code>。</li>
      </ul> </li>
    </ol> </td>
   <td><p>刷新页面/导航到另一页并返回（必须重新编译边栏JSP）</p> <p>如果这不起作用：</p>
    <ul>
     <li>发布资产。</li>
     <li>重新上传资产并发布它。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>集编辑器中的资产选择器在永久加载中卡住</td>
   <td><p>6.4中要修复的已知问题</p> </td>
   <td><p>关闭选择器并将其重新打开。</p> </td>
  </tr>
  <tr>
   <td><strong></strong> 在编辑资产集时选择资产后，“选择”按钮不处于活动状态</td>
   <td><p> </p> <p>6.4中要修复的已知问题</p> <p> </p> </td>
   <td><p>首先在资产选择器的其他文件夹中选择，然后返回以选择资产。</p> </td>
  </tr>
  <tr>
   <td>在幻灯片之间切换后，轮播热点会四处移动</td>
   <td><p>检查所有幻灯片的大小是否相同。</p> </td>
   <td><p>仅对轮播使用大小相同的图像。</p> </td>
  </tr>
  <tr>
   <td>图像不使用Dynamic Media查看器预览</td>
   <td><p>检查资产的元数据属性(CRXDE Lite)中是否包含<code>dam:scene7File</code></p> </td>
   <td><p>检查所有资产是否都已完成处理。</p> </td>
  </tr>
  <tr>
   <td>上传的资产不会显示在资产选择器中</td>
   <td><p>检查资产的属性<code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code>(CRXDE Lite)</p> </td>
   <td><p>检查所有资产是否都已完成处理。</p> </td>
  </tr>
  <tr>
   <td>卡片视图上的横幅会在资产尚未开始处理时显示<strong>New</strong></td>
   <td>检查资产<code>jcr:content</code> &gt; <code>dam:assetState</code> =如果工作流未提取<code>unprocessed</code>，请检查该资产。</td>
   <td>等待工作流提取资产。</td>
  </tr>
  <tr>
   <td>图像或图像集不显示查看器URL或嵌入代码</td>
   <td>检查查看器预设是否已发布。</td>
   <td><p>转到<strong>工具</strong> &gt; <strong>资产</strong> &gt; <strong>查看器预设</strong>并发布查看器预设。</p> </td>
  </tr>
 </tbody>
</table>

## 视频 {#video}

如果您在视频中遇到问题，请参阅以下疑难解答指南。

<table>
 <tbody>
  <tr>
   <td><strong>带有 OS 剪贴板</strong></td>
   <td><strong>如何调试</strong></td>
   <td><strong>解决方案</strong></td>
  </tr>
  <tr>
   <td>无法预览视频</td>
   <td>
    <ul>
     <li>检查文件夹是否分配了视频配置文件（如果不支持文件格式）。 如果不受支持，则仅显示图像。</li>
     <li>视频配置文件必须包含多个编码预设才能生成AVS集(单个编码被视为MP4文件的视频内容；对于不支持的文件，将其视为与未处理文件相同)。</li>
     <li>通过确认元数据中<code>dam:scene7File</code>的<code>dam:scene7FileAvs</code>，检查视频是否已完成处理。</li>
    </ul> </td>
   <td>
    <ol>
     <li>将视频配置文件分配给文件夹。</li>
     <li>编辑视频配置文件以包含多个编码预设。</li>
     <li>等待视频完成处理。</li>
     <li>重新加载视频时，请确保Dynamic Media编码视频工作流未运行。<br /> </li>
     <li>重新上传视频。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>视频未编码</td>
   <td>
    <ul>
     <li>检查运行模式是否为<code>dynamicmedia_scene7</code>。</li>
     <li>检查是否配置了Dynamic Media云服务。</li>
     <li>检查视频配置文件是否与上传文件夹关联。</li>
    </ul> </td>
   <td>
    <ol>
     <li>使用检查Experience Manager实例 <code>-r dynamicmedia_scene7</code></li>
     <li>检查Cloud Services下的Dynamic Media配置是否正确设置。</li>
     <li>检查文件夹是否包含视频配置文件。 此外，还应检查视频配置文件。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>视频处理过长</td>
   <td><p>要确定视频编码是否仍在进行中或是否已进入失败状态，请执行以下操作：</p>
    <ul>
     <li>检查视频状态<code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
     <li>从工作流控制台<code>https://localhost:4502/libs/cq/workflow/content/console.html</code> &gt;实例、存档、失败选项卡中监视视频。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>缺少视频呈现版本</td>
   <td><p>上传视频时，但没有经过编码的演绎版：</p>
    <ul>
     <li>检查文件夹是否分配了视频配置文件。</li>
     <li>通过确认元数据中的<code>dam:scene7FileAvs</code>，检查视频是否已完成处理。</li>
    </ul> </td>
   <td>
    <ol>
     <li>将视频配置文件分配给文件夹。</li>
     <li>等待视频完成处理。<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## 查看器 {#viewers}

如果您在查看器方面遇到问题，请参阅以下疑难解答指南。

<table>
 <tbody>
  <tr>
   <td><strong>带有 OS 剪贴板</strong></td>
   <td><strong>如何调试</strong></td>
   <td><strong>解决方案</strong></td>
  </tr>
  <tr>
   <td>查看器预设未发布</td>
   <td><p>继续执行示例管理器诊断页面： <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></p> <p>观察计算值。 正确操作时，您会看到以下内容：</p> <p><code>_DMSAMPLE status: 0 unsyced assets - activation not necessary
       _OOTB status: 0 unsyced assets - 0 unactivated assets</code></p> <p><strong>注意</strong>:配置Dynamic Media云设置后，可能需要大约10分钟才能同步查看器资产。</p> <p>如果未激活的资产仍保留，请选择<strong>列出所有未激活的资产</strong>按钮中的任一按钮，以查看详细信息。</p> </td>
   <td>
    <ol>
     <li>在管理工具中导航到查看器预设列表： <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></li>
     <li>选择所有查看器预设，然后选择<strong>发布</strong>。</li>
     <li>导航回示例管理器，并观察未激活的资产计数现在为零。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>查看器预设图稿会从资产详细信息的预览或复制URL/嵌入代码中返回404</td>
   <td><p>在CRXDE Lite中，执行以下操作：</p>
    <ol>
     <li>导航到Dynamic Media同步文件夹中的<code>&lt;sync-folder&gt;/_CSS/_OOTB</code>文件夹（例如，<code>/content/dam/_CSS/_OOTB</code>），</li>
     <li>查找有问题资产的元数据节点（例如<code>&lt;sync-folder&gt;/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/</code>）。</li>
     <li>检查是否存在<code>dam:scene7*</code>属性。 如果资产已成功同步和发布，您会看到<code>dam:scene7FileStatus</code>集设置为<strong>PublishComplete</strong>。</li>
     <li>尝试通过连接以下属性的值和字符串文本直接从Dynamic Media请求图稿
      <ul>
       <li><code>dam:scene7Domain</code></li>
       <li><code>"is/content"</code></li>
       <li><code>dam:scene7Folder</code></li>
       <li><code>&lt;asset-name&gt;</code></li>
       <li>示例: <code>https://&lt;server&gt;/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png</code></li>
      </ul> </li>
    </ol> </td>
   <td><p>如果示例资产或查看器预设图稿未同步或发布，请重新启动整个复制/同步过程：</p>
    <ol>
     <li>导航到CRXDE Lite。
      <ul>
       <li>删除 <code>&lt;sync-folder&gt;/_CSS/_OOTB</code>.</li>
      </ul> </li>
     <li>导航到CRX包管理器：<code>https://localhost:4502/crx/packmgr/</code><a href="https://localhost:4502/crx/packmgr/"></a>
      <ol>
       <li>在列表中搜索查看器包（以<code>cq-dam-scene7-viewers-content</code>开头）</li>
       <li>选择<strong>重新安装</strong>。</li>
      </ol> </li>
     <li>在“Cloud Services”下，导航到Dynamic Media配置页面，然后打开Dynamic Media - S7配置的配置对话框。
      <ul>
       <li>不进行更改，选择<strong>Save</strong>。 此操作会再次触发逻辑，以创建和同步示例资产、查看器预设CSS和图稿。<br />  </li>
      </ul> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>
