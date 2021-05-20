---
title: 预填自适应表单字段
seo-title: 预填自适应表单字段
description: 使用现有数据预填自适应表单的字段。
seo-description: 使用自适应表单，用户可以使用其社交用户档案登录以表单预填基本信息。 本文介绍了如何完成此操作。
uuid: 574de83a-7b5b-4a1f-ad37-b9717e5c14f1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 7139a0e6-0e37-477c-9e0b-aa356991d040
docset: aem65
feature: 自适应表单
exl-id: 29cbc330-7b3d-457e-ba4a-7ce6091f3836
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2202'
ht-degree: 0%

---

# 预填自适应表单字段{#prefill-adaptive-form-fields}

## 简介 {#introduction}

您可以使用现有数据预填自适应表单的字段。 用户打开表单时，将预填这些字段的值。 要在自适应表单中预填充数据，请以符合自适应表单预填充数据结构的格式，将用户数据作为预填充XML/JSON提供。

## 预填充数据{#the-prefill-structure}的结构

自适应表单可以混合绑定和未绑定字段。 绑定字段是从“内容查找器”选项卡中拖动的字段，在字段编辑对话框中包含非空的`bindRef`属性值。 未绑定字段直接从Sidekick的组件浏览器中拖动，其值为空`bindRef`。

您可以预填自适应表单的绑定和未绑定字段。 预填充数据包含afBoundData和afUnBoundData部分，用于预填充自适应表单的绑定和未绑定字段。 `afBoundData`部分包含绑定字段和面板的预填充数据。 此数据必须与关联的表单模型架构兼容：

* 对于使用[XFA表单模板](../../forms/using/prepopulate-adaptive-form-fields.md)的自适应表单，请使用与XFA模板的数据架构兼容的预填充XML。
* 对于使用[XML架构](#xml-schema-af)的自适应表单，请使用与XML架构结构兼容的预填充XML。
* 对于使用[JSON架构](#json-schema-based-adaptive-forms)的自适应表单，请使用与JSON架构兼容的预填充JSON。
* 对于使用FDM架构的自适应表单，请使用与FDM架构兼容的预填充JSON。
* 对于[没有表单模型](#adaptive-form-with-no-form-model)的自适应表单，没有绑定数据。 每个字段都是未绑定的字段，并使用未绑定的XML预填充。

### 预填充XML结构示例{#sample-prefill-xml-structure}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<afData>
  <afBoundData>
     <employeeData>
        .
     </employeeData>
  </afBoundData>

  <afUnboundData>
    <data>
      <textbox>Hello World</textbox>
         .
         .
      <numericbox>12</numericbox>
         . 
         .              
    </data>
  </afUnboundData>
</afData>
```

### 预填充JSON结构{#sample-prefill-json-structure}示例

```javascript
{
   "afBoundData": {
      "employeeData": { }
   },
   "afUnboundData": {
      "data": {
         "textbox": "Hello World",
         "numericbox": "12"
      }
   }
}
```

对于具有相同绑定字段或具有相同名称的未绑定字段，将在XML标记或JSON对象中指定的数据填写在所有字段中。 例如，表单中的两个字段会映射到预填充数据中的名称`textbox`。 在运行时，如果第一个文本框字段包含“A”，则“A”会自动填充到第二个文本框中。 此链接称为自适应表单字段的实时链接。

### 使用XFA表单模板{#xfa-based-af}的自适应表单

基于XFA的自适应表单的预填充XML和提交的XML的结构如下：

* **预填充XML结构**:基于XFA的自适应表单的预填充XML必须与XFA表单模板的数据架构兼容。要预填充未绑定字段，请将预填充XML结构包装到`/afData/afBoundData`标记中。

* **提交的XML结构**:当不使用预填充XML时，提交的XML包含包装器标记中绑定和未绑定字段 `afData` 的数据。如果使用预填充XML，则提交的XML与预填充XML的结构相同。 如果预填充XML以`afData`根标记开头，则输出XML也具有相同的格式。 如果预填充XML没有`afData/afBoundData`包装器，而是直接从架构根标记（如`employeeData`）启动，则提交的XML也将以`employeeData`标记开头。

Prefill-Submit-Data-ContentPackage.zip

[获取包](assets/prefill-submit-data-contentpackage.zip)
含预填充数据和已提交数据的FileSample

### 基于XML架构的自适应表单  {#xml-schema-af}

基于XML架构的自适应表单预填充XML和提交XML的结构如下：

* **预填充XML结构**:预填充XML必须与关联的XML架构兼容。要预填充未绑定的字段，请将预填充XML结构包装到/afData/afBoundData标记中。
* **提交的XML结构**:如果未使用预填充XML，则提交的XML包含包装器标记中绑定和未绑定字段 `afData` 的数据。如果使用预填充XML，则提交的XML与预填充XML的结构相同。 如果预填充XML以`afData`根标记开头，则输出XML的格式相同。 如果预填充XML没有`afData/afBoundData`包装器，而是直接从架构根标记（如`employeeData`）启动，则提交的XML也将以`employeeData`标记开头。

```xml
<?xml version="1.0" encoding="utf-8" ?> 
<xs:schema targetNamespace="https://adobe.com/sample.xsd"
            xmlns="https://adobe.com/sample.xsd"
            xmlns:xs="https://www.w3.org/2001/XMLSchema">
 
    <xs:element name="sample" type="SampleType"/>
         
    <xs:complexType name="SampleType">
        <xs:sequence>
            <xs:element name="noOfProjectsAssigned" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:schema>
```

对于模型为XML架构的字段，数据将预填充在`afBoundData`标记中，如以下示例XML所示。 它可用于预填具有一个或多个未绑定文本字段的自适应表单。

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <textbox>Ignorance is bliss :) </textbox>
    </data>
  </afUnboundData>
  <afBoundData>
    <data>
      <noOfProjectsAssigned>twelve</noOfProjectsAssigned>
    </data>
  </afBoundData>
</afData>
```

>[!NOTE]
>
>建议不要在绑定面板（具有非空`bindRef`的面板，这些面板是通过从Sidekick或数据源选项卡中拖动组件而创建的）中使用未绑定字段。 这可能导致这些未绑定字段的数据丢失。 此外，建议各个表单中字段的名称是唯一的，特别是对于未绑定字段。

#### 没有afData和afBoundData包装器{#an-example-without-afdata-and-afbounddata-wrapper}的示例

```xml
<?xml version="1.0" encoding="UTF-8"?><config>
 <assignmentDetails descriptionOfAssignment="Some Science Project" durationOfAssignment="34" financeRelatedProject="1" name="Lisa" numberOfMentees="1"/>
 <assignmentDetails descriptionOfAssignment="Kidding, right?" durationOfAssignment="4" financeRelatedProject="1" name="House" numberOfMentees="3"/>
</config>
```

### 基于JSON模式的自适应表单{#json-schema-based-adaptive-forms}

对于基于JSON架构的自适应表单，预填充JSON和提交JSON的结构如下所述。 有关更多信息，请参阅[使用JSON模式创建自适应表单](../../forms/using/adaptive-form-json-schema-form-model.md)。

* **预填充JSON结构**:预填充JSON必须与关联的JSON架构兼容。或者，如果您还希望预填充未绑定字段，也可以将其封装到/afData/afBoundData对象中。
* **已提交的JSON结构**:如果未使用预填充JSON，则提交的JSON包含afData包装器标记中绑定和未绑定字段的数据。如果使用预填充JSON，则提交的JSON的结构与预填充JSON的结构相同。 如果预填充JSON以afData根对象开头，则输出JSON的格式相同。 如果预填充JSON没有afData/afBoundData包装器，而是直接从架构根对象（如用户）启动，则提交的JSON也将以用户对象开头。

```json
{
    "id": "https://some.site.somewhere/entry-schema#",
    "$schema": "https://json-schema.org/draft-04/schema#",
    "type": "object",
    "properties": {
        "address": {
            "type": "object",
            "properties": { 
    "name": {
     "type": "string"
    },
    "age": {
     "type": "integer"
}}}}}
```

对于使用JSON模式模型的字段，数据将预填充到afBoundData对象中，如以下示例JSON中所示。 它可用于预填具有一个或多个未绑定文本字段的自适应表单。 以下是包装器为`afData/afBoundData`的数据示例：

```json
{
  "afData": {
    "afUnboundData": {
      "data": { "textbox": "Ignorance is bliss :) " }
    },
    "afBoundData": {
      "data": { {
   "user": {
    "address": {
     "city": "Noida",
     "country": "India"
}}}}}}}
```

以下是不带`afData/afBoundData`包装器的示例：

```json
{
 "user": {
  "address": {
   "city": "Noida",
   "country": "India"
}}}
```

>[!NOTE]
>
>建议&#x200B;**不**&#x200B;在绑定面板中使用未绑定字段（通过从Sidekick或数据源选项卡拖动组件来创建的具有非空bindRef的面板），因为它可能导致未绑定字段的数据丢失。 建议在整个表单中具有唯一的字段名称，特别是对于未绑定的字段。

### 没有表单模型{#adaptive-form-with-no-form-model}的自适应表单

对于没有表单模型的自适应表单，所有字段的数据都位于`<afUnboundData> tag`的`<data>`标记下。

另外，请注意以下事项：

为各个字段提交的用户数据的XML标记使用字段名称生成。 因此，字段名称必须是唯一的。

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <radiobutton>2</radiobutton>
      <repeatable_panel_no_form_model>
        <numericbox>12</numericbox>
      </repeatable_panel_no_form_model>
      <repeatable_panel_no_form_model>
        <numericbox>21</numericbox>
      </repeatable_panel_no_form_model>
      <checkbox>2</checkbox>
      <textbox>Nopes</textbox>
    </data>
  </afUnboundData>
  <afBoundData/>
</afData>
```

## 使用Configuration Manager {#configuring-prefill-service-using-configuration-manager}配置预填充服务

要启用预填充服务，请在AEM Web控制台配置中指定默认预填充服务配置。 请按照以下步骤配置预填充服务：

>[!NOTE]
>
>预填充服务配置适用于自适应表单、HTML5表单和HTML5表单集。

1. 使用URL打开&#x200B;**[!UICONTROL Adobe Experience Manager Web控制台配置]**:\
   https://&lt;server>:&lt;port>/system/console/configMgr
1. 搜索并打开&#x200B;**[!UICONTROL 默认预填充服务配置]**。

   ![预填充配置](assets/prefill_config_new.png)

1. 为&#x200B;**数据文件位置**&#x200B;输入数据位置或正则表达式（正则表达式）。 有效数据文件位置的示例包括：

   * file:///C:/Users/public/Document/Prefill/。*
   * https://localhost:8000/somesamplexmlfile.xml
   >[!NOTE]
   >
   >默认情况下，允许通过所有类型的自适应Forms（XSD、XDP、JSON、FDM，并且不基于表单模型）的crx文件进行预填充。 仅允许使用JSON和XML文件进行预填充。

1. 现在已为您的表单配置预填充服务。

   >[!NOTE]
   >
   >crx协议负责预填充数据的安全性，因此默认情况下允许使用。 使用通用正则表达式通过其他协议预填充可能会导致漏洞。 在配置中，指定用于保护数据的安全URL配置。

## 可重复面板的奇特案例{#the-curious-case-of-repeatable-panels}

通常，绑定（表单架构）和未绑定字段是在同一自适应表单中创作的，但在绑定可重复的情况下，以下是少数例外：

* 对于使用XFA表单模板、XSD、JSON架构或FDM架构的自适应表单，不支持未绑定的可重复面板。
* 请勿在绑定的可重复面板中使用未绑定字段。

>[!NOTE]
>
>作为经验法则，如果绑定和未绑定字段在未绑定字段中由最终用户填充的数据中相交，则不要混合这些字段。 如果可能，您应修改架构或XFA表单模板，并为未绑定字段添加一个条目，以便该模板也会绑定，并且其数据与已提交数据中的其他字段一样可用。

## 支持预填用户数据{#supported-protocols-for-prefilling-user-data}的协议

使用有效正则表达式配置后，可通过以下协议以预填充数据格式预填充用户数据：

### crx://协议{#the-crx-protocol}

```http
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=crx:///tmp/fd/af/myassets/sample.xml
```

指定的节点必须具有名为`jcr:data`的属性并保存数据。

### file://协议  {#the-file-protocol-nbsp}

```http
https://localhost:4502/content/forms/af/someAF.html?wcmmode=disabled&dataRef=file:///C:/Users/form-user/Downloads/somesamplexml.xml
```

引用的文件必须位于同一服务器上。

### https://协议{#the-http-protocol}

```http
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=https://localhost:8000/somesamplexmlfile.xml
```

### service://协议{#the-service-protocol}

```http
https://localhost:4502/content/forms/af/abc.html?wcmmode=disabled&dataRef=service://[SERVICE_NAME]/[IDENTIFIER]
```

* SERVICE_NAME是指OSGI预填充服务的名称。 请参阅[创建并运行预填充服务](../../forms/using/prepopulate-adaptive-form-fields.md#create-and-run-a-prefill-service)。
* 标识符是指OSGI预填充服务获取预填充数据所需的任何元数据。 已登录用户的标识符就是可使用的元数据示例。

>[!NOTE]
>
>不支持传递身份验证参数。

### 在slingRequest {#setting-data-attribute-in-slingrequest}中设置数据属性

您还可以在`slingRequest`中设置`data`属性，其中`data`属性是包含XML或JSON的字符串，如以下示例代码所示（XML的示例为）：

```javascript
<%
           String dataXML="<afData>" +
                            "<afUnboundData>" +
                                "<data>" +
                                    "<first_name>"+ "Tyler" + "</first_name>" +
                                    "<last_name>"+ "Durden " + "</last_name>" +
                                    "<gender>"+ "Male" + "</gender>" +
                                    "<location>"+ "Texas" + "</location>" +
                                    "</data>" +
                            "</afUnboundData>" +
                        "</afData>";
        slingRequest.setAttribute("data", dataXML);
%>
```

您可以编写一个包含所有数据的简单XML或JSON字符串，并在slingRequest中对其进行设置。 您可以轻松地在渲染器JSP中为任何组件完成此操作，您要将组件包含在可在其中设置slingRequest数据属性的页面中。

例如，您希望页面的特定设计具有特定类型的标题。 要实现此目的，您可以编写自己的`header.jsp`，该组件可包含在页面组件中并设置`data`属性。

另一个好示例是您希望通过Facebook、Twitter或LinkedIn等社交帐户预填登录数据的用例。 在这种情况下，您可以在`header.jsp`中包含一个简单的JSP，它从用户帐户中获取数据并设置数据参数。

prefill-page component.zip

[在页](assets/prefill-page-component.zip)
面组件中获取FileSample prefill.jsp

## AEM Forms自定义预填充服务{#aem-forms-custom-prefill-service}

对于您经常从预定义源中读取数据的情况，您可以使用自定义预填充服务。 预填充服务从定义的数据源中读取数据，并使用预填充数据文件的内容预填充自适应表单的字段。 它还可帮助您将预填数据与自适应表单永久关联。

### 创建并运行预填充服务{#create-and-run-a-prefill-service}

预填充服务是OSGi服务，通过OSGi包进行打包。 您可以创建、上传OSGi包并将其安装到AEM Forms包。 开始创建包之前：

* [下载AEM Forms客户端SDK](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html)
* 下载样板包

* 将数据（预填充数据）文件放置到crx-repository中。 您可以将文件放置在crx-repository的\contents文件夹中的任意位置。

[获取文件](assets/prefill-sumbit-xmlsandcontentpackage.zip)

#### 创建预填充服务{#create-a-prefill-service}

样板包（示例预填充服务包）包含AEM Forms预填充服务的示例实现。 在代码编辑器中打开样板包。 例如，在Eclipse中打开样板项目进行编辑。 在代码编辑器中打开样板包后，请执行以下步骤以创建服务。

1. 打开src\main\java\com\adobe\test\Prefill.java文件进行编辑。
1. 在代码中，将值设置为：

   * `nodePath:` 指向crx-repository位置的节点路径变量包含数据（预填充）文件的路径。例如， /content/prefilldata.xml
   * `label:` 标签参数指定服务的显示名称。例如，默认预填充服务

1. 保存并关闭`Prefill.java`文件。
1. 将`AEM Forms Client SDK`包添加到样板项目的构建路径中。
1. 编译项目并为包创建.jar。

#### 启动并使用预填充服务{#start-and-use-the-prefill-service}

要启动预填充服务，请将JAR文件上载到AEM Forms Web Console，然后激活该服务。 现在，服务开始在自适应表单编辑器中显示。 要将预填充服务与自适应表单关联，请执行以下操作：

1. 在Forms编辑器中打开自适应表单，然后打开表单容器的属性面板。
1. 在“属性”控制台中，导航到AEM Forms容器>基本>预填充服务。
1. 选择默认预填充服务，然后单击&#x200B;**[!UICONTROL 保存]**。 该服务与表单关联。

## 在客户端{#prefill-at-client}预填充数据

当您预填自适应表单时，AEM Forms服务器会将数据与自适应表单合并，并将填写的表单交付给您。 默认情况下，数据合并操作会在服务器中进行。

您可以配置AEM Forms服务器以在客户端而不是服务器上执行数据合并操作。 它显着缩短了预填充和渲染自适应表单所需的时间。 默认情况下，该功能处于禁用状态。 可以从配置管理器或命令行中启用它。

* 要从配置管理器中启用或禁用，请执行以下操作：
   1. 打开AEM Configuration Manager。
   1. 找到并打开自适应表单和交互式通信Web渠道配置
   1. 启用Configuration.af.clientside.datamerge.enabled.name选项
* 要从命令行中启用或禁用，请执行以下操作：
   * 要启用，请运行以下cURL命令：
      `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=true \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

   * 要禁用，请运行以下cURL命令：
      `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=false \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`
   要充分利用客户端预填充数据选项，请更新预填充服务以返回[FileAttachmentMap](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html)和[CustomContext](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html)
