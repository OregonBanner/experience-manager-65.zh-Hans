---
title: 与 Adobe Campaign Classic 集成
seo-title: Integrating with Adobe Campaign Classic
description: 瞭解如何將AEM與Adobe Campaign Classic整合
seo-description: Learn how to integrate AEM with Adobe Campaign Classic
uuid: 3c998b0e-a885-4aa9-b2a4-81b86f9327d3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: df94dd1b-1b65-478b-a28d-81807a8084b1
exl-id: a7281ca0-461f-4762-a631-6bb539596200
source-git-commit: 4712f57808ae769646b00d1098648686815121b6
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 67%

---


# 与 Adobe Campaign Classic 集成 {#integrating-campaign-classic}

將AEM與Adobe Campaign整合後，您可以直接在AEM中管理電子郵件傳送、內容和表單。 需要同时完成 Adobe Campaign Classic 和 AEM 的配置步骤才可以实现解决方案之间的双向通信。

此整合可讓AEM和Adobe Campaign Classic獨立使用。 行銷人員可以在Adobe Campaign中建立行銷活動並使用目標定位，而內容建立者則可以同時在AEM中設計內容。 透過整合，Adobe Campaign可鎖定在AEM中建立之行銷活動的內容和設計，並加以傳遞。

## 集成步骤 {#integration-steps}

AEM 和 Campaign 之间的集成需要在这两种解决方案中完成多个步骤。

1. [在 Campaign 中安装 AEM 集成包。](#install-package)
1. [在 Campaign 中为 AEM 创建一个运算符](#create-operator)
1. [在 AEM 中配置 Campaign 集成](#campaign-integration)
1. [配置 AEM 外部化器](#externalizer)
1. [在 AEM 中配置活动远程用户](#configure-user)
1. [在 Campaign 中配置 AEM 外部账户](#acc-setup)

本文档将详细介绍每一个步骤。

## 前提条件 {#prerequisites}

* 具有 Adobe Campaign Classic 管理员访问权限
   * 要执行集成，您需要一个有效的 Adobe Campaign Classic 实例，包括一个已配置的数据库。
   * 如果您需要有关如何设置和配置 Adobe Campaign Classic 的更多详细信息，请参阅 [Adobe Campaign Classic 文档](https://experienceleague.adobe.com/docs/campaign-classic/using/campaign-classic-home.html)，特别是《安装和配置指南》。
* AEM的管理員存取權

## 在Campaign中安裝AEM整合套件 {#install-package}

Adobe Campaign 中的 **AEM 集成**&#x200B;包含有连接到 AEM 所需的许多标准配置。

1. 作为管理员，使用客户端控制台登录到 Adobe Campaign 实例。

1. 选择&#x200B;**“工具”**>**“高级”**>**“导入软件包...”**。

   ![导入软件包](assets/import-package.png)

1. 单击&#x200B;**“安装标准包”**，然后单击&#x200B;**“下一个”**。

1. 检查&#x200B;**AEM 集成**&#x200B;包。

   ![安装标准包](assets/select-package.png)

1. 单击&#x200B;**“下一个”**，然后单击&#x200B;**“开始”**&#x200B;以开始安装。

   ![安装进度](assets/installation.png)

1. 安装完成后，单击&#x200B;**“关闭”**。

集成包现在已安装。

## 在Campaign中為AEM建立運運算元 {#create-operator}

集成包会自动创建 AEM 用于连接到 Adobe Campaign 的`aemserver`运算符。您必须为此运算符定义一个安全区域并设置密码。

1. 使用客户端控制台以管理员身份登录 Adobe Campaign。

1. 从菜单栏选择&#x200B;**“工具”** -> **“资源管理器”**。

1. 在资源管理器中，导航到&#x200B;**“管理”**>**“访问管理“**＞**”运算符“**&#x200B;节点。

1. 选择`aemserver`运算符。

1. 在运算符的&#x200B;**”编辑“**&#x200B;选项卡上，选择&#x200B;**”访问权限“**&#x200B;子选项卡，然后单击&#x200B;**”修改访问参数...“**&#x200B;链接。

   ![设置安全区域](assets/access-rights.png)

1. 选择适当的安全区域，并根据需要定义受信任的 IP 掩码。

1. 单击&#x200B;**”保存“**。

1. 注销 Adobe Campaign 客户端。

1. 在 Adobe Campaign 服务器的文件系统上，导航到 Campaign 安装位置，并以管理员身份编辑`serverConf.xml`文件。该文件通常位于以下位置：
   * `C:\Program Files\Adobe\Adobe Campaign Classic v7\conf`在 Windows 中。
   * `/usr/local/neolane/nl6/conf/eng` 在 Linux 中。

1. 搜索`securityZone`，并确保为 AEM 运算符的安全区域设置了以下参数。

   * `allowHTTP="true"`
   * `sessionTokenOnly="true"`
   * `allowUserPassword="true"`。

1. 保存文件。

1. 确保安全区域不会被`config-<server name>.xml`文件中的相应设置覆盖。

   * 如果配置文件包含单独的安全区域设置，则将`allowUserPassword`属性更改为`true`。

1. 如果要更改 Adobe Campaign Classic 服务器端口，请将`8080`替换为所需端口。

   >[!CAUTION]
   >
   >默认情况下，没有为运算符配置安全区域。要使 AEM 连接到 Adobe Campaign，您必须按照前面步骤中的详细说明选择一个区域。
   >
   >Adobe 强烈建议为 AEM 创建一个安全区域，以避免任何安全问题。有关此主题的更多信息，请参阅[ Adobe Campaign Classic 文档。](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/additional-configurations/security-zones.html)

1. 在 Campaign 客户端中，返回到`aemserver`运算符并选择&#x200B;**“常规”**&#x200B;选项卡。

1. 单击&#x200B;**“重置密码...”**&#x200B;链接。

1. 指定密码并将其存储在安全位置以供将来使用。

1. 单击&#x200B;**“确定”**&#x200B;以保存`aemserver`运算符的密码。

## 在AEM中設定Campaign整合 {#campaign-integration}

AEM 使用[您在 Campaign 中设置的运算符](#create-operator)与 Campaign 进行通信

1. 以管理员身份登录到您的 AEM 创作实例。

1. 从全局导航侧栏中，选择&#x200B;**“工具”**>**“Cloud Service”**＞**“传统 Cloud Service”**>**“Adobe Campaign”**，然后单击&#x200B;**“立即配置”**。

   ![配置 Adobe Campaign](assets/configure-campaign-service.png)

1. 在对话框中，通过输入&#x200B;**“标题”**&#x200B;并单击&#x200B;**“创建”**&#x200B;来创建 Campaign 服务配置。

   ![配置 Campaign 对话框](assets/configure-campaign-dialog.png)

1. 会打开新窗口和对话框会，用以编辑配置。 提供必要的信息。

   * **用户名** – 这是在上一步创建的[ Adobe Campaign AEM 集成包运算符。](#create-operator)默认情况下，这是 `aemserver`。
   * **密码** – 这是在上一步创建的 [Adobe Campaign AEM 集成包运算符的密码。](#create-operator)
   * **API 端点** – 这是 Adobe Campaign 实例 URL。

   ![在 AEM 中配置 Adobe Campaign](assets/configure-campaign.png)

1. 选择&#x200B;**“连接到 Adobe Campaign”**&#x200B;以验证连接，然后单击&#x200B;**确定**。

AEM 现在可以与 Adobe Campaign 通信。

>[!NOTE]
>
>确保您的 Adobe Campaign 服务器可以通过 Internet 访问。AEM無法存取私人網路。

## 設定復寫至AEM發佈執行個體的設定 {#replication}

Campaign內容是由內容作者在AEM編寫執行個體上建立。 此例項通常僅供貴組織內部使用。 為了讓行銷活動的收件者能夠存取影像和資產等內容，您需要發佈該內容。

復寫代理程式負責將您的內容從AEM製作執行個體發佈到發佈執行個體，且必須設定復寫代理程式，整合才能正常運作。 此步驟也是將某些編寫執行個體設定復寫到發佈執行個體所必需的。

若要設定從AEM編寫執行個體到發佈執行個體的復寫：

1. 以管理员身份登录到您的 AEM 创作实例。

1. 從全域導覽側邊欄中，選取 **工具** > **部署** > **復寫** > **作者上的代理**，然後點選或按一下 **預設代理程式（發佈）**.

   ![設定復寫代理程式](assets/acc-replication-config.png)

1. 點選或按一下 **編輯** 然後選取 **傳輸** 標籤。

1. 設定 **URI** 欄位，取代預設值 `localhost` 值為AEM發佈執行個體的IP位址。

   ![傳輸標籤](assets/acc-transport-tab.png)

1. 點選或按一下 **確定** 以儲存代理程式設定的變更。

您已設定復寫至AEM發佈執行個體，讓您的行銷活動收件者可以存取您的內容。

>[!NOTE]
>
>如果您不想使用復寫URL，而是使用公開顯示的URL，您可以透過OSGi在下列組態設定中設定公開URL
>
>從全域導覽側邊欄中，選取 **工具** > **作業** > **網頁主控台** > **OSGi設定** 並搜尋 **AEM Campaign整合 — 設定**. 編輯設定並變更欄位 **公開URL** (`com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl`)。

## 配置 AEM 外部化器 {#externalizer}

[外部化器是 AEM 中的一个 OSGi 服务，它可将资源路径转换为外部和绝对 URL，这是 AEM 提供 Campaign 可以使用的内容所必需的。](/help/sites-developing/externalizer.md)您必須加以設定，Campaign整合才能運作。

1. 以管理员身份登录到 AEM 创作实例。
1. 從全域導覽側邊欄中，選取 **工具** > **作業** > **網頁主控台** > **OSGi設定** 並搜尋 **Day CQ連結外部化器**.
1. 根據預設，最後一個專案位於 **網域** 欄位適用於發佈執行個體。 變更URL的預設值 `http://localhost:4503` 至公開可用的發佈執行個體。

   ![設定外部化程式](assets/acc-externalizer-config.png)

1. 点按或单击&#x200B;**保存**。

您已設定Externalizer，Adobe Campaign現在可以存取您的內容。

>[!NOTE]
发布实例必须可以从 Adobe Campaign 服务器中访问。如果它指向 `localhost:4503` 或Adobe Campaign無法存取的其他伺服器，來自AEM的影像將不會顯示在Adobe Campaign主控台中。

## 在AEM中設定行銷活動 — 遠端使用者 {#configure-user}

如要实现 Campaign 与 AEM 之间的通信，您需要在 AEM 中为 `campaign-remote` 用户设置一个密码。

1. 以管理员身份登录 AEM。
1. 在主导航控制台上，单击左栏中的&#x200B;**“工具”**。
1. 然后单击&#x200B;**“安全”**-＞**“用户”**，打开用户管理控制台。
1. 找到`campaign-remote`用户。
1. 选择`campaign-remote`用户，然后单击&#x200B;**“属性”**&#x200B;来编辑用户。
1. 在&#x200B;**“编辑用户设置”**&#x200B;窗口中，单击&#x200B;**“更改密码”**。
1. 为用户提供新密码，并将密码记在安全位置以备将来使用。
1. 单击&#x200B;**“保存”**&#x200B;以保存密码更改。
1. 单击&#x200B;**“保存并关闭”**&#x200B;以将更改保存到`campaign-remote`用户。

## 在Campaign中設定AEM外部帳戶 {#acc-setup}

当[在 Campaign 中安装&#x200B;**AEM 集成**&#x200B;包时，](#install-package)会为 AEM 创建一个外部帐户。透過設定此外部帳戶，Adobe Campaign可以連線至AEM，啟用解決方案之間的雙向通訊。

1. 使用客户端控制台以管理员身份登录 Adobe Campaign。

1. 从菜单栏选择&#x200B;**“工具”** -> **“资源管理器”**。

1. 在资源管理器中，导航到&#x200B;**“管理”** > **“Platform“**＞**”外部账户“**&#x200B;节点。

   ![外部帐户](assets/external-accounts.png)

1. 找到外部 AEM 帐户。默认情况下，它具有以下值：

   * **类型** - `AEM`
   * **標籤** - `AEM Instance`
   * **內部名稱** - `aemInstance`

1. 在该帐户的&#x200B;**“常规”**&#x200B;选项卡上，输入您在[设置活动远程用户密码](#set-campaign-remote-password)步骤中定义的用户信息。

   * **服务器** – AEM 作者服务器地址
      * AEM 作者服务器必须可以从 Adobe Campaign Classic 服务器实例中访问。
      * 确保服务器地址的&#x200B;**不是**&#x200B;以尾随斜杠结尾。
   * **帐户** – 默认情况下，这是您在[设置活动远程用户密码](#set-campaign-remote-password)步骤中在 AEM 中设置的`campaign-remote`用户。
   * **密码** – 该密码与在[设置活动远程用户密码](#set-campaign-remote-password)步骤中在 AEM 中设置的`campaign-remote`用户密码相同。

1. 选中&#x200B;**启用**&#x200B;复选框。

1. 单击&#x200B;**保存**。

Adobe Campaign 现在可以与 AEM 通信。

## 后续步骤 {#next-steps}

Adobe Campaign Classic和AEM都已設定完成，整合即可完成。

您现在可以通过继续阅读[本文档](/help/sites-authoring/campaign.md)学习如何在 Adobe Experience Manager 中创建新闻稿。
