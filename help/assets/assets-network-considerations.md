---
title: 網路考量與需求
description: 討論設計網路時的網路考量事項 [!DNL Adobe Experience Manager Assets] 部署。
contentOwner: AG
role: Architect, Admin
feature: Developer Tools
exl-id: 1313842c-18b1-4727-ba63-b454d0f5a2cc
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# [!DNL Assets] 網路考量事項 {#assets-network-considerations}

瞭解您的網路和瞭解一樣重要 [!DNL Adobe Experience Manager Assets]. 網路可能會影響上傳、下載和使用者體驗。 繪製網路拓撲圖有助於找出網路中的瓶頸點和次最佳化區域，您必須修正這些區域才能改善網路效能和使用者體驗。

請確定您的網路圖表中包含下列專案：

* 從使用者端裝置（例如電腦、行動裝置和平板電腦）連線到網路。
* 公司網路的拓撲。
* 從公司網路和 [!DNL Experience Manager] 環境。
* 的拓撲 [!DNL Experience Manager] 環境。
* 定義同時的消費者 [!DNL Experience Manager] 網路介面。
* 已定義的工作流程 [!DNL Experience Manager] 部署。

## 從使用者端裝置連線到企業網路 {#connectivity-from-the-client-device-to-the-corporate-network}

首先，繪製個別使用者端裝置與企業網路之間的連線圖。 在這個階段，識別共用資源，例如WiFi連線，讓多位使用者存取相同的點或乙太網路交換器以上傳和下載資產。

![chlimage_1-353](assets/chlimage_1-353.png)

使用者端裝置會以各種方式連線至企業網路，例如共用WiFi、乙太網路至共用交換器，以及VPN。 識別並瞭解此網路上的咽喉 [!DNL Assets] 規劃及修改網路。

在圖表的左上方，三個裝置被描繪為共用48 Mbps WiFi存取點。 如果所有裝置同時上傳，WiFi網路頻寬會在裝置之間共用。 相較於系統整體，使用者可能會在此劃分的管道中遇到三個使用者端的不同瓶頸。

測量WiFi網路的真實速度是一項挑戰，因為速度緩慢的裝置可能會影響存取點上的其他使用者端。 如果您打算使用WiFi進行資產互動，請同時從多個使用者端執行速度測試，以評估輸送量。

圖表左下角顯示兩個透過獨立通道連線至企業網路的裝置。 因此，每個裝置的最低速度可以是10 Mbps和100 Mbps。

右側顯示的電腦透過速度為1 Mbps的VPN上行至公司網路有限。 1Mbps連線的使用者體驗與1Gbps連線的使用者體驗大不相同。 根據使用者與之互動的資產大小，他們的VPN上行鏈路可能不足以完成任務。

## 公司網路的拓撲 {#topology-of-the-corporate-network}

![chlimage_1-354](assets/chlimage_1-354.png)

此圖表顯示公司網路內的上行鏈路速度高於一般使用的速度。 這些管道是共用資源。 如果共用交換器預期可處理50個使用者端，則可能是瓶頸。 在初始圖表中，只有兩台電腦共用特定連線。

## 從公司網路與網際網路的上行鏈路 [!DNL Experience Manager] 環境 {#uplink-to-the-internet-from-the-corporate-network-and-aem-environment}

![chlimage_1-355](assets/chlimage_1-355.png)

請務必考量網際網路和VPC連線上的未知因素，因為網際網路的頻寬可能會因為尖峰負載或大型提供者中斷而受損。 一般來說，網際網路連線非常可靠。 但是，它有時可能會引入瓶頸。

從企業網路到網際網路的上行鏈路上，可以使用頻寬提供其他服務。 請務必瞭解有多少頻寬可專用於資產或排定優先順序。 例如，如果1 Gbps的連結已經達到80%的使用率，您最多只能為分配20%的頻寬 [!DNL Experience Manager Assets].

企業防火牆和代理程式也可以以多種不同的方式調整頻寬。 這類裝置可使用服務品質、每位使用者的頻寬限制，或每位主機的位元速率限制，來排定頻寬優先順序。 這些是需要檢查的重要瓶頸，因為它們可能會產生重大影響 [!DNL Assets] 使用者體驗。

在此範例中，企業有10 Gbps的上行鏈路。 其大小應足以容納數個使用者端。 此外，防火牆會設定10 Mbps的主機速率限制。 即使網際網路的上行鏈路速度為10 Gbps，此限制仍可能會將單一主機的流量限製為10 Mbps。

這是最小的使用者端導向瓶頸。 不過，您可以透過負責此防火牆的網路作業群組評估變更或設定允許清單。

從範例圖表中，您可以得出以下結論：六部裝置共用概念10Mbps通道。 根據利用的資產規模，這可能不足以達成使用者的期望。

## 的拓撲 [!DNL Experience Manager] 環境 {#topology-of-the-aem-environment}

![chlimage_1-356](assets/chlimage_1-356.png)

設計拓撲 [!DNL Experience Manager] 環境需要詳細的系統設定知識以及使用者環境中網路的連線方式。

範例情境包含具有五部伺服器的發佈陣列、S3二進位存放區以及已設定的Dynamic Media。

Dispatcher會與兩個實體(外部世界和 [!DNL Experience Manager] 部署。 對於同時上載和下載作業，您應該將此數字除以二。 附加的外部儲存體使用單獨的連線。

此 [!DNL Experience Manager] 部署會將其的1Gbps連線與多項服務共用。 從網路拓撲的觀點來看，這等同於使用不同服務共用單一通道。

檢閱從使用者端裝置到 [!DNL Experience Manager] 部署時，最小的瓶頸似乎是10 Mbit企業防火牆限制。 您可以在的大小計算程式中使用這些值 [Assets規模調整指南](assets-sizing-guide.md) 以判斷使用者體驗。

## 已定義的工作流程 [!DNL Experience Manager] 部署 {#defined-workflows-of-the-aem-deployment}

在考慮網路效能時，請務必考量系統中可能發生的工作流程與發佈。 此外，您使用和I/O請求的S3或其他網路附加儲存裝置會消耗網路頻寬。 因此，即使在完全最佳化的網路中，效能也可能受到磁碟I/O的限制。

若要簡化資產擷取的相關程式（尤其是上傳大量資產時），請探索資產工作流程，並深入瞭解其設定。

評估內部工作流程拓撲時，您應該分析下列內容：

* 寫入資產的程式
* 修改資產/中繼資料時觸發的工作流程/事件
* 讀取資產的程式

以下是一些需要考量的專案：

* XMP中繼資料讀取/回寫
* 自動啟用和復寫
* 浮水印
* 子資產擷取/頁面擷取
* 重疊的工作流程。

以下是資產工作流程定義的客戶範例。

![chlimage_1-357](assets/chlimage_1-357.png)
