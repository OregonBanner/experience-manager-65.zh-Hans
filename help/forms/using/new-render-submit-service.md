---
title: 新渲染和提交服务
seo-title: New render and submit service
description: 在Workbench中定义渲染和提交服务，以根据从中访问XDP的设备将XDP表单渲染为HTML或PDF。
seo-description: Define render and submit services in Workbench to render XDP form as HTML or PDF depending on the device it is accessed from.
uuid: 7f8348a1-753c-4dab-87d5-4a4a301198dd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6a32d240-c6a6-4937-a31f-7a5ec3c60b1f
docset: aem65
exl-id: 46de0101-9607-4429-84c3-7c1f34d2da27
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---

# 新渲染和提交服务{#new-render-and-submit-service}

## 简介 {#introduction}

在Workbench中，当您定义 `AssignTask` 操作，请指定特定表单(XDP或PDF表单)。 此外，通过操作配置文件指定一组渲染和提交服务。

XDP可以呈现为PDF表单或HTML表单。 新功能包括：

* 作为HTML呈现和提交XDP表单
* 在桌面上以PDF身份呈现和提交XDP表单，并在移动设备(例如，iPad)上以HTML身份呈现和提交

### 新的HTMLForms服务 {#new-html-forms-service}

新的HTMLForms服务使用Forms中的新功能来支持将XDP表单渲染为HTML。 新的HTMLForms服务会公开以下方法：

```java
/*
 * Generates a URL (for the HTML Form) to be passed to client, given a TaskContext.
 * The output of this API is something like this - /lc/content/xfaforms/profiles/default.ws.html?ContentRoot=repository://Applications/MyApplication/MyFolder&template=MyForm.xdp
 * @param taskContext task context
 * @param profileName Forms servlet URL.
 * @return form URL string
 */
public String generateFormURL(TaskContext taskContext, String profileName);

/*
 * Render the XDP Form as HTML. Can be used directly for updating the runtimeMap in render.
 * It adds the following keys to the map -
 * hint:new html form = true
 * newHTMLFormURL = the URL returned after calling 'generateFormURL' API.
 * @param TaskContext taskContext
 * @param profileName Forms servlet URL.
 * @param runtimeMap runtime map<string,object> associated with form rendering.
 * return runtimeMap
 */
public Map<String, Object> renderHTMLForm (TaskContext taskContext, String profileName, Map<String,Object> runtimeMap);
```

有关移动设备表单配置文件的更多信息，请访问 [创建自定义用户档案](/help/forms/using/custom-profile.md).

## 新的HTML表单渲染和提交流程 {#new-html-form-render-amp-submit-processes}

对于每个“AssignTask”操作，使用表单指定渲染和提交进程。 这些进程由TaskManager调用 `renderForm`和 `submitForm`允许自定义处理的API。 新HTML表单的这些进程的语义：

### 渲染新的HTML表单 {#render-a-new-html-form}

呈现HTML的新进程与每个呈现进程一样，具有以下I/O参数 — 

输入 - `taskContext`

输出 - `runtimeMap`

输出 - `outFormDoc`

此方法可模拟以下对象的精确行为： `renderHTMLForm` NewHTMLFormsService的API。 它调用 `generateFormURL` 用于获取表单HTML演绎版URL的API。 然后，它使用以下一个或多个键值填充runtimeMap：

新建html表单= true

newHTMLFormURL =调用后返回的URL `generateFormURL` API。

### 提交新的HTML表单 {#submit-a-new-html-form}

提交新HTML表单的此流程适用于以下I/O参数 — 

输入 - `taskContext`

输出 - `runtimeMap`

输出 - `outputDocument`

该流程会设置 `outputDocument`到 `inputDocument`检索自 `taskContext`.

## 默认呈现或提交进程，以及操作配置文件 {#default-render-or-submit-processes-and-action-profiles}

利用默认呈现和提交服务，支持在桌面上呈现PDF，并在移动设备(iPad)上HTML。

### 默认渲染表单 {#default-render-form}

此过程可在多个平台上无缝呈现XDP表单。 进程从检索用户代理 `taskContext`，并使用数据调用进程来呈现HTML或PDF。

![default-render-form](assets/default-render-form.png)

### 默认提交表单 {#default-submit-form}

此过程可在多个平台上无缝提交XDP表单。 它会从中检索用户代理 `taskContext`并使用数据调用流程以提交HTML或PDF。

![default-submit-form](assets/default-submit-form.png)

## 将移动表单的渲染从PDF切换到HTML {#switch-the-rendering-of-mobile-forms-from-pdf-to-html}

浏览器正在逐渐撤销对基于NPAPI的插件的支持，包括适用于Adobe Acrobat和Adobe Acrobat Reader的插件。 您可以使用以下步骤将移动表单的渲染从PDF更改为HTML：

1. 以有效用户的身份登录Workbench。
1. 选择 **文件** > **获取应用程序**.

   将出现“获取应用程序”对话框。

1. 选择要更改其移动设备表单渲染的应用程序，然后单击 **确定**.
1. 打开要更改渲染的进程。
1. 打开目标起点/任务，导航到“演示文稿和数据”部分，然后单击 **管理操作配置文件**.

   此时将显示“管理操作配置文件”对话框。
1. 将默认渲染配置文件配置从PDF更改为HTML，然后单击 **确定**.
1. 在流程中签入。
1. 重复这些步骤以更改其他进程的渲染。
1. 部署与已更改的进程相关的应用程序。

### 默认操作配置文件 {#default-action-profile}

默认操作配置文件将XDP表单渲染为PDF。 此行为现在已更改为使用默认渲染表单和默认提交表单进程。

有关操作配置文件的一些常见问题如下所示：

![gen_question_b_20](assets/gen_question_b_20.png) **哪些渲染/提交流程将开箱即用？**

* 渲染指南（指南已弃用）
* 渲染表单指南
* 呈现PDF表单
* 呈现HTML表单
* 呈现新HTML表单（新）
* 默认渲染表单（新）

等同于提交流程。

![gen_question_b_20](assets/gen_question_b_20.png) **哪些操作配置文件将开箱即用？**

对于XDP Forms：

* 默认（使用新的“默认呈现/提交”进程呈现/提交）

![gen_question_b_20](assets/gen_question_b_20.png) **要使表单在设备上以HTML呈现，以及在桌面上PDF呈现，流程设计者需要执行哪些操作？**

没什么。 默认的“操作配置文件”是自动选择的，渲染模式也是自动处理的。

![gen_question_b_20](assets/gen_question_b_20.png) **要使表单在桌面上HTML呈现，需要执行哪些操作？**

用户必须为默认配置文件选择“HTML”单选按钮。

![gen_question_b_20](assets/gen_question_b_20.png) **更改默认操作配置文件行为是否会产生任何升级影响？**

会，由于与默认操作配置文件关联的上次渲染和提交服务不同，因此这些服务被视为现有表单的自定义。 单击 **恢复默认值**，则改为设置默认渲染和提交服务。

如果您修改了现有的渲染或提交PDF表单服务或创建了自定义服务（例如，custom1），现在希望将相同的功能用于HTML呈现。 您需要复制新的渲染或提交服务（如custom2）并将类似的自定义应用于这些服务。 现在，修改XDP的操作配置文件以开始使用custom2服务，而不是渲染或提交的custom1。

要使表单在设备上以HTML呈现，以及在桌面上PDF呈现，流程设计者需要执行哪些操作？
要使表单在设备上以HTML呈现，以及在桌面上PDF呈现，流程设计者需要执行哪些操作？
