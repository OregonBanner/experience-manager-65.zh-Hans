---
title: 对应管理配置属性
seo-title: 对应管理配置属性
description: 本主题介绍如何使用特定于解决方案的配置来修改资产书写器。 本主题详细介绍了您可以编辑的属性及其描述、默认值和可接受值。
seo-description: 本主题介绍如何使用特定于解决方案的配置来修改资产书写器。 本主题详细介绍了您可以编辑的属性及其描述、默认值和可接受值。
uuid: 6b401d51-9332-459b-b751-42a9b5a1462d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: f2955419-c680-44a7-9913-c594b4577551
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 对应管理配置属性 {#correspondence-management-configuration-properties}

要配置这些属性，请在浏览器中打开以下URL:并选 `https://<server>:<port>/<contextPath>/system/console/configMgr` 择“对 **应管理配置”**。

对应管理具有以下配置属性：

<table>
 <tbody>
  <tr>
   <th><p><strong>属性</strong></p> </th>
   <th><p><strong>描述</strong></p> </th>
   <th><p><strong>默认</strong></p> </th>
   <th><p><strong>可接受的值</strong></p> </th>
  </tr>
  <tr>
   <td><p>缩进</p> </td>
   <td>模块上的缩进<p> </p> </td>
   <td><p>12.7mm</p> </td>
   <td><p>任意数字</p> </td>
  </tr>
  <tr>
   <td>最小宽度数</td>
   <td>使用除罗马数字之外的编号列表时，项目符号／编号字段应用的最小宽度</td>
   <td>8.0mm</td>
   <td>任意数字</td>
  </tr>
  <tr>
   <td><p>罗马数字最小宽度</p> </td>
   <td><p>使用罗马数字时，项目符号／编号字段应用的最小宽度</p> </td>
   <td><p>12.7mm</p> </td>
   <td><p>任意数字</p> </td>
  </tr>
  <tr>
   <td>再现类型</td>
   <td>创建对应应用程序用于渲染字母预览的再现类型。 </td>
   <td>HTML再现</td>
   <td>HTML再现/PDF再现</td>
  </tr>
  <tr>
   <td><p>启用CCR PDF高亮显示</p> </td>
   <td><p>在“创建对应”应用程序中启用PDF高亮显示</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>目标高亮类型</p> </td>
   <td><p>“创建对应”应用程序中的目标高亮类型</p> </td>
   <td><p>边框</p> </td>
   <td><p>边框／填充／无</p> </td>
  </tr>
  <tr>
   <td><p>目标高亮颜色</p> </td>
   <td><p>“创建对应”应用程序中的目标高亮颜色</p> </td>
   <td><p>90;155;245</p> </td>
   <td><p>格式为R;G;B的任何RGB颜色</p> </td>
  </tr>
  <tr>
   <td><p>内容高亮显示类型</p> </td>
   <td><p>“创建对应”应用程序中的内容高亮显示类型</p> </td>
   <td><p>填充</p> </td>
   <td><p>边框／填充／无</p> </td>
  </tr>
  <tr>
   <td><p>内容高亮颜色</p> </td>
   <td><p>“创建对应”应用程序中的内容高亮颜色</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>格式为R;G;B的任何RGB颜色</p> </td>
  </tr>
  <tr>
   <td><p>字段高亮类型</p> </td>
   <td><p>“创建对应”应用程序中的字段高亮类型</p> </td>
   <td><p>填充</p> </td>
   <td><p>边框／填充／无</p> </td>
  </tr>
  <tr>
   <td><p>字段高亮颜色</p> </td>
   <td><p>“创建对应”应用程序中的字段高亮颜色</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>格式为R;G;B的任何RGB颜色</p> </td>
  </tr>
  <tr>
   <td><p>应用程序超时</p> </td>
   <td><p>应用程序超时（秒）</p> </td>
   <td><p>1200</p> </td>
   <td><p>任意数字</p> </td>
  </tr>
  <tr>
   <td><p>PDF文档参数名称</p> </td>
   <td><p>PDF文档在后期处理中的参数名称</p> </td>
   <td><p>inPDFoc</p> </td>
   <td><p>任何字符串变量名称</p> </td>
  </tr>
  <tr>
   <td><p>XML数据参数名称</p> </td>
   <td><p>XML文档（数据）在后期处理中的参数名称</p> </td>
   <td><p>inXMLDoc</p> </td>
   <td><p>任何字符串变量名称</p> </td>
  </tr>
  <tr>
   <td><p>XDP文档参数名称</p> </td>
   <td><p>发送到后处理的XDP文档的参数名称</p> </td>
   <td><p>inXDPDoc</p> </td>
   <td><p>任何字符串变量名称</p> </td>
  </tr>
  <tr>
   <td><p>重定向URL参数名称</p> </td>
   <td><p>从后续进程发送的重定向URL的参数名称此值可以是任何字符串变量名</p> </td>
   <td><p>redirectURL</p> </td>
   <td><p>任何字符串变量名称</p> </td>
  </tr>
  <tr>
   <td><p>PDF提交类型</p> </td>
   <td><p>PDF提交类型（通过“创建对应”应用程序提交时生成的PDF类型）</p> </td>
   <td><p>nonInteractive</p> </td>
   <td><p>交互／非交互</p> </td>
  </tr>
  <tr>
   <td><p>优化数据字典实例</p> </td>
   <td><p>支持优化数据字典实例b/w服务器和客户端的传输</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>自动更正不一致 </p> </td>
   <td><p>启用后，它会自动处理字母分配中可能出现的不一致问题</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>使用配置的数据格式</p> </td>
   <td><p>控制是否使用配置的数据编辑格式和数据显示格式</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>数据显示格式</p> </td>
   <td><p>指定特定于区域设置的数据显示格式</p> </td>
   <td><p>locale=en_US;dateFormat=dd-MM-yyyy;numberDecimalSeparator=。;numberGroupSeparator=,;numberUseGroupSeparator=truelocale=de_DE;dateFormat=dd-MM-yyyy;numberDecimalSeparator=,;numberGroupSeparator=。;numberUseGroupSeparator=truelocale=fr_FR;dateFormat=dd-MM-yyyy;numberDecimalSeparator=,;numberGroupSeparator= ;numberUseGroupSeparator=truelocale=ja_JP;dateFormat=dd-MM-yyyy;numberDecimalSeparator=。;numberGroupSeparator=,;numberUseGroupSeparator=true</p> </td>
   <td><p>--</p> </td>
  </tr>
  <tr>
   <td><p>数据编辑格式</p> </td>
   <td><p>编辑数据格式。 将数据写为字符串或从字符串分析数据时使用</p> </td>
   <td><p>locale=en_US;dateFormat=dd-MM-yyyy;numberDecimalSeparator=。;numberGroupSeparator=,;numberUseGroupSeparator=true</p> </td>
   <td>--<p> </p> </td>
  </tr>
  <tr>
   <td><p>在发布时管理书信实例</p> </td>
   <td><p>启用／禁用“管理信函”功能（仅适用于发布服务器）</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>启用审核</p> </td>
   <td><p>启用／禁用审核功能。 如果为false，则所有操作的审核日志都将被禁用</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>启用读审核</p> </td>
   <td><p>启用／禁用资产读取的审核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>启用创建审核</p> </td>
   <td><p>启用／禁用资产创建的审核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>启用更新审核</p> </td>
   <td><p>启用／禁用资产更新的审核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>启用还原审核</p> </td>
   <td><p>启用／禁用资产还原的审核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>启用发布审核</p> </td>
   <td><p>启用／禁用资产发布的审核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>启用“另存为草稿审核”</p> </td>
   <td><p>启用／禁用用于保存信函草稿的审核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>启用提交审核</p> </td>
   <td><p>启用／禁用信函提交的审核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>启用电子邮件审核</p> </td>
   <td><p>启用／禁用电子邮件发送的审核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>启用打印审核</p> </td>
   <td><p>启用／禁用用于打印信函的审核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>启用自定义交付审核</p> </td>
   <td><p>启用／禁用自定义传送信函的审计功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>附件文档参数名称</p> </td>
   <td><p>发送到后处理的附件文档的参数名称</p> </td>
   <td><p>inAttachmentDocs</p> </td>
   <td><p>任何字符串变量名称</p> </td>
  </tr>
  <tr>
   <td><p>CM用户根</p> </td>
   <td><p>包含所有Correponsement Management用户资产的文件夹的URL</p> </td>
   <td><p>--</p> </td>
   <td><p>有效的文件夹位置</p> </td>
  </tr>
  <tr>
   <td><p>字母缓存大小</p> </td>
   <td><p>指定要保存在缓存中的最大字母数。</p> <p>更改此值将导致清除缓存 <code>in-memory</code> 。</p> </td>
   <td><p>100</p> </td>
   <td><p>任何数字值</p> </td>
  </tr>
  <tr>
   <td><p>启用字母缓存</p> </td>
   <td><p>启用／禁用字母缓存。</p> <p>更改此值将导致清除缓存 <code>in-memory </code> 。</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>数据元素排序</p> </td>
   <td><p>在Letter中按照数据元素的顺序创建对应界面，保持数据元素的排序</p> </td>
   <td><p>true</p> </td>
   <td><p>true/false</p> </td>
  </tr>
  <tr>
   <td><p>支持重新加载</p> </td>
   <td><p>启用／禁用服务器端呈现的字母中的重新加载支持。</p> <p>禁用此功能将提高字母渲染性能。</p> </td>
   <td><p>false</p> </td>
   <td><p>true/false</p> <p> </p> </td>
  </tr>
  <tr>
   <td>临时文件夹</td>
   <td>临时文件夹的位置。</td>
   <td>acm.tpm文件夹</td>
   <td> </td>
  </tr>
  <tr>
   <td>远程保存</td>
   <td>将Letter实例保存到指定的处理作者上。</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>兼容性选项</td>
   <td>格式配置名的兼容性选项：configvalue，以逗号分隔。</td>
   <td>acm.compatibility选项</td>
   <td> </td>
  </tr>
  <tr>
   <td><p>调试目录 </p> <p> </p> </td>
   <td>用于调试的文件系统文件夹位置。 如果目录未生 <code>exists</code>成，则不会生成调试转储。</td>
   <td>acm.debugDirectory</td>
   <td> </td>
  </tr>
 </tbody>
</table>
