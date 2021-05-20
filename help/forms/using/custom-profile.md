---
title: 为HTML5表单创建自定义配置文件
seo-title: 为HTML5表单创建自定义配置文件
description: HTML5表单配置文件是Apache Sling中的资源节点。 它表示HTML5表单呈现服务的自定义版本。
seo-description: HTML5表单配置文件是Apache Sling中的资源节点。 它表示HTML5表单呈现服务的自定义版本。
uuid: b9938280-a92c-4dde-b465-04372db3ca8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 9cd22244-9aa6-4b5f-96cf-c9cb3d6f9c8a
feature: 移动设备表单
exl-id: cf86c810-c466-4894-acc2-d4faf49754cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---

# 为HTML5表单创建自定义配置文件{#creating-a-custom-profile-for-html-forms}

配置文件是[Apache Sling](https://sling.apache.org/)中的资源节点。 它表示HTML5表单演绎版服务的自定义版本。 您可以使用HTML5表单演绎版服务来自定义HTML5表单的外观、行为和交互。 JCR存储库的`/content`文件夹中存在配置文件节点。 您可以将节点直接放置在`/content`文件夹或`/content`文件夹的任何子文件夹下。

配置文件节点具有&#x200B;**sling:resourceSuperType**&#x200B;属性，默认值为&#x200B;**xfaforms/profile**。 节点的渲染脚本位于/libs/xfaforms/profile。

Sling脚本是JSP脚本。 这些JSP脚本用作容器，用于将请求表单的HTML和所需的JS/CSS工件放在一起。 这些Sling脚本也称为&#x200B;**配置文件渲染器脚本**。 配置文件渲染器调用Forms OSGi服务来渲染请求的表单。

配置文件脚本位于html.jsp和html.POST.jsp中，用于GET和POST请求。 您可以复制和修改一个或多个文件以覆盖和添加您的自定义设置。 不要进行任何就地更改，修补程序更新将覆盖此类更改。

用户档案包含各种模块。 这些模块包括formRuntime.jsp、config.jsp、toolbar.jsp、formBody.jsp、nav_footer.jsp和footer.jsp。

## formRuntime.jsp {#formruntime-jsp-br}

formRuntime.jsp模块包含客户端库的引用。 它还描述了从请求中提取区域设置信息的方法，并在请求中包含本地化消息。 您可以在formRuntime.jsp中包含自己的customJavaScript库或样式。

## config.jsp {#config-jsp}

config.jsp模块包含各种配置，如日志记录、代理服务和行为版本。 您可以向config.jsp模块添加您自己的配置和小组件自定义。 您还可以将自定义小组件注册等配置添加到config.jsp模块。

## toolbar.jsp {#toolbar-jsp}

toolbar.jsp包含用于创建彩色工具栏的代码。 要删除工具栏，请从HTML.jsp中删除toolbar.jsp

## formBody.jsp {#formbody-jsp}

formBody.jsp模块用于XFA表单的HTML表示形式。

## nav_footer.jsp {#nav-footer-jsp}

起初，HTML5表单仅呈现表单的第一页。 当用户滚动表单时，将加载其余表单。 它可加快加载体验的速度。 nav_footer.jsp组件包含所有样式和所需元素，以便于在滚动时加载页面。

## footer.jsp {#footer-jsp}

footer.jsp模块为空。 它允许您添加仅用于用户交互的脚本。

## 创建自定义配置文件{#creating-custom-profiles}

要创建自定义配置文件，请执行以下步骤：

### 创建配置文件节点{#create-profile-node}

1. 导航到位于URL的CRX DE界面：`https://'[server]:[port]'/crx/de` ，然后使用管理员凭据登录到界面。

1. 在左窗格中，导航到位置&#x200B;*/content/xfaforms/profiles*。

1. 复制默认节点，并将该节点粘贴到名称为&#x200B;*hrform*&#x200B;的不同文件夹(*/content/profiles*)中。

1. 选择新节点&#x200B;*hrform*，然后添加字符串属性：*sling:resourceType*，其值为：*hrform/demo*。

1. 单击工具栏菜单中的全部保存，以保存更改。

### 创建配置文件渲染器脚本{#create-the-profile-renderer-script}

创建自定义配置文件后，向此配置文件添加渲染信息。 在收到对新配置文件的请求时，CRX会验证要呈现的JSP页是否存在/apps文件夹。 在/apps文件夹中创建JSP页。

1. 在左窗格中，导航到`/apps`文件夹。
1. 右键单击`/apps`文件夹，然后选择创建名为&#x200B;**hrform**&#x200B;的文件夹。
1. 在&#x200B;**hrform**&#x200B;文件夹中，创建名为&#x200B;**demo**&#x200B;的文件夹。
1. 单击&#x200B;**Save All**&#x200B;按钮。
1. 导航到`/libs/xfaforms/profile/html.jsp`并复制节点&#x200B;**html.jsp**。
1. 将&#x200B;**html.jsp**&#x200B;节点粘贴到上面创建的同名&#x200B;**html.jsp**&#x200B;的`/apps/hrform/demo`文件夹中，然后单击&#x200B;**保存**。
1. 如果您有配置文件脚本的任何其他组件，请按照步骤1-6复制/apps/hrform/demo文件夹中的组件。

1. 要验证是否创建了配置文件，请打开URL `https://'[server]:[port]'/content/xfaforms/profiles/hrform.html`

要验证您的表单，请[将您的表单](/help/forms/using/get-xdp-pdf-documents-aem.md)从本地文件系统导入AEM Forms，并在AEM服务器创作实例上[预览表单](/help/forms/using/previewing-forms.md)。
