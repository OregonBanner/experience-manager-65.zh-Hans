---
title: 生成XDP表单的HTML5预览
seo-title: Generate HTML5 preview of an XDP form
description: LiveCycle设计器中的“预览HTML”选项卡可用于预览显示在浏览器中的表单。
seo-description: Preview HTML tab in LiveCycle Designer can be used to preview forms as they appear in a browser.
uuid: cbee956f-bf2d-40c5-8e03-58fce0fa215b
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 34e6d1bc-4eca-42dc-9ae5-9a2107fbefce
docset: aem65
feature: Mobile Forms
exl-id: 548f302b-57f0-4bdc-8a99-1a4967caa32f
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 0%

---

# 生成XDP表单的HTML5预览{#generate-html-preview-of-an-xdp-form}

在AEM Forms Designer中设计表单时，除了预览表单的PDF呈现版本外，您还可以预览表单的HTML5呈现版本。 您可以使用 **预览HTML** 制表符以预览显示在浏览器中的表单。

## 在Designer中启用XDP表单的HTML预览 {#html-preview-of-forms-in-forms-designer}

要使Designer能够生成XDP表单的HTML预览，请执行以下配置：

* 配置Apache Sling身份验证服务
* 禁用保护模式
* 提供AEM Forms服务器的详细信息

### 配置Apache Sling身份验证服务 {#configure-apache-sling-authentication-service}

1. 转到 `https://'[server]:[port]'/system/console/configMgr` 在OSGi上运行的AEM Forms上或
   `https://'[server]:[port]'/lc/system/console/configMgr` 在JEE上运行的AEM Forms上。
1. 找到并单击 **Apache Sling身份验证服务** 配置，以在编辑模式下打开它。

1. 根据您运行的是OSGi还是JEE上的AEM Forms，在 **身份验证要求** 字段：

   * JEE上的AEM Forms

      * -/content/xfaforms
      * -/etc/clientlibs

   * OSGi上的AEM Forms

      * -/content/xfaforms
      * -/etc/clientlibs/fd/xfaforms

   >[!NOTE]
   >
   >请勿在“Authentication Requirements（身份验证要求）”字段中复制粘贴指定的值，因为它可能会损坏值中的特殊字符。 相反，请在字段中键入指定的值。

1. 在中指定用户名和密码 **[!UICONTROL 匿名用户名]** 和 **[!UICONTROL 匿名用户密码]** 字段。 指定的凭据用于处理匿名身份验证并允许访问匿名用户。
1. 单击 **保存** 以保存配置。

### 禁用保护模式 {#disable-protected-mode}

此 [保护模式](../../forms/using/get-xdp-pdf-documents-aem.md) 默认情况下为开启。 保持为生产环境启用。 您可以在开发环境中禁用它，以便在设计器中预览HTML5 Forms。 执行以下步骤可禁用它：

1. 以管理员身份登录到AEM Web Console。

   * OSGi上的AEM Forms URL为 `https://'[server]:[port]'/system/console/configMgr`
   * JEE上的AEM Forms URL为 `https://'[server]:[port]'/lc/system/console/configMgr`

1. 打开 **[!UICONTROL 移动Forms配置]** 进行编辑。
1. 取消选择 **[!UICONTROL 保护模式]** 选项并单击 **[!UICONTROL 保存]**.

### 提供AEM Forms服务器的详细信息 {#provide-details-of-aem-forms-server}

1. 在设计器中，转到 **工具** > **选项**.
1. 在“选项”窗口中，选择 **服务器选项** 页面，提供以下详细信息，然后单击 **确定**.

   * **服务器URL**：AEM Forms服务器URL。

   * **HTTP端口号**：AEM服务器端口。 默认值为 4502。
   * **HTML预览上下文：** 用于渲染XFA表单的配置文件的路径。 以下默认配置文件用于在Designer中预览表单。 但是，您还可以指定自定义配置文件的路径。

      * `/content/xfaforms/profiles/default.html` (OSGi上的AEM Forms)

      * `/lc/content/xfaforms/profiles/default.html` (AEM Forms在吉)

   * **Forms Manager上下文：** Forms Manager UI部署位置的上下文路径。 默认值为：

      * `/aem/forms` (OSGi上的AEM Forms)
      * `/lc/forms` (AEM Forms在吉)

   >[!NOTE]
   >
   >确保AEM Forms服务器已启动并正在运行。 HTML预览连接到CRX服务器 *生成* 预览。

   ![AEM Forms Designer选项 ](assets/server_options.png)

   AEM Forms Designer选项

1. 要以HTML预览表单，请单击 **预览HTML** 选项卡。

   >[!NOTE]
   >
   >
   >
   >
   >    * 如果“HTML预览”选项卡处于关闭状态，请按F4打开“预览HTML”选项卡。 您还可以从“视图”菜单中选择“预览HTML”以打开“预览HTML”选项卡。
   >    * HTML预览不支持PDF文档，HTML预览仅适用于XDP文档。
   >
   >

   >[!CAUTION]
   >
   >要测试真正的最终用户体验，还可以在外部浏览器(Google Chrome、Microsoft Edge、Mozilla Firefox等)中预览表单。 由于每个浏览器使用单独的引擎来呈现HTML，因此在设计器中的表单预览方式与外部浏览器中可能存在一些差异。

## 使用示例数据预览表单 {#to-preview-a-form-using-sample-data}

Designer允许您使用示例XML数据预览和测试表单。 建议您经常使用示例数据测试表单，以确保表单正确呈现。

如果没有示例数据，Designer可以创建它，也可以自己创建它。 (请参阅 [自动生成示例数据以预览表单](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7efe.2) 和 [创建示例数据以预览表单](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7eff.2).)

使用示例数据源测试表单可确保映射数据和字段，并确保重复的子表单按预期重复。 您可以创建一个平衡的表单布局，为每个对象提供适当的空间以显示合并的数据。

1. 选择 **文件>表单属性**.

1. 单击 **预览** 选项卡，并在数据文件框中键入测试数据文件的完整路径。 您还可以使用“浏览”按钮导航到文件。

1. 单击&#x200B;**确定**。下次在 **预览HTML** 选项卡，示例XML文件中的数据值将显示在相应的对象中。

## 在存储库中预览表单 {#html-preview-of-forms-in-forms-manager}

在AEM Forms中，您可以预览存储库中的表单和文档。 预览有助于了解最终用户使用表单时的具体外观和行为。
