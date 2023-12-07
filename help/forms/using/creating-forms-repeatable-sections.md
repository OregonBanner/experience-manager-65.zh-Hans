---
title: 创建包含可重复部分的表单
description: 可重复部分是可动态添加到表单或从中移除的面板。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms
exl-id: f2abae0a-f7fd-4a39-bd8c-03492ce06fe9
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 4%

---

# 创建包含可重复部分的表单 {#creating-forms-with-repeatable-sections}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

可重复部分是可动态添加到表单或从中移除的面板。

例如，在申请工作时，求职者提供以前的雇用详细信息，如公司名称、角色、项目和其他信息。 所有雇主的信息要求不同但外观相似的部门。 在这种情况下，雇佣表单会提供一个雇主部分，并提供动态添加更多此类部分的选项。 这些动态添加的部分称为可重复部分。

您可以使用以下方法之一来创建可重复面板：

## 通过脚本使用实例管理器  {#using-instance-manager-via-scripts-nbsp}

1. 在编辑模式下，选择一个面板，然后选择 ![cmppr](assets/cmppr.png). 在侧栏中的属性下方，启用 **使面板可重复**. 指定以下各项的值： **[!UICONTROL 最大值]** 和 **[!UICONTROL 最小值]** 字段。

   “最大值”字段指定面板在页面上可出现的最大次数。 您可以在Maximum Count字段中指定–1 ，以允许该面板无限次显示。

   “最小值”字段指定面板在表单上显示的最小次数。 如果将Minimum Count字段设置为零，则以后可以在演绎版完成后通过脚本删除所有实例。

   >[!NOTE]
   >
   >要创建不可重复的面板，请将“最大值”和“最小值”字段的值设置为1。 折叠布局在Maximum Count字段中不支持–1。 您可以指定一个大数来给出无限值的概念。

1. 面板的父项（将重复）应包含添加和删除按钮以管理可重复面板的实例。 执行以下步骤将按钮插入到父代，并在按钮上启用脚本：

   1. 从侧栏中，将按钮组件拖放到面板的父面板。 选择组件并选择 ![edit-rules](assets/edit-rules.png). 该按钮的规则将在规则编辑器中打开。
   1. 在规则编辑器窗口中，单击 **创建**.

      选择 **可视编辑器** 表单对象和函数行中的。

      1. 在规则区域的WHEN下，选择state **已单击**.
      1. 在THEN下：

         * 要创建添加面板按钮，请选择 **添加实例**，并使用拖放面板 ![切换侧面板](assets/toggle-side-panel.png) 或使用以下方式选择它 **拖放对象或在此选择。**
         * 要创建删除面板按钮，请选择 **删除实例**，并使用拖放面板 ![切换侧面板](assets/toggle-side-panel.png) 或使用以下方式选择它 **拖放对象或在此选择。**

      选择 **代码编辑器** 表单对象和函数行中的。 单击 **编辑规则** 在代码区域中：

      * 要创建添加面板按钮，请指定 `this.panel.instanceManager.addInstance()`
      * 要创建删除面板按钮，请指定 `this.panel.instanceManager.removeInstance(this.panel.instanceIndex)`

      单击&#x200B;**完成**。

      >[!NOTE]
      >
      >如果某个字段属于可重复面板，则无法在脚本中使用该字段名称直接访问该字段。 要访问字段，请使用指定字段所属的可重复实例 `instances` 中的API `InstanceManager`. 要使用的语法 `instances` 中的API `InstanceManager` 为：
      >
      >
      >`<panelName>.instanceManager.instances[<instanceNumber>].<fieldname>`
      >
      >
      >例如，创建一个带有文本框的可重复面板的自适应表单。 使用三个可重复的文本框预填表单时，您需要以下xml：
      >
      >
      >`<panel1><textbox1>AA1</panel1></textbox1>`
      >
      >
      >`<panel1><textbox1>AA2</panel1></textbox1>`
      >
      >
      >`<panel1><textbox1>AA3</panel1></textbox1>`
      >
      >
      >要读取AA1数据，请指定：
      >
      >
      >`Panel1.instanceManager.instances[0].textbox.value`
      >
      >
      >要读取AA2数据，请指定：
      >
      >
      >`Panel1.instanceManager.instances[1].textbox.value`
      >
      >
      >有关详细信息，请参阅中的类：InstanceManager#instances [AEM Forms Java API参考](https://adobe.com/go/learn_aemforms_documentation_63).

      >[!NOTE]
      >
      >从自适应表单中删除面板的所有实例时，要添加已删除面板的实例，请使用_panelName语法捕获面板的实例管理器，并使用实例管理器的addInstance API添加已删除的实例。 例如，_panelName.addInstance()。 它会添加已删除面板的一个实例。

## 使用父面板的可折叠项布局   {#using-the-accordion-layout-for-the-parent-panel-nbsp}

面板具有各种布局选项。 折叠式设计的布局选项为可重复面板提供开箱即用支持。 对带有可折叠设计选项的布局的可重复面板执行以下步骤：

1. 在要重复的面板的父项上，选择 ![cmppr](assets/cmppr.png). 您可以在侧栏中看到属性。 在 **布局** 下拉列表，选择 **折叠**.
1. 在要重复的面板上，选择 ![cmppr](assets/cmppr.png). 您可以在侧栏中看到面板属性。 启用 **使面板可重复** 选项卡，并为 **最大值** 和 **最小值** 字段。

   现在，您可以使用加号(+)并删除( ![delete-panel](assets/delete-panel.png))按钮以添加和删除面板。

## 使用表单模板中的重复子表单(XDP/XSD) {#using-repeating-subforms-from-form-template-xdp-xsd}

可重复子表单类似于自适应Forms中的可重复面板。 在AEM Forms Designer中，执行以下步骤以创建重复的子表单：

1. 在层级调色板中，选择要重复的子表单的父子表单。
1. 在“对象”面板中，单击“子表单”选项卡，然后在“内容”列表中选择“流式”。
1. 选择要重复的子表单。
1. 在“对象”面板中，单击“子表单”选项卡，然后在“内容”列表中选择“已定位”或“已流动”。
1. 单击“绑定”选项卡，并为每个数据项选择“重复子表单”。
1. 要指定最小重复次数，请选择最小计数，然后在关联的框中键入一个数字。 如果将此选项设置为0，并且在数据合并时没有为子表单中的对象提供数据，则在呈现表单时不会放置子表单。
1. 要指定子表单重复的最大次数，请选择“最大”，然后在相关框中键入一个数字。 如果未在“最大值”框中指定值，则子表单的重复次数将无限制。
1. 要指定一组子表单重复次数，而不考虑数据量，请选择初始计数，然后在关联框中键入一个数字。 如果选择此选项，并且没有可用数据或存在的数据条目少于指定的初始计数值，则子表单的空实例仍会放置在表单上。
1. 在父子表单中添加两个按钮 — 一个用于添加实例，另一个用于删除可重复子表单的实例。 有关详细步骤，请参阅 [构建操作](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c74572b5612a87ca2b56-8000.2.html#WS107c29ade9134a2c-1f74d86012a87d4fe55-8000.2).
1. 现在，将表单模板链接到自适应表单。 有关详细步骤，请参阅 [基于模板创建自适应表单](/help/forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-a-template).
1. 使用在第9步中创建的按钮添加和删除子表单。

附加的.zip文件包含一个示例可重复的子表单。

[获取文件](assets/samplerepeatablesubform.zip)

## 使用XML架构(XSD)的重复设置 {#using-repeat-settings-of-an-xml-schema-xsd-br}

您可以从XML架构和任何复杂类型元素的minOccours和maxOccurs属性创建可重复面板。 有关XML架构的详细信息，请参见 [使用XML架构作为表单模型创建自适应表单](/help/forms/using/adaptive-form-xml-schema-form-model.md).

在以下代码中， `SampleType`面板使用minOccurs和maxOccurs属性。

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
                <xs:element name="assignmentStartDate" type="xs:date"/>
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
>对于非折叠布局，使用自适应表单按钮组件添加和删除实例。
