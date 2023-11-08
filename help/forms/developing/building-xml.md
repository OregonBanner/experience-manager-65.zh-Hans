---
title: 如何在AEM Forms on JEE Workbench中使用execute脚本服务来构建XML数据？
description: 使用AEM Forms on JEE Workbench中的执行脚本服务构建XML数据
exl-id: 2ec57cd4-f41b-4e5c-849d-88ca3d2cfe19
source-git-commit: e2a3470784beb04c2179958ac6cb98861acfaa71
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# 使用AEM Forms on JEE Workbench中的执行脚本服务构建XML数据 {#using-execute-script-service-forms-jee-workbench}

JEE流程管理工作流中AEM Forms涉及许多XML，例如：可以在流程中构建XML信息并将其发送到JEE Workspace上的AEM Forms中的Flex应用程序，用于系统设置，或者在表单之间传递信息。 在许多情况下，JEE上的AEM Forms开发人员需要管理XML，并且很多时候这需要通过JEE上的AEM Forms流程来管理XML。

在处理简单的XML设置时，可以使用 `Set Value` 服务，它是JEE服务中的默认AEM Forms。 此服务设置流程数据模型中一个或多个数据项的值。 对于简单的条件逻辑“如果为，则为”方案，此服务可以适合该目的。

但是，在更复杂的情况下，设置值服务没有那么有效。 在这些情况下，必须依赖一组更可靠的编程命令，如由Java™等编程语言提供的命令。 使用Java™构建复杂的XML比通过Set Value服务中的简单文本构建XML文档简单得多，也清晰得多。 此外，在Java™中纳入条件编程比在Set Value服务中更容易。

## 在进程中使用执行脚本服务 {#using-execute-script-service-in-process}

在AEM Forms on JEE Workbench中提供的一组AEM Forms on JEE标准服务中， `Execute Script` 服务。 此服务允许您在进程中执行脚本，并提供 `executeScript` 操作完成此操作。

### 使用定义为活动的“执行脚本”服务创建应用程序和进程 {#create-an-application}

在本教程中，整个应用程序和进程创建不在范围之内，但出于本说明的目的，已创建名为“DemoApplication02”的应用程序。 假定已创建应用程序，则需要在此应用程序中创建进程以调用executeScript服务。 向应用程序添加一个进程，其中包括 `Execute Script` 服务：

1. 右键单击您的应用程序并选择 **[!UICONTROL 新建]**. 在 **[!UICONTROL 新建]** 滑出菜单，选择 **[!UICONTROL 进程]**. 命名您的进程，添加说明（如有必要），然后选择要代表此进程的图标。 在本教程中，我们创建了一个流程，并将其命名为  `executeScriptDemoProcess`.
1. 定义您的起点，或简单地选择稍后添加起点。
1. 该流程现已创建，应会在以下位置自动打开： [!UICONTROL 流程设计] 窗口。 在此窗口中，单击“流程设计”窗口顶部的“活动选取器”图标，然后将新活动拖到泳道上。 此时， [!UICONTROL 定义活动窗口] （请参见下图）。
   ![定义活动](assets/define-activity.jpg)
1. executeScript服务位于 `Foundation` 服务集。 服务名称将对象列为 `Execute Script – 1.0` 具有操作名称 `executeScript`. 单击以选择此项目。
1. 现在应创建此流程，默认情况下， [!UICONTROL 进程属性] 窗口应出现在左侧的窗格中。

#### 使用“Execute Script”服务向进程添加脚本 {#add-script-to-process-with-execute-script}

在定义“执行脚本”服务活动的情况下创建进程后，即可向此进程添加脚本。 向此进程添加脚本：

1. 导航至 [!UICONTROL 进程属性] 调色板。 在此面板中，展开 [!UICONTROL 输入] 部分中，然后单击“……”图标。

1. 在出现的文本框中编写脚本。 编写脚本后，按“确定”（参见下图）。
   ![执行脚本](assets/execute-script.jpg)

## 使用Execute Script服务创建XML {#create-xml-execute-script-service}

一旦创建了包含了Execute Script服务的进程，就可以使用此脚本创建XML。 可以使用将脚本添加到进程中的文本框中的以下说明编写脚本 `Execute Script` “服务”部分。

**关于Execute Script服务的技术**

要了解Execute Script服务的功能和限制，必须了解该服务的技术基础。 JEE上的AEM Forms使用Apache Xerces文档对象模型(DOM)解析器在进程中创建和存储XML变量。 Xerces是W3C的Java™实现文档对象模型规范，定义了 [此处](https://dom.spec.whatwg.org/). DOM规范是自1998年以来出现的一种处理XML的标准方法。 Xerces的Java™实现Xerces-J支持DOM Level 2 1.0版。

用于存储XML变量的Java™类包括：

* org.apache.xerces.dom.NodeImpl和

* org.apache.xerces.dom.DocumentImpl

DocumentImpl是NodeImpl的子类，因此可以假定任何XML进程变量都是NodeImpl派生。 您可以找到有关NodeImpl的文档 [此处](https://xerces.apache.org/xerces-j/apiDocs/org/apache/xerces/dom/NodeImpl.html).

**使用Execute Script服务创建示例XML**

以下是在Execute Script服务中创建XML的示例。 进程具有XML类型的变量节点。 此活动的结果是一个XML文档。 该文档的作用，或它如何应用于整个过程在本教程中超出了范围；最终要归结到在整个应用程序中需要使用XML做什么。 正如简介中所述，XML在AEM Forms中可用于JEE表单和流程中的许多用途，这仅仅是说明如何对“执行脚本”活动进行编码以输出简单的XML文档。

用于输出XML的简单JavaScript如下所示：

```xml
import org.apache.xerces.dom.DocumentImpl;

import org.w3c.dom.Document;

import org.w3c.dom.Element;



Document document = new DocumentImpl();

Element topLevelResources = document.createElement("resources");

Element resource = document.createElement("resource");

resource.setAttribute("id", "first item id");

resource.setAttribute("value", "first item value");

topLevelResources.appendChild(resource);

document.appendChild(topLevelResources);

patExecContext.setProcessDataValue("/process_data/node", document);
```

>[!NOTE]
>
>必须将前面提到的DOM对象导入到脚本中。

此简单脚本的结果是新的XML文档，其变量节点设置为：

```xml
<resources>

<resource id="first item id" value="first item value"/>

</resources>
```

**使用迭代循环将节点添加到XML**

节点也可以添加到进程中的现有XML变量中。 变量node包含已创建的XML对象。

```xml
Document document = patExecContext.getProcessDataValue("/process_data/node");

NodeList childNodes = document.getChildNodes();

int numChildren = childNodes.getLength();

for (int i = 0; i < numChildren; i++)

{

Node currentChild = childNodes.item(i);

if (currentChild.getNodeType() == Node.ELEMENT_NODE)

{

// found the top-level node

Element newResource = document.createElement("resource");

newResource.setAttribute("id", "second item id");

newResource.setAttribute("value", "second item value");

currentChild.appendChild(newResource);

break;

}

}

patExecContext.setProcessDataValue("/process_data/node", document);
The variable node in the XML is now set to:

<resources> 

<resource id="first item id" value="first item value"/> 

<resource id="second item id" value="second item value"/> 

</resources>
```
