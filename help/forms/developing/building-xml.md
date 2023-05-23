---
title: 如何在AEM Forms on JEE Workbench中使用執行指令碼服務來建置XML資料？
description: 使用AEM Forms on JEE Workbench中的執行指令碼服務來建置XML資料
exl-id: 2ec57cd4-f41b-4e5c-849d-88ca3d2cfe19
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---

# 使用AEM Forms on JEE Workbench中的執行指令碼服務來建置XML資料 {#using-execute-script-service-forms-jee-workbench}

JEE程式管理工作流程中AEM Forms涉及許多XML，例如：XML資訊可建置在程式中，並傳送至JEE Workspace上AEM Forms的Flex應用程式，用於系統設定，或傳遞資訊至表單。 在許多情況下，JEE上的AEM Forms開發人員需要管理XML，而且很多時候這需要透過JEE上的AEM Forms流程來管理XML。

處理簡單XML設定時，可以使用 `Set Value` 服務，這是JEE服務的預設AEM Forms。 此服務會設定流程資料模型中一或多個資料專案的值。 對於非常簡單的條件邏輯「如果是，則是」情況，此服務可以符合目的。

不過，在更複雜的情況下，「設定值」服務並不那麼有效。 在這些情況下，需要依賴一組更強大的程式設計指令，例如Java等程式設計語言所提供的指令。 使用Java來建置複雜的XML，會比在Set Value服務內從簡單文字建置XML檔案簡單得多，也清楚得多。 此外，在Java中包含條件式程式設計比在Set Value服務中更容易。

## 在程式中使用執行指令碼服務 {#using-execute-script-service-in-process}

在AEM Forms on JEE Workbench提供的標準AEM Forms on JEE服務集內， `Execute Script` 服務。 此服務可讓您在程式中執行指令碼，並提供 `executeScript` 操作完成。

### 使用定義為活動的「執行指令碼」服務建立應用程式和程式 {#create-an-application}

在本教學課程中，整體應用程式和程式建立不在涵蓋範圍內，但基於此指示，我們已建立一個名為「DemoApplication02」的應用程式。 假設應用程式已建立，我們需要在此應用程式中建立程式來呼叫executeScript服務。 若要將流程新增至應用程式，其中包含 `Execute Script` 服務：

1. 以滑鼠右鍵按一下您的應用程式並選取 [!UICONTROL 新增]. 在 [!UICONTROL 新增] 滑出功能表，選取 [!UICONTROL 程式]. 為流程命名，並視需要新增說明，然後選取您要代表此流程的圖示。 出於本教學課程的目的，我們已建立一個流程，並將其命名為  `executeScriptDemoProcess`.
1. 定義您的起點，或稍後新增起點的簡單選擇。
1. 程式現在已建立，應會在以下位置自動開啟： [!UICONTROL 程式設計] 視窗。 在此視窗中，按一下「流程設計」視窗上方的「活動選擇器」圖示，並將新活動拖曳至泳道上。 此時， [!UICONTROL 定義活動視窗] （請參閱下圖）。
   ![定義活動](assets/define-activity.jpg)
1. executeScript服務可在 `Foundation` 服務集。 「服務」名稱會將物件列為 `Execute Script – 1.0` 具有作業名稱 `executeScript`. 按一下以選取此專案。
1. 現在應建立此程式，且預設為 [!UICONTROL 程式屬性] 視窗應出現在左側的窗格中。

#### 使用「執行指令碼」服務將指令碼新增至處理序 {#add-script-to-process-with-execute-script}

一旦使用定義的「執行指令碼」服務活動建立處理序後，就可以將指令碼新增至此處理序。 若要將指令碼新增至此程式：

1. 導覽至 [!UICONTROL 程式屬性] 調色盤。 在此浮動視窗中，展開 [!UICONTROL 輸入] 區段，然後按一下「……」圖示。

1. 在出現的文字方塊中，撰寫您的指令碼。 當指令碼已撰寫時，請按[確定] （請參閱下圖）。
   ![執行指令碼](assets/execute-script.jpg)

## 使用Execute Script Service建立XML {#create-xml-execute-script-service}

一旦建立包含Execute Script服務的處理程式後，就可以使用此指令碼來建立XML。 您可以使用將指令碼新增至處理序中所述的文字方塊來撰寫以下所述的指令碼 `Execute Script` 服務區段的上方。

**關於Execute Script服務的技術**

為了知道Execute Script服務的功能和限制，必須知道服務的技術基礎。 JEE上的AEM Forms使用Apache Xerces檔案物件模型(DOM)剖析器，在程式中建立和儲存XML變數。 Xerces是W3C檔案物件模型規格的Java實作；已定義 [此處](https://dom.spec.whatwg.org/). DOM規格是操作XML的標準方法，自1998年以來，XML便已出現。 Xerces的Java實作Xerces-J支援DOM Level 2 1.0版。

用來儲存XML變數的Java類別為：

* org.apache.xerces.dom.NodeImpl和

* org.apache.xerces.dom.DocumentImpl

DocumentImpl是NodeImpl的子類別，因此可以假設任何XML程式變數都是NodeImpl衍生。 您可以找到NodeImpl的檔案 [此處](https://xerces.apache.org/xerces-j/apiDocs/org/apache/xerces/dom/NodeImpl.html).

**使用Execute Script Service建立XML的範例**

以下是在Execute Script服務中建立XML的範例。 處理序有一個變數（節點），其型別為XML。 此活動的最終結果將為XML檔案。 此檔案有什麼作用，或如何套用至整個程式，這在本教學課程的討論範圍之外；最終要歸結為在整個應用程式中需要使用XML做什麼。 如簡介中所述，XML可用於AEM Forms中JEE表單和程式的許多用途，這僅僅是對如何編寫執行指令碼活動代碼以輸出簡單XML檔案的說明。

輸出XML的簡單Java指令碼看起來像這樣：

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
>上述DOM物件必須匯入指令碼中。

此簡單指令碼的結果是新XML檔案，其中變數節點設為：

```xml
<resources>

<resource id="first item id" value="first item value"/>

</resources>
```

**使用反複回圈將節點新增至XML**

節點也可以新增至程式中的現有XML變數。 變數node包含我們剛建立的XML物件。

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
