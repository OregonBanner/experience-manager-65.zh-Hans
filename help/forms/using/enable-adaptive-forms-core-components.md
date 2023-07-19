---
title: 如何在AEM 6.5 Forms上启用自适应Forms核心组件？
seo-title: How to enable Adaptive Forms Core Components on AEM 6.5 Forms?
description: 分步指南可帮助您在AEM 6.5 Forms环境中启用自适应Forms核心组件。
seo-description: Step-by-Step guide to help you enable Adaptive Forms Core Components on an AEM 6.5 Forms environment.
keywords: 启用核心组件、核心组件自适应Forms、6.5上的核心组件、AEM 6.5上的自适应Forms核心组件、AEM 6.5上的AF核心组件、AEM 6.5 Forms核心组件
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
source-git-commit: 1b97dc536550da8904bc7da09e983e0722c42a3d
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 21%

---


# 在AEM 6.5 Forms上启用自适应Forms核心组件 {#enable-adaptive-forms-core-components}

<span class="preview"> Adobe建议使用核心组件来 [将自适应Forms添加到AEM Sites页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 或 [创建独立的自适应Forms](/help/forms/using/create-an-adaptive-form-core-components.md). </span>

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | 本文 |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html) |

**适用于：** ✅用自适应表单核心组件❎自适应表单基础组件。

启用自适应Forms核心组件允许您开始创建、发布和交付 [基于核心组件的自适应Forms](create-an-adaptive-form-core-components.md) 和 [Headless自适应Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) 从AEM 6.5 Forms环境中。

要在AEM 6.5 Forms环境中启用HAdaptive Forms核心组件，请设置和部署 [AEM Archetype 41或更高版本](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 基于您的所有创作实例和发布实例上的项目（启用了表单选项）。

本文详细说明了如何在您的AEM 6.5 Forms环境中设置和部署基于AEM Archetype 41或更高版本的项目以启用Adaptive Forms核心组件。


## 前提条件 {#prerequisites}

在AEM 6.5 Forms环境中启用自适应Forms核心组件之前：

* [升级到AEM 6.5 Forms Service Pack 16 (6.5.16.0)或更高版本](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html).

* 安装最新版本的 [Apache Maven](https://maven.apache.org/download.cgi).

* 安装纯文本编辑器。 例如，Microsoft Visual Studio Code。

## 创建和部署最新的基于AEM原型的项目

创建AEM原型41或 [稍后](https://github.com/adobe/aem-project-archetype) 基于项目并将其部署到所有创作和发布实例：

1. 以管理员身份登录到您的计算机，托管并运行AEM 6.5 Forms实例。
1. 打开命令提示符或终端，然后运行以下命令以创建AEM Archetype项目（启用表单选项）：

   * Microsoft Windows

   ```Shell
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate ^
      -D archetypeGroupId=com.adobe.aem ^
      -D archetypeArtifactId=aem-project-archetype ^
      -D archetypeVersion=41 ^
      -D appTitle="My Form" ^
      -D appId="myform" ^
      -D groupId="com.myform" ^
      -D includeFormsenrollment="y" ^
      -D aemVersion="6.5.15" 
   ```

   * Linux或Apple macOS

   ```Shell
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate \
      -D archetypeGroupId=com.adobe.aem \
      -D archetypeArtifactId=aem-project-archetype \
      -D archetypeVersion=41 \
      -D appTitle="My Form" \
      -D appId="myform" \
      -D groupId="com.myform" \
      -D includeFormsenrollment="y" \
      -D aemVersion="6.5.15" 
   ```

   执行上述命令时，请务必考虑以下几点：

   * 不要更改的值 `aemVersion` 属性自 `6.5.15.0` 任何事都可以。

   * 设置 `archetypeVersion` 属性至 `41` 或更高版本。 有关最新版本，请参阅系统要求部分，位置在： [AEM项目原型](https://github.com/adobe/aem-project-archetype) 文档。

   * 更新命令以反映环境的特定值，包括 `appTitle`， `appId`、和 `groupId`. 此外，设置  `includeFormsenrollment` 属性至 `y`. 如果您使用Forms Portal，请设置 `includeExamples=y` 可在项目中包含Forms门户核心组件的选项。


1. （仅适用于基于Archetype版本41的项目）创建AEM Archetype项目后，请为基于核心组件的自适应Forms启用主题。 要启用主题：

   1. 打开 [AEM原型项目文件夹]/ui.apps/src/main/content/jcr_root/apps/__appId__/components/adaptiveForm/page/customheaderlibs.html进行编辑：

   1. 在第21行添加以下代码：

      ```XML
      <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
      data-sly-use.formstructparser="com.adobe.cq.forms.core.components.models.form.FormStructureParser"
      data-sly-test.themeClientLibRef="${formstructparser.themeClientLibRefFromFormContainer}">
      <sly data-sly-test="${themeClientLibRef}" data-sly-call="${clientlib.css @ categories=themeClientLibRef}"/>
      </sly>
      ```

      ![在第21行添加上述代码](/help/forms/using/assets/code-to-enable-themes.png)

   1. 保存并关闭该文件。

1. 更新项目以包含最新版本的Forms核心组件：

   1. 打开 [AEM原型项目文件夹]/pom.xml进行编辑。
   1. 设置版本 `core.forms.components.version` 和 `core.forms.components.af.version` 到 [最新Forms核心组件](https://github.com/adobe/aem-core-forms-components/tree/release/650) 版本。

   1. 保存并关闭该文件。


1. 成功创建AEM原型项目后，为您的环境构建部署包。 要生成包，请执行以下操作：

   1. 导航到AEM Archetype项目的根目录。

   1. 运行以下命令为您的环境构建AEM Archetype项目：

      ```Shell
      mvn clean install
      ```

      ![archetypebuild-success](/help/forms/using/assets/corecomponent-build-successful.png)


   成功构建AEM Archetype项目后，将生成AEM包。 您可以在以下位置找到该包： [AEM原型项目文件夹]\all\target\[appid].all-[version].zip

1. 使用 [包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en) 以部署 [AEM原型项目文件夹]\all\target\[appid].all-[version].zip包。

>[!NOTE]
>
>
>
> * 如果您在访问发布实例的登录对话框时遇到困难，要通过包管理器安装包，请尝试使用URL： `http://[Publish Server URL]:[PORT]/system/console` 以登录。 这允许您访问发布实例的登录页面，从而允许您继续安装过程。
> * 将原型项目部署到您的环境后，请勿将其删除或放弃。 将自定义的和新的自适应Forms核心组件主题添加到您的环境时，需要原型项目。

为您的环境启用了核心组件。 将基于空白核心组件的自适应表单模板和画布3.0主题部署到您的环境，使您能够 [创建基于核心组件的自适应Forms](create-an-adaptive-form-core-components.md).

## 常见问题解答

### 什么是核心组件？

[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)是一组用于 AEM 的标准化 Web 内容管理 (WCM) 组件，以缩短您网站的开发时间并降低维护成本。

### 在启用核心组件上添加了哪些功能？


为您的环境启用自适应表单核心组件时，将有一个空白的基于核心组件的自适应表单模板和 Canvas 3.0 主题添加到您的环境。为您的环境启用自适应表单核心组件后，您可以：

* 创建基于核心组件的自适应表单。
* 创建基于核心组件的自适应表单模板。
* 为基于核心组件的自适应表单模板创建自定义主题。
* 可以将基于核心组件的自适应表单的 JSON 表示形式提供给需要表单的 Headless 表示形式的移动、Web、原生应用程序和服务等渠道。

## 后续内容

* [创建基于核心组件的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)
* [创建自适应表单或将其添加到AEM Sites页面或体验片段](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [为基于核心组件的自适应Forms创建主题](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [为基于核心组件的自适应Forms创建模板](template-editor.md)