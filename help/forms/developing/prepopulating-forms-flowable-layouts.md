---
title: 使用可流布局预填充Forms
description: 使用Java API和Web服务API预填充具有流式布局的表单，以在呈现的表单中向用户显示数据。
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: ff087084-fb1c-43a4-ae54-cc77eb862493
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '3478'
ht-degree: 0%

---

# 使用可流布局预填充Forms {#prepopulating-forms-with-flowable-layouts1}

## 使用可流布局预填充Forms {#prepopulating-forms-with-flowable-layouts2}

预先填充的表单会在呈现的表单中向用户显示数据。 例如，假设用户使用用户名和密码登录到网站。 如果验证成功，则客户端应用程序将查询数据库以获取用户信息。 数据将合并到表单中，然后表单呈现给用户。 因此，用户能够在表单中查看个性化数据。

预先填充表单具有以下优点：

* 允许用户在表单中查看自定义数据。
* 减少用户填写表单时键入内容的次数。
* 通过控制数据的放置位置来确保数据完整性。

以下两个XML数据源可以预填充表单：

* XDP数据源，它是符合XFA语法的XML(或预填充使用Acrobat创建的表单的XFDF数据)。
* 包含与表单字段名称匹配的名称/值对的任意XML数据源（本节中的示例使用任意XML数据源）。

要预填充的每个表单字段都必须存在XML元素。 XML元素名称必须与字段名称匹配。 如果XML元素与表单字段不对应，或者如果XML元素名称与字段名称不匹配，则忽略该元素。 只要指定了所有XML元素，就不必匹配XML元素的显示顺序。

在预填充已包含数据的表单时，必须指定已在XML数据源中显示的数据。 假设包含10个字段的表单在四个字段中有数据。 接下来，假设您希望预填充其余六个字段。 在这种情况下，必须在XML数据源中指定用于预填充表单的10个XML元素。 如果仅指定六个元素，则原始的四个字段为空。

例如，您可以预填充窗体，如示例确认窗体。 (请参阅以下位置中的“确认表单”： [呈现交互式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md).)

要预填充示例确认表单，您必须创建一个XML数据源，该数据源包含与表单中的三个字段匹配的三个XML元素。 此表单包含以下三个字段： `FirstName`， `LastName`、和 `Amount`. 第一步是创建一个XML数据源，该数据源包含与表单设计中的字段匹配的XML元素。 下一步是将数据值分配给XML元素，如以下XML代码中所示。

```xml
     <Untitled>
         <FirstName>Jerry</FirstName>
         <LastName>Johnson</LastName>
         <Amount>250000</Amount>
     </Untitled>
```

使用此XML数据源预填充确认表单，然后呈现该表单后，将显示分配给XML元素的数据值，如下图所示。

![pf_pf_confirmxml3](assets/pf_pf_confirmxml3.png)

### 使用可流动布局预填充表单 {#prepopulating_forms_with_flowable_layouts-1}

带可流动布局的Forms可用于向用户显示未确定的数据量。 由于表单的布局会自动根据合并的数据量进行调整，因此您无需像处理具有固定布局的表单那样预先确定表单的固定布局或页数。

通常，表单会填充在运行时获取的数据。 因此，您可以通过创建内存中XML数据源并将数据直接放入内存中XML数据源来预填充表单。

考虑一个基于Web的应用程序，如在线商店。 在线购物者完成购买项目后，所有购买的项目都会放入内存中的XML数据源，该数据源用于预填充表单。 下图显示了此流程，图后的表中对此进行了说明。

![pf_pf_finsrv_webapp_v1](assets/pf_pf_finsrv_webapp_v1.png)

下表描述了此图中的步骤。

<table>
 <thead>
  <tr>
   <th><p>步骤</p></th>
   <th><p>描述</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>用户从基于Web的网上商店购买商品。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>用户完成采购物料并单击“提交”按钮后，将创建一个内存中的XML数据源。 购买的项目和用户信息都放入内存中的XML数据源中。 </p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>XML数据源用于预填充采购订单表单（此表后面显示了此表单的示例）。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>采购订单表单呈现给客户端Web浏览器。 </p></td>
  </tr>
 </tbody>
</table>

下图显示了采购订单表单的示例。 表中的信息可以根据XML数据中的记录数进行调整。

![pf_pf_poform](assets/pf_pf_poform.png)

>[!NOTE]
>
>可以使用来自其他源（如企业数据库或外部应用程序）的数据预填充表单。

### 窗体设计注意事项 {#form-design-considerations}

带有可流动布局的Forms基于在Designer中创建的表单设计。 表单设计指定一组布局、呈现和数据捕获规则，包括基于用户输入计算值。 数据输入到表单中时将应用规则。 添加到表单的字段是表单设计内的子表单。 例如，在上图所示的采购订单表单中，每行都是一个子表单。 有关创建包含子表单的表单设计的信息，请参阅 [创建具有流式布局的采购订单表单](https://www.adobe.com/go/learn_aemforms_qs_poformflowable_9).

### 了解数据子组 {#understanding-data-subgroups}

XML数据源用于预先填充具有固定布局和可流动布局的表单。 但是，不同之处在于，使用可流动布局预填充表单的XML数据源包含用于预填充表单内重复的子表单的重复XML元素。 这些重复的XML元素称为数据子组。

用于预填充上图所示的采购订单表单的XML数据源包含四个重复的数据子组。 每个数据子组对应于购买的项目。 所购物品包括显示器、台灯、电话和通讯录。

以下XML数据源用于预填充采购订单表单。

```xml
     <header>
         <!-- XML elements used to prepopulate non-repeating fields such as address
         <!and city
         <txtPONum>8745236985</txtPONum>
         <dtmDate>2004-02-08</dtmDate>
         <txtOrderedByCompanyName>Any Company Name</txtOrderedByCompanyName>
         <txtOrderedByAddress>555, Any Blvd.</txtOrderedByAddress>
         <txtOrderedByCity>Any City</txtOrderedByCity>
         <txtOrderedByStateProv>ST</txtOrderedByStateProv>
         <txtOrderedByZipCode>12345</txtOrderedByZipCode>
         <txtOrderedByCountry>Any Country</txtOrderedByCountry>
         <txtOrderedByPhone>(123) 456-7890</txtOrderedByPhone>
         <txtOrderedByFax>(123) 456-7899</txtOrderedByFax>
         <txtOrderedByContactName>Contact Name</txtOrderedByContactName>
         <txtDeliverToCompanyName>Any Company Name</txtDeliverToCompanyName>
         <txtDeliverToAddress>7895, Any Street</txtDeliverToAddress>
         <txtDeliverToCity>Any City</txtDeliverToCity>
         <txtDeliverToStateProv>ST</txtDeliverToStateProv>
         <txtDeliverToZipCode>12346</txtDeliverToZipCode>
         <txtDeliverToCountry>Any Country</txtDeliverToCountry>
         <txtDeliverToPhone>(123) 456-7891</txtDeliverToPhone>
         <txtDeliverToFax>(123) 456-7899</txtDeliverToFax>
         <txtDeliverToContactName>Contact Name</txtDeliverToContactName>
     </header>
     <detail>
         <!-- A data subgroup that contains information about the monitor>
         <txtPartNum>00010-100</txtPartNum>
         <txtDescription>Monitor</txtDescription>
         <numQty>1</numQty>
         <numUnitPrice>350.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the desk lamp>
         <txtPartNum>00010-200</txtPartNum>
         <txtDescription>Desk lamps</txtDescription>
         <numQty>3</numQty>
         <numUnitPrice>55.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the Phone>
             <txtPartNum>00025-275</txtPartNum>
             <txtDescription>Phone</txtDescription>
             <numQty>5</numQty>
             <numUnitPrice>85.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the address book>
         <txtPartNum>00300-896</txtPartNum>
         <txtDescription>Address book</txtDescription>
         <numQty>2</numQty>
         <numUnitPrice>15.00</numUnitPrice>
     </detail>
```

请注意，每个数据子组都包含对应于此信息的四个XML元素：

* 项目部件号
* 物料说明
* 物料数量
* 单价

数据子组的父XML元素的名称必须与窗体设计中的子窗体的名称匹配。 例如，在上图中，请注意数据子组的父XML元素的名称为 `detail`. 这与采购订单表单所基于的表单设计中子表单的名称相对应。 如果数据子组的父XML元素的名称与子表单不匹配，则不会预填充服务器端表单。

每个数据子组都必须包含与子表单中的字段名称匹配的XML元素。 此 `detail` 表单设计中的子表单包含以下字段：

* txtPartNum
* txtDescription
* numQty
* numUnitPrice

>[!NOTE]
>
>如果您尝试使用包含重复XML元素的数据源预填充表单，并且您设置了 `RenderAtClient` 选项至 `No`，则只有第一个数据记录会合并到表单中。 为确保所有数据记录都合并到表单中，请设置 `RenderAtClient` 到 `Yes`. 欲知关于 `RenderAtClient` 选项，请参见 [在客户端渲染Forms](/help/forms/developing/rendering-forms-client.md).

>[!NOTE]
>
>有关Forms服务的更多信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary-of-steps}

要使用可流式布局预填充表单，请执行以下任务：

1. 包括项目文件。
1. 创建内存中XML数据源。
1. 转换XML数据源。
1. 呈现预填充的表单。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

**创建内存中XML数据源**

您可以使用 `org.w3c.dom` 用于创建内存中XML数据源的类，以便使用可流布局预填充表单。 将数据放置到符合表单的XML数据源中。 有关具有流式布局的表单与XML数据源之间的关系的信息，请参阅 [了解数据子组](#understanding-data-subgroups).

**转换XML数据源**

内存中的XML数据源，它使用创建 `org.w3c.dom` 类可以转换为 `com.adobe.idp.Document` 对象之前，填充该对象以预填充表单。 内存中的XML数据源可以使用Java XML转换类进行转换。

>[!NOTE]
>
>如果您使用Forms服务的WSDL来预填充表单，则必须将 `org.w3c.dom.Document` 对象转换为 `BLOB` 对象。

**呈现预填充的表单**

您可以像呈现其他表单一样呈现预填充的表单。 唯一的区别是您使用 `com.adobe.idp.Document` 包含要预填充表单的XML数据源的对象。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服务API快速启动](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[呈现交互式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[创建可渲染Forms的Web应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API预填充表单 {#prepopulating-forms-using-the-java-api}

要使用Forms API (Java)预填充具有可流动布局的表单，请执行以下步骤：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，例如adobe-forms-client.jar。 有关这些文件的位置的信息，请参见 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. 创建内存中XML数据源

   * 创建Java `DocumentBuilderFactory` 对象，方法是 `DocumentBuilderFactory` 类&#39; `newInstance` 方法。
   * 创建Java `DocumentBuilder` 对象，方法是 `DocumentBuilderFactory` 对象的 `newDocumentBuilder` 方法。
   * 调用 `DocumentBuilder` 对象的 `newDocument` 实例化的方法 `org.w3c.dom.Document` 对象。
   * 通过调用 `org.w3c.dom.Document` 对象的 `createElement` 方法。 这会创建 `Element` 表示根元素的对象。 将表示元素名称的字符串值传递给 `createElement` 方法。 将返回值强制转换为 `Element`. 接下来，通过调用 `Document` 对象的 `appendChild` 方法，并将根元素对象作为参数传递。 以下代码行显示了此应用程序逻辑：

     ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * 通过调用 `Document` 对象的 `createElement` 方法。 将表示元素名称的字符串值传递给 `createElement` 方法。 将返回值强制转换为 `Element`. 接下来，通过调用 `root` 对象的 `appendChild` 方法，并将标头元素对象作为参数传递。 附加到标题元素的XML元素对应于表单的静态部分。 以下代码行显示此应用程序逻辑：

     ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * 通过调用 `Document` 对象的 `createElement` 方法，并传递表示元素名称的字符串值。 将返回值强制转换为 `Element`. 接下来，通过调用其子元素的 `appendChild` 方法，并传递 `Document` 对象的 `createTextNode` 方法作为参数。 指定作为子元素的值显示的字符串值。 最后，通过调用标头元素的 `appendChild` 方法，并将子元素对象作为参数传递。 以下代码行显示此应用程序逻辑：

     ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`


   * 通过重复表单静态部分中出现的每个字段的最后一个子步骤（在XML数据源图表中，这些字段显示在A部分中），将所有剩余的元素添加到标题元素中。(请参阅 [了解数据子组](#understanding-data-subgroups).)
   * 通过调用 `Document` 对象的 `createElement` 方法。 将表示元素名称的字符串值传递给 `createElement` 方法。 将返回值强制转换为 `Element`. 接下来，通过调用 `root` 对象的 `appendChild` 方法，并将detail元素对象作为参数传递。 附加到详细信息元素的XML元素对应于表单的动态部分。 以下代码行显示此应用程序逻辑：

     ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * 通过调用 `Document` 对象的 `createElement` 方法，并传递表示元素名称的字符串值。 将返回值强制转换为 `Element`. 接下来，通过调用其子元素的 `appendChild` 方法，并传递 `Document` 对象的 `createTextNode` 方法作为参数。 指定作为子元素的值显示的字符串值。 最后，通过调用detail元素的 `appendChild` 方法，并将子元素对象作为参数传递。 以下代码行显示此应用程序逻辑：

     ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * 对所有XML元素重复最后一个子步骤以附加到详细信息元素。 要正确创建用于填充采购订单表单的XML数据源，必须将以下XML元素附加到明细元素中： `txtDescription`， `numQty`、和 `numUnitPrice`.
   * 对用于预填充表单的所有数据项重复前两个子步骤。

1. 转换XML数据源

   * 创建 `javax.xml.transform.Transformer` 对象，方法是调用 `javax.xml.transform.Transformer` 对象的静态 `newInstance` 方法。
   * 创建 `Transformer` 对象，方法是调用 `TransformerFactory` 对象的 `newTransformer` 方法。
   * 创建 `ByteArrayOutputStream` 对象。
   * 创建 `javax.xml.transform.dom.DOMSource` 对象，使用它的构造函数传递 `org.w3c.dom.Document` 步骤1中创建的对象。
   * 创建 `javax.xml.transform.dom.DOMSource` 对象，使用它的构造函数传递 `ByteArrayOutputStream` 对象。
   * 填充Java `ByteArrayOutputStream` 对象，方法是调用 `javax.xml.transform.Transformer` 对象的 `transform` 方法和传递 `javax.xml.transform.dom.DOMSource` 和 `javax.xml.transform.stream.StreamResult` 对象。
   * 创建字节数组并分配 `ByteArrayOutputStream` 对象。
   * 通过调用 `ByteArrayOutputStream` 对象的 `toByteArray` 方法。
   * 创建 `com.adobe.idp.Document` 对象，使用它的构造函数传递字节数组。

1. 呈现预填充的表单

   调用 `FormsServiceClient` 对象的 `renderPDFForm` 方法并传递以下值：

   * 一个字符串值，它指定窗体设计名称，包括文件扩展名。
   * A `com.adobe.idp.Document` 包含要与表单合并的数据的对象。 确保您使用 `com.adobe.idp.Document` 在步骤1和步骤2中创建的对象。
   * A `PDFFormRenderSpec` 存储运行时选项的对象。
   * A `URLSpec` 包含Forms服务所需的URI值的对象。
   * A `java.util.HashMap` 存储文件附件的对象。 这是一个可选参数，您可以指定 `null` 如果您不想将文件附加到表单。

   此 `renderPDFForm` 方法返回 `FormsResult` 包含必须写入客户端Web浏览器的表单数据流的对象。

   * 创建 `javax.servlet.ServletOutputStream` 用于将表单数据流发送到客户端Web浏览器的对象。
   * 创建 `com.adobe.idp.Document` 对象，方法是调用 `FormsResult` 对象 `getOutputContent` 方法。
   * 创建 `java.io.InputStream` 对象，方法是调用 `com.adobe.idp.Document` 对象的 `getInputStream` 方法。
   * 创建一个字节数组，通过调用 `InputStream` 对象的 `read` 方法并将字节数组作为参数传递。
   * 调用 `javax.servlet.ServletOutputStream` 对象的 `write` 将表单数据流发送到客户端Web浏览器的方法。 将字节数组传递给 `write` 方法。

**另请参阅**

[快速入门（SOAP模式）：使用Java API在可流式布局中预填充Forms](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API预填充表单 {#prepopulating-forms-using-the-web-service-api}

要使用Forms API（Web服务）预填充具有可流动布局的表单，请执行以下步骤：

1. 包含项目文件

   * 创建使用Forms服务WSDL的Java代理类。 (请参阅 [使用Apache Axis创建Java代理类](/help/forms/developing/invoking-aem-forms-using-web.md#creating-java-proxy-classes-using-apache-axis).)
   * 将Java代理类包含在类路径中。

1. 创建内存中XML数据源

   * 创建Java `DocumentBuilderFactory` 对象，方法是 `DocumentBuilderFactory` 类&#39; `newInstance` 方法。
   * 创建Java `DocumentBuilder` 对象，方法是 `DocumentBuilderFactory` 对象的 `newDocumentBuilder` 方法。
   * 调用 `DocumentBuilder` 对象的 `newDocument` 实例化的方法 `org.w3c.dom.Document` 对象。
   * 通过调用 `org.w3c.dom.Document` 对象的 `createElement` 方法。 这会创建 `Element` 表示根元素的对象。 将表示元素名称的字符串值传递给 `createElement` 方法。 将返回值强制转换为 `Element`. 接下来，通过调用 `Document` 对象的 `appendChild` 方法，并将根元素对象作为参数传递。 以下代码行显示此应用程序逻辑：

     ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * 通过调用 `Document` 对象的 `createElement` 方法。 将表示元素名称的字符串值传递给 `createElement` 方法。 将返回值强制转换为 `Element`. 接下来，通过调用 `root` 对象的 `appendChild` 方法，并将标头元素对象作为参数传递。 附加到标题元素的XML元素对应于表单的静态部分。 以下代码行显示此应用程序逻辑：

     ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * 通过调用 `Document` 对象的 `createElement` 方法，并传递表示元素名称的字符串值。 将返回值强制转换为 `Element`. 接下来，通过调用其子元素的 `appendChild` 方法，并传递 `Document` 对象的 `createTextNode` 方法作为参数。 指定作为子元素的值显示的字符串值。 最后，通过调用标头元素的 `appendChild` 方法，并将子元素对象作为参数传递。 以下代码行显示了此应用程序逻辑：

     ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`

   * 通过重复表单静态部分中出现的每个字段的最后一个子步骤（在XML数据源图表中，这些字段显示在A部分中），将所有剩余的元素添加到标题元素中。(请参阅 [了解数据子组](#understanding-data-subgroups).)
   * 通过调用 `Document` 对象的 `createElement` 方法。 将表示元素名称的字符串值传递给 `createElement` 方法。 将返回值强制转换为 `Element`. 接下来，通过调用 `root` 对象的 `appendChild` 方法，并将detail元素对象作为参数传递。 附加到详细信息元素的XML元素对应于表单的动态部分。 以下代码行显示了此应用程序逻辑：

     ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * 通过调用 `Document` 对象的 `createElement` 方法，并传递表示元素名称的字符串值。 将返回值强制转换为 `Element`. 接下来，通过调用其子元素的 `appendChild` 方法，并传递 `Document` 对象的 `createTextNode` 方法作为参数。 指定作为子元素的值显示的字符串值。 最后，通过调用detail元素的 `appendChild` 方法，并将子元素对象作为参数传递。 以下代码行显示了此应用程序逻辑：

     ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * 对所有XML元素重复最后一个子步骤以附加到详细信息元素。 要正确创建用于填充采购订单表单的XML数据源，必须将以下XML元素附加到明细元素中： `txtDescription`， `numQty`、和 `numUnitPrice`.
   * 对用于预填充表单的所有数据项重复前两个子步骤。

1. 转换XML数据源

   * 创建 `javax.xml.transform.Transformer` 对象，方法是调用 `javax.xml.transform.Transformer` 对象的静态 `newInstance` 方法。
   * 创建 `Transformer` 对象，方法是调用 `TransformerFactory` 对象的 `newTransformer` 方法。
   * 创建 `ByteArrayOutputStream` 对象。
   * 创建 `javax.xml.transform.dom.DOMSource` 对象，使用它的构造函数传递 `org.w3c.dom.Document` 步骤1中创建的对象。
   * 创建 `javax.xml.transform.dom.DOMSource` 对象，使用它的构造函数传递 `ByteArrayOutputStream` 对象。
   * 填充Java `ByteArrayOutputStream` 对象，方法是调用 `javax.xml.transform.Transformer` 对象的 `transform` 方法和传递 `javax.xml.transform.dom.DOMSource` 和 `javax.xml.transform.stream.StreamResult` 对象。
   * 创建字节数组并分配 `ByteArrayOutputStream` 对象。
   * 通过调用 `ByteArrayOutputStream` 对象的 `toByteArray` 方法。
   * 创建 `BLOB` 对象，通过调用其构造函数 `setBinaryData` 方法，并传递字节数组。

1. 呈现预填充的表单

   调用 `FormsService` 对象的 `renderPDFForm` 方法并传递以下值：

   * 一个字符串值，它指定窗体设计名称，包括文件扩展名。
   * A `BLOB` 包含要与表单合并的数据的对象。 确保您使用 `BLOB` 在步骤1和步骤2中创建的对象。
   * A `PDFFormRenderSpecc` 存储运行时选项的对象。 有关更多信息，请参阅 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `URLSpec` 包含Forms服务所需的URI值的对象。
   * A `java.util.HashMap` 存储文件附件的对象。 这是一个可选参数，您可以指定 `null` 如果您不想将文件附加到表单。
   * 空的 `com.adobe.idp.services.holders.BLOBHolder` 方法填充的对象。 用于存储渲染的PDF表单。
   * 空的 `javax.xml.rpc.holders.LongHolder` 方法填充的对象。 （此参数将存储表单中的页数）。
   * 空的 `javax.xml.rpc.holders.StringHolder` 方法填充的对象。 （此参数将存储区域设置值）。
   * 空的 `com.adobe.idp.services.holders.FormsResultHolder` 将包含此操作结果的对象。

   此 `renderPDFForm` 方法填充 `com.adobe.idp.services.holders.FormsResultHolder` 作为最后一个参数值传递的对象，该对象具有必须写入客户端Web浏览器的表单数据流。

   * 创建 `FormResult` 对象，方法是获取 `com.adobe.idp.services.holders.FormsResultHolder` 对象的 `value` 数据成员。
   * 创建 `BLOB` 通过调用 `FormsResult` 对象的 `getOutputContent` 方法。
   * 获取的内容类型 `BLOB` 对象(通过调用其 `getContentType` 方法。
   * 设置 `javax.servlet.http.HttpServletResponse` 通过调用对象的内容类型 `setContentType` 方法和传递的内容类型 `BLOB` 对象。
   * 创建 `javax.servlet.ServletOutputStream` 用于通过调用 `javax.servlet.http.HttpServletResponse` 对象的 `getOutputStream` 方法。
   * 创建字节数组，并通过调用 `BLOB` 对象的 `getBinaryData` 方法。 此任务分配 `FormsResult` 对象。
   * 调用 `javax.servlet.http.HttpServletResponse` 对象的 `write` 将表单数据流发送到客户端Web浏览器的方法。 将字节数组传递给 `write` 方法。

   >[!NOTE]
   >
   >此 `renderPDFForm` 方法填充 `com.adobe.idp.services.holders.FormsResultHolder` 作为最后一个参数值传递的对象，该对象具有必须写入客户端Web浏览器的表单数据流。

**另请参阅**

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
