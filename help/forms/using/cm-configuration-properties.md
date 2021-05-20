---
title: 通信管理配置属性
seo-title: 通信管理配置属性
description: 本主题介绍如何使用特定于解决方案的配置来修改资产编辑器。 本主题详细介绍了可编辑的属性及其说明、默认值和可接受值。
seo-description: 本主题介绍如何使用特定于解决方案的配置来修改资产编辑器。 本主题详细介绍了可编辑的属性及其说明、默认值和可接受值。
uuid: 6b401d51-9332-459b-b751-42a9b5a1462d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: f2955419-c680-44a7-9913-c594b4577551
feature: 通信管理
exl-id: c9c007d0-c545-4738-b11b-4c50986342ee
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 3%

---

# 通信管理配置属性{#correspondence-management-configuration-properties}

要配置这些属性，请在浏览器中打开以下URL:`https://<server>:<port>/<contextPath>/system/console/configMgr`并选择&#x200B;**通信管理配置**。

通信管理具有以下配置属性：

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
   <td><p>12.7毫米</p> </td>
   <td><p>任意数字</p> </td>
  </tr>
  <tr>
   <td>最小宽度数</td>
   <td>使用编号列表和罗马数字之外的列表时，要应用于项目符号/数字字段的最小宽度</td>
   <td>8.0毫米</td>
   <td>任意数字</td>
  </tr>
  <tr>
   <td><p>罗马数字最小宽度</p> </td>
   <td><p>使用罗马数字时，要应用于项目符号/数字字段的最小宽度</p> </td>
   <td><p>12.7毫米</p> </td>
   <td><p>任意数字</p> </td>
  </tr>
  <tr>
   <td>演绎版类型</td>
   <td>创建通信应用程序用于呈现信件预览的呈现类型。 </td>
   <td>HTML呈现版本</td>
   <td>HTML呈现版本/PDF呈现版本</td>
  </tr>
  <tr>
   <td><p>启用CCR PDF突出显示</p> </td>
   <td><p>在“创建通信”应用程序中，在PDF上启用高亮显示</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>目标突出显示类型</p> </td>
   <td><p>创建通信应用程序中的目标高亮类型</p> </td>
   <td><p>边框</p> </td>
   <td><p>边框/填充/无</p> </td>
  </tr>
  <tr>
   <td><p>目标高亮显示颜色</p> </td>
   <td><p>创建通信应用程序中的目标高亮颜色</p> </td>
   <td><p>90;155;245</p> </td>
   <td><p>格式为R;G;B的任意RGB颜色</p> </td>
  </tr>
  <tr>
   <td><p>内容突出显示类型</p> </td>
   <td><p>创建通信应用程序中的内容突出显示类型</p> </td>
   <td><p>填充</p> </td>
   <td><p>边框/填充/无</p> </td>
  </tr>
  <tr>
   <td><p>内容高亮显示颜色</p> </td>
   <td><p>创建通信应用程序中的内容高亮显示颜色</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>格式为R;G;B的任意RGB颜色</p> </td>
  </tr>
  <tr>
   <td><p>字段高亮显示类型</p> </td>
   <td><p>创建通信应用程序中的字段高亮类型</p> </td>
   <td><p>填充</p> </td>
   <td><p>边框/填充/无</p> </td>
  </tr>
  <tr>
   <td><p>字段高亮显示颜色</p> </td>
   <td><p>创建通信应用程序中的字段高亮颜色</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>格式为R;G;B的任意RGB颜色</p> </td>
  </tr>
  <tr>
   <td><p>应用程序超时</p> </td>
   <td><p>应用程序超时（以秒为单位）</p> </td>
   <td><p>1200</p> </td>
   <td><p>任意数字</p> </td>
  </tr>
  <tr>
   <td><p>PDF文档参数名称</p> </td>
   <td><p>后处理中PDF文档的参数名称</p> </td>
   <td><p>inPDFDoc</p> </td>
   <td><p>任意字符串变量名称</p> </td>
  </tr>
  <tr>
   <td><p>XML数据参数名称</p> </td>
   <td><p>后处理中XML文档（数据）的参数名称</p> </td>
   <td><p>inXMLDoc</p> </td>
   <td><p>任意字符串变量名称</p> </td>
  </tr>
  <tr>
   <td><p>XDP文档参数名称</p> </td>
   <td><p>发送到后处理的XDP文档的参数名称</p> </td>
   <td><p>inXDPDoc</p> </td>
   <td><p>任意字符串变量名称</p> </td>
  </tr>
  <tr>
   <td><p>重定向URL参数名称</p> </td>
   <td><p>从后处理发送的重定向URL的参数名称此值可以是任何字符串变量名称</p> </td>
   <td><p>redirectURL</p> </td>
   <td><p>任意字符串变量名称</p> </td>
  </tr>
  <tr>
   <td><p>PDF提交类型</p> </td>
   <td><p>PDF提交类型（从“创建通信”应用程序提交时生成的PDF类型）</p> </td>
   <td><p>非交互式</p> </td>
   <td><p>交互式/非交互式</p> </td>
  </tr>
  <tr>
   <td><p>优化数据字典实例</p> </td>
   <td><p>支持优化数据字典实例b/w服务器和客户端的传输</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>自动更正不一致问题 </p> </td>
   <td><p>启用后，它会自动处理信件分配中可能出现的不一致问题</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>使用配置的数据格式</p> </td>
   <td><p>控制是否使用配置的数据编辑格式和数据显示格式</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>数据显示格式</p> </td>
   <td><p>为数据指定区域设置特定的显示格式</p> </td>
   <td><p>locale=en_US;dateFormat=dd-MM-yyyy;numberDecimalSeparator=.;numberGroupSeparator=,;numberUseGroupSeparator=truelocale=de_DE;dateFormat=dd-MM-yyyy;numberDecimalSeparator=,;numberGroupSeparator=.;numberUseGroupSeparator=truelocale=fr_FR;dateFormat=dd-MM-yyyy;numberDecimalSeparator=,;numberGroupSeparator= ;numberUseGroupSeparator=truelocale=ja_JP;dateFormat=dd-MM-yyyy;numberDecimalSeparator=.;numberGroupSeparator=,;numberUseGroupSeparator=true</p> </td>
   <td><p>—</p> </td>
  </tr>
  <tr>
   <td><p>数据编辑格式</p> </td>
   <td><p>编辑数据的格式。 将数据写为字符串或从字符串分析数据时，会使用此参数</p> </td>
   <td><p>locale=en_US;dateFormat=dd-MM-yyyy;numberDecimalSeparator=.;numberGroupSeparator=,;numberUseGroupSeparator=true</p> </td>
   <td>—<p> </p> </td>
  </tr>
  <tr>
   <td><p>在发布时管理信件实例</p> </td>
   <td><p>启用/禁用“管理信件”功能（仅适用于发布服务器）</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>启用审核</p> </td>
   <td><p>启用/禁用审核功能。 如果为false，则将禁用所有操作的审核日志</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>启用读取审核</p> </td>
   <td><p>启用/禁用资产读取的审核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>启用创建审核</p> </td>
   <td><p>启用/禁用资产创建的审核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>启用更新审核</p> </td>
   <td><p>启用/禁用资产更新的审核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>启用还原审核</p> </td>
   <td><p>启用/禁用资产还原的审核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>启用发布审核</p> </td>
   <td><p>启用/禁用资产发布的审核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>启用SaveAsDraft审核</p> </td>
   <td><p>启用/禁用用于保存信件草稿的审核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>启用提交审核</p> </td>
   <td><p>启用/禁用信件提交的审核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>启用电子邮件审核</p> </td>
   <td><p>启用/禁用电子邮件发送的审核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>启用打印审核</p> </td>
   <td><p>启用/禁用用于打印信件的审核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>启用自定义投放审核</p> </td>
   <td><p>启用/禁用用于自定义信件投放的审核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>附件文档参数名称</p> </td>
   <td><p>发送到后处理的附件文档的参数名称</p> </td>
   <td><p>inAttachmentDocs</p> </td>
   <td><p>任意字符串变量名称</p> </td>
  </tr>
  <tr>
   <td><p>CM用户根</p> </td>
   <td><p>包含所有通信管理用户资产的文件夹的URL</p> </td>
   <td><p>—</p> </td>
   <td><p>有效的文件夹位置</p> </td>
  </tr>
  <tr>
   <td><p>信件缓存大小</p> </td>
   <td><p>指定要保留在缓存中的最大字母数。</p> <p>更改此值将清理<code>in-memory</code>缓存。</p> </td>
   <td><p>100</p> </td>
   <td><p>任何数值</p> </td>
  </tr>
  <tr>
   <td><p>启用信件缓存</p> </td>
   <td><p>启用/禁用信件缓存。</p> <p>更改此值将清理<code>in-memory </code>缓存。</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>数据元素排序</p> </td>
   <td><p>按照信件中数据元素的顺序，在创建通信界面中保持数据元素排序</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>支持重新加载</p> </td>
   <td><p>启用/禁用服务器端呈现的信件中的重新加载支持。</p> <p>禁用此功能将提高信件渲染性能。</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> <p> </p> </td>
  </tr>
  <tr>
   <td>临时文件夹</td>
   <td>临时文件夹的位置。</td>
   <td>acm.tpmFolder</td>
   <td> </td>
  </tr>
  <tr>
   <td>远程保存</td>
   <td>保存指定处理作者的信件实例。</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>兼容性选项</td>
   <td>以逗号分隔的格式configname:configvalue的兼容性选项。</td>
   <td>acm.compatibilityOptions</td>
   <td> </td>
  </tr>
  <tr>
   <td><p>调试目录 </p> <p> </p> </td>
   <td>用于调试的文件系统文件夹位置。 如果目录不是<code>exists</code>，则不会生成任何调试转储。</td>
   <td>acm.debugDirectory</td>
   <td> </td>
  </tr>
 </tbody>
</table>
