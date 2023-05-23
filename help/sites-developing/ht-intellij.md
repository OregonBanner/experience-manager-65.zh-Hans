---
title: 如何使用IntelliJ IDEA開發AEM專案
description: 使用IntelliJ IDEA開發AEM專案
uuid: 382b5008-2aed-4e08-95be-03c48f2b549e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: df6410a2-794e-4fa2-ae8d-37271274d537
exl-id: 5a79c79b-df65-4cb2-b9d4-eda994c992ec
source-git-commit: af60428255fb883265ade7b2d9f363aacb84b9ad
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 0%

---

# 如何使用IntelliJ IDEA開發AEM專案{#how-to-develop-aem-projects-using-intellij-idea}

## 概述 {#overview}

若要開始在IntelliJ上進行AEM開發，必須執行下列步驟。

本主題其餘部分將更詳細地說明每個步驟。

* 安裝IntelliJ
* 根據Maven設定您的AEM專案
* 在Maven POM中為IntelliJ準備JSP支援
* 將Maven專案匯入IntelliJ

>[!NOTE]
>
>本指南以IntelliJ IDEA Ultimate Edition 12.1.4和AEM 5.6.1為基礎。

### 安裝IntelliJ IDEA {#install-intellij-idea}

下載IntelliJ IDEA，網址為 [JetBrains的下載頁面](https://www.jetbrains.com/idea/download/).

然後，請依照該頁面上的安裝指示操作。

### 根據Maven設定您的AEM專案 {#set-up-your-aem-project-based-on-maven}

接下來，使用Maven設定您的專案，如所述 [如何使用Apache Maven建置AEM專案](/help/sites-developing/ht-projects-maven.md).

若要開始使用IntelliJ IDEA中的AEM專案，請依下列步驟執行： [5分鐘搞定快速入門](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) 就足夠了。

### 為IntelliJ IDEA準備JSP支援 {#prepare-jsp-support-for-intellij-idea}

IntelliJ IDEA也可以提供使用JSP的支援，例如：

* 自動完成標籤程式庫
* 對物件的感知定義如下 `<cq:defineObjects />` 和 `<sling:defineObjects />`

若要讓此功能發揮作用，請遵循以下說明： [如何使用JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) 在 [如何使用Apache Maven建置AEM專案](/help/sites-developing/ht-projects-maven.md).

### 匯入Maven專案 {#import-the-maven-project}

1. 開啟 **匯入** IntelliJ IDEA中的對話方塊，作者：

   * 選取 **匯入專案** 在歡迎畫面上（如果您尚未開啟任何專案）
   * 選取 **檔案 — >匯入專案** 從主功能表

1. 在「匯入」對話方塊中，選取專案的POM檔案。

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. 繼續使用預設設定，如下方對話方塊所示。

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. 繼續下列對話方塊，按一下 **下一個** 和 **完成**.
1. 您現在已使用IntelliJ IDEA設定AEM開發

   ![chlimage_1-47](assets/chlimage_1-47a.png)

### 使用IntelliJ IDEA偵錯JSP {#debugging-jsps-with-intellij-idea}

使用IntelliJ IDEA偵錯JSP時，必須執行下列步驟

* 在專案中設定網頁面向
* 安裝JSR45支援外掛程式
* 設定偵錯設定檔
* 設定除錯模式的AEM

#### 在專案中設定網頁面向 {#set-up-a-web-facet-in-the-project}

IntelliJ IDEA必須瞭解在哪裡可以找到JSP以進行偵錯。 因為IDEA無法解譯 `content-package-maven-plugin` 設定，則必須手動設定。

1. 前往 **檔案 — >專案結構**
1. 選取 **內容** 模組
1. 按一下 **+** 在模組清單上方並選取 **Web**
1. 以「Web資源目錄」形式選取 `content/src/main/content/jcr_root subdirectory` ，如下方熒幕擷圖所示。

![chlimage_1-48](assets/chlimage_1-48a.png)

#### 安裝JSR45支援外掛程式 {#install-the-jsr-support-plugin}

1. 前往 **外掛程式** IntelliJ IDEA設定中的窗格
1. 導覽至 **JSR45整合** 外掛程式並選取其旁邊的核取方塊
1. 按一下 **套用**
1. 請求時重新啟動IntelliJ IDEA

![chlimage_1-49](assets/chlimage_1-49a.png)

#### 設定偵錯設定檔 {#configure-a-debug-profile}

1. 前往 **執行 — >編輯設定**
1. 點選 **+** 並選取 **JSR45遠端**
1. 在設定對話方塊中，選取 **設定** 旁邊 **應用程式伺服器** 並設定一般伺服器
1. 如果您要在開始偵錯時開啟瀏覽器，請將起始頁面設定為適當的URL
1. 全部移除 **啟動前** 任務（如果您使用vlt autosync），或配置適當的Maven任務（如果您未使用）
1. 於 **啟動/連線** 窗格，視需要調整連線埠
1. 複製IntelliJ IDEA建議的命令列引數

![chlimage_1-50](assets/chlimage_1-50a.png) ![chlimage_1-51](assets/chlimage_1-51a.png)

#### 設定除錯模式的AEM {#configure-aem-for-debug-mode}

最後一個必要步驟是使用IntelliJ IDEA建議的JVM選項啟動AEM。

直接啟動AEM jar檔案並新增這些選項，例如使用下列命令列：

`java -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y -Xmx1024m -jar cq-quickstart-6.5.0.jar`

您也可以在下列位置將這些選項新增至您的開始指令碼： `crx-quickstart/bin/start` 如下所示。

```shell
# ...

# default JVM options
if [ -z "$CQ_JVM_OPTS" ]; then
 CQ_JVM_OPTS='-server -Xmx1024m -Djava.awt.headless=true'
fi

CQ_JVM_OPTS="$CQ_JVM_OPTS -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y"

# ...
```

#### 開始偵錯 {#start-debugging}

您現在已準備好在AEM中偵錯JSP。

1. 選取 **執行 — >偵錯 — >您的偵錯設定檔**
1. 在元件程式碼中設定中斷點
1. 存取瀏覽器中的頁面

![chlimage_1-52](assets/chlimage_1-52a.png)

### 使用IntelliJ IDEA偵錯套件組合 {#debugging-bundles-with-intellij-idea}

可以使用標準通用遠端偵錯連線來偵錯套件中的程式碼。 您可以遵循 [有關遠端偵錯的Jetbrain檔案](https://www.jetbrains.com/help/idea/remote-debugging-with-product.html#remote-interpreter).
