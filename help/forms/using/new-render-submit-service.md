---
title: 新的渲染和提交服务
seo-title: 新的渲染和提交服务
description: 在Workbench中定义渲染和提交服务，以根据从中访问XDP的设备，将XDP表单渲染为HTML或PDF。
seo-description: 在Workbench中定义渲染和提交服务，以根据从中访问XDP的设备，将XDP表单渲染为HTML或PDF。
uuid: 7f8348a1-753c-4dab-87d5-4a4a301198dd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6a32d240-c6a6-4937-a31f-7a5ec3c60b1f
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 新的渲染和提交服务{#new-render-and-submit-service}

## 简介 {#introduction}

在Workbench中，定义操作 `AssignTask` 时，请指定特定表单（XDP或PDF表单）。 此外，通过操作用户档案指定一组渲染和提交服务。

XDP可以呈现为PDF表单或HTML表单。 新功能包括：

* 渲染XDP表单并将其提交为HTML
* 在桌面上以PDF格式渲染和提交XDP表单，在移动设备上以HTML格式渲染和提交XDP表单（例如iPad）

### 新的HTML Forms服务 {#new-html-forms-service}

新的HTML Forms服务利用Forms中的新功能支持将XDP表单呈现为HTML。 新的HTML Forms服务提供以下方法：

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

有关移动表单用户档案的更多信息，请参 [阅创建自定义用户档案](/help/forms/using/custom-profile.md)。

## 新的HTML表单渲染和提交进程 {#new-html-form-render-amp-submit-processes}

对于每个“AssignTask”操作，都可以使用表单指定渲染和提交进程。 这些进程由TaskManager和API调 `renderForm`用以 `submitForm`允许自定义处理。 新HTML表单的这些进程的语义：

### 渲染新的HTML表单 {#render-a-new-html-form}

与每个渲染进程一样，渲染HTML的新进程具有以下I/O参数-

输入 - `taskContext`

输出 - `runtimeMap`

输出 - `outFormDoc`

此方法模拟NewHTMLFormsService的 `renderHTMLForm` API的确切行为。 它调用 `generateFormURL` API以获取表单的HTML再现的URL。 然后，它使用以下键或值填充runtimeMap:

新的html表单= true

newHTMLFormURL =调用API后返回的 `generateFormURL` URL。

### 提交新的HTML表单 {#submit-a-new-html-form}

提交新HTML表单的过程可与以下I/O参数配合使用-

输入 - `taskContext`

输出 - `runtimeMap`

输出 - `outputDocument`

进程将从 `outputDocument`中检 `inputDocument`索到 `taskContext`。

## 默认渲染或提交进程和操作用户档案 {#default-render-or-submit-processes-and-action-profiles}

默认的渲染和提交服务支持在桌面上渲染PDF，在移动设备(iPad)上渲染HTML。

### 默认渲染表单 {#default-render-form}

此过程在多个平台上无缝地呈现XDP表单。 进程从中检索用户代理 `taskContext`，并使用数据调用进程以渲染HTML或PDF。

![default-render-form](assets/default-render-form.png)

### 默认提交表单 {#default-submit-form}

此过程在多个平台上无缝提交XDP表单。 它从中检索用户代 `taskContext`理并使用数据调用进程以提交HTML或PDF。

![default-submit-form](assets/default-submit-form.png)

## 将移动表单的渲染从PDF切换为HTML {#switch-the-rendering-of-mobile-forms-from-pdf-to-html}

浏览器正在逐步取消对基于NPAPI的插件的支持，包括Adobe Acrobat和Adobe Acrobat Reader的插件。 您可以按照以下步骤将移动表单的渲染从PDF更改为HTML:

1. 以有效用户身份登录Workbench。
1. 选择“ **文件** ”>“获 **取应用程序**”。

   将显示“获取应用程序”对话框。

1. 选择要更改其移动表单渲染的应用程序，然后单击“确 **定”**。
1. 打开要更改其渲染的进程。
1. 打开目标起点/任务，导航到“演示和数据”部分，然后单击“管 **理操作用户档案”**。

   此时会显示“管理操作用户档案”对话框。
1. 将“默认渲染用户档案配置”从PDF更改为HTML，然后单击“ **确定**”。
1. 登记。
1. 重复这些步骤以更改其他进程的呈现。
1. 部署与您更改的进程相关的应用程序。

### 默认操作用户档案 {#default-action-profile}

默认的操作用户档案将XDP表单渲染为PDF。 此行为现已更改为使用默认渲染表单和默认提交表单进程。

有关操作用户档案的一些常见问题如下：

![gen_question_b_20](assets/gen_question_b_20.png) 什 **么渲染／提交进程将开箱即用？**

* 渲染指南（已弃用参考线）
* 渲染表单指南
* 渲染PDF表单
* 渲染HTML表单
* 渲染新的HTML表单（新）
* 默认渲染表单（新增）

同等的提交过程。

![gen_question_b_20](assets/gen_question_b_20.png) 开 **箱即用有哪些操作用户档案?**

对于XDP表单：

* 默认（使用新的“默认渲染／提交”进程渲染／提交）

![gen_question_b_20](assets/gen_question_b_20.png)**流程设计人员需要做什么才能使表单在设备上以HTML和桌面上的PDF格式呈现？**

没什么。 将自动选择默认的“操作用户档案”，渲染模式也会自动处理。

![gen_question_b_20](assets/gen_question_b_20.png) **What needs to be defost to enable the form to be rederined in HTML on a desktop?**

用户必须为默认用户档案选择HTML单选按钮。

![gen_question_b_20](assets/gen_question_b_20.png)**是否会对更改默认操作用户档案行为产生任何升级影响？**

是的，因为与默认操作用户档案关联的先前渲染和提交服务不同，所以这些服务被视为现有表单的自定义。 单击“恢 **复默认值**”后，将设置默认的渲染和提交服务。

如果您修改了现有的“渲染”或“提交PDF表单”服务或创建了自定义服务（例如custom1），并且现在想对HTML再现使用相同的功能。 您需要复制新的渲染或提交服务（如custom2），并对这些服务应用类似的自定义。 现在，将XDP的操作用户档案修改为使用custom2服务开始，而不是使用custom1来渲染或提交。

流程设计人员需要做什么才能使表单在设备上以HTML和桌面上的PDF格式呈现？
流程设计人员需要做什么才能使表单在设备上以HTML和桌面上的PDF格式呈现？
