---
title: 数据字典
seo-title: 数据字典
description: Corrence Management中的数据字典允许您将后端数据与字母集成为输入，以用于客户通信。
seo-description: Corrence Management中的数据字典允许您将后端数据与字母集成为输入，以用于客户通信。
uuid: 178a285e-b4a4-4a36-a2aa-b43ecb0871ed
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: a1a0ad6b-023a-4822-9cce-0618657c3f9d
docset: aem65
translation-type: tm+mt
source-git-commit: 5831c173114a5a6f741e0721b55d85a583e52f78

---


# 数据字典{#data-dictionary}

## 简介 {#introduction}

数据字典使商业用户能够使用来自后端数据源的信息，而无需了解有关其基础数据模型的技术详细信息。 数据字典由数据字典元素(DDE)组成。 您使用这些数据元素将后端数据集成到字母中作为输入以用于客户通信。

数据字典是描述底层数据结构及其关联属性的元数据的独立表示形式。 数据字典是使用商业词汇来创建的。 它可以映射到一个或多个基础数据模型。

数据字典由三种类型的元素组成：“简单”、“合成”和“集合”元素。 简单DDE是简单元素，如字符串、数字、日期和布尔值，它们包含城市名称等信息。 复合DDE包含其他DDE，其类型可以是简单、复合或集合。 例如，地址，由街道地址、城市、省、国家和邮政编码组成。 集合是类似简单或复合DDE的列表。 例如，具有多个位置或不同帐单和送货地址的客户。

通信管理使用根据数据字典的结构存储的后端、客户或接收方特定数据来创建针对不同客户的通信。 例如，可以使用友好名称创建文档，如“尊敬的{First Name}”、“先生”。 {姓氏}&quot;.

通常，商业用户不需要有关元数据表示法(如XSD（XML架构）和Java类)的知识。 但是，他们通常需要访问这些数据结构和属性才能构建解决方案。

### 数据字典工作流程 {#data-dictionary-workflow}

1. 作者通 [过上传架构](#createdatadictionary) ，或从头开始创建数据字典。
1. 作者根据数据字典创建字母和交互式通信，并根据需要将字母和交互式通信中的数据字典元素关联起来。
1. 作者可以下载基于数据字典模式的示例数据XML文件。 作者可以修改样本数据XML文件，该文件可以作为测试数据与数据字典相关联。 在字母预览期间也会使用相同的功能。
1. 在预 [览字母时](../../forms/using/create-letter.md#p-types-of-linkage-available-for-each-of-the-fields-p)，作者选择使用数据预览字母（自定义预览）。 此时将打开预填充作者提供的数据的字母。 这将在创建对应界面中打开。 预览此信函的代理可以修改此信函中的内容、数据和附件，并可提交最终信函。 有关创建字母的详细信息，请参阅 [创建通信](../../forms/using/create-letter.md)。

## 入门项目 {#prerequisite}

安装兼 [容性包](compatibility-package.md) ，以在“表单”页 **面上查看“数** 据字典”选项 **** 。

## 创建数据字典 {#createdatadictionary}

您可以使用数据字典编辑器创建数据字典，也可以上传XSD架构文件以创建基于此的数据字典。 然后，您可以通过添加更多必需信息（包括字段）来扩展数据字典。 无论数据字典的创建方式如何，业务流程所有者都不需要后端系统的知识。 业务流程所有者只需要对域对象及其定义的知识，即可对其流程进行操作。

>[!NOTE]
>
>对于需要相似元素的多个字母，您可以创建公用数据字典。 但是，具有大量元素的大数据字典在使用数据字典和加载元素（如字母和文档片段）时可能会导致性能问题。 如果遇到性能问题，请尝试为不同的字母创建单独的数据字典。

1. 选择“ **表单** ”>“ **数据字典”**。
1. 点按 **创建数据字典**。
1. 在“属性”屏幕中，添加以下内容：

   * **** 标题：（可选）输入数据字典的标题。 标题不需要唯一，并且可以包含特殊字符和非英语字符。 字母和其他文档片段与其标题（如果可用）一起引用，例如在缩略图和资产属性中。 数据字典引用的是其名称而非标题。
   * **** 名称：数据字典的唯一名称。 在“名称”字段中，只能输入英语字符、数字和连字符。 “名称”字段会根据“标题”字段自动填充，而“标题”字段中输入的特殊字符、空格、数字和非英语字符将替换为连字符。 尽管“标题”字段中的值会自动复制到“名称”中，但您可以编辑该值。

   * **说明**:（可选）数据字典的说明。
   * **** 标记：（可选）要创建自定义标记，请在文本字段中输入值，然后按Enter。 您可以在标记文本字段下看到标记。 保存此文本时，还会创建新添加的标记。
   * **扩展属性**:（可选）点按 **添加字段** ，为数据字典指定元数据属性。 在“属性名称”列中，输入唯一的属性名称。 在“值”列中，输入要与属性关联的值。
   ![德语中指定的数据字典属性](do-not-localize/1_ddproperties.png)

1. （可选）要上传数据字典的XSD架构定义，请点按“数据字典结构”窗格下的“上 **传XML架构”**。 浏览至XSD文件，选择它，然后点按打 **开**。 根据上传的XML架构创建数据字典。 您需要调整数据字典中元素的显示名称和说明。 为此，请点按元素名称，然后在右侧窗格的字段中编辑其说明、显示名称和其他详细信息，以选择这些元素的名称。

   有关计算的DD元素的详细信息，请参 [阅计算的数据字典元素](#computedddelements)。

   >[!NOTE]
   >
   >您可以使用用户界面跳过上传架构文件并从头开始构建数据字典。 为此，请跳过此步骤并继续执行后续步骤。

1. 点按下 **一步**。
1. 在“添加属性”屏幕中，将元素添加到数据字典。 如果您上传了架构以获取数据字典的基本结构，则还可以添加／删除元素并编辑其详细信息。

   您可以点按元素右侧的三个点，并向数据字典结构添加元素。

   ![1_2_createanelement](assets/1_2_createanelement.png)

   选择合成元素、集合元素或基本元素。

   * 复合DDE包含其他DDE，其类型可以是简单、复合或集合。 例如，地址，由街道地址、城市、省、国家和邮政编码组成。
   * 简单DDE是字符串、数字、日期和布尔值等元素，它们包含城市名称等信息。
   * 集合是类似简单或复合DDE的列表。 例如，具有多个位置或不同帐单和送货地址的客户。
   以下是创建数据字典的一些规则：

   * 在数据字典中，仅允许将复合类型作为顶级DDE。
   * 名称、引用名称和元素类型是数据字典和DDE的必填字段。
   * 引用名称必须是唯一的。
   * 父DDE（复合）不能有两个同名的子代。
   * enums仅包含简单字符串类型。
   有关合成、集合和基元元素以及使用数据字典元素的详细信息，请参 [阅将数据字典元素映射到XML架构](#mappingddetoschema)。

   有关数据字典中验证的信息，请参阅 [数据字典编辑器验证](#ddvalidations)。

   ![2_adddpropertiesbasic](assets/2_addddpropertiesbasic.png)

1. （可选）选择元素后，在高级选项卡中，可以添加属性（属性）。 您还可以点按 **添加字段** ，并扩展DD元素的属性。

   ![3_adddproperties高级](assets/3_addddpropertiesadvanced.png)

1. （可选）通过点按元素右侧的三个圆点并选择删除，可以删除任何元 **素**。

   ![4_deleteelement](assets/4_deleteelement.png)

   >[!NOTE]
   >
   >删除包含子节点的复合／集合元素也会删除其子节点。

1. （可选）在“数据字典结构”窗格和“字段和变量列表”面板中选择元素。 更改或添加与元素关联的任何必需属性。
1. 点按&#x200B;**保存**。

### 创建一个或多个数据字典的副本 {#create-copies-of-one-or-more-data-dictionary}

要使用与现有数据字典相似的属性和元素快速创建一个或多个数据字典，您可以复制并粘贴它们。

1. 从数据字典列表中，选择相应的数据字典。 UI会显示复制图标。
1. 点按复制。 UI会显示粘贴图标。
1. 点按粘贴。 此时将显示粘贴对话框。 系统自动地为新数据字典分配名称和标题。
1. 如果需要，请编辑要用其保存数据字典副本的标题和名称。
1. 点按粘贴。 创建数据字典的副本。 现在，您可以在新创建的数据字典中进行所需的更改。

## 请参阅引用数据字典元素的文档片段或文档 {#see-the-document-fragments-or-documents-that-refer-to-a-data-dictionary-element}

在编辑或查看数据字典时，您可以看到数据字典中引用的元素包括文本、条件、字母和交互通信。

1. 执行以下操作之一以编辑数据字典：

   * 将鼠标悬停在数据字典上，然后点按编辑。
   * 选择数据字典，然后点按标题中的编辑。
   * 将鼠标悬停在数据字典上，然后点按选择。 然后点按标题中的编辑。
   或点按数据字典以查看它。

1. 在数据字典中，点按简单元素以选择它。 合成元素和集合元素没有引用。

   此外，还会显示“借出内容”以及元素的“基本”和“高级”属性。

1. 点按借出内容。

   此时会显示“借出内容”选项卡，其中包含以下内容：文本、条件、信函和交互通信。 其中每个标题还显示对所选元素的引用数。

1. 点按标题可查看引用元素的资产名称。

   ![lentcontent](assets/lentcontent.png)

1. 要查看其他元素的借出内容，请点按元素。
1. 要显示引用元素的资产，请点按其名称。 浏览器会显示资产、信函或交互式通信。

## 使用测试数据 {#working-with-test-data}

1. 在“数据字典”页面上，点按 **选择**。
1. 点按要为其下载测试数据的数据字典，然后点按下 **载示例XML数据**。
1. 点按 **警报消** 息中的确定。 下载XML文件。
1. 使用记事本或其他XML编辑器打开XML文件。 XML文件的结构与元素中的数据字典和占位符字符串相同。 将占位符字符串替换为要测试字母的数据。

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
   >在此示例中，XML为集合元素的三个值创建了空间，但可以根据需要增加／减少值的数量。

1. 创建数据条目后，在预览包含测试数据的字母时，可以使用此XML文件。

   您可以使用DD添加此测试数据（选择DD并点按上传测试数据并上传此xml文件），因此，在正常预览字母（而非自定义）后，此XML数据将用于字母。 您还可以点按自定义，然后上传此XML。

## 示例 {#samples}

以下代码示例显示数据字典的实施详细信息。

### 可上传到数据字典的示例架构 {#sample-schema-that-can-be-uploaded-to-the-data-dictionary}

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

## 与DDE关联的常见属性 {#common-attributes-associated-with-a-dde}

下表详细列出了与DDE关联的常用属性：

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
   <td>必填.<br /> DDE的名称。 它必须是独一无二的。</td>
  </tr>
  <tr>
   <td>Reference<br /> Name</td>
   <td>字符串</td>
   <td>必填. DDE的唯一引用名称允许对DDE的引用，这些引用与对数据字典的层次结构或结构的更改无关。 文本模块使用此名称进行映射</td>
  </tr>
  <tr>
   <td>displayname</td>
   <td>字符串</td>
   <td>DDE的可选用户友好名称。</td>
  </tr>
  <tr>
   <td>描述</td>
   <td>字符串</td>
   <td>DDE的说明。</td>
  </tr>
  <tr>
   <td>elementType</td>
   <td>字符串</td>
   <td>必填. DDE的类型：字符串、数字、日期、布尔值、合成、集合。</td>
  </tr>
  <tr>
   <td>elementSubType</td>
   <td>字符串</td>
   <td>DDE的子类型：ENUM。 仅允许用于STRING和NUMBER elementType。</td>
  </tr>
  <tr>
   <td>关键值</td>
   <td>布尔型</td>
   <td>指示DDE是否为关键元素的布尔字段。</td>
  </tr>
  <tr>
   <td>已计算</td>
   <td>布尔型</td>
   <td>指示是否计算DDE的布尔字段。 计算的DDE值是其它DDE值的函数。 默认情况下，支持jsp表达式。</td>
  </tr>
  <tr>
   <td>表达式</td>
   <td>字符串</td>
   <td>“已计算”DDE的表达式。 默认情况下提供的表达式评估服务支持JSP EL表达式。 您可以用自定义实现替换表达式服务。</td>
  </tr>
  <tr>
   <td>valueSet</td>
   <td>列表</td>
   <td>Enum类型DDE的一组允许值。 例如，帐户类型只能具有（保存，当前）值。</td>
  </tr>
  <tr>
   <td>extendedProperties</td>
   <td>Object</td>
   <td>添加到DDE的自定义属性的映射（特定于用户界面或任何其他信息）。</td>
  </tr>
  <tr>
   <td>必填</td>
   <td>布尔型</td>
   <td>标志指示与数据字典相对应的实例数据源必须包含此特定DDE的值。</td>
  </tr>
  <tr>
   <td>捆绑</td>
   <td>BindingElement</td>
   <td>元素的XML或Java绑定。</td>
  </tr>
 </tbody>
</table>

### 计算数据字典元素 {#computedddelements}

数据字典还可以包括计算元素。 计算的数据字典元素始终与表达式相关联。 计算此表达式以在运行时获得数据字典元素的值。 计算的DDE值是其他DDE值或文本的函数。 默认情况下，支持JSP表达式语言(EL)表达式。 EL表达式使用${ }字符，而有效表达式可以包括文本、运算符、变量（数据字典元素引用）和函数调用。 在表达式中引用数据字典元素时，将使用DDE的引用名称。 对于数据字典中的每个数据字典元素，引用名称是唯一的。

计算的DDE PersonFullName可以与EL连接表达式相关联，如${PersonFirstName} ${PersonLastName}。

## XSD与数据字典之间的数据类型映射 {#data-type-mapping-between-xsd-and-data-dictionary-br}

导出XSD需要特定的数据映射，下表详细介绍了该映射。 DDI列指示DDI中可用的DDE值的类型。

<table>
 <tbody>
  <tr>
   <td>XSD <br /> </td>
   <td><p>数据字典 <br /> </p> </td>
   <td>DDI（实例值数据类型）<br /> </p> </td>
  </tr>
  <tr>
   <td><p>xs：类型元素——复合类型<br /> </p> </td>
   <td>DDE类型——复合<br /> </p> </td>
   <td>java.util.Map<br /> </td>
  </tr>
  <tr>
   <td><p>xs:element where maxOccurs &gt; 1<br /> </p> </td>
   <td>DDE类型- COLLECTION-<br /> DDE节点创建在COLLECTION DDE旁边，该DDE从父COLLECTION节点捕获信息。 为简单／复合数据类型的集合创建相同的内容。 只要您有复合类型的COLLECTION,“数据字典”树就会捕获为捕获类型信息而创建的DDE的子项中的组成字段。<br /> - DDE(COLLECTION)<br /> - DDE(COMPOSITE for type info)<br /> - DDE(STRING)field1<br /> - DDE(STRING)field2<br /><br /> </p> </td>
   <td>java.util.List<br /> </td>
  </tr>
  <tr>
   <td>类型属性- xs:id <br /> </p> </td>
   <td>DDE类型- STRING <br /> </td>
   <td>java.lang.String<br /> </td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element类型- xs:string</p> </td>
   <td>DDE类型- STRING<br /> </td>
   <td>java.lang.String<br /> </td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element type - xs:布尔值 <br /> </td>
   <td>DDE类型——布尔值 <br /> </td>
   <td>java.lang.Boolean<br /> </td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element type - xs:date </td>
   <td>DDE类型- DATE </td>
   <td>java.lang.String</td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element type - xs:integer </td>
   <td>DDE类型- NUMBER </td>
   <td>java.lang.Double</td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element type - xs:long</td>
   <td>DDE类型- NUMBER </td>
   <td>java.lang.Double</td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element type - xs:double</td>
   <td>DDE类型- NUMBER </td>
   <td>java.lang.Double</td>
  </tr>
  <tr>
   <td>enum类型和baseType的元素- xs:string</td>
   <td>DDE of<br /> type - STRING<br /><br /> subtype - ENUM valueSet - ENUM的允许值<br /> </td>
   <td>java.lang.String</td>
  </tr>
 </tbody>
</table>

## 从数据字典下载示例数据文件 {#download-a-sample-data-file-from-a-data-dictionary}

创建数据字典后，可以将其下载为XML范例数据文件，以在其中生成文本条目。

1. 在“数据字典”页中，点按 **选择** ，然后点按数据字典以选择它。
1. Select **Download Sample XML Data**.
1. 点按 **警报消** 息中的确定。

   “对应管理”根据所选数据字典的结构创建XML文件，并将其下载到名为&lt;data-dictionary-name>-SampleData的计算机。 现在，您可以在XML或文本编辑器中编辑此文件，以在创建字母时进 [行数据输入](../../forms/using/create-letter.md)。

## 元数据的国际化 {#internationalization-of-meta-data}

当您希望向客户发送使用不同语言的同一字母时，您可以本地化数据字典和数据字典元素的显示名称、说明和枚举值集。

### 本地化数据字典 {#localize-data-dictionary}

1. 在“数据字典”页上，点按 **选择** ，然后点按数据字典以选择它。
1. 点按 **下载本地化数据**。
1. 点按 **警报中** 的确定。 “通信管理”将名为DataDictionary-&lt;Dname>.zip的zip文件下载到您的计算机。
1. Zip文件包含。properties文件。 此文件定义下载的数据字典。 属性文件的内容类似于以下内容：

   # 2015年5月20日16时6分23秒
   DataDictionary.EmployeeDD.description=DataDictionary.EmployeeDD.displayName=EmployeeDataDictionaryDataDictionaryElement.name.description=DataDictionaryElement.name.displayName=nameDataDictionaryElement.person.person.person.pson.dion.dion.displayDionname=person

   属性文件的结构为描述和数据字典中的数据字典和每个数据字典元素的显示名称定义一行。 此外，属性文件为每个数据字典元素的枚举值集定义一行。 与数据字典一样，相应的属性文件可以具有多个数据字典元素定义。 此外，该文件可以包含一个或多个枚举值集的定义。

1. 要在其他区域设置中更新。properties文件，请更新文件中的显示名称和说明值。 为要本地化的每种语言创建更多文件实例。 仅支持法语、德语、日语和英语。

1. 使用以下名称保存不同的已更新属性文件：

   _fr_FR.properties法语

   _de_DE.properties德语

   _ja_JA.properties日语

   _en_EN.properties英语

1. 将。properties文件（或多个区域设置的文件）存档到单个。zip文件中。

1. 在“数据字典”页中，选择“更 **多** ”>“上传本 **地化数据** ”，然后选择包含本地化属性文件的zip文件。
1. 要查看本地化更改，请更改浏览器区域设置。

## 数据字典验证 {#ddvalidations}

数据字典编辑器在创建或更新数据字典时强制执行以下验证。

* 在数据字典中，仅允许将复合类型作为顶级元素。
* 复合元素和集合元素不允许在叶级别使用。 叶级别仅允许Primitive(String, Date, Number, Boolean)元素。 此验证可确保没有子DDE的合成和集合元素。
* 在上传XSD文件以创建数据字典时，Data Dictionary editor会提示输入顶级元素（如果存在多个元素）以创建数据字典。
* 名称是数据字典的唯一必需参数。
* 父DDE（复合）不能有两个同名的子代
* 确保只有在DDE不是必需参数时，才将其标记为已计算。 不能计算所需元素，也不能需要计算元素。 此外，“集合”和“合成元素”不能是计算元素。
* 确保DDE标记为必需（仅在不计算时）。 它还确保它不是表示集合类型的“collectionElement”（即集合元素的唯一子项）。
* 数据字典或DDE的extendedProperties中不允许空键或重复键。
* 请勿在扩展属性的键或值中使用冒号(:)或垂直条(|)字符。 这些禁止的字符的使用没有验证。

在数据字典级别应用的验证

* 数据字典名称不得为null。
* 数据字典名称只能包含字母数字字符。
* 数据字典中的子元素列表不得为null或空。
* 数据字典不得包含多个顶级数据字典元素。
* 在数据字典中，只有复合类型才允许作为顶级元素。

在数据字典元素级别应用的验证。

* 所有DDE名称不得为null且不得包含空格。
* 所有DDE都必须具有“not null/non null”元素类型。
* 所有DDE引用名称不得为null。
* 所有DDE引用名称必须是唯一的。
* 所有DDE引用只能包含字母数字字符和“_”。
* 所有DDE显示名称只能包含字母数字字符和“_”。
* 复合元素和集合元素不允许在叶级别使用。 叶级别仅允许Primitive(String, Date, Number, Boolean)元素。 此验证可确保没有子DDE的合成和集合元素。
* 复合父DDE不能有两个同名的子元素。
* ENUM子类型仅用于字符串和数字元素。
* 无法计算集合和合成元素。
* DDE不能同时计算和要求。
* 计算的DDE必须包含有效的表达式。
* 计算的DDE不能有XML绑定。
* 表示集合DDE类型的DDE不能计算或必需。
* 子类型ENUM的DDE不得包含空值集或空值集。
* 集合DDE的XML绑定不能映射到属性。
* XML绑定语法必须有效，例如，只显示一个@，只有在后跟一个属性名时，才允许使用@。

## 将数据字典元素映射到XML架构 {#mappingddetoschema}

您可以从XML架构创建数据字典，或使用数据字典用户界面构建它。 数据字典中的所有数据字典元素(DDE)都有一个XML绑定字段，用于存储DDE与XML架构中元素的绑定。 每个DDE中的绑定相对于父DDE。

以下详细信息示例模型和代码示例显示数据字典的实施详细信息。

## 映射简单（简单）元素 {#mapping-simple-primitive-elements}

简单DDE表示本质上是原子的字段或属性。 在复杂类型（复合DDE）或重复元素（集合DDE）的范围外定义的基本DDE可以存储在XML架构中的任何位置。 对应于简单DDE的数据的位置不取决于其父DDE的映射。 Primitive DDE使用“XML绑定”字段的映射信息确定其值，并且映射转换为以下任一内容：

* 属性
* 元素
* 文本上下文
* nothing(an ignored DDE)

以下示例展示了一个简单的架构。

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

复合元素不支持绑定，如果提供绑定，则忽略它。 所有原始类型的构成子DDE的绑定必须是绝对的。 允许对复合DDE的子元素进行绝对映射在XPath绑定方面提供了更大的灵活性。 将复合DDE映射到XML架构中的复杂类型元素会限制其子元素的绑定范围。

以下示例显示了备注的架构。

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
   <td>附注</td>
   <td>空(null)<br /> </td>
  </tr>
  <tr>
   <td>到</td>
   <td>/note/to</td>
  </tr>
  <tr>
   <td>起始日期:</td>
   <td>/note/from</td>
  </tr>
  <tr>
   <td>标题</td>
   <td>/note/heading</td>
  </tr>
  <tr>
   <td>身体</td>
   <td>/note/body</td>
  </tr>
 </tbody>
</table>

### 映射集合元素 {#mapping-collection-elements}

集合元素仅映射到其他基数大于1的集合元素。 集合DDE的子DDE与其父项的XML绑定相关（本地）XML绑定。 由于集合元素的子DDE必须与父项的基数相同，因此要求相对绑定以确保基数约束，以便子DDE不指向非重复的XML架构元素。 在以下示例中，“TokenID”基数必须与“Tokens”（其父集合DDE）相同。

将集合DDE映射到XML架构元素时：

* 与Collection元素对应的DDE绑定必须是绝对XPath

* 不为表示“集合”元素类型的DDE提供绑定。 如果提供，则忽略绑定。

* 集合元素的所有子DDE的绑定必须相对于父集合元素。

下面的XML架构声明一个元素，其名称为Tokens，并且maxOccurs属性为“unbounded”。 因此，令牌是一个集合元素。

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

与此示例关联的Token.xsd将为：

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
| 根 | 空(null) |
| 令牌 | /根／令牌 |
| 复合 | 空(null) |
| TokenID | TokenID |
| TokenText | 空(null) |
| TokenHeading | TokenText/TextHeading |
| TokenBody | TokenText/TextBody |

