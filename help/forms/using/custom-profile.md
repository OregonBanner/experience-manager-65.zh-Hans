---
title: 为HTML5表单创建自定义用户档案
seo-title: 为HTML5表单创建自定义用户档案
description: HTML5表单用户档案是Apache Sling中的资源节点。 它表示HTML5表单渲染服务的自定义版本。
seo-description: HTML5表单用户档案是Apache Sling中的资源节点。 它表示HTML5表单渲染服务的自定义版本。
uuid: b9938280-a92c-4dde-b465-04372db3ca8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 9cd22244-9aa6-4b5f-96cf-c9cb3d6f9c8a
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 为HTML5表单创建自定义用户档案 {#creating-a-custom-profile-for-html-forms}

用户档案是 [Apache Sling中的资源节点](https://sling.apache.org/)。 它表示HTML5表单再现服务的自定义版本。 可以使用HTML5表单再现服务自定义HTML5表单的外观、行为和交互。 用户档案节点位于JCR存储库 `/content` 的文件夹中。 您可以将节点直接放在文件夹 `/content` 或该文件夹的任何子文件夹 `/content` 下。

用户档案节点具有 **sling:resourceSuperType** 属性，默认值为 **xfaforms/用户档案**。 节点的渲染脚本位于/libs/xfaforms/用户档案。

Sling脚本是JSP脚本。 这些JSP脚本用作容器，用于将请求表单的HTML和所需的JS/CSS对象组合在一起。 这些Sling脚本也称为 **用户档案渲染器脚本**。 用户档案渲染器调用Forms OSGi服务来渲染所请求的表单。

用户档案脚本为GET和POST请求的html.jsp和html.POST.jsp。 您可以复制和修改一个或多个文件以覆盖和添加您的自定义设置。 不要进行任何就地更改，修补程序更新会覆盖这些更改。

用户档案包含各种模块。 模块有formRuntime.jsp、config.jsp、toolbar.jsp、formBody.jsp、nav_footer.jsp和footer.jsp。

## formRuntime.jsp {#formruntime-jsp-br}

formRuntime.jsp模块包含客户端库的引用。 它还描述了从请求中提取区域设置信息的方法，并在请求中包含本地化的消息。 您可以在formRuntime.jsp中包含自己的自定义javascript库或样式。

## config.jsp {#config-jsp}

config.jsp模块包含各种配置，如日志记录、代理服务和行为版本。 您可以向config.jsp模块添加您自己的配置和构件自定义。 您还可以向config.jsp模块添加自定义构件注册等配置。

## 工具栏。jsp {#toolbar-jsp}

toolbar.jsp包含用于创建彩色工具栏的代码。 要删除工具栏，请从HTML.jsp中删除toolbar.jsp

## formBody.jsp {#formbody-jsp}

formBody.jsp模块用于XFA表单的HTML表示。

## nav_footer.jsp {#nav-footer-jsp}

最初，HTML5表单仅呈现表单的第一页。 当用户滚动表单时，将加载其余的表单。 它使加载体验更快。 nav_footer.jsp组件包含所有样式和必需元素，以便于在滚动时加载页面。

## footer.jsp {#footer-jsp}

footer.jsp模块为空。 它允许您添加仅用于用户交互的脚本。

## 创建自定义用户档案 {#creating-custom-profiles}

要创建自定义用户档案，请执行以下步骤：

### 创建用户档案节点 {#create-profile-node}

1. 导航到URL上的CRX DE界面：然后 `https://'[server]:[port]'/crx/de` 使用管理员凭据登录到界面。

1. 在左侧窗格中，导航到位 *置/content/xfaforms/用户档案*。

1. 复制节点默认值，并将该节点粘贴到名称为hrform的不&#x200B;*同文件夹(*/content/ *用户档案)中*。

1. 选择新节点 *hrform*，然后添加字符串属性： *sling:resourceType* with value:hrform/ *demo*。

1. 单击工具栏菜单中的全部保存以保存更改。

### 创建用户档案渲染器脚本 {#create-the-profile-renderer-script}

创建自定义用户档案后，向此用户档案添加渲染信息。 在收到对新用户档案的请求时，CRX将验证要呈现的JSP页是否存在/apps文件夹。 在/apps文件夹中创建JSP页。

1. 在左窗格中，导览至该文 `/apps` 件夹。
1. 右键单击该文件夹 `/apps` 并选择创建名为hrform的文 **件夹**。
1. 在hrform文件 **夹中** ，创建一个名为demo的 **文件夹**。
1. 单击“全 **部保存** ”按钮。
1. 导航到 `/libs/xfaforms/profile/html.jsp` 并复制节 **点html.jsp**。
1. 将 **html.jsp** 节点粘贴到以上创建的 `/apps/hrform/demo` 名称相同的html.jsp文件夹中，然 **后单击“保** 存” ****。
1. 如果您有任何其他用户档案脚本组件，请按照步骤1-6复制/apps/hrform/demo文件夹中的组件。

1. 要验证是否已创建用户档案，请打开URL `https://'[server]:[port]'/content/xfaforms/profiles/hrform.html`

要验证表单，请将 [表单从本地文件系统导入](/help/forms/using/get-xdp-pdf-documents-aem.md) AEM Forms，然后在AEM服务器作 [者实例上预览表单](/help/forms/using/previewing-forms.md) 。
