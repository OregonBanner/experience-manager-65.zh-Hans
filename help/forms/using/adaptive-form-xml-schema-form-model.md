---
title: 如何使用XML架构创建自适应Forms？
description: 了解如何在自适应表单中将XML架构用作表单模型。 您可以应用现有XSD模板来创建自适应表单，并将架构元素从XSD拖放到自适应表单上。 深入了解XML架构示例，向使用XML架构的字段添加特殊属性，并限制自适应表单组件的可接受值。
feature: Adaptive Forms
role: User, Developer
level: Beginner, Intermediate
exl-id: 35d5859f-54c4-4d14-9c64-0d9291ef9029
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 6%

---

# 使用XML架构创建自适应表单 {#creating-adaptive-forms-using-xml-schema}

<span class="preview"> Adobe建议使用现代化的、可扩展的数据捕获 [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) 对象 [创建新的自适应Forms](/help/forms/using/create-an-adaptive-form-core-components.md) 或 [将自适应Forms添加到AEM Sites页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). 这些组件在创建自适应Forms方面实现了重大进步，确保了令人印象深刻的用户体验。 本文介绍了使用基础组件创作自适应Forms的旧方法。 </span>

## 前提条件 {#prerequisites}

使用XML架构作为表单模型创作自适应表单需要基本了解XML架构。 此外，建议在阅读本文之前通读以下内容。

* [创建自适应表单](creating-adaptive-form.md)
* [XML架构](https://www.w3.org/TR/xmlschema-2/)

## 将XML架构用作表单模型 {#using-an-xml-schema-as-form-model}

[!DNL Experience Manager Forms] 支持使用现有XML架构作为表单模型来创建自适应表单。 此XML架构表示组织中的后端系统生成或使用数据的结构。

使用XML架构的主要功能包括：

* 在自适应表单的创作模式下，XSD的结构在“内容查找器”选项卡中显示为树。 您可以将元素从XSD层次结构拖放到自适应表单中。
* 您可以使用与相关架构兼容的XML预填充表单。
* 在提交时，用户输入的数据将作为XML提交，这与关联的架构一致。

XML架构由简单和复杂的元素类型组成。 元素具有向元素添加规则的属性。 将这些元素和属性拖动到自适应表单上时，会自动映射到相应的自适应表单组件。

带有自适应表单组件的XML元素映射如下：

<table>
 <tbody>
  <tr>
   <th><strong>XML元素或属性 </strong></th>
   <th><strong>自适应表单组件</strong></th>
  </tr>
  <tr>
   <td><code>xs:string</code></td>
   <td>文本框</td>
  </tr>
  <tr>
   <td><code>xs:boolean</code></td>
   <td>复选框</td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><code>xs:unsignedInt</code></li>
     <li><code>xs:xs:int</code></li>
     <li><code class="code">xs:decimal
        </code></li>
     <li>所有类型的数值</li>
    </ul> </td>
   <td>数值框</td>
  </tr>
  <tr>
   <td><code>xs:date</code></td>
   <td>日期选取器</td>
  </tr>
  <tr>
   <td><code class="code">xs:enumeration
      </code></td>
   <td>下拉列表</td>
  </tr>
  <tr>
   <td>任何复杂类型的元素</td>
   <td>面板</td>
  </tr>
 </tbody>
</table>

## 示例XML架构 {#sample-xml-schema}

以下是XML架构的示例。

```xml
<?xml version="1.0" encoding="utf-8" ?>
    <xs:schema targetNamespace="https://adobe.com/sample.xsd"
                    xmlns="https://adobe.com/sample.xsd"
                    xmlns:xs="https://www.w3.org/2001/XMLSchema"
                >

        <xs:element name="sample" type="SampleType"/>

        <xs:complexType name="SampleType">
            <xs:sequence>
                <xs:element name="leaderName" type="xs:string" default="Enter Name"/>
                <xs:element name="assignmentStartBirth" type="xs:date"/>
                <xs:element name="gender" type="GenderEnum"/>
                <xs:element name="noOfProjectsAssigned" type="IntType"/>
                <xs:element name="assignmentDetails" type="AssignmentDetails"
                                            minOccurs="0" maxOccurs="10"/>
            </xs:sequence>
        </xs:complexType>

        <xs:complexType name="AssignmentDetails">
            <xs:attribute name="name" type="xs:string" use="required"/>
            <xs:attribute name="durationOfAssignment" type="xs:unsignedInt" use="required"/>
            <xs:attribute name="numberOfMentees" type="xs:unsignedInt" use="required"/>
             <xs:attribute name="descriptionOfAssignment" type="xs:string" use="required"/>
             <xs:attribute name="financeRelatedProject" type="xs:boolean"/>
       </xs:complexType>
  <xs:simpleType name="IntType">
            <xs:restriction base="xs:int">
            </xs:restriction>
        </xs:simpleType>
  <xs:simpleType name="GenderEnum">
            <xs:restriction base="xs:string">
                <xs:enumeration value="Female"/>
                <xs:enumeration value="Male"/>
            </xs:restriction>
        </xs:simpleType>
    </xs:schema>
```

>[!NOTE]
>
>确保XML架构只有一个根元素。 不支持具有多个根元素的XML架构。

## 使用XML架构向字段添加特殊属性 {#adding-special-properties-to-fields-using-xml-schema}

可以将以下属性添加到XML架构元素，以将特殊属性添加到关联的自适应表单的字段。

<table>
 <tbody>
  <tr>
   <th><strong>架构属性</strong></th>
   <th><strong>在自适应表单中使用</strong></th>
   <th><strong>中支持 </strong></th>
  </tr>
  <tr>
   <td><code>use=required </code></td>
   <td>将字段标记为必填<br /> </td>
   <td>属性</td>
  </tr>
  <tr>
   <td><code>default="default value"</code></td>
   <td>添加默认值</td>
   <td>元素和属性</td>
  </tr>
  <tr>
   <td><code>minOccurs="3"</code></td>
   <td><p>指定最小出现次数</p> <p>(对于可重复的子表单（复杂类型）)</p> </td>
   <td>元素（复杂类型）</td>
  </tr>
  <tr>
   <td><code class="code">maxOccurs="10"
      </code></td>
   <td><p>指定最大发生次数</p> <p>(对于可重复的子表单（复杂类型）)</p> </td>
   <td>元素（复杂类型）</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>将架构元素拖到自适应表单中时，会通过以下方式生成默认题注：
>
>* 将元素名称的第一个字符变为大写
>* 在“驼峰式大小写”边界处插入空格。
>
>例如，如果添加 `userFirstName` 架构元素中，在自适应表单中生成的标题为 `User First Name`.

## 限制自适应表单组件的可接受值 {#limit-acceptable-values-for-an-adaptive-form-component}

您可以向XML架构元素添加以下限制，以限制自适应表单组件可以接受的值：

<table>
 <tbody>
  <tr>
   <td><p><strong> 架构属性</strong></p> </td>
   <td><p><strong>数据类型</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
   <td><p><strong>组件</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>totalDigits</code></p> </td>
   <td><p>字符串</p> </td>
   <td><p>指定组件中允许的最大位数。 指定的位数必须大于零。</p> </td>
   <td>
    <ul>
     <li>数值框</li>
     <li>数值步进器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>字符串</p> </td>
   <td><p>指定数值和日期的上限。 默认情况下，包含最大值。</p> </td>
   <td>
    <ul>
     <li>数值框</li>
     <li>数值步进器<br /> </li>
     <li>日期选取器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minimum</code></p> </td>
   <td><p>字符串</p> </td>
   <td><p>指定数字值和日期的下限。 默认情况下，包含最小值。</p> </td>
   <td>
    <ul>
     <li>数值框</li>
     <li>数值步进器</li>
     <li>日期选取器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>布尔值</p> </td>
   <td><p>如果为true，则表单组件中指定的数值或日期必须小于为maximum属性指定的数值或日期。</p> <p>如果为false，则表单组件中指定的数值或日期必须小于或等于为maximum属性指定的数值或日期。</p> </td>
   <td>
    <ul>
     <li>数值框</li>
     <li>数值步进器</li>
     <li>日期选取器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>布尔值</p> </td>
   <td><p>如果为true，则表单组件中指定的数值或日期必须大于为最小属性指定的数值或日期。</p> <p>如果为false，则表单组件中指定的数值或日期必须大于或等于为最小属性指定的数值或日期。</p> </td>
   <td>
    <ul>
     <li>数值框</li>
     <li>数值步进器</li>
     <li>日期选取器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minLength</code></p> </td>
   <td><p>字符串</p> </td>
   <td><p>指定组件中允许的最小字符数。 最小长度必须等于或大于零。</p> </td>
   <td>
    <ul>
     <li>文本框</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>maxLength</code></p> </td>
   <td><p>字符串</p> </td>
   <td><p>指定组件中允许的最大字符数。 最大长度必须大于零。</p> </td>
   <td>
    <ul>
     <li>文本框</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>length</code></p> </td>
   <td><p>字符串</p> </td>
   <td><p>指定组件中允许的确切字符数。 长度必须等于或大于零。</p> </td>
   <td>
    <ul>
     <li>文本框</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>fractionDigits</code></p> </td>
   <td><p>字符串</p> </td>
   <td><p>指定组件中允许的最多小数位数。 fractionDigits必须等于或大于零。</p> </td>
   <td>
    <ul>
     <li> 具有数据类型浮点数或小数的数字框</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>字符串</p> </td>
   <td><p>指定字符的序列。 如果字符符合指定的模式，组件将接受这些字符。</p> <p>pattern属性映射到相应自适应表单组件的验证模式。</p> </td>
   <td>
    <ul>
     <li>映射到XSD架构的所有自适应表单组件 </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 常见问题 {#frequently-asked-questions}

**如何知道树中的哪个元素与哪个XML元素关联？**

在Content Finder中双击某个元素时，会有一个弹出窗口显示一个字段名称和一个名为的属性 `bindRef`. 此属性将树元素映射到架构中的元素或属性。

![XML架构元素的bindref字段](assets/dblclick.png)

此 <code>bindRef</code> 字段显示树元素与架构中的元素或属性之间的关联。

>[!NOTE]
>
>属性具有 `@` 符号位于它们的 `bindRef`值，以将其与元素区分开。 例如：`/config/projectDetails/@duration`。

**为什么我无法为可重复的子表单（minOccours或maxOccurs值大于1）拖动子表单的单个元素（从任何复杂类型生成的结构）？**

在可重复的子表单中，您必须使用“完成”子表单。 如果只需要选择字段，请使用整个结构并删除不需要的字段。

**我在内容查找器中有一个长且复杂的结构。 如何查找特定元素？**

您有两个选项：

* 滚动浏览树结构
* 使用搜索框查找元素

**什么是bindRef？**

A `bindRef` 是自适应表单组件与架构元素或属性之间的连接。 它规定 `XPath` 其中从此组件或字段捕获的值在输出XML中可用。 A `bindRef`在从预填充（预填充）的XML中预填充字段值时也可使用。
