---
title: 如何在JEE Workbench上使用AEM Forms中的执行脚本服务来构建XML数据？
description: 使用JEE Workbench上AEM Forms中的执行脚本服务来构建XML数据
source-git-commit: 730ae7cd6cd04eb6377b37eafe29db597e93cce3
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---

# 使用JEE Workbench上AEM Forms中的执行脚本服务来构建XML数据 {#using-execute-script-service-forms-jee-workbench}

在JEE流程管理工作流中，AEM Forms涉及大量XML，例如：XML信息可以在流程中构建，并发送到JEE Workspace上AEM Forms中的Flex应用程序，用于系统设置，或将信息传递到表单和表单。 在很多情况下，JEE上的AEM Forms开发人员需要管理XML，但很多时候这要求XML通过JEE上的AEM Forms流程进行管理。

处理简单的XML设置时，您可以使用`Set Value`服务，该服务是JEE服务上的默认AEM Forms。 此服务设置流程数据模型中一个或多个数据项的值。 对于非常简单的条件逻辑“如果这样，那么就是那样”方案，此服务可以满足其目的。

但是，在更复杂的情况下，“设置值”服务没有那么有效。 在这些情况下，需要依赖一组更强健的编程命令，例如由诸如Java之类的编程语言提供的那些命令。 使用Java构建复杂的XML比在“设置值”服务中从简单文本构建XML文档更简单、更清晰。 此外，在Java中包含条件编程比在设置值服务中更容易。

## 在进程中使用执行脚本服务 {#using-execute-script-service-in-process}

在JEE Workbench上AEM Forms中提供的JEE上的标准AEM Forms服务的集合中，是`Execute Script`服务。 此服务允许您在进程中执行脚本，并提供`executeScript`操作来执行。

### 创建将“执行脚本”服务定义为活动的应用程序和进程 {#create-an-application}

在本教程中，整个应用程序和进程创建都不适合，但为了本说明，我们创建了一个名为“DemoApplication02”的应用程序。 假定已创建应用程序，我们需要在此应用程序中创建一个进程以调用executeScript服务。 要向包含`Execute Script`服务的应用程序添加进程，请执行以下操作：

1. 右键单击您的应用程序并选择[!UICONTROL 新建]。 在[!UICONTROL New]滑出菜单中，选择[!UICONTROL Process]。 相应地命名您的流程，根据需要添加描述，然后选择要表示此流程的图标。 在本教程中，我们创建了一个进程，并将其命名为`executeScriptDemoProcess`。
1. 定义起点，或简单选择稍后添加起点。
1. 该进程现已创建完成，应在[!UICONTROL 流程设计]窗口中自动打开。 在此窗口中，单击“流程设计”窗口顶部的活动选取器图标，然后将新活动拖动到泳道上。 此时应会显示[!UICONTROL 定义活动窗口]（请参阅下图）。
   ![定义活动](assets/define-activity.jpg)
1. executeScript服务可在`Foundation`服务集下找到。 服务名称将对象列为`Execute Script – 1.0`，操作名称为`executeScript`。 单击以选择此项目。
1. 此时应创建此进程，默认情况下，[!UICONTROL 进程属性]窗口应显示在左侧的窗格中。

#### 使用“执行脚本”服务向进程添加脚本 {#add-script-to-process-with-execute-script}

在定义了“执行脚本”服务活动创建进程后，您便可以向此进程添加脚本。 要向此过程添加脚本，请执行以下操作：

1. 导航到[!UICONTROL Process Properties]面板。 在此面板中，展开[!UICONTROL Input]部分，然后单击“……”图标。

1. 在显示的文本框中，写入您的脚本。 写完脚本后，按“确定”（请参阅下图）。
   ![执行脚本](assets/execute-script.jpg)

## 使用Execute Script服务创建XML {#create-xml-execute-script-service}

创建包含执行脚本服务的进程后，可以使用此脚本创建XML。 您可以在上面`Execute Script`服务向流程添加脚本一节中描述的文本框中编写下面描述的脚本。

**关于执行脚本服务的技术**

为了了解执行脚本服务的能力和限制，您必须了解该服务的技术基础。 AEM Forms on JEE使用Apache Xerces文档对象模型(DOM)解析器在进程中创建和存储XML变量。 Xerces是W3C文档对象模型规范的Java实现；此处](https://dom.spec.whatwg.org/)定义了[。 DOM规范是处理自1998年以来一直存在的XML的一种标准方式。 Xerces - J的Java实现支持DOM 2级1.0版。

用于存储XML变量的Java类包括：

* org.apache.xerces.dom.NodeImpl和

* org.apache.xerces.dom.DocumentImpl

DocumentImpl是NodeImpl的子类，因此可以假定任何XML进程变量都是NodeImpl派生。 您可以在此处](http://xerces.apache.org/xerces-j/apiDocs/org/apache/xerces/dom/NodeImpl.html)找到有关NodeImpl [的文档。

**使用Execute Script服务创建XML的示例**

以下是在执行脚本服务中创建XML的示例。 该进程具有XML类型的变量节点。 此活动的最终结果将是XML文档。 该文档的用途或它如何适用于整个过程，在本教程中是不可用的；最终取决于XML在整个应用程序中所需执行的操作。 正如导言中所述，XML可在JEE表单和流程上的AEM Forms中用于多种目的，这只是对如何对执行脚本活动进行代码以输出简单XML文档的说明。

用于输出XML的简单Java脚本如下所示：

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
>必须将上述DOM对象导入脚本。

此简单脚本的结果是新的XML文档，其变量节点设置为：

```xml
<resources>

<resource id="first item id" value="first item value"/>

</resources>
```

**使用迭代循环向XML添加节点**

节点也可以添加到进程内的现有XML变量中。 变量（节点）包含我们刚刚创建的XML对象。

```xml
Document document = patExecContext.getProcessDataValue("/process_data/node");

NodeList childNodes = document.getChildNodes();

int numChildren = childNodes.getLength();

for (int i = 0; i < numChildren; i++)

{

Node currentChild = childNodes.item(i);

if (currentChild.getNodeType() == Node.ELEMENT_NODE)

{

// found the top level node

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



