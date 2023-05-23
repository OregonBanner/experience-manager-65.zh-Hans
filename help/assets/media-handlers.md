---
title: 使用媒體處理常式和工作流程處理資產
description: 瞭解媒體處理常式，以及如何使用工作流程對您的數位資產執行任務。
mini-toc-levels: 1
contentOwner: AG
role: User
feature: Workflow,Renditions
exl-id: cfd6c981-1a35-4327-82d7-cf373d842cc3
source-git-commit: acc4b78f551e0e0694f41149fff7e24d855f504f
workflow-type: tm+mt
source-wordcount: '2161'
ht-degree: 3%

---

# 使用媒體處理常式和工作流程處理資產 {#processing-assets-using-media-handlers-and-workflows}

[!DNL Adobe Experience Manager Assets] 隨附一組預設工作流程和媒體處理常式，以處理資產。 工作流程會定義要在資產上執行的任務，然後將特定任務委派給媒體處理常式，例如縮圖產生或中繼資料擷取。

您可以將工作流程設定為在上傳特定MIME型別的資產時自動執行。 處理步驟的定義如下 [!DNL Assets] 媒體處理常式。 [!DNL Experience Manager] 提供一些 [內建處理常式，](#default-media-handlers) 其他選項可能是 [自訂開發](#creating-a-new-media-handler) 或透過將程式委派給 [命令列工具](#command-line-based-media-handler).

媒體處理常式是中的服務 [!DNL Assets] 對資產執行特定動作的使用者。 例如，將MP3音訊檔案上傳至時 [!DNL Experience Manager]，工作流程會觸發擷取中繼資料並產生縮圖的MP3處理常式。 媒體處理常式通常會與工作流程搭配使用。 最常見的MIME型別支援於 [!DNL Experience Manager]. 您可以透過延伸/建立工作流程、延伸/建立媒體處理常式或停用/啟用媒體處理常式，在資產上執行特定工作。

>[!NOTE]
>
>請參閱 [資產支援的格式](assets-formats.md) 頁面，以取得支援的所有格式的說明 [!DNL Assets] 以及每種格式支援的功能。

## 預設媒體處理常式 {#default-media-handlers}

下列媒體處理常式可在 [!DNL Assets] 並處理最常見的MIME型別：

<!-- TBD: Java versions shouldn't be set to 1.5. Must be updated.
-->

| 處理常式名稱 | 服務名稱（在系統主控台中） | 支援的MIME型別 |
|--------------|--------------------------------------|----------------------|
| [!UICONTROL TextHandler] | com.day.cq.dam.core.impl.handler.TextHandler | text/plain |
| [!UICONTROL PdfHandler] | com.day.cq.dam.handler.standard.pdf.PdfHandler | <ul><li>application/pdf</li><li>application/illustrator</li></ul> |
| [!UICONTROL JpegHandler] | com.day.cq.dam.core.impl.handler.JpegHandler | image/jpeg |
| [!UICONTROL Mp3Handler] | com.day.cq.dam.handler.standard.mp3.Mp3Handler | audio/mpeg<br><b>重要</b>  — 上傳MP3檔案時，它會 [使用協力廠商程式庫處理](https://www.zxdr.it/programmi/SistEvolBDD/LibJava/doc/de/vdheide/mp3/MP3File.html). 如果MP3有可變位元速率(VBR)，程式庫會計算不精確的近似長度。 |
| [!UICONTROL ZipHandler] | com.day.cq.dam.handler.standard.zip.ZipHandler | <ul><li>application/java-archive </li><li> application/zip</li></ul> |
| [!UICONTROL PictHandler] | com.day.cq.dam.handler.standard.pict.PictHandler | image/pict |
| [!UICONTROL StandardImageHandler] | com.day.cq.dam.core.impl.handler.StandardImageHandler | <ul><li>image/gif </li><li> image/png </li> <li>application/photoshop </li> <li>image/jpeg </li><li> image/tiff </li> <li>image/x-ms-bmp </li><li> image/bmp</li></ul> |
| [!UICONTROL MSOfficeHandler] | com.day.cq.dam.handler.standard.msoffice.MSOfficeHandler | application/msword |
| [!UICONTROL MSPowerPointHandler] | com.day.cq.dam.handler.standard.msoffice.MSPowerPointHandler | application/vnd.ms-powerpoint |
| [!UICONTROL OpenOfficeHandler] | com.day.cq.dam.handler.standard.ooxml.OpenOfficeHandler | <ul><li>application/vnd.openxmlformats-officedocument.wordprocessingml.document</li><li> application/vnd.openxmlformats-officedocument.spreadsheetml.sheet</li><li> application/vnd.openxmlformats-officedocument.presentationml.presentation</li></ul> |
| [!UICONTROL EPubHandler] | com.day.cq.dam.handler.standard.epub.EPubHandler | application/epub+zip |
| [!UICONTROL GenericAssetHandler] | com.day.cq.dam.core.impl.handler.GenericAssetHandler | 找不到其他處理常式來從資產擷取資料時備援 |

{style="table-layout:auto"}

所有處理常式都會執行下列工作：

* 從資產擷取所有可用的中繼資料。
* 建立資產的縮圖影像。

若要檢視作用中的媒體處理常式：

1. 在您的瀏覽器中，導覽至 `https://localhost:4502/system/console/components`.
1. 单击 `com.day.cq.dam.core.impl.store.AssetStoreImpl`.
1. 會顯示包含所有使用中媒體處理常式的清單。 例如：

![chlimage_1-437](assets/chlimage_1-437.png)

## 在工作流程中使用媒體處理常式來執行資產上的工作 {#using-media-handlers-in-workflows-to-perform-tasks-on-assets}

媒體處理常式是常與工作流程搭配使用的服務。

[!DNL Experience Manager] 有一些處理資產的預設工作流程。 若要檢視，請開啟「工作流程」主控台，然後按一下 **[!UICONTROL 模型]** 索引標籤：開頭為的工作流程標題 [!DNL Assets] 是資產特定專案。

您可以擴充現有的工作流程，並建立新的工作流程，以根據特定需求處理資產。

以下示例演示如何增强 **[!UICONTROL AEM Assets 同步工作流]**，以便为除 PDF 文档外的所有资产生成子资产。

### 停用或啟用媒體處理常式 {#disabling-enabling-a-media-handler}

您可以透過Apache Felix Web Management Console停用或啟用媒體處理常式。 停用媒體處理常式時，不會對資產執行其工作。

若要啟用/停用媒體處理常式：

1. 在您的瀏覽器中，導覽至 `https://<host>:<port>/system/console/components`.
1. 按一下 **[!UICONTROL 停用]** 位於媒體處理常式名稱旁。 例如：`com.day.cq.dam.handler.standard.mp3.Mp3Handler`。
1. 重新整理頁面：媒體處理常式旁會顯示一個圖示，指出頁面已停用。
1. 若要啟用媒體處理常式，請按一下 **[!UICONTROL 啟用]** 位於媒體處理常式名稱旁。

### 建立新的媒體處理常式 {#creating-a-new-media-handler}

若要支援新媒體型別或在資產上執行特定工作，必須建立新的媒體處理常式。 本節說明如何繼續。

#### 重要類別和介面 {#important-classes-and-interfaces}

開始實作的最佳方式是繼承自提供的抽象實作，該實作會處理大多數事情並提供合理的預設行為： `com.day.cq.dam.core.AbstractAssetHandler` 類別。

此類別已經提供抽象服務描述元。 因此，如果您繼承自此類別並使用maven-sling-plugin，請務必將inherit標幟設為 `true`.

實作下列方法：

* `extractMetadata()`：擷取所有可用的中繼資料。
* `getThumbnailImage()`：以傳遞的資產建立縮圖影像。
* `getMimeTypes()`：傳回資產MIME型別。

範例範本如下：

```Java
package my.own.stuff; /** * @scr.component inherit="true" * @scr.service */ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the relevant parts }
```

介面和類別包括：

* `com.day.cq.dam.api.handler.AssetHandler` 介面：此介面說明新增特定MIME型別支援的服務。 新增新的MIME型別需要實作此介面。 介麵包含匯入和匯出特定檔案的方法、建立縮圖和擷取中繼資料的方法。
* `com.day.cq.dam.core.AbstractAssetHandler` 類別：此類別可作為所有其他資產處理常式實作的基礎，並提供常用的功能。
* `com.day.cq.dam.core.AbstractSubAssetHandler` class:
   * 此類別可作為所有其他資產處理常式實作的基礎，並提供常用功能以及子資產擷取的常用功能。
   * 開始實作的最佳方式是繼承自提供的抽象實作，該實作會處理大多數事情並提供合理的預設行為： com.day.cq.dam.core.AbstractAssetHandler類別。
   * 此類別已經提供抽象服務描述元。 因此，如果您繼承自此類別並使用maven-sling-plugin，請務必將inherit標幟設為true。

需要實作下列方法：

* `extractMetadata()`：此方法會擷取所有可用的中繼資料。
* `getThumbnailImage()`：此方法會使用通過資產建立縮圖影像。
* `getMimeTypes()`：此方法會傳回資產MIME型別。

範例範本如下：

封裝my.own.stuff； /&amp;ast；&amp;ast； &amp;ast； @scr.component inherit=&quot;true&quot; &amp;ast； @scr.service &amp;ast；/公用類別MyMediaHandler擴充com.day.cq.dam.core.AbstractAssetHandler { //實作相關部分}

介面和類別包括：

* `com.day.cq.dam.api.handler.AssetHandler` 介面：此介面說明新增特定MIME型別支援的服務。 新增新的MIME型別需要實作此介面。 介麵包含匯入和匯出特定檔案的方法、建立縮圖和擷取中繼資料的方法。
* `com.day.cq.dam.core.AbstractAssetHandler` 類別：此類別可作為所有其他資產處理常式實作的基礎，並提供常用的功能。
* `com.day.cq.dam.core.AbstractSubAssetHandler` 類別：此類別可作為所有其他資產處理常式實作的基礎，並提供常用功能以及子資產擷取的常用功能。

#### 範例：建立特定的文書處理常式 {#example-create-a-specific-text-handler}

在本節中，您將建立特定文書處理常式，以產生包含浮水印的縮圖。

請依照下列步驟進行：

請參閱 [開發工具](../sites-developing/dev-tools.md) 以安裝和設定Eclipse [!DNL Maven] 外掛程式和，用於設定所需的相依性 [!DNL Maven] 專案。

執行以下程式後，當您上傳TXT檔案到 [!DNL Experience Manager]，則會擷取檔案的中繼資料並產生兩個含有浮水印的縮圖。

1. 在Eclipse中，建立 `myBundle` [!DNL Maven] 專案：

   1. 在功能表列中，按一下 **[!UICONTROL 檔案]** > **[!UICONTROL 新增]** > **[!UICONTROL 其他]**.
   1. 在對話方塊中，展開 [!DNL Maven] 資料夾，選取 [!DNL Maven] 專案並按一下 **[!UICONTROL 下一個]**.
   1. 勾選「建立簡單專案」方塊和「使用預設工作區位置」方塊，然後按一下 **[!UICONTROL 下一個]**.
   1. 定義 [!DNL Maven] 專案：

      * 群組ID： `com.day.cq5.myhandler`.
      * 成品ID： myBundle。
      * 名稱：我的 [!DNL Experience Manager] 套件組合。
      * 說明：這是我的 [!DNL Experience Manager] 套件組合。
   1. 按一下 **[!UICONTROL 完成]**.


1. 設定 [!DNL Java] 編譯器至1.5版：

   1. 以滑鼠右鍵按一下 `myBundle` 專案，選取 [!UICONTROL 屬性].
   1. 選取 [!UICONTROL Java編譯器] 並將下列屬性設定為1.5：

      * 編譯器相容性層級
      * 產生的.class檔案相容性
      * 來源相容性
   1. 单击&#x200B;**[!UICONTROL 确定]**。在對話方塊視窗中，按一下 **[!UICONTROL 是]**.


1. 在中取代程式碼 `pom.xml` 檔案，其程式碼如下：

   ```xml
   <project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <!-- ====================================================================== -->
    <!-- P A R E N T P R O J E C T D E S C R I P T I O N -->
    <!-- ====================================================================== -->
    <parent>
     <groupId>com.day.cq.dam</groupId>
     <artifactId>dam</artifactId>
     <version>5.2.14</version>
     <relativePath>../parent</relativePath>
    </parent>
    <!-- ====================================================================== -->
    <!-- P R O J E C T D E S C R I P T I O N -->
    <!-- ====================================================================== -->
    <groupId>com.day.cq5.myhandler</groupId>
    <artifactId>myBundle</artifactId>
    <name>My CQ5 bundle</name>
    <version>0.0.1-SNAPSHOT</version>
    <description>This is my CQ5 bundle</description>
    <packaging>bundle</packaging>
    <!-- ====================================================================== -->
    <!-- B U I L D D E F I N I T I O N -->
    <!-- ====================================================================== -->
    <build>
     <plugins>
      <plugin>
       <groupId>org.apache.felix</groupId>
       <artifactId>maven-scr-plugin</artifactId>
      </plugin>
      <plugin>
       <groupId>org.apache.sling</groupId>
       <artifactId>maven-sling-plugin</artifactId>
       <configuration>
        <slingUrlSuffix>/libs/dam/install/</slingUrlSuffix>
       </configuration>
      </plugin>
      <plugin>
       <groupId>org.apache.felix</groupId>
       <artifactId>maven-bundle-plugin</artifactId>
       <extensions>true</extensions>
       <configuration>
        <instructions>
         <Bundle-Category>cq5</Bundle-Category>
         <Export-Package> com.day.cq5.myhandler </Export-Package>
        </instructions>
       </configuration>
      </plugin>
     </plugins>
    </build>
    <!-- ====================================================================== -->
    <!-- D E P E N D E N C I E S -->
    <!-- ====================================================================== -->
    <dependencies>
     <dependency>
      <groupId>com.day.cq.dam</groupId>
      <artifactId>cq-dam-api</artifactId>
      <version>5.2.10</version>
      <scope>provided</scope>
     </dependency>
     <dependency>
      <groupId>com.day.cq.dam</groupId>
      <artifactId>cq-dam-core</artifactId>
      <version>5.2.10</version>
      <scope>provided</scope>
     </dependency>
     <dependency>
      <groupId>com.day.cq</groupId>
      <artifactId>cq-commons</artifactId>
     </dependency>
     <dependency>
      <groupId>javax.jcr</groupId>
      <artifactId>jcr</artifactId>
     </dependency>
     <dependency>
      <groupId>org.apache.felix</groupId>
      <artifactId>org.osgi.compendium</artifactId>
     </dependency>
     <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-api</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-lang</groupId>
      <artifactId>commons-lang</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-collections</groupId>
      <artifactId>commons-collections</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-io</groupId>
      <artifactId>commons-io</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.commons</groupId>
      <artifactId>day-commons-gfx</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.commons</groupId>
      <artifactId>day-commons-text</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.cq.workflow</groupId>
      <artifactId>cq-workflow-api</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.cq.wcm</groupId>
      <artifactId>cq-wcm-foundation</artifactId>
      <version>5.2.22</version>
     </dependency>
    </dependencies>
   ```

1. 建立套件 `com.day.cq5.myhandler` 包含 [!DNL Java] 類別位於 `myBundle/src/main/java`：

   1. 在myBundle下，按一下滑鼠右鍵 `src/main/java`，選取新增，然後選取封裝。
   1. 將其命名 `com.day.cq5.myhandler` 並按一下「完成」。

1. 建立 [!DNL Java] 類別 `MyHandler`：

   1. 在 [!DNL Eclipse]，下 `myBundle/src/main/java`，以滑鼠右鍵按一下 `com.day.cq5.myhandler` 封裝。 選取 [!UICONTROL 新增]，則 [!UICONTROL 類別].
   1. 在對話方塊視窗中，將 [!DNL Java] 類別 `MyHandler` 並按一下 [!UICONTROL 完成]. [!DNL Eclipse] 建立並開啟檔案 `MyHandler.java`.
   1. 在 `MyHandler.java` 以下列專案取代現有程式碼，然後儲存變更：

   ```java
   package com.day.cq5.myhandler;
   import java.awt.Color;
   import java.awt.Rectangle;
   import java.awt.image.BufferedImage;
   import java.io.IOException;
   import java.io.InputStream;
   import java.io.InputStreamReader;
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   import org.apache.commons.io.IOUtils;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import com.day.cq.dam.api.metadata.ExtractedMetadata;
   import com.day.cq.dam.core.AbstractAssetHandler;
   import com.day.image.Font;
   import com.day.image.Layer;
   import com.day.cq.wcm.foundation.ImageHelper;
   
   /**
    * The <code>MyHandler</code> can extract text files
    * @scr.component inherit="true" immediate="true" metatype="false"
    * @scr.service
    *
    **/
   
   public class MyHandler extends AbstractAssetHandler {
    /** * Logger instance for this class. */
    private static final Logger log = LoggerFactory.getLogger(MyHandler.class);
    /** * Music icon margin */
    private static final int MARGIN = 10;
    /** * @see com.day.cq.dam.api.handler.AssetHandler#getMimeTypes() */
    public String[] getMimeTypes() {
     return new String[] {"text/plain"};
    }
   
    public ExtractedMetadata extractMetadata(Node asset) {
     ExtractedMetadata extractedMetadata = new ExtractedMetadata();
     InputStream data = getInputStream(asset);
     try {
      // read text data
      InputStreamReader reader = new InputStreamReader(data);
      char[] buffer = new char[4096];
      String text = "";
      while (reader.read(buffer) != -1) {
       text += new String(buffer);
      }
      reader.close();
      long wordCount = this.wordCount(text);
      extractedMetadata.setProperty("text", text);
      extractedMetadata.setMetaDataProperty("Word Count",wordCount);
      setMimetype(extractedMetadata, asset);
     } catch (Throwable t) {
      log.error("handling error: " + t.toString(), t);
     } finally {
      IOUtils.closeQuietly(data);
     }
     return extractedMetadata; }
    // ----------------------< helpers >----------------------------------------
    protected BufferedImage getThumbnailImage(Node node) {
     ExtractedMetadata metadata = extractMetadata(node);
     final String text = (String) metadata.getProperty("text");
     // create text layer
     final Layer layer = new Layer(500, 600, Color.WHITE);
     layer.setPaint(Color.black);
     Font font = new Font("Arial", 12);
     String displayText = this.getDisplayText(text, 600, 12);
     if(displayText!=null && displayText.length() > 0) {
      // commons-gfx Font class would throw IllegalArgumentException on empty or null text
      layer.drawText(10, 10, 500, 600, displayText, font, Font.ALIGN_LEFT, 0, 0);
     }
     // create watermark and merge with text layer
     Layer watermarkLayer;
     try {
      final Session session = node.getSession();
      watermarkLayer = ImageHelper.createLayer(session, "/content/dam/we-retail/en/products/apparel/gloves/Gloves.jpg");
      watermarkLayer.setX(MARGIN);
      watermarkLayer.setY(MARGIN);
      layer.merge(watermarkLayer);
     } catch (RepositoryException e) {
      // TODO Auto-generated catch block
      e.printStackTrace();
     } catch (IOException e) {
      // TODO Auto-generated catch block
      e.printStackTrace(); }
     layer.crop(new Rectangle(510, 600));
     return layer.getImage(); }
    // ---------------< private >-----------------------------------------------
    /**
     * This method cuts lines if the text file is too long..
     * * @param text
     * * text to check
     * * @param height
     * * text box height (px)
     * * @param fontheight
     * * font height (px)
     * * @return the text which will fit into the box
     */
    private String getDisplayText(String text, int height, int fontheight) {
     String trimmedText = text.trim();
     int numOfLines = height / fontheight;
     String lines[] = trimmedText.split("\n");
     if (lines.length <= numOfLines) {
      return trimmedText;
     } else {
      String cuttetText = "";
      for (int i = 0; i < numOfLines; i++) {
       cuttetText += lines[i] + "\n";
      }
      return cuttetText;
     }
    }
    /**
     * * This method counts the number of words in a string
     * * @param text the String whose words would like to be counted
     * * @return the number of words in the string
     * */
    private long wordCount(String text) {
     // We need to keep track of the last character, if we have two whitespaces in a row we don't want to double count.
     // The starting of the document is always a whitespace.
     boolean prevWhiteSpace = true;
     boolean currentWhiteSpace = true;
     char c; long numwords = 0;
     int j = text.length();
     int i = 0;
     while (i < j) {
      c = text.charAt(i++);
      if (c == 0) { break; }
      currentWhiteSpace = Character.isWhitespace(c);
      if (currentWhiteSpace && !prevWhiteSpace) { numwords++; }
      prevWhiteSpace = currentWhiteSpace;
     }
     // If we do not end with a whitespace then we need to add one extra word.
     if (!currentWhiteSpace) { numwords++; }
     return numwords;
    }
   }
   ```

1. 編譯 [!DNL Java] 類別並建立組合：

   1. 以滑鼠右鍵按一下 `myBundle` 專案，選取 **[!UICONTROL 執行身分]**，則 **[!UICONTROL Maven安裝]**.
   1. 組合 `myBundle-0.0.1-SNAPSHOT.jar` （包含編譯的類別）建立於 `myBundle/target`.

1. 在CRX Explorer中，在下建立新節點 `/apps/myApp`. 名稱= `install`，型別= `nt:folder`.
1. 複製組合 `myBundle-0.0.1-SNAPSHOT.jar` 並將其儲存在 `/apps/myApp/install` （例如WebDAV）。 新的文書處理常式現在於 [!DNL Experience Manager].
1. 在您的瀏覽器中，開啟 [!UICONTROL Apache Felix Web管理主控台]. 選取 [!UICONTROL 元件] 定位並停用預設文書處理常式 `com.day.cq.dam.core.impl.handler.TextHandler`.

## 以命令列為基礎的媒體處理常式 {#command-line-based-media-handler}

[!DNL Experience Manager] 可讓您在工作流程中執行任何命令列工具來轉換資產(例如 [!DNL ImageMagick])，並將新轉譯新增至資產。 您只需在託管的磁碟上安裝命令列工具 [!DNL Experience Manager] ，以將流程步驟新增及設定至工作流程。 叫用的程式，稱為 `CommandLineProcess`，也能根據特定的MIME型別進行篩選，以及根據新轉譯建立多個縮圖。

下列轉換可自動執行並儲存在 [!DNL Assets]：

* EPS和AI轉換，使用 [ImageMagick](https://www.imagemagick.org/script/index.php) 和 [Ghostscript](https://www.ghostscript.com/).
* 使用的FLV視訊轉碼 [FFmpeg](https://ffmpeg.org/).
* 使用的MP3編碼 [LAME](https://lame.sourceforge.io/).
* 音訊處理使用 [SOX](https://sox.sourceforge.io/).

>[!NOTE]
>
>在非Windows系統上，FFmpeg工具在為檔案名稱中包含單引號(&#39;)的視訊資產產生轉譯時傳回錯誤。 如果您的視訊檔案名稱包含單引號，請先將其移除，然後再上傳至 [!DNL Experience Manager].

此 `CommandLineProcess` 處理會依照列出的順序執行下列操作：

* 根據特定的MIME型別篩選檔案（如果指定）。
* 在託管的磁碟上建立暫存目錄 [!DNL Experience Manager] 伺服器。
* 將原始檔案串流至暫存目錄。
* 執行由步驟的引數定義的命令。 命令正在暫存目錄中執行，且執行中的使用者有許可權 [!DNL Experience Manager].
* 將結果串流回的轉譯資料夾 [!DNL Experience Manager] 伺服器。
* 刪除暫存目錄。
* 如果指定，會根據這些轉譯建立縮圖。 縮圖的編號和尺寸由步驟的引數定義。

### 使用的範例 [!DNL ImageMagick] {#an-example-using-imagemagick}

下列範例說明如何設定命令列處理步驟，以便每次將具有miMIME e-typeGIF或TIFF的資產新增到時 `/content/dam` 於 [!DNL Experience Manager] 「伺服器」(Server)會建立原始的翻轉影像，連同三個額外的縮圖（140x100、48x48和10x250）。

若要這麼做，請使用 [!DNL ImageMagick]. [!DNL ImageMagick] 是用來建立、編輯及撰寫點陣圖影像的自由命令列軟體。

安裝 [!DNL ImageMagick] 在託管的磁碟上 [!DNL Experience Manager] 伺服器：

1. 安裝 [!DNL ImageMagick]：請參閱 [ImageMagick檔案](https://www.imagemagick.org/script/download.php).
1. 設定工具，以便在命令列上執行轉換。
1. 若要檢視工具是否已正確安裝，請執行以下命令 `convert -h` 在命令列上。

   它會顯示說明畫面，其中包含轉換工具的所有可能選項。

   >[!NOTE]
   >
   >在某些Windows版本中，轉換命令可能會無法執行，因為它與所屬的原生轉換公用程式衝突 [!DNL Windows] 安裝。 在此情況下，請提及 [!DNL ImageMagick] 用於將影像檔案轉換為縮圖的軟體。 例如：`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`。

1. 若要檢視工具是否正確執行，請將JPG影像新增至工作目錄，然後執行convert指令 `<image-name>.jpg -flip <image-name>-flipped.jpg` 在命令列上。 翻轉的影像會新增至目錄。 然後，將命令列處理步驟新增至 **[!UICONTROL DAM更新資產]** 工作流程。
1. 前往 **[!UICONTROL 工作流程]** 主控台。
1. 在 **[!UICONTROL 模型]** 標籤，編輯 **[!UICONTROL DAM更新資產]** 模型。
1. 變更 [!UICONTROL 引數] 的 **[!UICONTROL 啟用Web的轉譯]** 步驟至： `mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`.
1. 儲存工作流程。

若要測試修改的工作流程，請將資產新增至 `/content/dam`.

1. 在檔案系統中，取得您選擇的TIFF影像。 將其重新命名為 `myImage.tiff` 並將其複製到 `/content/dam`，例如使用WebDAV。
1. 前往 **[!UICONTROL CQ5 DAM]** 例如主控台 `https://localhost:4502/libs/wcm/core/content/damadmin.html`.
1. 開啟資產 **[!UICONTROL myImage.tiff]** 並確認已建立翻轉的影像和三個縮圖。

#### 設定CommandLineProcess程式步驟 {#configuring-the-commandlineprocess-process-step}

本节介绍如何设置 [!UICONTROL CommandLineProcess] 的[!UICONTROL 进程参数]。

將下列專案的值分開： [!UICONTROL 程式引數] 逗號，且請勿以空格開頭。

| 引數 — 格式 | 描述 |
|---|---|
| mime：&lt;mime-type> | 選用引數。 如果資產的MIME型別與引數的MIME型別相同，則會套用程式。 <br>可以定義數種MIME型別。 |
| tn：&lt;width>：&lt;height> | 選用引數。 此程式會使用引數中定義的維度建立縮圖。 <br>可以定義數個縮圖。 |
| cmd： &lt;command> | 定義執行的命令。 語法取決於命令列工具。 只能定義一個指令。 <br>下列變數可用來建立命令：<br>`${filename}`：輸入檔案的名稱，例如original.jpg <br> `${file}`：輸入檔案的完整路徑名稱，例如 `/tmp/cqdam0816.tmp/original.jpg` <br> `${directory}`：輸入檔案的目錄，例如 `/tmp/cqdam0816.tmp` <br>`${basename}`：無副檔名的輸入檔案名稱，例如原始檔案 <br>`${extension}`：輸入檔案的副檔名，例如JPG。 |

例如，如果 [!DNL ImageMagick] 安裝在託管的磁碟上 [!DNL Experience Manager] 伺服器和如果您建立程式步驟，請使用 [!UICONTROL 命令列程式] as實作，以及下列值 [!UICONTROL 程式引數]：

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

然後，當工作流程執行時，步驟僅適用於具有 `image/gif` 或 `mime:image/tiff` 作為 `mime-types`，它會建立原始影像的翻轉影像、將其轉換為JPG並建立三個尺寸縮圖：140x100、48x48和10x250。

使用下列專案 [!UICONTROL 程式引數] 若要使用建立三個標準縮圖 [!DNL ImageMagick]：

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

使用下列專案 [!UICONTROL 程式引數] 若要使用建立可支援Web的轉譯 [!DNL ImageMagick]：

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>此 [!UICONTROL 命令列程式] 步驟僅適用於資產（型別的節點） `dam:Asset`)或資產的子代。

>[!MORELIKETHIS]
>
>* [處理資產](assets-workflow.md)

