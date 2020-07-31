---
title: 调试HTML5表单
seo-title: 调试HTML5表单
description: 文档列表步骤，用于诊断各种已知问题。
seo-description: 文档列表步骤，用于诊断各种已知问题。
uuid: df1835aa-6033-4ecb-97c8-4c3b7b96b943
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5260d981-da40-40ab-834e-88e091840813
translation-type: tm+mt
source-git-commit: 998a127ce00c6cbb3db3a81d8a89d97ab9ef7469
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 0%

---


# 调试HTML5表单 {#debugging-html-forms}

此文档包括若干故障排除方案。 对于每种情况，都会提供一些步骤来解决问题。 按照以下步骤操作，如果问题仍然存在，请配置记录器以获取并查看日志中的错误／警告。 有关HTML5表单日志记录的更多详细信息，请 [参阅为HTML5表单生成日志](/help/forms/using/enable-logs.md)。

## 问题： 呈现表单时，我会看到org.apache.sling.api.SlingException异常页 {#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page}

在异常详细信息中，搜索由 **引起的词**。

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
   <td>模板和关联资源所在的路径</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>与模板合并的数据文件的绝对路径。<br /> 注意： 路径定义数据文件的绝对路径。</td>
  </tr>
  <tr>
   <td>数据</td>
   <td>与模板合并的UTF-8编码数据字节。</td>
  </tr>
 </tbody>
</table>

## 问题： 无法呈现表单（显示错误消息） {#problem-unable-to-render-form}

1. 确保指定的参数正确。 有关参数的详细信息，请参阅 [渲染参数](#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page)。
1. 登录到CRX包管理器(位于https://&lt;server>:&lt;port>/crx/packmgr/index.jsp)并检查以下包是否已正确安装：

   * adobe-lc-forms-content-pkg-&lt;version>.zip
   * adobe-lc-forms-runtime-pkg-&lt;version>.zip

1. 登录到CQ Web控制台(Felix Console)，网址为https://&lt;server>:&lt;port>/system/console/bundles。

   确保以下捆绑包的状态为“活动”:

   * scala-lang.bundle [osgi]

   (com.adobe.livecyclescala-lang.bundle)

   * AdobeXFAForms渲染器

   (com.adobe.livecycle.adobe-lc-forms-core)

   * AdobeXFAFormsLC连接器

   (com.adobe.livecycle.adobe-lc-forms-lc-connector)

## 问题： 无样式的表单渲染 {#problem-form-renders-without-styles}

1. 在您的浏览器中，打开“开 **发人员工具**”。 确保用户档案.css可用。
1. 如果用户档案.css文件不可用，请登录https://&lt;server>:&lt;port>/crx/de的CRX DE。
1. 在左侧的文件夹层次结构中，导航到/etc/clientlibs/fd/xfaforms/。 打开文件夹中列出的css.txt文件。

   * 配置文件
   * 运行时
   * 滚动导航
   * 工具栏
   * xfalib

1. 验证css.txt中提及的文件是否在CRX DElite中，地址为/libs/fd/xfaforms/clientlibs/xfalib/css。

   ```css
   #base=css
   application.css
   dialog.css
   datepicker.css
   scribble.css
   listboxwidget.css
   ```

1. 如果上述文件不可用，请再次安装adobe-lc-forms-runtime-pkg-&lt;version>.zip包。

### 问题： 遇到意外错误 {#problem-unexpected-error-encountered}

1. 在表单URL中，添加一个查询参数debugClientLibs并将其值设置为true(例如： https://&lt;server>:&lt;port>/content/xfaforms/profiles/test.html?contentRoot=&lt;some path>&amp;template=&lt;xdp文件的名称>&amp;log=1-a9-b9-c9&amp;debugClientLibs=true)
1. 在桌面浏览器（如chrome）中，转至“开发人员工具”->“控制台”。
1. 打开日志以标识错误类型。 有关日志的详细信息，请参 [阅HTML5表单的日志](/help/forms/using/enable-logs.md)。
1. 转到“开发人员工具”->“控制台”。 使用堆栈跟踪查找导致错误的代码。 调试错误以解决问题。

   >[!NOTE]
   >
   >如果脚本编写失败，请检查表单的PDF再现过程中是否也出现同样的问题。 如果是，则表单脚本逻辑有问题。

## 问题： 无法提交表单 {#problem-unable-to-submit-the-form}

1. 确保您有权访问AEM服务器，并且已连接到服务器。
1. 检查参数submitUrl是否正确。
1. 使用调试选项(1-a5- [b5-c5)为HTML](/help/forms/using/enable-logs.md) 5表单启 **用日志中所述的客户端日志**。 然后渲染表单并单击“提交”。 打开浏览器调试控制台并检查是否有错误。
1. 找到HTML5表单的日志 [中所述的服务器日志](/help/forms/using/enable-logs.md)。 检查提交期间服务器日志中是否有错误。

## 问题： 不显示本地化的错误消息 {#problem-localized-error-messages-do-not-display}

1. 在桌面浏览器中用其 **他查询参数debugClientLibs** =true渲染表单，然后转到“开发人员工具”->“资源”并检查文件I18N.css。
1. 如果文件不可用，请登录CRX DE，网址为https://&lt;server>:&lt;port>/crx/de。
1. 在左侧的文件夹层次结构中，导航到/libs/fd/xfaforms/clientlibs/I18N并确保存在以下文件和文件夹：

   * Namespace.js
   * LogMessages.js
   * 语言文件夹

1. 如果以上任何文件或文件夹不存在，请 **再次安装adobe-lc-forms-runtime-pkg-&lt;version>.zip** 包。
1. 导航到与区域设置名称同名的文件夹并检查其内容。 该文件夹必须包含以下文件：

   * I18N.js
   * js.txt

1. 检查js.txt的内容，并确保它包含以下条目。

   ```javascript
   ../Namespace.js
   I18N.js
   ../LogMessages.js
   ```

## 问题： 图像未显示 {#problem-image-not-showing-up}

1. 确保图像URL正确。
1. 检查您的浏览器是否支持此类图像。
1. 在异常详细信息中，搜索由 **引起的词**。

   可能的原因是URL中的一个或多个参数不正确。

   检查以下参数：
步骤文本

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
   <td>模板和关联资源所在的路径</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>与模板合并的数据文件的绝对路径。<br /> 注意： 路径定义数据文件的绝对路径。</td>
  </tr>
  <tr>
   <td>数据</td>
   <td>与模板合并的UTF-8编码数据字节。</td>
  </tr>
 </tbody>
</table>

1. 在桌面浏览器中，转到“开发人员工具”->“资源”。

   如果显示该图像，请在“帧”中检查左侧。
