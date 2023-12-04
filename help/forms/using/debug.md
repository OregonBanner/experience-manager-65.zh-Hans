---
title: 调试HTML5表单
seo-title: Debugging HTML5 forms
description: 本文档列出了解决各种已知问题的步骤。
seo-description: The document list steps to troubleshoot various known issues.
uuid: df1835aa-6033-4ecb-97c8-4c3b7b96b943
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5260d981-da40-40ab-834e-88e091840813
feature: Mobile Forms
exl-id: 7330c03f-7102-43c0-aac6-825cce8a113d
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---

# 调试HTML5表单 {#debugging-html-forms}

本文档包含多个疑难解答场景。 对于每种情况，都提供了一些解决问题的步骤。 按照以下步骤操作，如果问题仍然存在，请配置日志记录器以获取并查看错误/警告日志。 有关HTML5表单日志记录的更多详细信息，请参阅 [为HTML5表单生成日志](/help/forms/using/enable-logs.md).

## 问题：在渲染表单时，我看到org.apache.sling.api.SlingException异常页面 {#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page}

在例外详细信息中，搜索word **引发者**.

可能的原因是URL中的一个或多个参数不正确。

检查以下参数：

<table>
 <tbody>
  <tr>
   <td><strong>参数</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>模板</td>
   <td>模板的文件名</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>模板和相关资源所在的路径</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>与模板合并的数据文件的绝对路径。<br /> 注意：路径定义数据文件的绝对路径。</td>
  </tr>
  <tr>
   <td>数据</td>
   <td>与模板合并的UTF-8编码数据字节。</td>
  </tr>
 </tbody>
</table>

## 问题：无法呈现表单（显示错误消息） {#problem-unable-to-render-form}

1. 请确保指定的参数正确。 有关参数的详细信息，请参阅 [渲染参数](#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page).
1. 登录到CRX包管理器(位于https://)&lt;server>：&lt;port>/crx/packmgr/index.jsp)，并检查是否正确安装了以下软件包：

   * adobe-lc-forms-content-pkg-&lt;version>.zip
   * adobe-lc-forms-runtime-pkg-&lt;version>.zip

1. 登录到CQ Web控制台（Felix控制台），网址为https://&lt;server>：&lt;port>/system/console/bundles.

   确保以下捆绑包的状态为“活动”：

   * scala-lang.bundle [osgi]

   (com.adobe.livecyclescala-lang.bundle)

   * AdobeXFA Forms渲染器

   (com.adobe.livecycle.adobe-lc-forms-core)

   * AdobeXFA Forms LC连接器

   (com.adobe.livecycle.adobe-lc-forms-lc-connector)

## 问题：表单渲染时没有样式 {#problem-form-renders-without-styles}

1. 在浏览器中，打开 **开发人员工具**. 确保profile.css可用。
1. 如果profile.css文件不可用，请登录CRX DE，网址为https://&lt;server>：&lt;port>/crx/de.
1. 在左侧的文件夹层次结构中，导航到/etc/clientlibs/fd/xfaforms/ 。 打开文件夹中列出的css.txt文件。

   * 侧面像
   * 运行时
   * scrollnav
   * 工具栏
   * xfalib

1. 验证css.txt中提到的文件是否存在于CRX DE Lite的/libs/fd/xfaforms/clientlibs/xfalib/css中。

   ```css
   #base=css
   application.css
   dialog.css
   datepicker.css
   scribble.css
   listboxwidget.css
   ```

1. 如果上述文件不可用，请安装adobe-lc-forms-runtime-pkg-&lt;version>.zip包。

### 问题：遇到意外错误 {#problem-unexpected-error-encountered}

1. 在表单URL中，添加查询参数debugClientLibs并将其值设置为true(例如：https://)&lt;server>：&lt;port>/content/xfaforms/profiles/test.html？contentRoot=&lt;some path=&quot;&quot;>模板(&amp;T)=&lt;name of=&quot;&quot; xdp=&quot;&quot; file=&quot;&quot;>&amp;log=1-a9-b9-c9&amp;debugClientLibs=true)
1. 在桌面浏览器（如Chrome）中，转到“开发人员工具”>“控制台”。
1. 打开日志以标识错误类型。 有关日志的详细信息，请参阅 [HTML5表单的日志](/help/forms/using/enable-logs.md).
1. 转到“开发人员工具”>“控制台”。 使用栈栈跟踪来查找导致错误的代码。 调试错误以解决问题。

   >[!NOTE]
   >
   >如果脚本编写失败，请检查在表单PDF呈现期间是否也出现同样的问题。 如果为“是”，则表明表单脚本逻辑存在问题。

## 问题：无法提交表单 {#problem-unable-to-submit-the-form}

1. 确保您有权访问AEM服务器，并且已连接到该服务器。
1. 检查参数submitUrl是否正确。
1. 启用客户端日志，如中所述 [HTML5表单的日志](/help/forms/using/enable-logs.md) 将调试选项用作 **1-a5-b5-c5**. 然后渲染表单并单击提交。 打开浏览器调试控制台并检查是否存在错误。
1. 找到服务器日志，如中所述 [HTML5表单的日志](/help/forms/using/enable-logs.md). 检查在提交期间服务器日志中是否有任何错误。

## 问题：本地化的错误消息不显示 {#problem-localized-error-messages-do-not-display}

1. 使用其他查询参数呈现表单 **debugClientLibs=true** 在桌面浏览器中，然后转到“开发人员工具”>“资源”并检查文件I18N.css。
1. 如果文件不可用，请在https://登录CRX DE&lt;server>：&lt;port>/crx/de.
1. 在左侧的文件夹层次结构中，导航到/libs/fd/xfaforms/clientlibs/I18N ，并确保存在以下文件和文件夹：

   * Namespace.js
   * LogMessages.js
   * 语言文件夹

1. 如果以上任何文件或文件夹不存在，请安装 **adobe-lc-forms-runtime-pkg-&lt;version>.zip** 再次打包。
1. 导航到与区域设置名称相同的文件夹，并检查其内容。 文件夹必须包含以下文件：

   * I18N.js
   * js.txt

1. 检查js.txt的内容，并确保它包含以下条目。

   ```javascript
   ../Namespace.js
   I18N.js
   ../LogMessages.js
   ```

## 问题：图像未显示 {#problem-image-not-showing-up}

1. 确保图像URL正确。
1. 检查浏览器是否支持此类型的图像。
1. 在例外详细信息中，搜索word **引发者**.

   可能的原因是URL中的一个或多个参数不正确。

   检查以下参数：步骤文本

<table>
 <tbody>
  <tr>
   <td><strong>参数</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>模板</td>
   <td>模板的文件名</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>模板和相关资源所在的路径</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>与模板合并的数据文件的绝对路径。<br /> 注意：路径定义数据文件的绝对路径。</td>
  </tr>
  <tr>
   <td>数据</td>
   <td>与模板合并的UTF-8编码数据字节。</td>
  </tr>
 </tbody>
</table>

1. 在桌面浏览器中，转到开发人员工具>资源。

   在“帧”中检查左侧的图像（如果该图像显示）。
