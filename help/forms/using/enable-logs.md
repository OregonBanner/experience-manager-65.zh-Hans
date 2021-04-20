---
title: 启用HTML5表单日志记录
seo-title: 启用HTML5表单日志记录
description: 记录器实用程序支持对表单进行记录，并帮助您调试与表单相关的问题。
seo-description: 记录器实用程序支持对表单进行记录，并帮助您调试与表单相关的问题。
uuid: 322306ba-8ad7-463d-8a9d-4cea5a0c4b55
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 973806f8-fb44-4d52-ad3f-bfbf335f60a1
docset: aem65
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 6%

---


# 为HTML5表单启用日志记录{#enable-logging-for-html-forms}

可以将记录器实用程序配置为开始为HTML5表单创建日志。 记录器实用程序具有各种级别，您可以根据需要设置一个级别。 HTML5表单包含服务器和客户端组件。 您可以为这两个组件配置日志。

## 配置服务器端日志{#configuring-server-side-logging}

请执行以下步骤以配置服务器端日志：

1. 转到 `https://'[server]:[port]'/system/console/configMgr`. 找到并打开&#x200B;*Apace Sling日志记录记录器配置*&#x200B;选项。 将出现一个对话框：

   ![ Apace Sling日志记录记录器配置选项对话框](assets/logconfig.png)

   Apace Sling日志记录记录器配置选项

1. 将&#x200B;**日志级别**&#x200B;更改为&#x200B;**调试**。

1. 指定&#x200B;**日志文件**&#x200B;的名称和路径。

   >[!NOTE]
   >
   >要在HTML5表单日志目录中生成日志，请在文件名前添加……/logs/。

1. 将&#x200B;**Logger**&#x200B;更改为&#x200B;**HTMLFormsPerfLogger**。 单击&#x200B;**保存**。

## 配置客户端日志记录{#configuring-client-logging}

可以使用以下方法在HTML5表单中启用客户端日志记录：

* 使用名为`log`的请求参数
* 使用CQ Configuration Manager

### 使用请求参数{#enabling-logging-using-request-parameter}启用日志记录

使用此方法，可以为特定请求生成日志。 请求参数的名称为“log”。 日志URL如下所示：

`https://<server>:<port>/content/xfaforms/profiles/test.html?contentRoot=<path of the folder containing form xdp>&template=<name of the xdp>&log=<log configuration>.`

日志配置由日志级别和记录器类别组成。

#### 日志目标{#log-destination}

<table>
 <tbody>
  <tr>
   <th><strong>日志目标</strong></th>
   <th><strong>描述</strong></th>
  </tr>
  <tr>
   <td>1</td>
   <td>日志将定向到浏览器<strong>控制台</strong></td>
  </tr>
  <tr>
   <td>2</td>
   <td>日志在客户端的JavaScript对象中收集，并可以发布到<strong>Server</strong> </td>
  </tr>
  <tr>
   <td>3</td>
   <td>以上两个选项<br /> </td>
  </tr>
 </tbody>
</table>

#### 日志级别{#log-levels}

<table>
 <tbody>
  <tr>
   <th>日志级别</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>0</td>
   <td>关闭<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>3</td>
   <td>FATAL<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>2</td>
   <td>错误<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>3</td>
   <td>警告<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>4</td>
   <td>信息<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>5</td>
   <td>DEBUG<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>6</td>
   <td>TRACE<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>7</td>
   <td>全部<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

#### 记录器类别{#logger-categories}

<table>
 <tbody>
  <tr>
   <th>日志类别</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>某个 </td>
   <td>xfa（脚本引擎相关日志）</td>
  </tr>
  <tr>
   <td>b</td>
   <td>xfaView（与布局引擎相关的日志）<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>c</td>
   <td>xfaPerf（与性能相关的日志）<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

#### 日志配置{#log-configuration}

在日志URL中，日志配置查询字符串参数定义如下：

`{destination}-{a level}-{b level}-{c level}`

例如：

<table>
 <tbody>
  <tr>
   <th>日志配置</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>2-a4-b5-c6<br type="_moz" /> </td>
   <td>目标：服务器<br /> xfa级别：INFO<br /> xfaView级别：DEBUG<br /> xfaPerf级别：TRACE</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>每个日志类别a(xfa)、b(xfaView)和c(xfaPerf)的默认日志级别为2(ERROR)。 因此，对于日志配置：2-b6，不同类别的日志级别为：
>a(xfa):2（默认级别错误）
>b(xfaView):6(用户指定的TRACE)
>a(xfaPerf):2（默认级别错误）

### 使用Configuration Manager {#enabling-logging-using-configuration-manager}启用日志记录

如果使用Configuration Manager启用日志记录，则会为每个渲染请求生成日志，直到再次禁用日志记录。

1. 登录到`https://'[server]:[port]'/system/console/configMgr`的CQ Configuration Manager，然后使用管理员凭据登录。
1. 搜索并单击&#x200B;**移动Forms配置**。
1. 在“调试选项”文本框中，输入上一节所述的日志配置，例如&#x200B;**2-a4-b5-c6**

   ![表单配置](assets/forms_configuration.png)

   表单配置

## 正在上载日志{#uploading-logs}

如果目标设置为1，则所有客户端脚本日志消息都将定向到控制台。 如果管理员需要这些日志以及服务器日志，请将目标级别设置为2。 在此级别上，所有日志都收集在客户端的JS对象中，如果表单以默认用户档案呈现，则工具栏中的&#x200B;**高亮显示现有字段**&#x200B;按钮左侧将显示&#x200B;**发送日志**&#x200B;按钮。 当用户单击该链接时，所有收集的日志都将发布到服务器，并记录在服务器上的已配置错误日志文件中。

默认情况下，所有信息都会添加到/crx-repository/logs/目录下的error.log文件。

要更改日志文件的位置和名称：

1. 以管理员身份登录到Configuration Manager。 Configuration Manager的默认URL为`https://'[server]:[port]'/system/console/configMgr`。
1. 单击&#x200B;**Apache Sling日志记录记录器配置**。 将显示一个对话框。

   ![logconfig-1](assets/logconfig-1.png)

1. 将&#x200B;**日志级别**&#x200B;更改为“调试”。

1. 指定&#x200B;**日志文件**&#x200B;的路径和名称。

   >[!NOTE]
   >
   >要在保存其他日志文件的同一目录中创建日志，请在“日志文件”属性中指定……/logs/&lt;filename>。

1. 将&#x200B;**Logger**&#x200B;更改为&#x200B;**HTMLFormsPerfLogger**&#x200B;并单击&#x200B;**保存**。
