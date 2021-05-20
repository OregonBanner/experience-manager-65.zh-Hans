---
title: 使用可重复部分创建表单
seo-title: 使用可重复部分创建表单
description: 可重复部分是可以动态添加到表单或将其删除的面板。
seo-description: 可重复部分是可以动态添加到表单或将其删除的面板。
uuid: c3fa2aa4-a6b4-458e-8534-138e075290b1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 01724ca0-6901-45e7-b045-f44814ed574e
feature: 自适应表单
exl-id: f2abae0a-f7fd-4a39-bd8c-03492ce06fe9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 0%

---

# 创建具有可重复部分的表单{#creating-forms-with-repeatable-sections}

可重复部分是可动态添加到表单或将其删除的面板。

例如，在申请工作时，求职者会提供以前的雇佣详细信息，如公司名称、职责、项目和其他信息。 所有雇主的信息都需要不同但相似的部分。 在这种情况下，雇佣表提供了雇主部分，还提供了动态添加更多此类部分的选项。 这些动态添加的部分称为可重复部分。

您可以使用以下方法之一创建可重复面板：

## 通过脚本使用实例管理器  {#using-instance-manager-via-scripts-nbsp}

1. 在编辑模式下，选择一个面板，然后点按![cmppr](assets/cmppr.png)。 在侧栏中的属性下，启用&#x200B;**使面板可重复**。 为&#x200B;**[!UICONTROL Maximum]**&#x200B;和&#x200B;**[!UICONTROL Minimum]**&#x200B;字段指定值。

   最大值字段指定面板在页面上显示的最大次数。 您可以在“最大计数”字段中指定–1，以允许该面板出现无限次。

   “最小”字段指定面板在窗体上显示的最小次数。 如果将“最小计数”字段设置为零，则以后可以在演绎版完成后通过脚本删除所有实例。

   >[!NOTE]
   >
   >要创建非可重复面板，请将“最大”和“最小”字段的值设置为1。 “最大计数”字段中的折叠项布局不支持–1。 您可以指定一个高数字来给出无限值的概念。

1. 要重复的面板的父面板应包含“添加”和“删除”按钮，以管理可重复面板的实例。 执行以下步骤以将按钮插入父按钮，并启用按钮上的脚本：

   1. 在侧栏中，将按钮组件拖放到面板的父级。 选择组件并点按![edit-rules](assets/edit-rules.png)。 按钮的规则将在规则编辑器中打开。
   1. 在规则编辑器窗口中，单击&#x200B;**创建**。

      在“表单对象和函数”行中选择&#x200B;**可视编辑器**。

      1. 在规则区域的WHEN下，选择状态&#x200B;**被单击**。
      1. 在THEN下：

         * 要创建添加面板按钮，请选择&#x200B;**添加实例**，然后使用![切换侧面板](assets/toggle-side-panel.png)拖放面板，或者使用&#x200B;**放置对象或选择此处。**
         * 要创建删除面板按钮，请选择&#x200B;**删除实例**，然后使用![切换侧面板](assets/toggle-side-panel.png)拖放面板，或者使用&#x200B;**放置对象或选择此处。**

      在“表单对象和函数”行中选择&#x200B;**代码编辑器**。 单击&#x200B;**编辑规则**&#x200B;并在代码区域中：

      * 要创建添加面板按钮，请指定`this.panel.instanceManager.addInstance()`
      * 要创建删除面板按钮，请指定`this.panel.instanceManager.removeInstance(this.panel.instanceIndex)`

      单击&#x200B;**完成**。

      >[!NOTE]
      >
      >如果字段属于可重复面板，则无法在脚本中使用其名称直接访问该面板。 要访问该字段，请使用`InstanceManager`中的`instances` API指定该字段所属的可重复实例。 在`InstanceManager`中使用`instances` API的语法为：
      >
      >
      >`<panelName>.instanceManager.instances[<instanceNumber>].<fieldname>`
      >
      >
      >例如，您使用带文本框的可重复面板创建自适应表单。 当您使用三个可重复的文本框预填表单时，您需要以下xml:
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
      >有关更多信息，请参阅：类：[AEM Forms Java API引用中的InstanceManager#instances](https://adobe.com/go/learn_aemforms_documentation_63)。

      >[!NOTE]
      >
      >从自适应表单中删除面板的所有实例后，若要添加已删除面板的实例，请使用_panelName语法来捕获面板的实例管理器，并使用实例管理器的addInstance API来添加已删除的实例。 例如，_panelName.addInstance()。 它会添加删除面板的实例。















## 使用父面板的折叠面板布局   {#using-the-accordion-layout-for-the-parent-panel-nbsp}

面板具有各种布局选项。 可折叠设计布局选项开箱即用于支持可重复面板。 执行以下步骤以使用“为折叠设计设置布局”选项来重复面板：

1. 在要重复的面板的父项上，点按![cmppr](assets/cmppr.png)。 您可以在侧栏中看到这些属性。 在&#x200B;**布局**&#x200B;下拉列表中，选择&#x200B;**折叠面板**。
1. 在要重复的面板上，点按![cmppr](assets/cmppr.png)。 您可以在侧栏中看到面板属性。 启用&#x200B;**使面板可重复**&#x200B;选项卡，并为&#x200B;**最大**&#x200B;和&#x200B;**最小**&#x200B;字段指定值。

   现在，您可以使用加号(+)和删除(![delete-panel](assets/delete-panel.png))按钮来添加和删除面板。

## 使用表单模板中的重复子表单(XDP/XSD){#using-repeating-subforms-from-form-template-xdp-xsd}

可重复子表单与自适应Forms中的可重复面板类似。 在AEM Forms Designer中，执行以下步骤以创建重复子表单：

1. 在“层次结构”面板中，选择要重复的子表单的父子表单。
1. 在“对象”面板中，单击“子表单”选项卡，然后在“内容”列表中，选择“流”。
1. 选择要重复的子表单。
1. 在“对象”面板中，单击子表单选项卡，然后在“内容”列表中，选择“已定位”或“已流”。
1. 单击“绑定”选项卡，然后为每个数据项选择“重复子表单”。
1. 要指定最小重复次数，请选择最小计数，然后在关联的框中键入数字。 如果将此选项设置为0，并且在数据合并时没有为子表单中的对象提供数据，则在表单呈现时不会放置子表单。
1. 要指定子表单重复次数的最大值，请选择“最大”，然后在关联的框中键入一个数字。 如果未在“最大”框中指定值，则子表单重复次数将无限。
1. 要指定子表单重复的集数，而不考虑数据量，请选择“初始计数”，然后在关联框中键入一个数字。 如果选择此选项，并且没有可用数据或数据条目少于指定的“初始计数”值，则子表单的空实例仍会放置在表单上。
1. 在父子表单中添加两个按钮 — 一个用于添加实例，另一个用于删除可重复子表单的实例。 有关详细步骤，请参阅[构建操作](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c74572b5612a87ca2b56-8000.2.html#WS107c29ade9134a2c-1f74d86012a87d4fe55-8000.2)。
1. 现在，将表单模板链接到自适应表单。 有关详细步骤，请参阅[根据模板创建自适应表单](/help/forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-a-template)。
1. 使用在步骤9中创建的按钮添加和删除子表单。

附加的.zip文件包含一个可重复的子表单示例。

[获取文件](assets/samplerepeatablesubform.zip)

## 使用XML架构(XSD){#using-repeat-settings-of-an-xml-schema-xsd-br}的重复设置

您可以从XML架构和任何复杂类型元素的minOccours &amp; maxOccurs属性创建可重复面板。 有关XML架构的详细信息，请参阅[使用XML架构作为表单模型创建自适应表单](/help/forms/using/adaptive-form-xml-schema-form-model.md)。

在以下代码中，`SampleType`面板使用minOccours &amp; maxOccurs属性。

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
>对于非折叠布局，请使用自适应表单按钮组件来添加和删除实例。
