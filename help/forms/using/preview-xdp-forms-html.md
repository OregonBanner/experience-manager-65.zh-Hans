---
title: 生成XDP表单的HTML5预览
seo-title: 生成XDP表单的HTML5预览
description: LiveCycle设计器中的“预览HTML”选项卡可用于预览在浏览器中显示的表单。
seo-description: LiveCycle设计器中的“预览HTML”选项卡可用于预览在浏览器中显示的表单。
uuid: cbee956f-bf2d-40c5-8e03-58fce0fa215b
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 34e6d1bc-4eca-42dc-9ae5-9a2107fbefce
docset: aem65
feature: 移动设备表单
exl-id: 548f302b-57f0-4bdc-8a99-1a4967caa32f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# 生成XDP表单的HTML5预览{#generate-html-preview-of-an-xdp-form}

在AEM Forms Designer中设计表单时，除了预览表单的PDF呈现版本外，您还可以预览表单的HTML5呈现版本。 您可以使用&#x200B;**预览HTML**&#x200B;选项卡预览在浏览器中显示的表单。

## 在Designer {#html-preview-of-forms-in-forms-designer}中为XDP表单启用HTML预览

要启用Designer以生成XDP表单的HTML预览，请执行以下配置：

* 配置Apache Sling身份验证服务
* 禁用保护模式
* 提供AEM Forms服务器的详细信息

### 配置Apache Sling身份验证服务{#configure-apache-sling-authentication-service}

1. 转到OSGi上运行的AEM Forms上的`https://'[server]:[port]'/system/console/configMgr`，或
   `https://'[server]:[port]'/lc/system/console/configMgr` 在JEE上运行的AEM Forms上。
1. 找到并单击&#x200B;**Apache Sling Authentication Service**&#x200B;配置，以在编辑模式下将其打开。

1. 根据您在OSGi或JEE上运行的是AEM Forms，在&#x200B;**Authentication Requirements**&#x200B;字段中添加以下内容：

   * AEM Forms on JEE

      * -/content/xfaforms
      * -/etc/clientlibs
   * AEM Forms on OSGi

      * -/content/xfaforms
      * -/etc/clientlibs/fd/xfaforms

   >[!NOTE]
   >
   >请勿在“身份验证要求”字段中复制并粘贴指定的值，因为该值可能会损坏值中的特殊字符。 而是在字段中键入指定的值。

1. 分别在&#x200B;**[!UICONTROL 匿名用户名]**&#x200B;和&#x200B;**[!UICONTROL 匿名用户密码]**&#x200B;字段中指定用户名和密码。 指定的凭据用于处理匿名身份验证并允许匿名用户访问。
1. 单击&#x200B;**Save**&#x200B;以保存配置。

### 禁用受保护模式{#disable-protected-mode}

默认情况下，[受保护模式](../../forms/using/get-xdp-pdf-documents-aem.md)处于开启状态。 保持为生产环境启用该功能。 您可以在开发环境中禁用它，以在设计中预览HTML5 Forms。 请执行以下步骤以禁用该功能：

1. 以管理员身份登录AEM Web Console。

   * OSGi上AEM Forms的URL为`https://'[server]:[port]'/system/console/configMgr`
   * JEE上AEM Forms的URL是`https://'[server]:[port]'/lc/system/console/configMgr`

1. 打开&#x200B;**[!UICONTROL 移动Forms配置]**&#x200B;进行编辑。
1. 取消选择&#x200B;**[!UICONTROL 保护模式]**&#x200B;选项，然后单击&#x200B;**[!UICONTROL 保存]**。

### 提供AEM Forms服务器{#provide-details-of-aem-forms-server}的详细信息

1. 在Designer中，转到&#x200B;**工具** > **选项**。
1. 在“选项”窗口中，选择&#x200B;**服务器选项**&#x200B;页，提供以下详细信息，然后单击&#x200B;**确定**。

   * **服务器URL**:AEM Forms服务器URL。

   * **HTTP端口号**:AEM服务器端口。默认值为 4502。
   * **HTML预览上下文：** 呈现XFA表单的配置文件路径。以下默认配置文件用于在Designer中预览表单。 但是，您还可以指定自定义配置文件的路径。

      * `/content/xfaforms/profiles/default.html` (OSGi上的AEM Forms)

      * `/lc/content/xfaforms/profiles/default.html` (JEE上的AEM Forms)
   * **Forms Manager上下文：** 部署Forms Manager UI的上下文路径。默认值为：

      * `/aem/forms` (OSGi上的AEM Forms)
      * `/lc/forms` (JEE上的AEM Forms)

   >[!NOTE]
   >
   >确保AEM Forms服务器已启动并正在运行。 HTML预览连接到CRX服务器以生成&#x200B;*预览。*

   ![AEM Forms Designer选项  ](assets/server_options.png)

   AEM Forms Designer选项

1. 要预览HTML格式的表单，请单击&#x200B;**预览HTML**&#x200B;选项卡。

   >[!NOTE]
   >
   >
   >
   >
   >    * 如果“HTML预览”选项卡已关闭，请按F4以打开“预览HTML”选项卡。 您还可以从“视图”菜单中选择“预览HTML”以打开“预览HTML”选项卡。
   >    * HTML预览不支持PDF文档，HTML预览仅适用于XDP文档。


   >[!CAUTION]
   >
   >要测试真正的最终用户体验，还可在外部浏览器（Google Chrome、Microsoft Edge、Mozilla Firefox等）中预览您的表单。 每个浏览器都使用单独的引擎来渲染HTML，因此在Designer和外部浏览器中预览表单的方式可能存在一些差异。

## 使用示例数据{#to-preview-a-form-using-sample-data}预览表单

Designer允许您使用示例XML数据预览和测试表单。 建议您经常使用示例数据测试表单，以确保表单正确呈现。

如果您没有示例数据，Designer可以创建它，也可以自己创建它。 （请参阅[自动生成示例数据以预览表单](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7efe.2)和[创建示例数据以预览表单](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7eff.2)。）

使用示例数据源测试表单可确保数据和字段已映射，并且重复子表单会按预期重复。 您可以创建平衡的表单布局，以便为每个对象提供适当的空间以显示合并的数据。

1. 选择&#x200B;**文件>表单属性**。

1. 单击&#x200B;**Preview**&#x200B;选项卡，然后在“数据文件”框中键入测试数据文件的完整路径。 您还可以使用“浏览”按钮导航到文件。

1. 单击&#x200B;**确定**。下次在&#x200B;**预览HTML**&#x200B;选项卡中预览表单时，示例XML文件中的数据值将显示在相应的对象中。

## 预览位于存储库{#html-preview-of-forms-in-forms-manager}中的表单

在AEM Forms中，您可以预览存储库中的表单和文档。 预览有助于准确了解表单的外观和行为方式，就像最终用户使用的一样。
