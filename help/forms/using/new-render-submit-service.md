---
title: 新的呈现和提交服务
seo-title: 新的呈现和提交服务
description: 在Workbench中定义渲染和提交服务，以根据从中访问XDP表单的设备，将XDP表单渲染为HTML或PDF。
seo-description: 在Workbench中定义渲染和提交服务，以根据从中访问XDP表单的设备，将XDP表单渲染为HTML或PDF。
uuid: 7f8348a1-753c-4dab-87d5-4a4a301198dd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6a32d240-c6a6-4937-a31f-7a5ec3c60b1f
docset: aem65
exl-id: 46de0101-9607-4429-84c3-7c1f34d2da27
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 0%

---

# 新的呈现和提交服务{#new-render-and-submit-service}

## 简介 {#introduction}

在Workbench中，定义`AssignTask`操作时，请指定特定表单（XDP或PDF表单）。 此外，还可以通过操作配置文件指定一组渲染和提交服务。

XDP可以呈现为PDF表单或HTML表单。 新功能包括：

* 呈现XDP表单并将其提交为HTML
* 在桌面上以PDF格式呈现和提交XDP表单，在移动设备（例如iPad）上以HTML格式呈现和提交XDP表单

### 新的HTML Forms服务{#new-html-forms-service}

新的HTML Forms服务利用Forms中的新功能支持将XDP表单渲染为HTML。 新的HTML Forms服务公开了以下方法：

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

有关移动设备表单配置文件的更多信息，请访问[创建自定义配置文件](/help/forms/using/custom-profile.md)。

## 新的HTML表单渲染和提交进程{#new-html-form-render-amp-submit-processes}

对于每个“AssignTask”操作，使用表单指定“渲染”和“提交”进程。 TaskManager `renderForm`和`submitForm`API会调用这些进程，以允许自定义处理。 新HTML表单的这些进程的语义：

### 渲染新的HTML表单{#render-a-new-html-form}

与每个渲染过程一样，渲染HTML的新过程具有以下I/O参数 — 

输入 - `taskContext`

输出 - `runtimeMap`

输出 - `outFormDoc`

此方法模拟NewHTMLFormsService的`renderHTMLForm` API的确切行为。 它会调用`generateFormURL` API以获取表单HTML呈现版本的URL。 然后，它会使用以下键或值填充runtimeMap:

新建html表单= true

newHTMLFormURL =调用`generateFormURL` API后返回的URL。

### 提交新的HTML表单{#submit-a-new-html-form}

提交新HTML表单的流程可与以下I/O参数配合使用 — 

输入 - `taskContext`

输出 - `runtimeMap`

输出 - `outputDocument`

该进程将`outputDocument`设置为从`taskContext`检索到的`inputDocument`。

## 默认呈现或提交进程和操作配置文件{#default-render-or-submit-processes-and-action-profiles}

默认的渲染和提交服务支持在桌面上渲染PDF，在移动设备(iPad)上渲染HTML。

### 默认渲染表单{#default-render-form}

此过程可无缝地在多个平台上渲染XDP表单。 进程从`taskContext`中检索用户代理，并使用数据调用进程以呈现HTML或PDF。

![default-render-form](assets/default-render-form.png)

### 默认提交表单{#default-submit-form}

此过程可在多个平台上无缝提交XDP表单。 它会从`taskContext`中检索用户代理，并使用数据调用进程以提交HTML或PDF。

![default-submit-form](assets/default-submit-form.png)

## 将移动表单的呈现从PDF切换为HTML {#switch-the-rendering-of-mobile-forms-from-pdf-to-html}

浏览器正逐步取消对基于NPAPI的插件的支持，包括适用于Adobe Acrobat和Adobe AcrobatReader的插件。 您可以按照以下步骤将移动表单的呈现从PDF更改为HTML:

1. 以有效用户身份登录Workbench。
1. 选择&#x200B;**文件** > **获取应用程序**。

   将显示“获取应用程序”对话框。

1. 选择要更改其移动表单呈现的应用程序，然后单击&#x200B;**确定**。
1. 打开要更改其渲染的进程。
1. 打开目标起点/任务，导航到Presentation &amp; Data部分，然后单击&#x200B;**Manage Action Profiles**。

   此时将显示管理操作配置文件对话框。
1. 将默认渲染配置文件配置从PDF更改为HTML，然后单击&#x200B;**OK**。
1. 检查进程。
1. 重复这些步骤以更改其他进程的呈现。
1. 部署与您更改的流程相关的应用程序。

### 默认操作配置文件{#default-action-profile}

默认的“操作配置文件”将XDP表单渲染为PDF。 现在，此行为已更改为使用默认呈现表单和默认提交表单进程。

有关操作用户档案的一些常见问题解答如下：

![gen_question_b_20](assets/gen_question_b_20.png) **哪些渲染/提交进程可开箱即用？**

* 渲染指南（已弃用指南）
* Render Form指南
* 渲染PDF表单
* 呈现HTML表单
* 渲染新HTML表单（新）
* 默认渲染表单（新）

和等效的提交流程。

![gen_question_b_20](assets/gen_question_b_20.png) **哪些操作配置文件现成可用？**

对于XDP Forms:

* 默认（使用新的“默认渲染/提交”进程渲染/提交）

![gen_question_b_20](assets/gen_question_b_20.png) **流程设计器需要执行哪些操作才能使表单在设备上以HTML形式呈现，在桌面上以PDF形式呈现？**

没有。 默认的“操作配置文件”会自动选择，并且渲染模式也会自动进行处理。

![gen_question_b_20](assets/gen_question_b_20.png) **需要执行哪些操作才能在桌面上以HTML形式呈现表单？**

用户必须为默认配置文件选择HTML单选按钮。

![gen_question_b_20](assets/gen_question_b_20.png) **更改默认操作配置文件行为是否会有任何升级影响？**

是，由于之前与默认操作配置文件关联的渲染和提交服务不同，因此这些服务被视为现有表单的自定义服务。 单击&#x200B;**恢复默认值**&#x200B;后，将设置默认呈现和提交服务。

如果您已修改现有的“渲染”或“提交PDF表单”服务或创建了自定义服务（例如custom1），并且现在希望对HTML呈现使用相同的功能。 您需要复制新的呈现或提交服务（如custom2），并对这些服务应用类似的自定义设置。 现在，修改XDP的操作配置文件以开始使用custom2服务，而不是custom1来呈现或提交。

流程设计人员需要执行哪些操作才能使表单在设备上以HTML形式呈现，在桌面上以PDF形式呈现？
流程设计人员需要执行哪些操作才能使表单在设备上以HTML形式呈现，在桌面上以PDF形式呈现？
