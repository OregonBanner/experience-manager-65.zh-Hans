---
title: 预填自适应表单字段
seo-title: 预填自适应表单字段
description: 使用现有数据预填自适应表单的字段。
seo-description: 使用自适应表单，用户可以通过登录其社交用户档案来预填表单中的基本信息。 本文介绍如何完成此操作。
uuid: 574de83a-7b5b-4a1f-ad37-b9717e5c14f1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 7139a0e6-0e37-477c-9e0b-aa356991d040
docset: aem65
translation-type: tm+mt
source-git-commit: 49da3dbe590f70b98185a6bc330db6077dc864c0

---


# 预填自适应表单字段{#prefill-adaptive-form-fields}

## 简介 {#introduction}

您可以使用现有数据预填自适应表单的字段。 用户打开表单时，将预填这些字段的值。 要在自适应表单中预填数据，请以符合自适应表单预填数据结构的格式，将用户数据作为预填XML/JSON提供。

## 预填充数据的结构 {#the-prefill-structure}

自适应表单可以具有绑定和未绑定字段的混合。 绑定字段是从“内容查找器”选项卡中拖动的字段，并在字段编辑对 `bindRef` 话框中包含非空属性值。 未绑定的字段直接从Sidekick的组件浏览器中拖动，并且值 `bindRef` 为空。

您可以预填自适应表单的绑定和未绑定字段。 预填数据包含afBoundData和afUnBoundData部分以预填自适应表单的绑定和未绑定字段。 该部 `afBoundData` 分包含绑定字段和面板的预填数据。 此数据必须符合关联的表单模型模式:

* 对于使用 [XFA表单模板的自适应表单](../../forms/using/prepopulate-adaptive-form-fields.md)，请使用符合XFA模板数据模式的预填XML。
* 对于使用 [XML模式的自适应表单](#xml-schema-af)，请使用与XML模式结构兼容的预填XML。
* 对于使用 [JSON模式的自适应表单](#json-schema-based-adaptive-forms)，请使用符合JSON模式的预填JSON。
* 对于使用FDM模式的自适应表单，请使用符合FDM模式的预填JSON。
* 对于没有表单模 [型的自适应表单](#adaptive-form-with-no-form-model)，没有绑定数据。 每个字段都是未绑定字段，并使用未绑定的XML预填充。

### 范例预填充XML结构 {#sample-prefill-xml-structure}

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

### 示例预填JSON结构 {#sample-prefill-json-structure}

```
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

对于具有相同绑定字段或未绑定字段且名称相同的绑定字段，在XML标记或JSON对象中指定的数据将填充所有字段。 例如，表单中的两个字段将映射到预填数据 `textbox` 中的名称。 在运行时，如果第一个文本框字段包含“A”，则“A”会自动填写在第二个文本框中。 此链接称为自适应表单字段的实时链接。

### 使用XFA表单模板的自适应表单 {#xfa-based-af}

基于XFA的自适应表单的预填XML和提交的XML的结构如下：

* **预填充XML结构**:基于XFA的自适应表单的预填XML必须符合XFA表单模板的数据模式。 要预填充未绑定的字段，请将预填充XML结构包含在标 `/afData/afBoundData` 签中。

* **已提交的XML结构**:当不使用预填充XML时，提交的XML包含包装器标签中绑定字段和未绑定字段的 `afData` 数据。 如果使用预填充XML，则提交的XML与预填充XML的结构相同。 如果预填XML开始带有根标 `afData` 签，则输出XML也具有相同的格式。 如果预填充XML没有包装器，而 `afData/afBoundData`是直接从开始根标签(如模式)中 `employeeData`，则提交的XML也会与标签一起 `employeeData` 开始。

Prefill-Submit-Data-ContentPackage.zip

[获取包含](assets/prefill-submit-data-contentpackage.zip)预填数据和已提交数据的文件范例

### 基于XML模式的自适应表单 {#xml-schema-af}

基于XML模式的自适应表单预填XML和提交XML的结构如下：

* **预填充XML结构**:预填充XML必须符合关联的XML模式。 要预填充未绑定的字段，请将预填充XML结构包含在/afData/afBoundData标签中。
* **提交的XML结构**:如果未使用预填充XML，则提交的XML包含包装器标签中绑定字段和未绑定字段 `afData` 的数据。 如果使用预填充XML，则提交的XML与预填充XML的结构相同。 如果预填XML开始带有根标 `afData` 签，则输出XML的格式相同。 如果预填充XML没有包装器，而 `afData/afBoundData` 是直接从开始根标签(如模式)中 `employeeData`，则提交的XML也会与标签开始 `employeeData` 。

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

对于模型为XML模式的字段，数据预填充到标 `afBoundData` 签中，如以下示例XML所示。 它可用于用一个或多个未绑定文本字段预填充自适应表单。

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
>建议不要在绑定面板中使用未绑定字段(面板中的非空 `bindRef` 字段是通过从Sidekick或数据源选项卡拖动组件创建的)。 这可能导致这些未绑定字段的数据丢失。 此外，建议字段名称在表单中是唯一的，特别是对于未绑定的字段。

#### 不带afData和afBoundData包装器的示例 {#an-example-without-afdata-and-afbounddata-wrapper}

```xml
<?xml version="1.0" encoding="UTF-8"?><config>
 <assignmentDetails descriptionOfAssignment="Some Science Project" durationOfAssignment="34" financeRelatedProject="1" name="Lisa" numberOfMentees="1"/>
 <assignmentDetails descriptionOfAssignment="Kidding, right?" durationOfAssignment="4" financeRelatedProject="1" name="House" numberOfMentees="3"/>
</config>
```

### 基于JSON模式的自适应表单 {#json-schema-based-adaptive-forms}

对于基于JSON模式的自适应表单，预填JSON和提交的JSON的结构如下所述。 有关详细信息，请参 [阅使用JSON模式创建自适应表单](../../forms/using/adaptive-form-json-schema-form-model.md)。

* **预填JSON结构**:预填JSON必须符合关联的JSON模式。 或者，如果您也要预填充未绑定的字段，也可以将其打包到/afData/afBoundData对象中。
* **已提交的JSON结构**:如果未使用预填JSON，则提交的JSON包含afData包装器标记中绑定字段和未绑定字段的数据。 如果使用预填JSON，则提交的JSON的结构与预填JSON相同。 如果预填JSON开始有afData根对象，则输出JSON的格式相同。 如果预填JSON没有afData/afBoundData包装器，而是直接从模式根对象（如用户）开始，则提交的JSON也会与用户对象开始。

```
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

对于使用JSON模式模型的字段，数据预填充到afBoundData对象中，如下面的示例JSON所示。 它可用于用一个或多个未绑定文本字段预填充自适应表单。 以下是包装器的数据示 `afData/afBoundData` 例：

```
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

下面是一个没有包装器的 `afData/afBoundData` 示例：

```
{
 "user": {
  "address": {
   "city": "Noida",
   "country": "India"
}}}
```

>[!NOTE]
>
>不建议在绑定面板中使用未绑定字段（具有非空bindRef的面板，这些面板是通过从Sidekick或“数据源”选项卡中拖动组件创建的） **** ，因为这可能导致未绑定字段的数据丢失。 建议在表单中具有唯一的字段名称，尤其是对于未绑定的字段。

### 没有表单模型的自适应表单 {#adaptive-form-with-no-form-model}

对于没有表单模型的自适应表单，所有字段的数据位于的标 `<data>` 签下 `<afUnboundData> tag`。

另外，请注意以下事项：

为各个字段提交的用户数据生成的XML标记使用字段名称。 因此，字段名称必须是唯一的。

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

## 使用Configuration Manager配置预填服务 {#configuring-prefill-service-using-configuration-manager}

要启用预填服务，请在AEM Web控制台配置中指定默认预填服务配置。 使用以下步骤配置预填服务：

>[!NOTE]
>
>“预填服务配置”适用于自适应表单、HTML5表单和HTML5表单集。

1. 使用 **[!UICONTROL URL打开Adobe Experience Manager Web Console配置]** :\
   https://&lt;server>:&lt;port>/system/console/configMgr
1. 搜索并打开默 **[!UICONTROL 认预填服务配置]**。

   ![预填配置](assets/prefill_config_new.png)

1. 输入数据位置或数据文件位置的正则表达式(正 **则表达式)**。 有效数据文件位置的示例包括：

   * file:///C:/Users/public/Document/Prefill/。*
   * https://localhost:8000/somesamplexmlfile.xml
   >[!NOTE]
   >
   >默认情况下，允许通过crx文件预填所有类型的自适应表单（XSD、XDP、JSON、FDM和不基于表单模型）。 仅对JSON和XML文件允许预填充。

1. 现在为表单配置了预填服务。

   >[!NOTE]
   >
   >crx协议负责预填充的数据安全性，因此，默认情况下允许使用。 使用通用正则表达式通过其他协议预填充可能会导致漏洞。 在配置中，指定用于保护数据的安全URL配置。

## 可重复面板的奇特案例 {#the-curious-case-of-repeatable-panels}

通常，绑定(表单模式)和未绑定字段在同一自适应表单中创作，但是，如果绑定可重复，以下是少数例外情况：

* 对于使用XFA表单模板、XSD、JSON模式或FDM模式的自适应表单，不支持未绑定的可重复面板。
* 请勿在绑定的可重复面板中使用未绑定字段。

>[!NOTE]
>
>根据经验法则，如果绑定和未绑定字段在未绑定字段中由最终用户填充的数据中交叉，则不要混合绑定和未绑定字段。 如果可能，您应修改模式或XFA表单模板，并为未绑定字段添加一个条目，以便它也会被绑定，并且其数据与提交数据中的其他字段一样可用。

## 支持的预填充用户数据的协议 {#supported-protocols-for-prefilling-user-data}

当配置了有效的正则表达式时，可以通过以下协议以预填充数据格式预填充自适应表单的用户数据：

### crx://协议 {#the-crx-protocol}

```xml
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=crx:///tmp/fd/af/myassets/sample.xml
```

指定的节点必须有一个名为并保 `jcr:data` 存数据的属性。

### file://协议 {#the-file-protocol-nbsp}

```xml
https://localhost:4502/content/forms/af/someAF.html?wcmmode=disabled&dataRef=file:///C:/Users/form-user/Downloads/somesamplexml.xml
```

引用的文件必须位于同一台服务器上。

### https://协议 {#the-http-protocol}

```xml
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=https://localhost:8000/somesamplexmlfile.xml
```

### service://协议 {#the-service-protocol}

```xml
https://localhost:4502/content/forms/af/abc.html?wcmmode=disabled&dataRef=service://[SERVICE_NAME]/[IDENTIFIER]
```

* SERVICE_NAME引用OSGI预填服务的名称。 请参 [阅创建并运行预填服务](../../forms/using/prepopulate-adaptive-form-fields.md#create-and-run-a-prefill-service)。
* 标识符引用OSGI预填充服务获取预填充数据所需的任何元数据。 登录用户的标识符是可以使用的元数据示例。

>[!NOTE]
>
>不支持传递身份验证参数。

### 在slingRequest中设置数据属性 {#setting-data-attribute-in-slingrequest}

您还可以在中设 `data` 置属性 `slingRequest``data` ，其中属性是包含XML或JSON的字符串，如以下示例代码所示（示例为XML）:

```java
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

您可以编写一个包含所有数据的简单XML或JSON字符串，并在slingRequest中设置它。 这可以在任何组件的呈示器JSP中轻松完成，您要将其包含在可设置slingRequest数据属性的页面中。

例如，您希望页面具有特定类型标题的特定设计的位置。 为此，您可以编写自己的内 `header.jsp`容，将其包含在页面组件中并设置属 `data` 性。

另一个示例是您希望通过Facebook、Twitter或LinkedIn等社交帐户在登录时预填数据的用例。 在这种情况下，您可以在中包含一个简单的JSP `header.jsp`，它从用户帐户中获取数据并设置数据参数。

prefill-page component.zip

[获取页](assets/prefill-page-component.zip)面组件中的FileSample prefill.jsp

## AEM Forms自定义预填服务 {#aem-forms-custom-prefill-service}

您可以对场景使用自定义预填服务，在这些场景中，您经常从预定义的源读取数据。 预填充服务从定义的数据源读取数据，并用预填充数据文件的内容预填充自适应表单的字段。 它还可以帮助您将预填数据与自适应表单永久关联。

### 创建和运行预填服务 {#create-and-run-a-prefill-service}

预填充服务是OSGi服务，并通过OSGi捆绑打包。 您可以创建OSGi捆绑包、上传它并将其安装到AEM Forms捆绑包。 在开始创建捆绑之前：

* [下载AEM Forms客户端SDK](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html)
* 下载样板包

* 将数据（预填数据）文件放入crx-repository中。 可以将文件放在crx-repository的\contents文件夹中的任意位置。

[获取文件](assets/prefill-sumbit-xmlsandcontentpackage.zip)

#### 创建预填服务 {#create-a-prefill-service}

样板文件包（示例预填服务包）包含AEM Forms预填服务的示例实现。 在代码编辑器中打开样板包。 例如，在Eclipse中打开样板项目进行编辑。 在代码编辑器中打开样板包后，请执行以下步骤以创建服务。

1. 打开src\main\java\com\adobe\test\Prefill.java文件进行编辑。
1. 在代码中，设置以下值：

   * `nodePath:` 指向crx-repository位置的节点路径变量包含数据（预填充）文件的路径。 例如，/content/prefilldata.xml
   * `label:` 标签参数指定服务的显示名称。 例如，默认预填服务

1. 保存并关闭 `Prefill.java` 文件。
1. 将包添 `AEM Forms Client SDK` 加到样板项目的构建路径。
1. 编译项目并为包创建。jar。

#### 开始和使用预填服务 {#start-and-use-the-prefill-service}

要开始预填服务，请将JAR文件上传到AEM Forms Web控制台，然后激活该服务。 现在，在自适应表单编辑器中显示的服务开始。 要将预填服务关联到自适应表单，请执行以下操作：

1. 在表单编辑器中打开自适应表单，然后打开表单容器的“属性”面板。
1. 在“属性”控制台中，导航到“AEM表单容器”>“基本”>“预填服务”。
1. 选择“默认预填服务”，然后单击“ **[!UICONTROL 保存]**”。 服务与表单相关联。

