---
title: Dynamic Media疑难解答- Scene7模式
description: 对Scene7运行模式中的Dynamic Media进行疑难解答。
uuid: 77e04ccf-33dc-4d2f-8950-318d4b008f74
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 0d48c031-d3ee-4143-b739-a79ba28fd63a
docset: aem65
translation-type: tm+mt
source-git-commit: e916f70549197ac9f95443e972401a78735b0560
workflow-type: tm+mt
source-wordcount: '1282'
ht-degree: 0%

---


# Dynamic Media疑难解答- Scene7模式{#troubleshooting-dynamic-media-scene-mode}

以下文档介绍了运行dynamicmedia_scene7运 **行模式的Dynamic Media的疑** 难解答。

## 设置和配置 {#setup-and-configuration}

通过执行以下操作，确保正确设置Dynamic Media:

* 开始设置命令包含 `-r dynamicmedia_scene7` runmode参数。
* 任何AEM 6.4累积修补程序包(CFP)都是先安装的，然后再安装 *任何* 可用的Dynamic Media功能包。
* 安装可选功能包18912。

   此可选功能包用于FTP支持，或者如果您要将资产从Dynamic Media经典(Scene7)迁移到Dynamic Media。

* 导航到Cloud Service用户界面，确认设置的帐户显示在“可用 **[!UICONTROL 配置”下。]**
* 确保已启 `Dynamic Media Asset Activation (scene7)` 用复制代理。

   此复制代理位于作者上的代理下。

## 常规（所有资产） {#general-all-assets}

以下是所有资源的一些一般提示和技巧。

### 资产同步状态属性 {#asset-synchronization-status-properties}

可以在CRXDE Lite中查看以下资产属性，以确认资产从AEM成功同步到Dynamic Media:

| **属性** | **示例** | **描述** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a|364266`** | 节点链接到Dynamic Media的常规指示符。 |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **PublishComplete** 或错误文本 | 资产上传到Dynamic Media的状态。 |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | 必须填充才能生成Dynamic Media远程资产的URL。 |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **成功** 或 **失败：`<error text>`** | 集（旋转集、图像集等）、图像预设、查看器预设、资产的图像映射更新或已编辑图像的同步状态。 |

### 同步记录 {#synchronization-logging}

同步错误和问题已记录 `error.log` 在(AEM服务器目 `/crx-quickstart/logs/`录)中。 可以使用足够的日志记录来确定大多数问题的根本原因，但是您可以通过Sling Console( `com.adobe.cq.dam.ips` https://localhost:4502/system/console/slinglog)将日志记录增加[到](https://localhost:4502/system/console/slinglog)DEBUG以收集更多信息。

### 移动、复制、删除 {#move-copy-delete}

在执行移动、复制或删除操作之前，请执行以下操作：

* 对于图像和视频，在执行移 `<object_node>/jcr:content/metadata/dam:scene7ID` 动、复制或删除操作之前，请先确认存在一个值。
* 对于图像预设和查看器预设，在执 `https://<server>/crx/de/index.jsp#/etc/dam/presets/viewer/testpreset/jcr%3Acontent/metadata` 行移动、复制或删除操作之前，请先确认某个值存在。
* 如果缺少上述元数据值，您需要在移动、复制或删除操作之前重新上传资产。

### 版本控制 {#version-control}

替换现有Dynamic Media资产（同名和位置）时，您可以选择保留两个资产或替换／创建版本：

* 同时保留这两个属性将为已发布的资产URL创建一个具有唯一名称的新资产。 例如， `image.jpg` 是原始资产 `image1.jpg` 和新上传的资产。

* Dynamic Media不支持创建版本- Scene7模式投放。 新版本将替换投放中的现有资产。

## 图像和集 {#images-and-sets}

如果您对图像和集有问题，请参阅以下疑难解答指南。

<table>
 <tbody>
  <tr>
   <td><strong>带有 OS 剪贴板</strong></td>
   <td><strong>如何调试</strong></td>
   <td><strong>解决方案</strong></td>
  </tr>
  <tr>
   <td>无法访问资产详细信息视图中的复制URL/嵌入按钮</td>
   <td>
    <ol>
     <li><p>转到CRX/DE:</p>
      <ul>
       <li>检查JCR中是否定义了预 <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> 设。 请注意，如果您从AEM 6.x升级到6.4并选择退出迁移，则此位置适用。 否则，位置为 <code>/conf/global/settings/dam/dm/presets/viewer</code>。</li>
       <li>检查以确保JCR中的资产在元数据 <code>dam:scene7FileStatus</code><strong> 下 </strong>显示为 <code>PublishComplete</code>。</li>
      </ul> </li>
    </ol> </td>
   <td><p>刷新页面／导航到其他页面并返回（需要重新编译侧边栏JSP）</p> <p>如果这行不通：</p>
    <ul>
     <li>发布资产。</li>
     <li>重新上传资产并发布它。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>在永久加载时，集编辑器中的资产选择器卡住</td>
   <td><p>6.4中要修复的已知问题</p> </td>
   <td><p>关闭选择器并重新打开它。</p> </td>
  </tr>
  <tr>
   <td><strong>选择</strong> “选择”按钮在选择资产作为编辑集的一部分后不处于活动状态</td>
   <td><p> </p> <p>6.4中要修复的已知问题</p> <p> </p> </td>
   <td><p>首先在资产选择器中单击另一个文件夹，然后返回以选择资产。</p> </td>
  </tr>
  <tr>
   <td>在幻灯片之间切换后，旋转热点移动</td>
   <td><p>检查所有幻灯片的大小是否相同。</p> </td>
   <td><p>仅对传送使用大小相同的图像。</p> </td>
  </tr>
  <tr>
   <td>图像与Dynamic Media查看器不预览</td>
   <td><p>检查资产是否包含 <code>dam:scene7File</code> 在元数据属性(CRXDE Lite)中</p> </td>
   <td><p>检查所有资产是否已完成处理。</p> </td>
  </tr>
  <tr>
   <td>上传的资产不会显示在资产选择器中</td>
   <td><p>检查资产的属性 <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>检查所有资产是否已完成处理。</p> </td>
  </tr>
  <tr>
   <td>卡上的横幅视图在 <strong>资产</strong> 尚未开始处理时显示“新增”</td>
   <td>检查资 <code>jcr:content</code> 产&gt; <code>dam:assetState</code> =是否 <code>unprocessed</code> 未被工作流拾取。</td>
   <td>等待工作流选取资产。</td>
  </tr>
  <tr>
   <td>图像或图像集不显示查看器URL或嵌入代码</td>
   <td>检查查看器预设是否已发布。</td>
   <td><p>转到工 <strong>具</strong> &gt;资 <strong>产</strong> &gt;查 <strong>看器预设</strong> ，然后发布查看器预设。</p> </td>
  </tr>
 </tbody>
</table>

## 视频 {#video}

如果您对视频有问题，请参阅以下疑难解答指南。

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
     <li>检查文件夹是否分配了视频用户档案（如果不支持文件格式）。 如果不支持，则仅显示图像。</li>
     <li>视频用户档案必须包含多个编码预设才能生成AVS集(单个编码被视为MP4文件的视频内容； 对于不支持的文件，与未处理文件一样处理)。</li>
     <li>确认元数据中的视频，检查该视频 <code>dam:scene7FileAvs</code> 是否已 <code>dam:scene7File</code> 完成处理。</li>
    </ul> </td>
   <td>
    <ol>
     <li>为文件夹分配视频用户档案。</li>
     <li>编辑视频用户档案以包含多个编码预设。</li>
     <li>等待视频完成处理。</li>
     <li>如果重新加载视频，请确保Dynamic Media编码视频工作流未运行。<br /> </li>
     <li>重新上传视频。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>视频未编码</td>
   <td>
    <ul>
     <li>检查运行模式是 <code>dynamicmedia_scene7</code>否。</li>
     <li>检查是否配置了Dynamic Media云服务。</li>
     <li>检查视频用户档案是否与上传文件夹关联。</li>
    </ul> </td>
   <td>
    <ol>
     <li>通过 <code>-r dynamicmedia_scene7</code></li>
     <li>检查Dynamic Media下的Cloud Service配置是否正确设置。</li>
     <li>检查文件夹是否包含视频用户档案。 另外，检查视频用户档案。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>视频处理过长</td>
   <td><p>要确定视频编码是否仍在进行中或是否已进入失败状态：</p>
    <ul>
     <li>检查视频状态 <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
     <li>从“工作流”控制台&gt;“实例”、“存 <code>https://localhost:4502/libs/cq/workflow/content/console.html</code> 档”、“失败”选项卡监视视频。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>视频再现缺失</td>
   <td><p>上传视频时，但没有编码的演绎版：</p>
    <ul>
     <li>检查文件夹是否分配了视频用户档案。</li>
     <li>通过确认元数据，检查视频是否已完成 <code>dam:scene7FileAvs</code> 处理。</li>
    </ul> </td>
   <td>
    <ol>
     <li>为文件夹分配视频用户档案。</li>
     <li>等待视频完成处理。<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## 查看器 {#viewers}

如果查看器有问题，请参阅以下疑难解答指南。

<table>
 <tbody>
  <tr>
   <td><strong>带有 OS 剪贴板</strong></td>
   <td><strong>如何调试</strong></td>
   <td><strong>解决方案</strong></td>
  </tr>
  <tr>
   <td>查看器预设未发布</td>
   <td><p>继续执行示例管理器诊断页面： <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></p> <p>观察计算值。 正确运行时，您应当看到：</p> <p><code>_DMSAMPLE status: 0 unsyced assets - activation not necessary
       _OOTB status: 0 unsyced assets - 0 unactivated assets</code></p> <p><strong>注意</strong>: 配置Dynamic Media云设置后，查看器资产可能需要大约10分钟才能同步。</p> <p>如果未激活的资产仍保留，请单击“列表所有 <strong>未激活的资产</strong> ”按钮之一以查看详细信息。</p> </td>
   <td>
    <ol>
     <li>在管理工具中导航到查看器预设列表: <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></li>
     <li>选择所有查看器预设，然后单击“ <strong>发布</strong>”。</li>
     <li>导航回示例管理器，并观察未激活的资产计数现在为零。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>查看器预设图稿会从资产详细信息中的预览或复制URL/嵌入代码返回404</td>
   <td><p>在CRXDE Lite中，执行以下操作：</p>
    <ol>
     <li>导航到 <code>&lt;sync-folder&gt;/_CSS/_OOTB</code> Dynamic Media同步文件夹中的文件夹( <code>/content/dam/_CSS/_OOTB</code>例如，</li>
     <li>查找有问题的资产的元数据节点(例如 <code>&lt;sync-folder&gt;/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/</code>)。</li>
     <li>检查属性的存 <code>dam:scene7*</code> 在情况。 如果资产已成功同步并发布，您会看 <code>dam:scene7FileStatus</code> 到设置为 <strong>PublishComplete</strong>。</li>
     <li>尝试通过连接以下属性和字符串文字的值直接从Dynamic Media请求图稿
      <ul>
       <li><code>dam:scene7Domain</code></li>
       <li><code>"is/content"</code></li>
       <li><code>dam:scene7Folder</code></li>
       <li><code>&lt;asset-name&gt;</code></li>
       <li>示例: <code>https://&lt;server&gt;/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png</code></li>
      </ul> </li>
    </ol> </td>
   <td><p>如果示例资产或查看器预设图稿尚未同步或发布，则重新启动整个复制／同步过程：</p>
    <ol>
     <li>导航到CRXDE Lite。
      <ul>
       <li>删除 <code>&lt;sync-folder&gt;/_CSS/_OOTB</code>.</li>
      </ul> </li>
     <li>导航到CRX包管理器： <code>https://localhost:4502/crx/packmgr/</code><a href="https://localhost:4502/crx/packmgr/"></a>
      <ol>
       <li>在列表中搜索查看器包(它开始 <code>cq-dam-scene7-viewers-content</code>)</li>
       <li>单击“ <strong>重新安装</strong>”。</li>
      </ol> </li>
     <li>在Cloud Service下，导航到Dynamic Media配置页，然后打开Dynamic Media的配置对话框- S7配置。
      <ul>
       <li>不进行更改，请单击“ <strong>保存</strong>”。 这会再次触发创建和同步示例资产、查看器预设CSS和图稿的逻辑。<br />  </li>
      </ul> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

