---
title: 为HTML5表单创建自定义配置文件
description: HTML5表单配置文件是Apache Sling中的资源节点。 它表示HTML5表单渲染服务的自定义版本。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
feature: Mobile Forms
exl-id: cf86c810-c466-4894-acc2-d4faf49754cc
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# 为HTML5表单创建自定义配置文件 {#creating-a-custom-profile-for-html-forms}

配置文件是中的资源节点 [Apache Sling](https://sling.apache.org/). 它表示HTML5表单呈现服务的自定义版本。 您可以使用HTML5表单演绎版服务自定义HTML5表单的外观、行为和交互。 中存在配置文件节点 `/content` JCR存储库中的文件夹。 您可以将节点直接放在 `/content` 文件夹或其任何子文件夹 `/content` 文件夹。

配置文件节点具有 **sling：resourceSuperType** 属性，默认值为 **xfaforms/profile**. 节点的渲染脚本位于/libs/xfaforms/profile。

Sling脚本是JSP脚本。 这些JSP脚本用作容器，用于将所请求表单的HTML和所需的JS/CSS工件组合在一起。 这些Sling脚本也称为 **配置文件渲染器脚本**. 配置文件渲染器调用Forms OSGi服务来渲染请求的表单。

POST对于GET和POST请求，配置文件脚本位于html.jsp和html.request.jsp中。 您可以复制和修改一个或多个文件以覆盖和添加自定义项。 不进行任何就地更改，修补程序更新将覆盖此类更改。

配置文件包含各种模块。 这些模块包括formRuntime.jsp 、 config.jsp 、 toolbar.jsp 、 formBody.jsp 、 nav_footer.jsp和footer.jsp。

## formRuntime.jsp {#formruntime-jsp-br}

formRuntime.jsp模块包含客户端库的引用。 它还描述了从请求中提取区域设置信息并在请求中包含本地化消息的方法。 您可以在formRuntime.jsp中包含自己的customJavaScript库或样式。

## config.jsp {#config-jsp}

config.jsp模块包含各种配置，如日志记录、代理服务和行为版本。 您可以将自己的配置和构件定制添加到config.jsp模块。 您还可以将自定义构件注册等配置添加到config.jsp模块。

## toolbar.jsp {#toolbar-jsp}

toolbar.jsp包含用于创建彩色工具栏的代码。 要删除工具栏，请从HTML.jsp中删除toolbar.jsp

## formBody.jsp {#formbody-jsp}

formBody.jsp模块用于XFA表单的HTML表示形式。

## nav_footer.jsp {#nav-footer-jsp}

最初，HTML5表单仅呈现表单的第一页。 当用户滚动表单时，则会加载其余表单。 这样可加快加载体验。 nav_footer.jsp组件包含所有样式和必需的元素，以便于在滚动时加载页面。

## footer.jsp {#footer-jsp}

footer.jsp模块为空。 它允许您添加仅用于用户交互的脚本。

## 创建自定义配置文件 {#creating-custom-profiles}

要创建自定义配置文件，请执行以下步骤：

### 创建配置文件节点 {#create-profile-node}

1. 导航到CRX DE接口，网址为： `https://'[server]:[port]'/crx/de` 并使用管理员凭据登录到界面。

1. 在左窗格中，导航到位置 */content/xfaforms/profiles*.

1. 复制节点默认值，并将节点粘贴到其他文件夹中(*/content/profiles*)，其名称为 *hrform*.

1. 选择新节点， *hrform*，并添加字符串属性： *sling：resourceType* 值： *hrform/demo*.

1. 单击工具栏菜单中的“全部保存”以保存更改。

### 创建配置文件渲染器脚本 {#create-the-profile-renderer-script}

创建自定义配置文件后，将渲染信息添加到此配置文件。 在收到对新配置文件的请求时，CRX会验证要呈现的JSP页面的/apps文件夹是否存在。 在/apps文件夹中创建JSP页。

1. 在左窗格中，导航到 `/apps` 文件夹。
1. 右键单击 `/apps` 文件夹并选择创建名为的文件夹 **hrform**.
1. 内部人员 **hrform** 文件夹创建名为的文件夹 **演示**.
1. 单击 **全部保存** 按钮。
1. 导航到 `/libs/xfaforms/profile/html.jsp` 并复制节点 **html.jsp**.
1. 粘贴 **html.jsp** 节点移入 `/apps/hrform/demo` 上面创建的具有相同名称的文件夹 **html.jsp** 并单击 **保存**.
1. 如果您有配置文件脚本的任何其他组件，请按照步骤1-6复制/apps/hrform/demo文件夹中的组件。

1. 要验证是否已创建配置文件，请打开URL `https://'[server]:[port]'/content/xfaforms/profiles/hrform.html`

要验证您的表单， [导入您的表单](/help/forms/using/get-xdp-pdf-documents-aem.md) 从本地文件系统到AEM Forms和 [预览表单](/help/forms/using/previewing-forms.md) 在AEM服务器创作实例上。
