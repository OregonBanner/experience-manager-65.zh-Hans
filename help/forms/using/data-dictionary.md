---
title: 数据字典
seo-title: Data Dictionary
description: 通信管理中的数据字典允许您将后端数据集成到信件中，作为输入用于客户通信。
seo-description: Data dictionary in Correspondence Management lets you integrate back-end data to letters as inputs for use in customer correspondence.
uuid: 178a285e-b4a4-4a36-a2aa-b43ecb0871ed
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: a1a0ad6b-023a-4822-9cce-0618657c3f9d
docset: aem65
feature: Correspondence Management
exl-id: aaed75e6-8849-46a8-b986-896ad729adda
source-git-commit: 10227bcfcfd5a9b0f126fee74dce6ec7842f5e95
workflow-type: tm+mt
source-wordcount: '3840'
ht-degree: 1%

---

# 数据字典{#data-dictionary}

## 简介 {#introduction}

数据字典使企业用户能够使用来自后端数据源的信息，而无需了解其底层数据模型的技术细节。 数据字典由数据字典元素(DDE)组成。 您可以使用这些数据元素将后端数据集成到信件作为输入，以便在客户通信中使用。

数据字典是描述基础数据结构及其关联属性的元数据的独立表示形式。 使用业务词汇创建数据字典。 它可以映射到一个或多个底层数据模型。

数据字典由三种类型的元素组成：简单、复合和集合元素。 简单DDE是一些原始元素，例如字符串、数字、日期和布尔值，它们包含城市名称等信息。 复合DDE包含其他DDE，它们可以是原始类型、复合类型或集合类型。 例如，由街道地址、城市、省/自治区/直辖市、国家/地区和邮政编码组成的地址。 集合是类似的简单或复合DDE的列表。 例如，客户具有多个地点或不同的帐单和送货地址。

通信管理使用后端、客户或根据数据字典的结构存储的收件人特定数据来创建针对不同客户的通信。 例如，可以创建具有友好名称的文档，例如“尊敬的{First Name}”、“先生”。 {姓氏}&quot;.

通常，业务用户不需要了解元数据表示法，如XSD（XML架构）和Java类。 但是，它们通常需要访问这些数据结构和属性才能构建解决方案。

### 数据字典工作流程 {#data-dictionary-workflow}

1. 作者 [创建数据字典](#createdatadictionary) 通过上传架构或从头开始。
1. 作者根据数据字典创建信件及交互式通信，并根据需要关联信件及交互式通信中的数据字典元素。
1. 作者可以下载基于数据字典模式的示例数据XML文件。 作者可以修改示例数据XML文件，该文件可以作为测试数据与数据字典关联。 在信件预览期间也会使用相同的参数。
1. 同时 [预览信件](../../forms/using/create-letter.md#p-types-of-linkage-available-for-each-of-the-fields-p)，作者选择预览包含数据的信件（自定义预览）。 此时会打开书信，其中预填充了作者提供的数据。 这将在创建通信界面中打开。 预览此信件的工程师可以修改此信件中的内容、数据和附件，并可以提交最终信件。 有关创建信件的更多信息，请参阅 [创建通信](../../forms/using/create-letter.md).

## 先决条件 {#prerequisite}

安装 [兼容包](compatibility-package.md) 查看 **数据字典** 上的选项 **Forms** 页面。

## 创建数据字典 {#createdatadictionary}

您可以使用数据字典编辑器创建数据字典，也可以上传XSD架构文件以基于它创建数据字典。 然后，您可以通过添加更多必填信息（包括字段）来扩展数据字典。 无论数据字典是如何创建的，业务流程所有者不需要了解后端系统。 业务流程所有者只需要了解域对象及其定义，即可完成其流程。

>[!NOTE]
>
>对于需要相似元素的多个字母，您可以创建通用数据字典。 但是，如果大数据字典含有大量元素，则在使用数据字典和加载元素（如字母和文档片段）时，可能会导致性能问题。 如果您遇到性能问题，请尝试为不同的字母创建单独的数据字典。

1. 选择 **Forms** > **数据字典**.
1. 点按 **创建数据字典**.
1. 在Properties屏幕中，添加以下内容：

   * **标题：** （可选）输入数据字典的标题。 标题不需要是唯一的，并且可以包含特殊字符和非英语字符。 字母和其他文档片段通过其标题（如果可用）进行引用，例如在缩略图和资产属性中。 引用数据词典时使用了它们的名称，而不是标题。
   * **名称：** 数据字典的唯一名称。 在“名称”字段中，只能输入英语字符、数字和连字符。 “名称”字段会根据“标题”字段自动填充，并且在“标题”字段中输入的特殊字符、空格、数字和非英语字符会被替换为连字符。 虽然“标题”字段中的值会自动复制到“名称”，但您可以编辑该值。

   * **描述**：（可选）数据字典的描述。
   * **标记：** （可选）要创建自定义标记，请在文本字段中输入值，然后按Enter。 您可以在标记的文本字段下方看到您的标记。 保存此文本时，也会创建新添加的标记。
   * **扩展属性**：（可选）点按 **添加字段** 用于指定数据字典的元数据属性。 在属性名称列中，输入唯一的属性名称。 在值列中，输入要与属性关联的值。

   ![德语指定的数据字典属性](do-not-localize/1_ddproperties.png)

1. （可选）要上传数据字典的XSD架构定义，请在“数据字典结构”窗格下点击 **上载XML架构**. 浏览到XSD文件，选择它，然后点按 **打开**. 将根据上载的XML架构创建数据字典。 您需要调整数据字典中元素的显示名称和描述。 要实现此目的，请通过点按元素来选择元素的名称，并在右侧窗格的字段中编辑其描述、显示名称和其他详细信息。

   有关计算的DD元素的详细信息，请参阅 [计算的数据字典元素](#computedddelements).

   >[!NOTE]
   >
   >您可以跳过上载架构文件，并使用用户界面从头开始构建数据字典。 为此，请跳过此步骤并继续后续步骤。

1. 点按 **下一个**.
1. 在“添加属性”屏幕中，将元素添加到数据字典。 如果您已上传架构以获取数据字典的基本结构，则还可以添加/删除元素并编辑其详细信息。

   您可以点按元素右侧的三个圆点，并将元素添加到数据字典结构。

   ![1_2_createanelement](assets/1_2_createanelement.png)

   选择“复合元素”、“收集元素”或“基本元素”。

   * 复合DDE包含其他DDE，它们可以是原始类型、复合类型或集合类型。 例如，由街道地址、城市、省/自治区/直辖市、国家/地区和邮政编码组成的地址。
   * 原始DDE是字符串、数字、日期和布尔值等元素，用于保存城市名称等信息。
   * 集合是类似的简单或复合DDE的列表。 例如，客户具有多个地点或不同的帐单和送货地址。

   以下是创建数据字典的一些规则：

   * 仅复合类型才允许作为数据字典中的顶级DDE。
   * 名称、引用名称和元素类型是数据字典和DDE的必填字段。
   * 引用名称必须是唯一的。
   * 父DDE（复合）不能有两个同名的子项。
   * 枚举仅包含原始字符串类型。

   有关Composite、Collection和Primitive元素以及使用数据字典元素的更多信息，请参阅 [将数据字典元素映射到XML架构](#mappingddetoschema).

   有关数据字典中验证的信息，请参阅 [数据字典编辑器验证](#ddvalidations).

   ![2_adddpropertiesbasic](assets/2_addddpropertiesbasic.png)

1. （可选）选择元素后，您可以在高级选项卡中添加属性（属性）。 您也可以点按 **添加字段** 和扩展DD元素的属性。

   ![3_adddpropertiesadvanced](assets/3_addddpropertiesadvanced.png)

1. （可选）通过点按元素右侧的三个点并选择 **删除**.

   ![4_deleteelement](assets/4_deleteelement.png)

   >[!NOTE]
   >
   >删除具有子节点的复合/收集要素也会删除其子节点。

1. （可选）在“数据字典结构”窗格以及“字段和变量列表”面板中选择一个元素。 更改或添加与元素关联的任何必需属性。
1. 点按 **保存**.

### 创建一个或多个数据字典的副本 {#create-copies-of-one-or-more-data-dictionary}

要快速创建一个或多个具有与现有数据字典类似的属性和元素的数据字典，您可以复制并粘贴它们。

1. 从数据字典列表中，选择适当的数据字典。 UI会显示复制图标。
1. 点按复制。UI将显示“粘贴”图标。
1. 点按粘贴。 将显示“粘贴”对话框。 系统会自动为新数据字典指定名称和标题。
1. 如果需要，请编辑要用于保存数据字典副本的标题和名称。
1. 点按粘贴。 将创建数据字典的副本。 现在，您可以在新建的数据字典中进行所需的更改。

## 请参阅引用数据字典元素的文档片段或文档 {#see-the-document-fragments-or-documents-that-refer-to-a-data-dictionary-element}

在编辑或查看数据字典时，您可以看到数据字典中的哪些元素在文本、条件、字母和交互式通信中被引用。

1. 执行以下操作之一以编辑数据字典：

   * 将鼠标悬停在数据字典上，然后点按编辑。
   * 选择数据字典，然后点按标题中的编辑。
   * 将鼠标悬停在数据字典上并点按选择。 然后点按标题中的编辑。

   或者点击数据字典以查看它。

1. 在数据字典中，点按一个简单元素以将其选定。 复合元素和收藏集元素没有引用。

   除了元素的Basic和Advanced属性外，还显示Lent Content。

1. 点按借出内容。

   “借出内容”选项卡显示如下：文本、条件、信件和交互式通信。 每个标题还会显示对选定元素的引用数量。

1. 点按标题可查看引用该元素的资产的名称。

   ![lentcontent](assets/lentcontent.png)

1. 要查看其他元素的借出内容，请点击元素。
1. 要显示引用该元素的资产，请点按其名称。 浏览器显示资产、信件或交互式通信。

## 使用测试数据 {#working-with-test-data}

1. 在数据字典页面上，点击 **选择**.
1. 点按要为其下载测试数据的数据字典，然后点按 **下载示例XML数据**.
1. 点按 **确定** 在警报消息中。 下载XML文件。
1. 使用记事本或其他XML编辑器打开XML文件。 XML文件的结构与元素中的数据字典和占位符字符串相同。 将占位符字符串替换为要用于测试信件的数据。

   ```xml
   <?xml version="1.0" encoding="UTF-8" standalone="no"?>
   <Company>
   <Name>string</Name>
   <Type>string</Type>
   <HeadOfficeAddress>
   <Street>string</Street>
   <City>string</City>
   <State>string</State>
   <Zip>string</Zip>
   </HeadOfficeAddress>
   <SalesOfficeAddress>
   <Street>string</Street>
   <City>string</City>
   <State>string</State>
   <Zip>string</Zip>
   </SalesOfficeAddress>
   <HeadCount>1.0</HeadCount>
   <CEO>
   <PersonName>
   <FirstName>string</FirstName>
   <MiddleName>string</MiddleName>
   <LastName>string</LastName>
   </PersonName>
   <DOB>string</DOB>
   <CurrAddress>
   <Street>string</Street>
   <City>string</City>
   <State>string</State>
   <Zip>string</Zip>
   </CurrAddress>
   <DOJ>14-04-1973</DOJ>
   <Phone>1.0</Phone>
   </CEO>
   </Company>
   ```

   >[!NOTE]
   >
   >在本例中，XML为收集要素的三个值创建空间，但可以根据需要增加/减少值的数量。

1. 创建数据条目后，您可以在预览包含测试数据的信件时使用此XML文件。

   您可以使用DD添加此测试数据（选择DD并点按上传测试数据并上传此xml文件）。因此，在此之后当您正常预览信件时（非自定义），此XML数据将在信件中使用。 您还可以点按自定义，然后上传此XML。

## 示例 {#samples}

以下代码示例显示了数据字典的实施详细信息。

### 可以上载到数据字典的示例架构 {#sample-schema-that-can-be-uploaded-to-the-data-dictionary}

```xml
<?xml version="1.0" encoding="utf-8"?>
<xs:schema xmlns="DCT" targetNamespace="DCT" xmlns:xs="https://www.w3.org/2001/XMLSchema"
  elementFormDefault="qualified" attributeFormDefault="unqualified">
  <xs:element name="Company">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="Name" type="xs:string"/>
        <xs:element name="Type" type="xs:anySimpleType"/>
        <xs:element name="HeadOfficeAddress" type="Address"/>
        <xs:element name="SalesOfficeAddress" type="Address" minOccurs="0"/>
        <xs:element name="HeadCount" type="xs:integer"/>
        <xs:element name="CEO" type="Employee"/>
        <xs:element name="Workers" type="Employee" maxOccurs="unbounded"/>
      </xs:sequence>
    </xs:complexType>
  </xs:element>
  <xs:complexType name="Employee">
    <xs:complexContent>
      <xs:extension  base="Person">
        <xs:sequence>
          <xs:element name="CurrAddress" type="Address"/>
          <xs:element name="DOJ" type="xs:date"/>
          <xs:element name="Phone" type="xs:integer"/>
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
  <xs:complexType name="Person">
    <xs:sequence>
      <xs:element name="PersonName" type="Name"/>
      <xs:element name="DOB" type="xs:dateTime"/>
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Name">
    <xs:sequence>
      <xs:element name="FirstName" type="xs:string"/>
      <xs:element name="MiddleName" type="xs:string"/>
      <xs:element name="LastName" type="xs:string"/>
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Address">
    <xs:sequence>
      <xs:element name="Street" type="xs:string"/>
      <xs:element name="City" type="xs:string"/>
      <xs:element name="State" type="xs:string"/>
      <xs:element name="Zip" type="xs:string"/>
    </xs:sequence>
  </xs:complexType>
</xs:schema>
```

## 与DDE关联的公共属性 {#common-attributes-associated-with-a-dde}

下表详细列出了与DDE关联的通用属性：

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>名称</td>
   <td>字符串</td>
   <td>必填.<br /> DDE的名称。 它必须是唯一的。</td>
  </tr>
  <tr>
   <td>引用<br /> 名称</td>
   <td>字符串</td>
   <td>必填. DDE的唯一引用名称，允许对DDE的引用独立于对数据字典的层次结构或结构的更改。 使用此名称映射文本模块</td>
  </tr>
  <tr>
   <td>displayname</td>
   <td>字符串</td>
   <td>DDE的可选用户友好名称。</td>
  </tr>
  <tr>
   <td>说明</td>
   <td>字符串</td>
   <td>DDE的说明。</td>
  </tr>
  <tr>
   <td>元素类型</td>
   <td>字符串</td>
   <td>必填. DDE的类型：STRING、NUMBER、DATE、Boolean、COMPOSITE、COLLECTION。</td>
  </tr>
  <tr>
   <td>元素子类型</td>
   <td>字符串</td>
   <td>DDE的子类型： ENUM。 仅允许用于STRING和NUMBER elementType。</td>
  </tr>
  <tr>
   <td>键</td>
   <td>布尔值</td>
   <td>用于指示DDE是否为关键元素的布尔字段。</td>
  </tr>
  <tr>
   <td>已计算</td>
   <td>布尔值</td>
   <td>用于指示是否计算DDE的布尔字段。 计算的DDE值是其他DDE值的函数。 默认情况下，支持jsp表达式。</td>
  </tr>
  <tr>
   <td>表达式</td>
   <td>字符串</td>
   <td>“已计算”DDE的表达式。 默认提供的表达式计算服务支持JSP EL表达式。 您可以使用自定义实施替换表达式服务。</td>
  </tr>
  <tr>
   <td>值集</td>
   <td>列表</td>
   <td>枚举类型DDE的一组允许值。 例如，帐户类型只能有（保存、当前）值。</td>
  </tr>
  <tr>
   <td>extendedProperties</td>
   <td>对象</td>
   <td>添加到DDE的自定义属性映射（用户界面特定或任何其他信息）。</td>
  </tr>
  <tr>
   <td>必填</td>
   <td>布尔值</td>
   <td>该标记指示与数据字典对应的实例数据源必须包含此特定DDE的值。</td>
  </tr>
  <tr>
   <td>捆绑</td>
   <td>绑定元素</td>
   <td>元素的XML或Java绑定。</td>
  </tr>
 </tbody>
</table>

### 计算的数据字典元素 {#computedddelements}

数据字典还可以包括计算元素。 计算的数据字典元素始终与表达式关联。 此表达式的计算结果是在运行时获取数据字典元素的值。 计算的DDE值是其他DDE值或文字的函数。 默认情况下，支持JSP表达式语言(EL)表达式。 EL表达式使用${ }个字符，有效的表达式可以包括文本、运算符、变量（数据字典元素引用）和函数调用。 在表达式中引用数据字典元素时，使用DDE的引用名称。 引用名称对于数据字典中的每个数据字典元素都是唯一的。

计算的DDE PersonFullName可以与EL连接表达式（如$）关联{PersonFirstName} ${PersonLastName}.

## XSD和数据字典之间的数据类型映射 {#data-type-mapping-between-xsd-and-data-dictionary-br}

导出XSD需要特定数据映射，下表对此进行了详细说明。 DDI列指示DDI中可用的DDE值的类型。

<table>
 <tbody>
  <tr>
   <td>XSD <br /> </td>
   <td><p>数据字典 <br /> </p> </td>
   <td>DDI（实例值数据类型）<br /> </p> </td>
  </tr>
  <tr>
   <td><p>xs：元素类型 — 复合类型<br /> </p> </td>
   <td>类型为“复合”的DDE<br /> </p> </td>
   <td>java.util.Map<br /> </td>
  </tr>
  <tr>
   <td><p>xs：元素，其中maxOccurs &gt; 1<br /> </p> </td>
   <td>DDE类型 — 收藏集 — <br /> 在捕获来自父COLLECTION节点的信息的COLLECTION DDE旁边创建一个DDE节点。 对于简单/复合数据类型的集合，也将创建相同的变量。 只要您拥有类型组合的COLLECTION，数据字典树就会捕获为捕获类型信息而创建的DDE子项中的组成字段。<br /> - DDE（收藏集）<br /> - DDE（类型信息的复合）<br /> - DDE(STRING)字段1<br /> - DDE(STRING)字段2<br /> <br /> </p> </td>
   <td>java.util.List<br /> </td>
  </tr>
  <tr>
   <td>类型的属性 — xs：id <br /> </p> </td>
   <td>类型为STRING的DDE <br /> </td>
   <td>java.lang.String<br /> </td>
  </tr>
  <tr>
   <td>xs：attribute /xs：element类型 — xs：string</p> </td>
   <td>类型为STRING的DDE<br /> </td>
   <td>java.lang.String<br /> </td>
  </tr>
  <tr>
   <td>xs：attribute /xs：element类型 — xs：布尔值 <br /> </td>
   <td>DDE类型 — 布尔型 <br /> </td>
   <td>java.lang.Boolean<br /> </td>
  </tr>
  <tr>
   <td>xs：attribute /xs：element类型 — xs：date </td>
   <td>DDE类型 — 日期 </td>
   <td>java.lang.String</td>
  </tr>
  <tr>
   <td>xs：attribute /xs：element类型 — xs：integer </td>
   <td>DDE类型 — 数字 </td>
   <td>java.lang.Double</td>
  </tr>
  <tr>
   <td>xs：attribute /xs：element类型 — xs：long</td>
   <td>DDE类型 — 数字 </td>
   <td>java.lang.Double</td>
  </tr>
  <tr>
   <td>xs：attribute /xs：element类型 — xs：double</td>
   <td>DDE类型 — 数字 </td>
   <td>java.lang.Double</td>
  </tr>
  <tr>
   <td>枚举类型和baseType的元素 — xs：string</td>
   <td>DDE /<br /> 类型 — 字符串<br /> 子类型 — 枚举<br /> valueSet - ENUM允许的值<br /> </td>
   <td>java.lang.String</td>
  </tr>
 </tbody>
</table>

## 从数据字典下载示例数据文件 {#download-a-sample-data-file-from-a-data-dictionary}

创建数据字典后，您可以将其下载为XML示例数据文件，以便在其中输入文本。

1. 在“数据字典”页面中，点按 **选择** 然后点按数据字典以将其选定。
1. 选择 **下载示例XML数据**.
1. 点按 **确定** 在警报消息中。

   通信管理会根据所选数据字典的结构创建一个XML文件，然后将该文件下载到具有此名称的计算机 &lt;data-dictionary-name>-Sampledata。 现在，您可以在XML或文本编辑器中编辑此文件，以输入数据，同时 [创建书信](../../forms/using/create-letter.md).

## 元数据国际化 {#internationalization-of-meta-data}

如果想要以不同语言向客户发送相同的信件，则可以将数据字典和数据字典元素的显示名称、描述和枚举值集本地化。

### 本地化数据字典 {#localize-data-dictionary}

1. 在数据字典页面上，点击 **选择** 然后点按数据字典以将其选定。
1. 点按 **下载本地化数据**.
1. 点按 **确定** 在警报中。 通信管理会将名为DataDictionary的zip文件下载到您的计算机 — &lt;ddname>.zip.
1. Zip文件包含.properties文件。 此文件定义下载的数据字典。 属性文件的内容类似于以下内容：

   ```ini
   #Wed May 20 16:06:23 BST 2015
   DataDictionary.EmployeeDD.description=
   DataDictionary.EmployeeDD.displayName=EmployeeDataDictionary
   DataDictionaryElement.name.description=
   DataDictionaryElement.name.displayName=name
   DataDictionaryElement.person.description=
   DataDictionaryElement.person.displayName=person
   ```

   属性文件的结构分别定义一行，用于描述数据字典以及数据字典中每个数据字典元素的显示名称。 此外，属性文件为每个数据字典元素设置的枚举值定义一行。 与数据字典一样，相应的属性文件可以有多个数据字典元素定义。 此外，文件可以包含一个或多个枚举值集的定义。

1. 要更新其他区域设置的.properties文件，请更新文件中的显示名称和说明值。 为要本地化的每种语言创建更多文件实例。 仅支持法语、德语、日语和英语。

1. 使用以下名称保存不同的已更新属性文件：

   _fr_FR.properties法语

   _de_DE.properties德语

   _ja_JA.properties日语

   _en_EN.properties英语

1. 将.properties文件（或多个区域设置的文件）存档到一个.zip文件中。

1. 在“数据字典”页面中，选择 **更多** > **上传本地化数据** 并选择zip文件以及本地化的属性文件。
1. 要查看本地化更改，请更改您的浏览器区域设置。

## 数据字典验证 {#ddvalidations}

数据字典编辑器在创建或更新数据字典时强制进行以下验证。

* 仅复合类型才允许作为数据字典中的顶层元素。
* 叶层不允许使用复合元素和收集元素。 叶级别只允许使用原始(String、Date、Number、Boolean)元素。 此验证可确保没有没有没有子DDE的组合和收集要素。
* 上传XSD文件以创建数据字典时，数据字典编辑器会提示输入顶级元素（如果存在）以创建数据字典。
* 名称是数据字典的唯一必需参数。
* 父DDE（复合）不能有两个同名的子项
* 确保仅在将DDE标记为非必需参数时将其标记为已计算。 无法计算所需的元素，也无法计算所需的元素。 此外，集合和复合元素不能是计算元素。
* 确保仅在未计算DDE时将其标记为必需。 它还确保它不是表示收集类型的“collectionElement”（即收集要素的唯一子项）。
* 数据字典或DDE的extendedProperties中不允许使用空键或重复键。
* 请勿在扩展属性的键或值中使用冒号(：)或垂直条(|)字符。 对于这些禁止使用的字符，无法进行验证。

在数据字典级别应用的验证

* 数据字典名称不能为空。
* 数据字典名称必须只包含字母数字字符。
* 数据字典中的子元素列表不得为Null或为空。
* 数据字典不得包含多个顶层数据字典元素。
* 仅复合类型才允许作为数据字典中的顶层元素。

在数据字典元素级别应用的验证。

* 所有DDE名称不能为Null且不能包含空格。
* 所有DDE都必须具有“非null/非null”元素类型。
* 所有DDE引用名称不能为Null。
* 所有DDE引用名称必须是唯一的。
* 所有DDE引用必须只包含字母数字字符和“_”。
* 所有DDE显示名称必须只包含字母数字字符和“_”。
* 叶层不允许使用复合元素和收集元素。 叶级别只允许使用原始(String、Date、Number、Boolean)元素。 此验证可确保没有没有没有子DDE的组合和收集要素。
* 复合父DDE不能有两个同名的子元素。
* ENUM子类型仅用于String和Number元素。
* 无法计算集合和复合元素。
* DDE不能既为已计算又为必需。
* 计算的DDE必须包含有效的表达式。
* 计算的DDE不能有XML绑定。
* 不能计算或要求表示集合DDE类型的DDE。
* 子类型ENUM的DDE不得包含null或空值集。
* 集合DDE的XML绑定不得映射到属性。
* XML绑定语法必须有效，例如，只显示一个@，仅在后面跟有属性名称时才允许@。

## 将数据字典元素映射到XML架构 {#mappingddetoschema}

您可以从XML架构创建数据字典，也可以使用数据字典用户界面构建数据字典。 数据字典中的所有数据字典元素(DDE)都有一个XML绑定字段，用于存储DDE与XML架构中某个元素的绑定。 每个DDE中的绑定都相对于父DDE。

以下详细列出了示例模型和代码示例，这些示例显示了数据字典的实施详细信息。

## 映射简单（原始）元素 {#mapping-simple-primitive-elements}

原始DDE表示具有原子性质的字段或属性。 在复杂类型（复合DDE）或重复元素（集合DDE）的范围之外定义的基元DDE可以存储在XML Schema中的任何位置。 与原始DDE对应的数据的位置不依赖于其父DDE的映射。 原始DDE使用XML绑定字段中的映射信息来确定其值，并且映射将转换为以下内容之一：

* 属性
* 元素
* 文本上下文
* 无（忽略的DDE）

以下示例显示了一个简单的架构。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="https://www.w3.org/2001/XMLSchema">
  <xs:element name='age' type='integer'/>
  <xs:element name='price' type='decimal'/>
</xs:schema>
```

| **数据字典元素** | **默认XML绑定** |
|---|---|
| 年龄 | /年龄 |
| 价格 | /价格 |

### 映射复合元素 {#mapping-composite-elements}

复合元素不支持绑定，如果提供了绑定，则会忽略该绑定。 原始类型的所有组成子DDE的绑定必须是绝对的。 允许复合DDE的子元素的绝对映射，在XPath绑定方面提供了更大的灵活性。 将复合DDE映射到XML架构中的复杂类型元素会限制其子元素的绑定范围。

以下示例显示了注释的架构。

```xml
<xs:element name="note">
    <xs:complexType>
        <xs:sequence>
            <xs:element name="to" type="xs:string"/>
            <xs:element name="from" type="xs:string"/>
            <xs:element name="heading" type="xs:string"/>
            <xs:element name="body" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:element>
```

<table>
 <tbody>
  <tr>
   <td><strong>数据字典元素</strong></td>
   <td><strong>默认XML绑定</strong></td>
  </tr>
  <tr>
   <td>注意</td>
   <td>empty(null)<br /> </td>
  </tr>
  <tr>
   <td>到</td>
   <td>/note/to</td>
  </tr>
  <tr>
   <td>从</td>
   <td>/note/from</td>
  </tr>
  <tr>
   <td>标题</td>
   <td>/note/heading</td>
  </tr>
  <tr>
   <td>正文</td>
   <td>/note/body</td>
  </tr>
 </tbody>
</table>

### 映射收集要素 {#mapping-collection-elements}

收集要素仅映射到基数> 1的另一个收集要素。 集合DDE的子DDE具有与其父级的XML绑定相关的相对（本地）XML绑定。 由于集合元素的子DDE必须与父元素的子DDE具有相同的基数，因此要求相对绑定确保基数约束，以便子DDE不会指向非重复的XML架构元素。 在下面的示例中，“TokenID”的基数必须与“Tokens”相同，后者是其父集合DDE。

将集合DDE映射到XML架构元素时：

* 与Collection元素对应的DDE的绑定必须是绝对XPath

* 没有为表示收集元素类型的DDE提供绑定。 如果提供，则将忽略绑定。

* “收集”元素的所有子DDE的绑定必须相对于父“收集”元素。

以下XML架构声明了一个名为Tokens的元素，其maxOccurs属性为“unbounded”。 因此，令牌是一个收集元素。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Root>
  <Tokens>
    <TokenID>string</TokenID>
    <TokenText>
      <TextHeading>string</TextHeading>
      <TextBody>string</TextBody>
    </TokenText>
  </Tokens>
  <Tokens>
    <TokenID>string</TokenID>
    <TokenText>
      <TextHeading>string</TextHeading>
      <TextBody>string</TextBody>
    </TokenText>
  </Tokens>
  <Tokens>
    <TokenID>string</TokenID>
    <TokenText>
      <TextHeading>string</TextHeading>
      <TextBody>string</TextBody>
    </TokenText>
  </Tokens>
</Root>
```

与此示例关联的Token.xsd应为：

```xml
<xs:element name="Root">
  <xs:complexType>
    <xs:sequence>
      <xs:element name="Tokens" type="TokenType" maxOccurs="unbounded"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>

<xs:complexType name="TokenType">
  <xs:sequence>
    <xs:element name="TokenID" type="xs:string"/>
    <xs:element name="TokenText">
      <xs:complexType>
        <xs:sequence>
          <xs:element name="TextHeading" type="xs:string"/>
          <xs:element name="TextBody" type="xs:string"/>
        </xs:sequence>
      </xs:complexType>
    </xs:element>
  </xs:sequence>
</xs:complexType>
```

| **数据字典元素** | **默认XML绑定** |
|---|---|
| 根 | empty(null) |
| 令牌 | /Root/Tokens |
| 复合 | empty(null) |
| 令牌ID | 令牌ID |
| 令牌文本 | empty(null) |
| 令牌标题 | 令牌文本/文本标题 |
| 令牌主体 | 令牌文本/文本正文 |
