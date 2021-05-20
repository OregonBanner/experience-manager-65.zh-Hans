---
title: 如何使用XML架构创建自适应Forms?
description: 了解如何在自适应表单中将XML模式用作表单模型。 您可以应用现有XSD模板来创建自适应表单，并将XSD中的架构元素拖放到自适应表单上。 使用XML架构的示例深入挖掘，使用XML架构向字段添加特殊属性，并限制自适应表单组件的可接受值。
feature: 自适应表单
role: Business Practitioner, Developer
level: Beginner, Intermediate
exl-id: 35d5859f-54c4-4d14-9c64-0d9291ef9029
source-git-commit: ad67634278088f8f953fde61a3543acdd70537dd
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 6%

---

# 使用XML架构{#creating-adaptive-forms-using-xml-schema}创建自适应表单

## 前提条件 {#prerequisites}

使用XML架构作为其表单模型来创作自适应表单需要对XML架构有基本的了解。 此外，还建议在阅读本文之前阅读以下内容。

* [创建自适应表单](creating-adaptive-form.md)
* [XML 架构](https://www.w3.org/TR/xmlschema-2/)

## 使用XML架构作为表单模型{#using-an-xml-schema-as-form-model}

[!DNL Experience Manager Forms] 支持使用现有XML架构作为表单模型来创建自适应表单。此XML架构表示组织内的后端系统生成或使用数据的结构。

使用XML架构的主要功能包括：

* XSD的结构在自适应表单创作模式的“内容查找器”选项卡中显示为树。 您可以将XSD层次结构中的元素拖放到自适应表单中。
* 您可以使用与关联架构兼容的XML预填充表单。
* 提交时，用户输入的数据将以与关联架构一致的XML形式提交。

XML架构由简单和复杂的元素类型组成。 元素具有可向元素添加规则的属性。 将这些元素和属性拖动到自适应表单上后，会自动将它们映射到相应的自适应表单组件。

XML元素与自适应表单组件的映射如下所示：

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
   <td>任何复杂类型元素</td>
   <td>面板</td>
  </tr>
 </tbody>
</table>

## XML架构{#sample-xml-schema}示例

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

## 使用XML架构{#adding-special-properties-to-fields-using-xml-schema}向字段添加特殊属性

您可以将以下属性添加到XML架构元素，以向关联的自适应表单的字段添加特殊属性。

<table>
 <tbody>
  <tr>
   <th><strong>架构属性</strong></th>
   <th><strong>在自适应表单中使用</strong></th>
   <th><strong>在 </strong></th>
  </tr>
  <tr>
   <td><code>use=required </code></td>
   <td>将字段标记为必填字段<br /> </td>
   <td>属性</td>
  </tr>
  <tr>
   <td><code>default="default value"</code></td>
   <td>添加默认值</td>
   <td>元素和属性</td>
  </tr>
  <tr>
   <td><code>minOccurs="3"</code></td>
   <td><p>指定最小发生次数</p> <p>(对于可重复的子表单（复杂类型）)</p> </td>
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
>将架构元素拖动到自适应表单时，会生成默认标题：
>
>* 将元素名称的第一个字符大写
>* 在驼峰式大小写边界处插入空格。

>
>
例如，如果添加`userFirstName`架构元素，则在自适应表单中生成的标题为`User First Name`。

## 限制自适应表单组件{#limit-acceptable-values-for-an-adaptive-form-component}的可接受值

您可以向XML架构元素添加以下限制，以限制自适应表单组件可接受的值：

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
   <td><p>指定数值和日期的下限。 默认情况下，包含最小值。</p> </td>
   <td>
    <ul>
     <li>数值框</li>
     <li>数值步进器</li>
     <li>日期选取器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>布尔型</p> </td>
   <td><p>如果为true，则在表单组件中指定的数值或日期必须小于为maximum属性指定的数值或日期。</p> <p>如果为false，则表单组件中指定的数值或日期必须小于或等于为最大属性指定的数值或日期。</p> </td>
   <td>
    <ul>
     <li>数值框</li>
     <li>数值步进器</li>
     <li>日期选取器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>布尔型</p> </td>
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
   <td><p>指定组件中允许的字符数。 长度必须等于或大于零。</p> </td>
   <td>
    <ul>
     <li>文本框</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>fractionDigits</code></p> </td>
   <td><p>字符串</p> </td>
   <td><p>指定组件中允许的最大小数位数。 fractionDigits必须等于或大于零。</p> </td>
   <td>
    <ul>
     <li> 具有数据类型浮点或小数的数字框</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>字符串</p> </td>
   <td><p>指定字符的顺序。 如果字符符合指定的模式，则组件接受字符。</p> <p>模式属性映射到相应自适应表单组件的验证模式。</p> </td>
   <td>
    <ul>
     <li>映射到XSD架构的所有自适应表单组件 </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 常见问题 {#frequently-asked-questions}

**如何知道树中的哪个元素与哪个XML元素相关联？**

在内容查找器中双击某个元素时，弹出窗口会显示一个字段名称和一个名为`bindRef`的属性。 此属性将树元素映射到架构中的元素或属性。

![XML架构元素的bindref字段](assets/dblclick.png)

bindRef</code>字段显示树元素与架构中元素或属性之间的关联。

>[!NOTE]
>
>属性的`bindRef`值中有一个`@`符号，用于与元素区分开来。 例如，`/config/projectDetails/@duration`。

**为什么我无法为可重复的子表单（minOccours或maxOccurs值大于1）拖动子表单的单个元素（从任何复杂类型生成的结构）？**

在可重复的子表单中，您必须使用“完成”子表单。 如果只希望选择字段，请使用整个结构并删除不需要的字段。

**我在内容查找器中有一个很长的复杂结构。如何查找特定元素？**

您有两个选项：

* 滚动浏览树结构
* 使用“搜索”框查找元素

**什么是bindRef?**

`bindRef`是自适应表单组件与架构元素或属性之间的连接。 它指示`XPath`，在输出XML中，可从此组件或字段捕获的值可用。 从预填充（预填充）XML中预填充字段值时，也会使用`bindRef`。
