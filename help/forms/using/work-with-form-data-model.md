---
title: 使用表单数据模型
seo-title: 使用表单数据模型
description: 数据集成提供表单数据模型编辑器，用于配置和使用表单数据模型。
seo-description: 数据集成提供表单数据模型编辑器，用于配置和使用表单数据模型。
uuid: ed78f7f7-8123-4778-9252-89924cec09d6
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c47ef627-261e-4b4b-8846-873d3d84234b
docset: aem65
translation-type: tm+mt
source-git-commit: 726163106ddb80600eaa7cc09b1a2e9b035a223e

---


# 使用表单数据模型{#work-with-form-data-model}

![](do-not-localize/data-integeration.png)

表单数据模型编辑器提供了直观的用户界面和工具，用于编辑和配置表单数据模型。 使用编辑器，您可以在表单数据模型中添加和配置来自关联数据源的数据模型对象、属性和服务。 此外，它允许您创建数据模型对象和属性，而无需数据源，并稍后将它们与相应的数据模型对象和属性绑定。 您还可以为数据模型对象属性生成和编辑示例数据，在预览时使用这些数据预填自适应表单和交互式通信。 您可以测试在表单数据模型中配置的数据模型对象和服务，以确保它与数据源正确集成。

如果您不熟悉表单数据集成，并且尚未配置数据源或创建表单数据模型，请参阅以下主题：

* [AEM Forms数据集成](/help/forms/using/data-integration.md)
* [配置数据源](/help/forms/using/configure-data-sources.md)
* [创建表单数据模型](/help/forms/using/create-form-data-models.md)

阅读有关各种任务和配置的详细信息，您可以使用表单数据模型编辑器执行这些操作。

>[!NOTE]
>
>您必须是 **fdm-author****和forms-user** 组的成员才能创建和使用表单数据模型。 请联系AEM管理员以成为用户组的成员。

## 添加数据模型对象和服务 {#add-data-model-objects-and-services}

如果您使用数据源创建了表单数据模型，则可以使用表单数据模型编辑器来添加数据模型对象和服务、配置其属性、在数据模型对象之间建立关联以及测试表单数据模型和服务。

您可以在表单数据模型中添加来自可用数据源的数据模型对象和服务。 当添加的数据模型对象显示在“模型”选项卡中时，添加的服务显示在“服务”选项卡中。

要添加数据模型对象和服务，请执行以下操作：

1. 登录AEM作者实例，导航到“表单”>“数据集成 ****”，然后打开要在其中添加数据模型对象的表单数据模型。
1. 在“数据源”窗格中，展开数据源以视图可用的数据模型对象和服务。
1. 选择要添加到表单数据模型的数据模型对象和服务，然后点按添 **[!UICONTROL 加选定]**。

   ![选定对象](assets/selected-objects.png)

   所选数据模型对象和服务

   “模型”(Model)选项卡显示所有数据模型对象及其添加到表单数据模型的属性的图形表示形式。 每个数据模型对象由表单数据模型中的框表示。

   ![模型标签](assets/model-tab.png)

   “模型”选项卡显示添加的数据模型对象

   >[!NOTE] {graybox=&quot;true&quot;}
   >
   >您可以按住并拖动数据模型对象框，以在内容区域中组织它们。 在“数据源”窗格中，在表单数据模型中添加的所有数据模型对象都灰显。

   “服务”选项卡列表添加了服务。

   ![services-tab](assets/services-tab.png)

   “服务”选项卡显示数据模型服务

   >[!NOTE]
   >
   >除了数据模型对象和服务外，OData服务元数据文档还包括定义两个数据模型对象之间的关联的导航属性。 有关详细信息，请参 [阅使用OData服务的导航属性](#navigation-properties-odata)。

1. 点按 **[!UICONTROL 保存]** ，以保存表单模型对象。

   >[!NOTE] {graybox=&quot;true&quot;}
   >
   >您可以使用自适应表单规则调用在表单数据模型的“服务”选项卡中配置的服务。 配置的服务在规则编辑器的调用服务操作中可用。有关在自适应表单规则中使用这些服务的详细信息，请参阅在规则编辑器中调用服务和设置规 [则值](/help/forms/using/rule-editor.md)。

## 创建数据模型对象和子属性 {#create-data-model-objects-and-child-properties}

### 创建数据模型对象 {#create-data-model-objects}

虽然可以从配置的数据源添加数据模型对象，但也可以创建没有数据源的数据模型对象或实体。 如果您尚未在表单数据模型中配置数据源，则此功能特别有用。

要创建没有数据源的数据模型对象，请执行以下操作：

1. 登录AEM作者实例，导航到“表单”>“数据集成 ****”，然后打开要在其中创建数据模型对象或实体的表单数据模型。
1. 点按 **[!UICONTROL 创建实体]**。
1. 在“创建数据模型”对话框中，指定数据模型对象的名称，然后点按“添 **[!UICONTROL 加”]**。 数据模型对象被添加到表单数据模型。 请注意，新添加的数据模型对象未绑定到数据源，并且没有任何属性，如下图所示。

   ![新实体](assets/new-entity.png)

接下来，您可以在未绑定数据模型对象中添加子属性。

### 添加子属性 {#child-properties}

表单数据模型编辑器允许您在数据模型对象中创建子属性。 创建时的属性不绑定到数据源中的任何属性。 您以后可以将子属性与包含数据模型对象中的另一个属性绑定。

要创建子属性，请执行以下操作：

1. 在表单数据模型中，选择数据模型对象，然后点按创 **[!UICONTROL 建子属性]**。
1. 在“创 **[!UICONTROL 建子属性]** ”对话框中，分别在“名称”和“类型”字段中为属性指定名称 ******** 和数据类型。 您可以选择指定属性的标题和说明。
1. 启用计算（如果属性是计算属性）。 基于规则或表达式来评估计算属性的值。 有关详细信息，请参阅 [编辑属性](#edit-properties)。
1. 如果数据模型对象绑定到数据源，则添加的子属性将自动绑定到具有相同名称和数据类型的父数据模型对象的属性。

   要手动将子属性与数据模型对象属性绑定，请点按“绑定引用”字段旁边的浏 **[!UICONTROL 览图标]** 。 “选 **[!UICONTROL 择对象]** ”对话框列表父数据模型对象的所有属性。 选择要绑定的属性，然后点按勾号图标。 请注意，只能选择与子属性具有相同数据类型的属性。

1. 点按 **[!UICONTROL 完成]** ，以保存子属性，然后点 **[!UICONTROL 按保存]** ，以保存表单数据模型。 子属性现已添加到数据模型对象。

创建数据模型对象和属性后，您可以继续创建基于表单数据模型的自适应表单和交互式通信。 稍后，当您有可用的数据源并进行配置时，您可以将表单数据模型与数据源绑定。 绑定将自动在相关的自适应表单和交互式通信中进行更新。 有关使用表单数据模型创建自适应表单和交互式通信的更多信息，请参 [阅使用表单数据模型](/help/forms/using/using-form-data-model.md)。

### 绑定数据模型对象和属性 {#bind-data-model-objects-and-properties}

当要与表单数据模型集成的数据源可用时，您可以按“更新数据源”中所述将其添加到表单数 [据模型中](/help/forms/using/create-form-data-models.md#update)。 然后，执行以下操作以绑定未绑定的数据模型对象和属性：

1. 在表单数据模型中，选择要与数据源绑定的未绑定数据源。
1. 点按 **[!UICONTROL 编辑属性]**。
1. 在“编 **[!UICONTROL 辑属性]** ”窗格中，点按“绑定”字段旁边的浏览 **[!UICONTROL 图标]** 。 它打开“选 **[!UICONTROL 择对象]** ”对话框，该对话框列表在表单数据模型中添加的数据源。

   ![select-object](assets/select-object.png)

1. 展开数据源树，选择要与之绑定的数据模型对象，然后点按勾号图标。
1. 点按 **[!UICONTROL 完成]** ，以保存属性，然后点 **[!UICONTROL 按保存]** ，以保存表单数据模型。 数据模型对象现在与数据源绑定。 注意，数据模型对象不再标记为“未绑定”。

   ![绑定模型对象](assets/bound-model-object.png)

## 配置服务 {#configure-services}

要读写数据模型对象的数据，请执行以下操作以配置读写服务：

1. 选中数据模型对象顶部的复选框以将其选中，然后点按编辑 **[!UICONTROL 属性]**。

   ![edit-properties](assets/edit-properties.png)

   编辑属性以为数据模型对象配置读和写服务

   此时将打开编辑属性对话框。

   ![edit-properties-2](assets/edit-properties-2.png)

   “编辑属性”对话框

   >[!NOTE]
   >
   >除了数据模型对象和服务外，OData服务元数据文档还包括定义两个数据模型对象之间的关联的导航属性。 将OData服务数据源添加到表单数据模型时，在表单数据模型中有一个可用于数据模型对象中所有导航属性的服务。 您可以使用此服务读取相应数据模型对象的导航属性。
   >
   >
   >有关使用服务的详细信息，请参 [阅使用OData服务的导航属性](#navigation-properties-odata)。

1. 切换 **[!UICONTROL 顶级对象]** ，以指定数据模型对象是否为顶级模型对象。

   在表单数据模型中配置的数据模型对象可用于基于表单数据模型的自适应表单的内容浏览器的“数据模型对象”选项卡中。 在两个数据模型对象之间添加关联时，您要关联的数据模型对象嵌套在您要从“数据模型对象”(Data Model Objects)选项卡中关联的数据模型对象下。 如果嵌套的数据模型是顶级对象，它也将单独显示在“数据模型对象”选项卡中。 因此，您将看到它的两个条目，一个在嵌套层次结构内，另一个在嵌套层次结构外，这可能会混淆表单作者。 要使关联的数据模型对象仅显示在嵌套层次中，请禁用“顶级对象”属性。

1. 为所选数据模型对象选择“读取和写入服务”。 将显示服务的参数。

   ![读写服务](assets/read-write-services.png)

   为员工数据源配置的读写服务

1. 点 ![按aem_6_3_edit](assets/aem_6_3_edit.png) ，获取读取服务参数，将该参数绑定到“用户用户档案属性”、“请求属性”或“文本”值 [](#bindargument) ，然后指定绑定值。
1. 点 **[!UICONTROL 按完成]** ，保存参数， **[!UICONTROL 单击完成]** ，保存属性，然后 **[!UICONTROL 单击保存]** ，保存表单数据模型。

### 绑定读取服务参数 {#bindargument}

根据绑定值，将读取服务参数绑定到用户用户档案属性、请求属性或文本值。 该值作为参数传递给服务以从数据源获取与指定值关联的详细信息。

#### Literal value {#literal-value}

从“ **[!UICONTROL 绑定到]****[!UICONTROL ”下拉菜单中选择“文本”，然后在“绑定值”字段]** 中输入值 **** 。 从数据源检索与该值相关联的详细信息。 使用此选项可检索与静态值关联的详细信息。

在此示例中，从数据源检索与 **4367655678**(作为参数的值 `mobilenum` )关联的详细信息。 如果传递了移动号码参数的值，则关联的详细信息可以包括客户名称、客户地址和城市等属性。

![文本值](assets/fdm_binding_literal_new.png)

#### 用户配置文件属性 {#user-profile-attribute}

从“ **[!UICONTROL 绑定到]****[!UICONTROL ”下拉菜单中选择“用户用户档案属性”，并在“绑定值”字段中输]** 入属性名称 **** 。 登录到AEM实例的用户的详细信息将基于属性名称从数据源检索。

在“绑定值”字段中指 **[!UICONTROL 定的属性名称]** ，必须包括完整的绑定路径，直到用户的属性名。 打开以下URL以访问CRXDE上的用户详细信息：

https://&lt;server-name>:&lt;port number>/crx/de/index.jsp#/home/users/

![用户个人资料](assets/binding_crxde_user_profile_new.png)

在此示例中，在用 `profile.empid` 户的“ **[!UICONTROL 绑定值]** ”字段中指 `grios` 定。

![编辑参数](assets/edit_argument_user_profile_new.png)

该参 `id` 数使用用户用户档案的 `empid` 属性值，并将它作为参数传递给读取服务。 它从员工数据模型对象中读取并返回与登录用户关 `empid` 联的相关属性值。

#### 请求属性 {#request-attribute}

使用request属性从数据源检索关联的属性。

1. 从“ **[!UICONTROL 绑定到]****[!UICONTROL ”下拉菜单中选择“请求属性”，然后在“绑定值”字段中输入]** 属性名称 **** 。

1. 打开head.jsp以定义CRXDE上的属性详细信息：\
   `https://<server-name>:<port number>/crx/de/index.jsp#/libs/fd/af/components/page2/afStaticTemplatePage/head.jsp`

1. 在head.jsp文件中包含以下文本：

   ```
   <%Map paraMap = new HashMap();
    paraMap.put("<request_attribute>",request.getParameter("<request_attribute>"));
    request.setAttribute("paramMap",paraMap);%>
   ```

根据在请求中指定的属性名称从数据源检索详细信息。

例如，在请求中指定属 `petid=100` 性会从数据源中检索与属性值关联的属性。

## 添加关联 {#add-associations}

通常，在数据源中的数据模型对象之间构建关联。 关联可以是一对一或一对多。 例如，可以有多个与某个员工关联的依赖项。 它称为一对多关联，由连接相关数据模型对象 `1:n` 的线上所描绘。 但是，如果某个关联为给定的员工ID返回唯一的员工姓名，则它称为一对一关联。

将数据源中的关联数据模型对象添加到表单数据模型时，它们的关联将保留并显示为通过箭头线连接。 您可以在表单数据模型中跨不同数据源添加数据模型对象之间的关联。

>[!NOTE] {graybox=&quot;true&quot;}
>
>JDBC数据源中的预定义关联不会保留在表单数据模型中。 您必须手动创建它们。

要添加关联，请执行以下操作：

1. 选中数据模型对象顶部的复选框以将其选中，然后点按添加 **[!UICONTROL 关联]**。 此时将打开“添加关联”对话框。

   ![添加关联](assets/add-association.png)

   >[!NOTE]
   >
   >除了数据模型对象和服务外，OData服务元数据文档还包括定义两个数据模型对象之间的关联的导航属性。 在表单数据模型中添加关联时，可以使用这些导航属性。 有关详细信息，请参 [阅使用OData服务的导航属性](#navigation-properties-odata)。

   此时将打开“添加关联”对话框。

   ![add-association-2](assets/add-association-2.png)

   “添加关联”对话框

1. 在“添加关联”窗格中：

   * 指定关联的标题。
   * 选择关联类型— 一对一或一对多。
   * 选择要与之关联的数据模型对象。
   * 选择读取服务以从所选模型对象读取数据。 将显示读取服务参数。 编辑以更改参数（如果需要），并将其绑定到要关联的数据模型对象的属性。
   在以下示例中，Dependents数据模型对象的读取服务的默认参数是 `dependentid`。

   ![add-association-example](assets/add-association-example.png)

   依赖项读取服务的默认参数是dependentid

   但是，参数必须是关联数据模型对象之间的公用属性，在本例中为 `Employeeid`。 因此，该参 `Employeeid` 数必须绑定到Employee数据模型对象的属 `id` 性，才能从Dependents数据模型对象中获取关联的依赖项详细信息。

   ![add-association-example-2](assets/add-association-example-2.png)

   更新了参数和绑定

   点按 **[!UICONTROL 完成]** ，以保存参数。

1. 点按 **[!UICONTROL 完成]** ，以保存关联，然后 **[!UICONTROL 点按保存]** ，以保存表单数据模型。
1. 重复这些步骤以根据需要创建更多关联。

>[!NOTE] {graybox=&quot;true&quot;}
>
>添加的关联显示在数据模型对象框中，具有指定的标题和连接相关数据模型对象的线。
>
>您可以通过选中关联对应的复选框来编辑关联，然后点按编 **[!UICONTROL 辑关联]**。

![添加的关联](assets/added-association.png)

## 编辑属性 {#properties}

您可以编辑数据模型对象的属性、其属性以及在表单数据模型中添加的服务。

要编辑属性，请执行以下操作：

1. 选中表单数据模型中数据模型对象、属性或服务旁边的复选框。
1. 点按 **[!UICONTROL 编辑属性]**。 此时 **[!UICONTROL 将打开选定模型对象]** 、属性或服务的“编辑属性”(Edit Properties)窗格。

   * **数据模型对象**:指定读写服务和编辑参数。
   * **属性**:指定属性的类型、子类型和格式。 您还可以指定选定属性是否为数据模型对象的主要键。
   * **服务**:指定服务的输入模型对象、输出类型和参数。 对于Get服务，您可以指定它是否需要返回数组。
   ![edit-properties-service](assets/edit-properties-service.png)

   获取服务的“编辑属性”对话框

1. 点按 **[!UICONTROL 完成]** ，以保存属性，然后 **[!UICONTROL 点按保存]** ，以保存表单数据模型。

### 创建计算属性 {#computed}

计算属性是根据规则或表达式计算其值的属性。 使用规则，您可以将计算属性的值设置为表单数据模型中的文本字符串、数字、数学表达式的结果或其他属性的值。

例如，可以创建一个计算属性 **FullName** ，其值是将现有 **FirstName** 和 **** LastName属性串联的结果。 为此，请执行以下操作：

1. 使用数据类型为“字符串” `FullName` 的名称创建新属性。
1. 启用 **[!UICONTROL 计算]** ，然后点 **[!UICONTROL 按完成]** ，以创建属性。

   ![已计算](assets/computed.png)

   将创建FullName计算属性。 请注意属性旁边的图标以描述计算的属性。

   ![computed-prop](assets/computed-prop.png)

1. 选择FullName属性，然后点按编 **[!UICONTROL 辑规则]**。 规则编辑器窗口将打开。
1. 在规则编辑器窗口中，点按创 **[!UICONTROL 建]**。 “设 **[!UICONTROL 置值]** ”规则窗口打开。

   从“选择选项”下拉菜单中，选择“数学 **[!UICONTROL 表达式”]**。 其他可用选项是 **[!UICONTROL 表单数据模型对象]** 和 **[!UICONTROL 字符串]**。

1. 在数学表达式中，分别 **[!UICONTROL 在第一个对象和第]** 二个对象中选择FirstName **[!UICONTROL 和]** LastName。 选择 **[!UICONTROL 加号]** ，作为运算符。

   点按 **[!UICONTROL 完成]** ，然后点 **[!UICONTROL 按关闭]** ，以关闭规则编辑器窗口。 该规则类似于以下内容。

   ![规则](assets/rule.png)

1. 在表单数据模型上，点按保 **[!UICONTROL 存]**。 已配置计算属性。

## 使用OData服务的导航属性 {#work-with-navigation-properties-of-odata-services}

在OData服务中，导航属性用于定义两个数据模型对象之间的关联。 这些属性是在实体类型或复杂类型上定义的。 例如，在从示例 [TripPin](https://www.odata.org/blog/trippin-new-odata-v4-sample-service/) OData示例服务的元数据文件中提取的以下内容中，人物实体包含三个导航属性——朋友、最好朋友和旅行。

有关导航属性的详细信息，请参阅 [OData文档](https://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part3-csdl/odata-v4.0-errata03-os-part3-csdl-complete.html#_Toc453752536)。

```xml
<edmx:Edmx xmlns:edmx="https://docs.oasis-open.org/odata/ns/edmx" Version="4.0">
<script/>
<edmx:DataServices>
<Schema xmlns="https://docs.oasis-open.org/odata/ns/edm" Namespace="Microsoft.OData.Service.Sample.TrippinInMemory.Models">
<EntityType Name="Person">
<Key>
<PropertyRef Name="UserName"/>
</Key>
<Property Name="UserName" Type="Edm.String" Nullable="false"/>
<Property Name="FirstName" Type="Edm.String" Nullable="false"/>
<Property Name="LastName" Type="Edm.String"/>
<Property Name="MiddleName" Type="Edm.String"/>
<Property Name="Gender" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.PersonGender" Nullable="false"/>
<Property Name="Age" Type="Edm.Int64"/>
<Property Name="Emails" Type="Collection(Edm.String)"/>
<Property Name="AddressInfo" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Location)"/>
<Property Name="HomeAddress" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Location"/>
<Property Name="FavoriteFeature" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Feature" Nullable="false"/>
<Property Name="Features" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Feature)" Nullable="false"/>
<NavigationProperty Name="Friends" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Person)"/>
<NavigationProperty Name="BestFriend" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Person"/>
<NavigationProperty Name="Trips" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Trip)"/>
</EntityType>
```

在表单数据模型中配置OData服务时，实体容器中的所有导航属性都可通过表单数据模型中的服务来使用。 在TripPin OData服务的此示例中，可以使用表单数据模型中的一个服务读取实体容器中 `Person``GET LINK` 的三个导航属性。

以下内容突出 `GET LINK of Person /People` 了表单数据模型中的服务，表单数据模型是TripPin OData服务实体中三个导航属 `Person` 性的组合服务。

![nav-prop-service](assets/nav-prop-service.png)

将服务添加 `GET LINK` 到表单数据模型中的“服务”选项卡后，您可以编辑属性以选择要在服务中使用的输出模型对象和导航属性。 例如，以下示例 `GET LINK of Person /People` 中的下列服务使用Trip作为输出模型对象，使用导航属性作为Trips。

![edit-prop-nav-prop](assets/edit-prop-nav-prop.png)

>[!NOTE]
>
>NavigationPropertyName参数的 **Default Value** （默认值）字段中 **的可用值取决于****Return数组的状态？** 切换按钮。 启用此选项后，将显示“集合”类型的导航属性。

在此示例中，您还可以选择输出模型对象作为Person，选择导航属性参数作为Friends或BestFriend(取决于 **Return数组？** 启用或禁用)。

![edit-prop-nav-prop2](assets/edit-prop-nav-prop2.png)

同样，在表单数据模型 `GET LINK` 中添加关联时，您可以选择服务并配置其导航属性。 但是，要能够选择导航属性，请确保将“绑 **[!UICONTROL 定到”字段设]** 置为 **Literal**。

![add-association-nav-prop](assets/add-association-nav-prop.png)

## 生成和编辑示例数据 {#sample}

表单数据模型编辑器允许您为表单数据模型中的所有数据模型对象属性（包括计算属性）生成示例数据。 它是一组随机值，它们符合为每个属性配置的数据类型。 您还可以编辑和保存数据，即使重新生成示例数据，数据也会保留。

执行以下操作以生成和编辑示例数据：

1. 打开表单数据模型并点按编 **[!UICONTROL 辑示例数据]**。 它会在“编辑示例数据”窗口中生成并显示示例数据。

   ![生成示例数据](assets/form_data_model_generate_sample_data_new.png)

1. 在“ **[!UICONTROL 编辑示例数据]** ”窗口中，根据需要编辑数据，然后点按 **[!UICONTROL 保存]**。

接下来，您可以使用范例数据基于表单数据模型预填和测试交互式通信。 有关详细信息，请参 [阅使用表单数据模型](/help/forms/using/using-form-data-model.md)。

## 测试数据模型对象和服务 {#test-data-model-objects-and-services}

您的表单数据模型已配置，但在投入使用之前，您可能希望测试配置的数据模型对象和服务是否按预期工作。 要测试数据模型对象和服务，请执行以下操作：

1. 在表单数据模型中选择数据模型对象或服务，并分别点按 **[!UICONTROL 测试模型对象]****[!UICONTROL 或测试服务]**。

   “测试表单数据模型”窗口将打开。

   ![测试数据模型](assets/test-data-model.png)

1. 在“测试表单数据模型”窗口中，从“输入”窗格中选择要测试的数据模型对象或服务。

1. 在测试代码中指定参数值，然后点按 **[!UICONTROL 测试]**。 成功的测试会在“输出”窗格中返回输出。

   ![测试结果](assets/test_results_form_data_model_new.png)

同样，您可以测试表单数据模型中的其他数据模型对象和服务。

## 输入数据的自动验证 {#automated-validation-of-input-data}

表单数据模型（基于表单数据模型中可用的验证标准）验证在调用DermisBridge API时作为输入接收的数据。 验证基于在用于调 `ValidationOptions` 用API的查询对象中设置的标志。

该标志可以设置为以下任意值：

* **完整**:FDM根据所有约束执行验证
* **关闭**:无验证
* **基本**:FDM根据“必需”和“nullable”约束执行验证

如果没有为标记设置任何 `ValidationOptions`值，则 **对输入数据执行BASIC** 验证。

以下是将验证标志设置为 **FULL的示例**:

```java
operationOptions.setValidationOptions(ValidationOptions.FULL);
```

>[!NOTE]
>
>您为输入数据中的属性提供的值必须与为元数据文档中的属性定义的数据类型相匹配。\
>如果该值与为属性定义的数据类型不匹配，则DermisBridge API将显示一个例外，而不考虑标志的 `ValidationOptions` 值。 如果日志级别设置为“调试”，则错误将记录到 **error.log文件** 。

表单数据模型基于数据类型约束的列表验证输入数据。 输入数据的约束列表可能因数据源而异。

下表列表了基于数据源的输入数据的约束：

<table>
 <tbody> 
  <tr> 
   <td>约束</td> 
   <td>描述</td> 
   <td>输入数据源</td> 
  </tr> 
  <tr> 
   <td>必需</td> 
   <td>如果为true，则该参数必须包含在输入数据中。</td> 
   <td>Swagger、WSDL和数据库</td> 
  </tr> 
  <tr> 
   <td>null</td> 
   <td>如果为true，则输入数据中的参数值可设置为Null。</td> 
   <td>WSDL、Odata和数据库</td> 
  </tr> 
  <tr> 
   <td>最大</td> 
   <td>指定数值的上界。 指定为上界的最大值也可以分配给输入数据中的参数。</td> 
   <td>Swagger和WSDL</td> 
  </tr> 
  <tr> 
   <td>最小</td> 
   <td>指定数值的下界。 指定为下限的最小值也可以分配给输入数据中的参数。</td> 
   <td>Swagger和WSDL</td> 
  </tr> 
  <tr> 
   <td>exclusiveMaximum</td> 
   <td>指定数值的上界。 指定为上限的最大值不能分配给输入数据中的参数。</td> 
   <td>Swagger和WSDL</td> 
  </tr> 
  <tr> 
   <td>exclusiveMinimum</td> 
   <td>指定数值的下界。 指定为下限的最小值不能分配给输入数据中的参数。</td> 
   <td>Swagger和WSDL</td> 
  </tr> 
  <tr> 
   <td>minLength</td> 
   <td>指定字符串中包含的字符数的下界。 指定为下限的最小值也可以分配给输入数据中的参数。</td> 
   <td>Swagger和WSDL</td> 
  </tr> 
  <tr> 
   <td>maxLength</td> 
   <td>指定字符串中包含的字符数的上界。 指定为上界的最大值也可以分配给输入数据中的参数。</td> 
   <td>Swagger、WSDL、Odata和数据库</td> 
  </tr> 
  <tr> 
   <td>图案</td> 
   <td>指定固定的字符序列。 仅当字符符合指定的模式时，输入字符串才成功验证。</td> 
   <td>斯瓦格</td> 
  </tr> 
  <tr> 
   <td>minItems</td> 
   <td>指定数组中最小项数。 指定为下限的最小值也可以分配给输入数据中的参数。</td> 
   <td>Swagger和WSDL</td> 
  </tr> 
  <tr> 
   <td>maxItems</td> 
   <td>指定数组中最大项数。 指定为上界的最大值也可以分配给输入数据中的参数。</td> 
   <td>Swagger和WSDL</td> 
  </tr> 
  <tr> 
   <td>uniqueItems</td> 
   <td>如果为true，则该数组的所有元素在输入数据中必须是唯一的。</td> 
   <td>斯瓦格</td> 
  </tr> 
  <tr> 
   <td>enum(string)<br /><br /> </td> 
   <td>将输入数据中参数的值限制为一组固定的字符串值。 它必须是至少一个元素的数组，其中每个元素都是唯一的。</td> 
   <td>Swagger、WSDL和Odata</td> 
  </tr> 
  <tr> 
   <td>enum(number)<br /><br /> </td> 
   <td>将输入数据中参数的值限制为一组固定的数字值。 它必须是至少一个元素的数组，其中每个元素都是唯一的。</td> 
   <td>WSDL</td> 
  </tr> 
 </tbody> 
</table>

在此示例中，根据Swagger文件中定义的最大、最小和必需约束验证输入数据。 仅当订单ID存在且其值在1到10之间时，输入数据才符合验证标准。

```xml
parameters: [
{
name: "orderId",
in: "path",
description: "ID of pet that needs to be fetched",
required: true,
type: "integer",
maximum: 10,
minimum: 1,
format: "int64"
}
]
```

如果输入数据不符合验证条件，则显示异常。 如果日志级别设置为 **Debug**，则错误将记录到 **error.log文件** 。 例如，

```java
21.01.2019 17:26:37.411 *ERROR* com.adobe.aem.dermis.core.validation.JsonSchemaValidator {"errorCode":"AEM-FDM-001-044","errorMessage":"Input validations failed during operation execution.","violations":{"/orderId":["numeric instance is greater than the required maximum (maximum: 10, found: 16)"]}}
```

## 后续步骤 {#next-steps}

您有一个工作表单数据模型，它现在可以在自适应表单和交互式通信工作流中使用。 有关详细信息，请参 [阅使用表单数据模型](/help/forms/using/using-form-data-model.md)。
