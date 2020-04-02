---
title: 使用可流动布局预填充表单
seo-title: 使用可流动布局预填充表单
description: 'null'
seo-description: 'null'
uuid: 93ccb496-e1c2-4b79-8e89-7a2abfce1537
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 30a12fc6-07b8-4c7c-b9e2-caa2bec0ac48
translation-type: tm+mt
source-git-commit: ebb60e79aa7fb45e059e2d2451f6d549cd24b8b0

---


# 使用可流动布局预填充表单 {#prepopulating-forms-with-flowable-layouts1}

## 使用可流动布局预填充表单 {#prepopulating-forms-with-flowable-layouts2}

预填充表单可向呈现的表单中的用户显示数据。 例如，假定用户使用用户名和口令登录到网站。 如果身份验证成功，则客户端应用程序将查询数据库以获取用户信息。 数据将合并到表单中，然后表单呈现给用户。 因此，用户能够在表单中视图个性化数据。

预填充表单具有以下优点：

* 使用户能够视图表单中的自定义数据。
* 减少用户填写表单时的键入量。
* 通过控制放置数据的位置来确保数据的完整性。

以下两个XML数据源可以预填充表单：

* XDP数据源，它是符合XFA语法（或XFDF数据以预填充使用Acrobat创建的表单）的XML。
* 一个任意XML数据源，它包含与表单的字段名称相匹配的名称／值对（本节中的示例使用任意XML数据源）。

要预填充的每个表单字段都必须存在XML元素。 XML元素名称必须与字段名称匹配。 如果XML元素与表单字段不对应，或XML元素名称与字段名称不匹配，则忽略该元素。 只要指定了所有XML元素，就不必与XML元素的显示顺序匹配。

预填充已包含数据的表单时，必须指定XML数据源中已显示的数据。 假定一个包含10个字段的表单在四个字段中包含数据。 接下来，假设您要预填充其余六个字段。 在这种情况下，必须在用于预填充表单的XML数据源中指定10个XML元素。 如果仅指定六个元素，则原始的四个字段为空。

例如，您可以预填充表单，如示例确认表单。 (请参阅渲染交互式PDF表单 [中的“确认表单](/help/forms/developing/rendering-interactive-pdf-forms.md)”。)

要预填充示例确认表单，您必须创建一个XML数据源，该数据源包含三个与表单中三个字段匹配的XML元素。 此表单包含以下三个字段： `FirstName`、 `LastName`和 `Amount`。 第一步是创建一个XML数据源，它包含与表单设计中的字段相匹配的XML元素。 下一步是为XML元素分配数据值，如以下XML代码所示。

```as3
     <Untitled>
         <FirstName>Jerry</FirstName>
         <LastName>Johnson</LastName>
         <Amount>250000</Amount>
     </Untitled>
```

在您用此XML数据源预填充确认表单，然后渲染表单后，将显示您分配给XML元素的数据值，如下图所示。

![pf_pf_confirmxml3](assets/pf_pf_confirmxml3.png)

### 使用可流动布局预填充表单 {#prepopulating_forms_with_flowable_layouts-1}

具有可流动布局的表单可用于向用户显示未确定数量的数据。 由于表单的布局会自动调整为合并后的数据量，因此您无需为表单预先确定固定布局或页数，就像处理具有固定布局的表单一样。

通常，表单中填充了在运行时获取的数据。 因此，您可以通过创建内存中的XML数据源并将数据直接放入内存中的XML数据源来预填充表单。

考虑基于Web的应用程序，如在线商店。 在线购物者完成购买项目后，所有购买的项目将放入用于预填充表单的内存中XML数据源中。 下图显示了此过程，如图后的表中所述。

![pf_pf_finsrv_webapp_v1](assets/pf_pf_finsrv_webapp_v1.png)

下表介绍了此图中的步骤。

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
   <td><p>用户从基于Web的在线商店购买物品。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>用户完成购买项目并单击“提交”按钮后，将创建内存中的XML数据源。 购买的物品和用户信息将放入内存中的XML数据源中。 </p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>XML数据源用于预填充采购订单表单（下表显示了此表单的示例）。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>采购订单表将呈现给客户端Web浏览器。 </p></td>
  </tr>
 </tbody>
</table>

下图显示了采购订单表单的示例。 表中的信息可以根据XML数据中的记录数进行调整。

![pf_pf_poform](assets/pf_pf_poform.png)

>[!NOTE]
>
>表单可以预填充来自其他来源的数据，如企业数据库或外部应用程序。

### 表单设计注意事项 {#form-design-considerations}

具有可流动布局的表单基于在Designer中创建的表单设计。 表单设计指定一组布局、表示和数据捕获规则，包括基于用户输入计算值。 在表单中输入数据时，会应用这些规则。 添加到表单的字段是表单设计中的子表单。 例如，在上图所示的采购订单表单中，每行都是子表单。 有关创建包含子表单的表单设计的信息，请参 [阅创建具有可流式布局的采购订单表单](https://www.adobe.com/go/learn_aemforms_qs_poformflowable_9)。

### 了解数据子组 {#understanding-data-subgroups}

XML数据源用于预填充具有固定布局和可流式布局的表单。 但是，区别在于，使用可流式布局预填充表单的XML数据源包含用于预填充表单中重复的子表单的重复XML元素。 这些重复的XML元素称为数据子组。

用于预填充上图所示采购订单表单的XML数据源包含四个重复数据子组。 每个数据子组对应于购买的项目。 购买的物品包括显示器、台灯、电话和通讯簿。

以下XML数据源用于预填充采购订单表单。

```as3
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

请注意，每个数据子组都包含四个与此信息对应的XML元素：

* 项目部件号
* 项目说明
* 项目数量
* 单价

数据子组的父XML元素的名称必须与位于表单设计中的子表单的名称匹配。 例如，在上一个图中，请注意数据子组的父XML元素的名称是 `detail`。 这与位于采购订单表单所基于的表单设计中的子表单的名称相对应。 如果数据子组的父XML元素的名称与子表单的名称不匹配，则不会预填充服务器端表单。

每个数据子组必须包含与子表单中的字段名称匹配的XML元素。 位于 `detail` 表单设计中的子表单包含以下字段：

* txtPartNum
* txtDescription
* numQty
* numUnitPrice

>[!NOTE]
>
>如果尝试用包含重复XML元素的数据源预填充表单，并将选项设置为 `RenderAtClient``No`，则只有第一条数据记录会合并到表单中。 要确保所有数据记录都合并到表单中，请将 `RenderAtClient` 设置为 `Yes`。 有关此选项的信 `RenderAtClient` 息，请参阅 [在客户端渲染表单](/help/forms/developing/rendering-forms-client.md)。

>[!NOTE]
>
>有关Forms服务的详细信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary-of-steps}

要使用可流式布局预填充表单，请执行以下任务:

1. 包括项目文件。
1. 创建内存中的XML数据源。
1. 转换XML数据源。
1. 渲染预填充的表单。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建内存中的XML数据源**

您可以使用 `org.w3c.dom` 类创建内存中的XML数据源，以用可流式布局预填充表单。 必须将数据放入符合表单的XML数据源中。 有关具有可流式布局的表单与XML数据源之间关系的信息，请参阅了 [解数据子组](#understanding-data-subgroups)。

**转换XML数据源**

使用类创建的内存中XML数据源可 `org.w3c.dom` 以转换为对象，然 `com.adobe.idp.Document` 后才能用于预填充表单。 内存中的XML数据源可以使用Java XML转换类进行转换。

>[!NOTE]
>
>如果使用Forms服务的WSDL预填充表单，则必须将对象转 `org.w3c.dom.Document` 换为对 `BLOB` 象。

**渲染预填充的表单**

您可以像渲染其他表单一样渲染预填充的表单。 唯一的区别是您使用包 `com.adobe.idp.Document` 含XML数据源的对象预填充表单。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速开始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[渲染交互式PDF表单](/help/forms/developing/rendering-interactive-pdf-forms.md)

[创建呈现表单的Web 应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API预填充表单 {#prepopulating-forms-using-the-java-api}

要使用Forms API(Java)预填充具有可流式布局的表单，请执行以下步骤：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar。 有关这些文件的位置的信息，请参 [阅包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

1. 创建内存中的XML数据源

   * 通过调用 `DocumentBuilderFactory` 类的方法创建 `DocumentBuilderFactory` 一个Java `newInstance` 对象。
   * 通过调 `DocumentBuilder` 用对象的方 `DocumentBuilderFactory` 法创建Java对 `newDocumentBuilder` 象。
   * 调用对 `DocumentBuilder` 象的方 `newDocument` 法来实例化对 `org.w3c.dom.Document` 象。
   * 通过调用对象的方法创建XML数据源 `org.w3c.dom.Document` 的根元 `createElement` 素。 这将创建 `Element` 一个表示根元素的对象。 将表示元素名称的字符串值传递给方 `createElement` 法。 将返回值转换为 `Element`。 接下来，通过调用对象的方法将根元素追加 `Document` 到文档中，并 `appendChild` 将根元素对象作为参数传递。 下面几行代码显示了此应用程序逻辑：

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * 通过调用对象的方法创建XML数据源 `Document` 的头元 `createElement` 素。 将表示元素名称的字符串值传递给方 `createElement` 法。 将返回值转换为 `Element`。 接下来，通过调用对象的方法将头元素追加到根元 `root` 素，并 `appendChild` 将头元素对象作为参数传递。 附加到标题元素的XML元素与表单的静态部分相对应。 以下几行代码显示此应用程序逻辑：

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * 通过调用对象的方法创建属于标题元素的 `Document` 子元素，并传 `createElement` 递表示元素名称的字符串值。 将返回值转换为 `Element`。 接下来，通过调用子元素的方法为其设置一个 `appendChild` 值，并将对象的方 `Document` 法作为 `createTextNode` 参数进行传递。 指定一个字符串值，它显示为子元素的值。 最后，通过调用标题元素的方法将子元素追加到标题元素，并 `appendChild` 将子元素对象作为参数传递。 以下几行代码显示此应用程序逻辑：

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`


   * 通过重复表单静态部分中显示的每个字段的最后一个子步骤，将所有剩余元素添加到标题元素中（在XML数据源图中，这些字段显示在A节中）。(请参阅 [了解数据子组](#understanding-data-subgroups)。)
   * 通过调用对象的方法创建XML数据源的 `Document` 详细信息元 `createElement` 素。 将表示元素名称的字符串值传递给方 `createElement` 法。 将返回值转换为 `Element`。 接下来，通过调用对象的方法将detail元素追加到根元 `root` 素，并 `appendChild` 将detail元素对象作为参数传递。 附加到详细元素的XML元素与表单的动态部分相对应。 以下几行代码显示此应用程序逻辑：

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * 通过调用对象的方法创建属于detail元素的子元 `Document` 素，并传 `createElement` 递表示元素名称的字符串值。 将返回值转换为 `Element`。 接下来，通过调用子元素的方法为其设置一个 `appendChild` 值，并将对象的方 `Document` 法作为 `createTextNode` 参数进行传递。 指定一个字符串值，它显示为子元素的值。 最后，通过调用detail元素的方法将子元素追加到detail元素，并将 `appendChild` 子元素对象作为参数传递。 以下几行代码显示此应用程序逻辑：

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * 对所有XML元素重复最后一个子步骤，以附加到detail元素。 要正确创建用于填充采购订单表单的XML数据源，您必须在详细信息元素后面附加以下XML元素： `txtDescription`、 `numQty`和 `numUnitPrice`。
   * 对用于预填充表单的所有数据项重复最后两个子步骤。

1. 转换XML数据源

   * 通过 `javax.xml.transform.Transformer` 调用对象的静态 `javax.xml.transform.Transformer` 方法创建对 `newInstance` 象。
   * 通过 `Transformer` 调用对象的方 `TransformerFactory` 法创建对 `newTransformer` 象。
   * 使用对 `ByteArrayOutputStream` 象的构造函数创建对象。
   * 通过使用 `javax.xml.transform.dom.DOMSource` 其构造函数并传递在步骤1中创 `org.w3c.dom.Document` 建的对象来创建对象。
   * 使用对 `javax.xml.transform.dom.DOMSource` 象的构造函数并传递该对象来创建 `ByteArrayOutputStream` 对象。
   * 通过调用 `ByteArrayOutputStream` 对象的方法并传 `javax.xml.transform.Transformer` 递对象和对象来填 `transform` 充Java对 `javax.xml.transform.dom.DOMSource``javax.xml.transform.stream.StreamResult` 象。
   * 创建一个字节数组，并将对象的大 `ByteArrayOutputStream` 小分配给该字节数组。
   * 通过调用对象的方法 `ByteArrayOutputStream` 填充字节数 `toByteArray` 组。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递字节数组来创建对象。

1. 渲染预填充的表单

   调用对 `FormsServiceClient` 象的方 `renderPDFForm` 法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。
   * 包含 `com.adobe.idp.Document` 要与表单合并的数据的对象。 确保使用在步骤1 `com.adobe.idp.Document` 和步骤2中创建的对象。
   * 存 `PDFFormRenderSpec` 储运行时选项的对象。
   * 包 `URLSpec` 含Forms服务所需的URI值的对象。
   * 存储 `java.util.HashMap` 文件附件的对象。 这是一个可选参数，您可 `null` 以指定是否不想将文件附加到表单。
   该方 `renderPDFForm` 法返回一个对 `FormsResult` 象，该对象包含必须写入客户端Web浏览器的表单数据流。

   * 创建一 `javax.servlet.ServletOutputStream` 个对象，用于将表单数据流发送到客户端Web浏览器。
   * 通过 `com.adobe.idp.Document` 调用对象的方 `FormsResult` 法创建对 `getOutputContent` 象。
   * 通过 `java.io.InputStream` 调用对象的方 `com.adobe.idp.Document` 法创建对 `getInputStream` 象。
   * 通过调用对象的方法并将字节数组作为参数传递，创 `InputStream` 建一个用 `read` 表单数据流填充它的字节数组。
   * 调用对 `javax.servlet.ServletOutputStream` 象的方 `write` 法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给该 `write` 方法。


**另请参阅**

[快速开始（SOAP模式）:使用Java API使用可流动布局预填充表单](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API预填充表单 {#prepopulating-forms-using-the-web-service-api}

要使用Forms API（Web服务）预填充具有可流式布局的表单，请执行以下步骤：

1. 包括项目文件

   * 创建使用Forms服务WSDL的Java代理类。 (请参 [阅使用Apache Axis创建Java代理类](/help/forms/developing/invoking-aem-forms-using-web.md#creating-java-proxy-classes-using-apache-axis)。)
   * 将Java代理类包含到类路径中。

1. 创建内存中的XML数据源

   * 通过调用 `DocumentBuilderFactory` 类的方法创建 `DocumentBuilderFactory` 一个Java `newInstance` 对象。
   * 通过调 `DocumentBuilder` 用对象的方 `DocumentBuilderFactory` 法创建Java对 `newDocumentBuilder` 象。
   * 调用对 `DocumentBuilder` 象的方 `newDocument` 法来实例化对 `org.w3c.dom.Document` 象。
   * 通过调用对象的方法创建XML数据源 `org.w3c.dom.Document` 的根元 `createElement` 素。 这将创建 `Element` 一个表示根元素的对象。 将表示元素名称的字符串值传递给方 `createElement` 法。 将返回值转换为 `Element`。 接下来，通过调用对象的方法将根元素追加 `Document` 到文档中，并 `appendChild` 将根元素对象作为参数传递。 以下几行代码显示此应用程序逻辑：

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * 通过调用对象的方法创建XML数据源 `Document` 的头元 `createElement` 素。 将表示元素名称的字符串值传递给方 `createElement` 法。 将返回值转换为 `Element`。 接下来，通过调用对象的方法将头元素追加到根元 `root` 素，并 `appendChild` 将头元素对象作为参数传递。 附加到标题元素的XML元素与表单的静态部分相对应。 以下几行代码显示此应用程序逻辑：

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * 通过调用对象的方法创建属于标题元素的 `Document` 子元素，并传 `createElement` 递表示元素名称的字符串值。 将返回值转换为 `Element`。 接下来，通过调用子元素的方法为其设置一个 `appendChild` 值，并将对象的方 `Document` 法作为 `createTextNode` 参数进行传递。 指定一个字符串值，它显示为子元素的值。 最后，通过调用标题元素的方法将子元素追加到标题元素，并 `appendChild` 将子元素对象作为参数传递。 下面几行代码显示了此应用程序逻辑：

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`

   * 通过重复表单静态部分中显示的每个字段的最后一个子步骤，将所有剩余元素添加到标题元素中（在XML数据源图中，这些字段显示在A节中）。(请参阅 [了解数据子组](#understanding-data-subgroups)。)
   * 通过调用对象的方法创建XML数据源的 `Document` 详细信息元 `createElement` 素。 将表示元素名称的字符串值传递给方 `createElement` 法。 将返回值转换为 `Element`。 接下来，通过调用对象的方法将detail元素追加到根元 `root` 素，并 `appendChild` 将detail元素对象作为参数传递。 附加到详细元素的XML元素与表单的动态部分相对应。 下面几行代码显示了此应用程序逻辑：

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * 通过调用对象的方法创建属于detail元素的子元 `Document` 素，并传 `createElement` 递表示元素名称的字符串值。 将返回值转换为 `Element`。 接下来，通过调用子元素的方法为其设置一个 `appendChild` 值，并将对象的方 `Document` 法作为 `createTextNode` 参数进行传递。 指定一个字符串值，它显示为子元素的值。 最后，通过调用detail元素的方法将子元素追加到detail元素，并将 `appendChild` 子元素对象作为参数传递。 下面几行代码显示了此应用程序逻辑：

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * 对所有XML元素重复最后一个子步骤，以附加到detail元素。 要正确创建用于填充采购订单表单的XML数据源，您必须在详细信息元素后面附加以下XML元素： `txtDescription`、 `numQty`和 `numUnitPrice`。
   * 对用于预填充表单的所有数据项重复最后两个子步骤。

1. 转换XML数据源

   * 通过 `javax.xml.transform.Transformer` 调用对象的静态 `javax.xml.transform.Transformer` 方法创建对 `newInstance` 象。
   * 通过 `Transformer` 调用对象的方 `TransformerFactory` 法创建对 `newTransformer` 象。
   * 使用对 `ByteArrayOutputStream` 象的构造函数创建对象。
   * 通过使用 `javax.xml.transform.dom.DOMSource` 其构造函数并传递在步骤1中创 `org.w3c.dom.Document` 建的对象来创建对象。
   * 使用对 `javax.xml.transform.dom.DOMSource` 象的构造函数并传递该对象来创建 `ByteArrayOutputStream` 对象。
   * 通过调用 `ByteArrayOutputStream` 对象的方法并传 `javax.xml.transform.Transformer` 递对象和对象来填 `transform` 充Java对 `javax.xml.transform.dom.DOMSource``javax.xml.transform.stream.StreamResult` 象。
   * 创建一个字节数组，并将对象的大 `ByteArrayOutputStream` 小分配给该字节数组。
   * 通过调用对象的方法 `ByteArrayOutputStream` 填充字节数 `toByteArray` 组。
   * 使用对 `BLOB` 象的构造函数创建对象，调用其方 `setBinaryData` 法并传递字节数组。

1. 渲染预填充的表单

   调用对 `FormsService` 象的方 `renderPDFForm` 法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。
   * 包含 `BLOB` 要与表单合并的数据的对象。 确保您使用在 `BLOB` 步骤1和步骤2中创建的对象。
   * 存 `PDFFormRenderSpecc` 储运行时选项的对象。 有关详细信息，请参 [阅AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 包 `URLSpec` 含Forms服务所需的URI值的对象。
   * 存储 `java.util.HashMap` 文件附件的对象。 这是一个可选参数，您可 `null` 以指定是否不想将文件附加到表单。
   * 由方 `com.adobe.idp.services.holders.BLOBHolder` 法填充的空对象。 它用于存储渲染的PDF表单。
   * 由方 `javax.xml.rpc.holders.LongHolder` 法填充的空对象。 （此参数将存储表单中的页数）。
   * 由方 `javax.xml.rpc.holders.StringHolder` 法填充的空对象。 （此参数将存储区域设置值）。
   * 将包含 `com.adobe.idp.services.holders.FormsResultHolder` 此操作结果的空对象。
   该方 `renderPDFForm` 法使用必 `com.adobe.idp.services.holders.FormsResultHolder` 须写入客户端Web浏览器的表单数据流填充作为最后一个参数值传递的对象。

   * 通过 `FormResult` 获取对象数据成员的 `com.adobe.idp.services.holders.FormsResultHolder` 值来创建 `value` 对象。
   * 通过调 `BLOB` 用对象的方法创建包含表 `FormsResult` 单数据的对 `getOutputContent` 象。
   * 通过调用对象的方 `BLOB` 法获取对象的内容 `getContentType` 类型。
   * 通过调 `javax.servlet.http.HttpServletResponse` 用对象的方法并传递对象的 `setContentType` 内容类型来设置对象的内容 `BLOB` 类型。
   * 创建一 `javax.servlet.ServletOutputStream` 个对象，该对象通过调用该对象的方法将表单数据流写入客户端Web `javax.servlet.http.HttpServletResponse` 浏览器 `getOutputStream` 中。
   * 创建一个字节数组，并通过调用对象的 `BLOB` 方法填充该 `getBinaryData` 数组。 此任务将对象的内 `FormsResult` 容指定给字节数组。
   * 调用对 `javax.servlet.http.HttpServletResponse` 象的方 `write` 法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给该 `write` 方法。
   >[!NOTE]
   >
   >该方 `renderPDFForm` 法使用必 `com.adobe.idp.services.holders.FormsResultHolder` 须写入客户端Web浏览器的表单数据流填充作为最后一个参数值传递的对象。

**另请参阅**

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

