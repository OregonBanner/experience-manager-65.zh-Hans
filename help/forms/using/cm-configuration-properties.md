---
title: 通信管理配置属性
description: 本主题介绍如何使用特定于解决方案的配置来修改资产编辑器。 本主题详细介绍可编辑的属性、其说明、默认值和可接受值。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
exl-id: c9c007d0-c545-4738-b11b-4c50986342ee
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 3%

---

# 通信管理配置属性 {#correspondence-management-configuration-properties}

要配置这些属性，请在浏览器中打开以下URL： `https://<server>:<port>/<contextPath>/system/console/configMgr` 并选择 **通信管理配置**.

通信管理具有以下配置属性：

<table>
 <tbody>
  <tr>
   <th><p><strong>属性</strong></p> </th>
   <th><p><strong>描述</strong></p> </th>
   <th><p><strong>默认</strong></p> </th>
   <th><p><strong>可接受值</strong></p> </th>
  </tr>
  <tr>
   <td><p>缩进</p> </td>
   <td>模块缩进<p> </p> </td>
   <td><p>12.7mm</p> </td>
   <td><p>任意数字</p> </td>
  </tr>
  <tr>
   <td>数字最小宽度</td>
   <td>使用罗马数字以外的编号列表时，应用于项目符号/编号字段的最小宽度</td>
   <td>8.0mm</td>
   <td>任意数字</td>
  </tr>
  <tr>
   <td><p>罗马数字最小宽度</p> </td>
   <td><p>使用罗马数字时要应用于项目符号/数字字段的最小宽度</p> </td>
   <td><p>12.7mm</p> </td>
   <td><p>任意数字</p> </td>
  </tr>
  <tr>
   <td>节目类型</td>
   <td>“创建通信”应用程序用于呈现信件预览的演绎版类型。 </td>
   <td>HTML演绎版</td>
   <td>HTML呈现版本/PDF呈现版本</td>
  </tr>
  <tr>
   <td><p>启用CCRPDF高亮显示</p> </td>
   <td><p>在“创建通信”应用程序中启用对PDF的突出显示</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>目标高亮类型</p> </td>
   <td><p>创建通信应用程序中的目标高亮类型</p> </td>
   <td><p>边框</p> </td>
   <td><p>边框/填充/无</p> </td>
  </tr>
  <tr>
   <td><p>目标高亮颜色</p> </td>
   <td><p>创建通信应用程序中的目标高亮颜色</p> </td>
   <td><p>90;155;245</p> </td>
   <td><p>R；G；B格式的任意RGB</p> </td>
  </tr>
  <tr>
   <td><p>内容高亮类型</p> </td>
   <td><p>创建通信应用程序中的内容高亮类型</p> </td>
   <td><p>填充</p> </td>
   <td><p>边框/填充/无</p> </td>
  </tr>
  <tr>
   <td><p>内容高亮颜色</p> </td>
   <td><p>创建通信应用程序中的内容高亮颜色</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>R；G；B格式的任意RGB</p> </td>
  </tr>
  <tr>
   <td><p>字段高亮类型</p> </td>
   <td><p>创建通信应用程序中的字段高亮类型</p> </td>
   <td><p>填充</p> </td>
   <td><p>边框/填充/无</p> </td>
  </tr>
  <tr>
   <td><p>字段高亮颜色</p> </td>
   <td><p>创建通信应用程序中的字段高亮颜色</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>R；G；B格式的任意RGB</p> </td>
  </tr>
  <tr>
   <td><p>应用程序超时</p> </td>
   <td><p>应用程序超时（以秒为单位）</p> </td>
   <td><p>1200</p> </td>
   <td><p>任意数字</p> </td>
  </tr>
  <tr>
   <td><p>文档参数名称PDF</p> </td>
   <td><p>后处理中PDF文档的参数名称</p> </td>
   <td><p>inPDFDoc</p> </td>
   <td><p>任何字符串变量名称</p> </td>
  </tr>
  <tr>
   <td><p>XML数据参数名称</p> </td>
   <td><p>后处理中的XML文档（数据）的参数名称</p> </td>
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
   <td><p>从后处理发送的重定向URL的参数名称此值可以是任何字符串变量名称</p> </td>
   <td><p>redirecturl</p> </td>
   <td><p>任何字符串变量名称</p> </td>
  </tr>
  <tr>
   <td><p>PDF提交类型</p> </td>
   <td><p>PDF提交类型(从“创建通信”应用产品提交时生成的PDF类型)</p> </td>
   <td><p>非交互式</p> </td>
   <td><p>交互式/非交互式</p> </td>
  </tr>
  <tr>
   <td><p>优化数据字典实例</p> </td>
   <td><p>支持数据字典实例b/w服务器和客户端的优化传输</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>自动更正不一致 </p> </td>
   <td><p>启用后，它会自动处理信件分配中可能出现的不一致情况</p> </td>
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
   <td><p>指定数据的区域设置特定显示格式</p> </td>
   <td><p>locale=en_US； dateFormat=dd-MM-yyyy； numberDecimalSeparator=.； numberGroupSeparator=，； numberUseGroupSeparator=truelocale=de_DE； dateFormat=dd-MM-yyyy； numberDecimalSeparator=，； numberGroupSeparator=.； numberUseGroupSeparator=truelocale=fr_FR； dateFormat=dd-MM-yyyy； numberDecimalSeparator=，； numberGroupSeparator= ； numberUseGroupSeparator=truelocale=ja_JP； dateFormat=dd-MM-yyy； numberDecimalSeparator=。； numberGroupSeparator=，； numberUseGroupSeparator=true</p> </td>
   <td><p>—</p> </td>
  </tr>
  <tr>
   <td><p>数据编辑格式</p> </td>
   <td><p>编辑数据格式。 当将数据写入字符串或从字符串中解析数据时，将使用此选项</p> </td>
   <td><p>locale=en_US； dateFormat=dd-MM-yyyy； numberDecimalSeparator=.； numberGroupSeparator=，； numberUseGroupSeparator=true</p> </td>
   <td>--<p> </p> </td>
  </tr>
  <tr>
   <td><p>管理发布时的书信实例</p> </td>
   <td><p>启用/禁用管理书信功能（仅适用于发布服务器）</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>启用审核</p> </td>
   <td><p>启用/禁用审核功能。 为false时，将禁用所有操作的审核日志</p> </td>
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
   <td><p>启用“创建审核”</p> </td>
   <td><p>启用/禁用用于创建资产的审核功能</p> </td>
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
   <td><p>启用/禁用用于资源还原的审核功能</p> </td>
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
   <td><p>启用/禁用用于保存书信草稿的审核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>启用提交审核</p> </td>
   <td><p>启用/禁用书信提交的审核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>启用电子邮件审核</p> </td>
   <td><p>启用/禁用电子邮件信件的审核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>启用打印审核</p> </td>
   <td><p>启用/禁用打印信件的审核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>启用自定义投放审核</p> </td>
   <td><p>启用/禁用自定义信件投放的审核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>附件文档参数名称</p> </td>
   <td><p>发送到发布流程的附件文档的参数名称</p> </td>
   <td><p>inAttachmentDocs</p> </td>
   <td><p>任何字符串变量名称</p> </td>
  </tr>
  <tr>
   <td><p>CM用户根目录</p> </td>
   <td><p>包含所有通信管理用户资产的文件夹的URL</p> </td>
   <td><p>--</p> </td>
   <td><p>有效的文件夹位置</p> </td>
  </tr>
  <tr>
   <td><p>书信缓存大小</p> </td>
   <td><p>指定缓存中保留的最大字母数。</p> <p>更改此值将导致清理 <code>in-memory</code> 缓存。</p> </td>
   <td><p>100</p> </td>
   <td><p>任何数值</p> </td>
  </tr>
  <tr>
   <td><p>启用书信缓存</p> </td>
   <td><p>启用/禁用信件缓存。</p> <p>更改此值将导致清理 <code>in-memory </code> 缓存。</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>数据元素排序</p> </td>
   <td><p>根据数据元素在Letter中的顺序，保持数据元素在创建通信界面中的排序</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>支持重新加载</p> </td>
   <td><p>启用/禁用在服务器端呈现的字母中的重新加载支持。</p> <p>禁用此项将提高信件渲染性能。</p> </td>
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
   <td>将书信实例保存在指定的处理作者上。</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>兼容性选项</td>
   <td>以逗号分隔的configname：configvalue格式的兼容性选项。</td>
   <td>acm.compatibilityOptions</td>
   <td> </td>
  </tr>
  <tr>
   <td><p>调试目录 </p> <p> </p> </td>
   <td>用于调试的文件系统文件夹位置。 如果目录没有 <code>exists</code>，将不会生成调试转储。</td>
   <td>acm.debugDirectory</td>
   <td> </td>
  </tr>
 </tbody>
</table>
