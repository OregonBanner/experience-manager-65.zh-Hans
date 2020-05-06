---
title: 使用媒体处理程序和工作流处理资源
description: 了解媒体处理程序以及如何使用工作流对您的数字资产执行任务。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 99ce6e0572797b7bccf755aede93623be6bd5698
workflow-type: tm+mt
source-wordcount: '2197'
ht-degree: 4%

---


# 使用媒体处理程序和工作流处理资源 {#processing-assets-using-media-handlers-and-workflows}

Adobe Experience Manager(AEM)资产附带一组默认工作流和媒体处理程序，用于处理资产。 工作流定义要在资产上执行的任务，然后将特定任务委派给媒体处理程序，例如缩略图生成或元数据提取。

可以将工作流配置为在上传特定MIME类型的资产时自动执行。 这些处理步骤是通过一系列AEM Assets媒体处理程序定义的。 AEM提供一些 [内置的处理函数](#default-media-handlers) ，其他处理函数可以是自定 [义开发的](#creating-a-new-media-handler) ，也可以通过将进程委派到命令行工 [具来定义](#command-line-based-media-handler)。

媒体处理程序是AEM资产中对资产执行特定操作的服务。 例如，当MP3音频文件上传到AEM时，工作流会触发一个MP3处理程序，该处理程序会提取元数据并生成缩略图。 媒体处理程序通常与工作流结合使用。 AEM中支持大多数常见的MIME类型。 通过扩展／创建任务、扩展／创建媒体处理函数或禁用／启用媒体处理函数，可以对资产执行特定工作流。

>[!NOTE]
>
>有关AEM Assets支 [持的所有格式](assets-formats.md) 以及每种格式支持的功能的说明，请参阅资产支持的格式页面。

## 默认媒体处理函数 {#default-media-handlers}

AEM资产中提供以下媒体处理程序，并处理最常见的MIME类型：

<!-- TBD: Apply correct formatting once table is moved to MD.
-->

| 处理程序名称 | 服务名称（在系统控制台中） | 支持的MIME类型 |
|---|---|---|
| [!UICONTROL TextHandler] | `com.day.cq.dam.core.impl.handler.TextHandler` | text/plain |
| [!UICONTROL PdfHandler] | `com.day.cq.dam.handler.standard.pdf.PdfHandler` | <ul><li>application/pdf</li><li>application/illustrator</li></ul> |
| [!UICONTROL JpegHandler] | `com.day.cq.dam.core.impl.handler.JpegHandler` | image/jpeg |
| [!UICONTROL Mp3Handler] | `com.day.cq.dam.handler.standard.mp3.Mp3Handler` | audio/mpeg |
| [!UICONTROL ZipHandler] | `com.day.cq.dam.handler.standard.zip.ZipHandler` | <ul><li>application/java-archive </li><li> application/zip</li></ul> |
| [!UICONTROL PictHandler] | `com.day.cq.dam.handler.standard.pict.PictHandler` | image/pict |
| [!UICONTROL StandardImageHandler] | `com.day.cq.dam.core.impl.handler.StandardImageHandler` | <ul><li>image/gif </li><li> image/png </li> <li>application/photoshop </li> <li>image/jpeg </li><li> image/tiff </li> <li>image/x-ms-bmp </li><li> image/bmp</li></ul> |
| [!UICONTROL MSOfficeHandler] | `com.day.cq.dam.handler.standard.msoffice.MSOfficeHandler` | application/msword |
| [!UICONTROL MSPowerPointHandler] | `com.day.cq.dam.handler.standard.msoffice.MSPowerPointHandler` | application/vnd.ms-powerpoint |
| [!UICONTROL OpenOfficeHandler] | `com.day.cq.dam.handler.standard.ooxml.OpenOfficeHandler` | <ul><li>application/vnd.openxmlformats-officedocument.wordprocessingml.document</li><li> application/vnd.openxmlformats-officedocument.spreadsheetml.sheet</li><li> application/vnd.openxmlformats-officedocument.presentationml.presentation</li></ul> |
| [!UICONTROL EPubHandler] | `com.day.cq.dam.handler.standard.epub.EPubHandler` | application/epub+zip |
| [!UICONTROL GenericAssetHandler] | `com.day.cq.dam.core.impl.handler.GenericAssetHandler` | 回退，以防找不到其他处理程序从资产提取数据 |

所有处理函数都执行以下任务:

* 从资产提取所有可用元数据。
* 创建资产的缩略图。

要视图活动媒体处理程序：

1. In your browser, navigate to `http://localhost:4502/system/console/components`.
1. 单击 `com.day.cq.dam.core.impl.store.AssetStoreImpl`.
1. 将显示具有所有活动媒体处理函数的列表。 例如：

![chlimage_1-437](assets/chlimage_1-437.png)

## 在工作流中使用媒体处理程序对资产执行任务 {#using-media-handlers-in-workflows-to-perform-tasks-on-assets}

媒体处理程序是通常与工作流结合使用的服务。

AEM具有一些处理资产的默认工作流。 要视图这些模型，请打开工作流控制台，然后单 **[!UICONTROL 击模型]** 选项卡： 与AEM资产开始的工作流标题是特定于资产的标题。

现有工作流可以扩展，也可以创建新客户，以根据特定要求处理资产。

以下示例演示如何增强 **[!UICONTROL AEM Assets 同步工作流]**，以便为除 PDF 文档外的所有资产生成子资产。

### 禁用或启用媒体处理程序 {#disabling-enabling-a-media-handler}

可以通过Apache Felix Web管理控制台禁用或启用媒体处理程序。 禁用媒体处理程序后，不会对资产执行其任务。

启用／禁用媒体处理程序：

1. In your browser, navigate to `https://<host>:<port>/system/console/components`.
1. 单击 **[!UICONTROL 媒体处]** 理程序名称旁边的“禁用”。 For example: `com.day.cq.dam.handler.standard.mp3.Mp3Handler`.
1. 刷新页面： 媒体处理程序旁边会显示一个图标，指示它已禁用。
1. 要启用媒体处理程序，请单 **[!UICONTROL 击]** 媒体处理程序名称旁的“启用”。

### 创建新的媒体处理程序 {#creating-a-new-media-handler}

要支持新的媒体类型或对资产执行特定任务，必须创建新的媒体处理程序。 本节介绍如何继续。

#### 重要类和接口 {#important-classes-and-interfaces}

开始实现的最佳方法是继承所提供的抽象实现，该实现能够处理大多数事情并提供合理的默认行为： 课 `com.day.cq.dam.core.AbstractAssetHandler` 程。

该类已提供抽象服务描述符。 因此，如果您继承了此类并使用maven-sling-plugin，请确保将inherit标志设置为 `true`。

实现以下方法：

* `extractMetadata()`: 提取所有可用的元数据。
* `getThumbnailImage()`: 在传递的资产中创建缩略图。
* `getMimeTypes()`: 返回资产MIME类型。

以下是一个示例模板：

```Java
package my.own.stuff; /** * @scr.component inherit="true" * @scr.service */ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the relevant parts }
```

接口和类包括：

* `com.day.cq.dam.api.handler.AssetHandler` 接口： 此接口描述添加对特定MIME类型的支持的服务。 添加新的MIME类型需要实现此接口。 该界面包含用于导入和导出特定文档、创建缩略图和提取元数据的方法。
* `com.day.cq.dam.core.AbstractAssetHandler` 类： 此类用作所有其他资产处理程序实现的基础，并提供常用功能。
* `com.day.cq.dam.core.AbstractSubAssetHandler` class:
   * 此类用作所有其他资产处理程序实现的基础，并为子资产提取提供常用功能以及常用功能。
   * 开始实现的最佳方法是继承所提供的抽象实现，该实现能够处理大多数事情并提供合理的默认行为： com.day.cq.dam.core.AbstractAssetHandler类。
   * 该类已提供抽象服务描述符。 因此，如果您继承了此类并使用maven-sling-plugin，请确保将inherit标志设置为true。

需要实现以下方法：

* `extractMetadata()`: 此方法会提取所有可用的元数据。
* `getThumbnailImage()`: 此方法会从传递的资产中创建缩略图。
* `getMimeTypes()`: 此方法返回资产mime类型。

以下是一个示例模板：

打包my.own.stuff; /&amp;ast;&amp;ast; &amp;ast; @scr.component inherit=&quot;true&quot; &amp;ast; @scr.service &amp;ast;/公共类MyMediaHandler扩展com.day.cq.dam.core.AbstractAssetHandler { //实现相关部分}

接口和类包括：

* `com.day.cq.dam.api.handler.AssetHandler` 接口： 此接口描述添加对特定MIME类型的支持的服务。 添加新的MIME类型需要实现此接口。 该界面包含用于导入和导出特定文档、创建缩略图和提取元数据的方法。
* `com.day.cq.dam.core.AbstractAssetHandler` 类： 此类用作所有其他资产处理程序实现的基础，并提供常用功能。
* `com.day.cq.dam.core.AbstractSubAssetHandler` 类： 此类用作所有其他资产处理程序实现的基础，并为子资产提取提供常用功能以及常用功能。

#### 示例： 创建特定文本处理程序 {#example-create-a-specific-text-handler}

在本节中，您将创建一个特定的文本处理程序，它生成带有水印的缩略图。

按如下方式继续：

请参 [阅开发工具](../sites-developing/dev-tools.md) ，安装Eclipse并设置Maven插件以及设置Maven项目所需的依赖项。

执行以下过程后，当您将txt文件上传到AEM时，将提取该文件的元数据并生成两个带水印的缩略图。

1. 在Eclipse中，创建 `myBundle` Maven项目：

   1. 在菜单栏中，单击“文 **[!UICONTROL 件”>“新建”>“其他]**”。
   1. 在对话框中，展开Maven文件夹，选择Maven Project，然后单击“下 **[!UICONTROL 一步”]**。
   1. 选中创建简单项目框和使用默认工作区位置框，然后单击下 **[!UICONTROL 一步]**。
   1. 定义Maven项目：

      * 组ID: com.day.cq5.myhandler
      * 对象ID: myBundle
      * 名称： 我的AEM捆绑
      * 描述： 这是我的AEM捆绑
   1. 单击 **[!UICONTROL 完成]**。


1. 将Java编译器设置为版本1.5:

   1. 右键单击项目， `myBundle` 选择属性。
   1. 选择“Java编译器”并将以下属性设置为1.5:

      * 编译器规范级别
      * 生成的。class文件兼容性
      * 源兼容性
   1. 单击&#x200B;**[!UICONTROL 确定]**。在对话框窗口中，单击 **[!UICONTROL 是]**。


1. 将文件中的代 `pom.xml` 码替换为以下代码：

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

1. 创建包 `com.day.cq5.myhandler` 含以下Java类的包 `myBundle/src/main/java`:

   1. 在myBundle下，右键单击， `src/main/java`选择“新建”，然后选择“打包”。
   1. 将其命名 `com.day.cq5.myhandler` 并单击“完成”。

1. 创建Java类 `MyHandler`:

   1. 在Eclipse中，右 `myBundle/src/main/java`键单击包， `com.day.cq5.myhandler` 选择新建，然后选择类。
   1. 在对话框窗口中，将Java类命名为MyHandler，然后单击“完成”。 Eclipse创建并打开文件MyHandler.java。
   1. 在将 `MyHandler.java` 现有代码替换为以下代码时，请保存更改：

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
      watermarkLayer = ImageHelper.createLayer(session, "/content/dam/geometrixx/icons/certificate.png");
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
     // We need to keep track of the last character, if we have two white spaces in a row we dont want to double count
     // The starting of the document is always a whitespace
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
     // If we do not end with a white space then we need to add one extra word
     if (!currentWhiteSpace) { numwords++; }
     return numwords;
    }
   }
   ```

1. 编译Java类并创建包：

   1. 右键单击项 `myBundle` 目，选 **[!UICONTROL 择运行]**, **[!UICONTROL 然后执行安装]**。
   1. 将在 `myBundle-0.0.1-SNAPSHOT.jar` 下创建包（包含编译类） `myBundle/target`。

1. 在CRX资源管理器中，在下面创建新节点 `/apps/myApp`。 名称= `install`，类型= `nt:folder`。
1. 复制捆绑包 `myBundle-0.0.1-SNAPSHOT.jar` 并将其存储 `/apps/myApp/install` 在下面（例如WebDAV）。 新文本处理函数现在在AEM中处于活动状态。
1. 在您的浏览器中，打 [!UICONTROL 开Apache Felix Web管理控制台]。 选择“组 [!UICONTROL 件] ”选项卡并禁用默认文本处理程序 `com.day.cq.dam.core.impl.handler.TextHandler`。

## 基于命令行的媒体处理程序 {#command-line-based-media-handler}

AEM允许您在工作流中运行任何命令行工具来转换资产（如ImageMagick），并将新演绎版添加到资产。 您只需在承载AEM服务器的磁盘上安装命令行工具，并向工作流中添加和配置流程步骤。 调用的过程( `CommandLineProcess`称为)还允许根据特定MIME类型进行筛选，并基于新演绎版创建多个缩略图。

以下转换可以自动运行并在AEM资产中存储：

* 使用ImageMagick和Ghostscript [实现EPS](https://www.imagemagick.org/script/index.php) 和 [AI转换](https://www.ghostscript.com/)。
* 使用FFmpeg的FLV视 [频转码](https://ffmpeg.org/)。
* 使用LAME进行MP3 [编码](http://lame.sourceforge.net/)。
* 使用SOX进行音 [频处理](http://sox.sourceforge.net/)。

>[!NOTE]
>
>在非Windows系统上，FFmpeg工具为文件名中包含单引号(&#39;)的视频资产生成演绎版时返回错误。 如果视频文件的名称包含单引号，请在上传到AEM之前将其删除。

该流 `CommandLineProcess` 程按其列出的顺序执行以下操作：

* 过滤器文件，如果指定，则根据特定的mime类型。
* 在承载AEM服务器的磁盘上创建临时目录。
* 将原始文件流化到临时目录。
* 执行由步骤的参数定义的命令。 该命令将在具有运行AEM的用户权限的临时目录中执行。
* 将结果流回AEM服务器的再现文件夹。
* 删除临时目录。
* 根据这些演绎版创建缩略图（如果已指定）。 缩略图的编号和尺寸由步骤的参数定义。

### 使用ImageMagick的示例 {#an-example-using-imagemagick}

以下示例显示如何设置命令行处理步骤，以便每次将mime-type gif或tiff的资产添加到AEM服务器上的/content/dam时，将创建原始图像的翻转图像以及三个额外的缩略图（140x100、48x48和10x250）。

为此，您将使用ImageMagick。 ImageMagick是用于创建、编辑和合成位图图像的免费软件套件，通常通过命令行使用。

首先在承载AEM服务器的磁盘上安装ImageMagick:

1. 安装ImageMagick: 请参阅ImageMagick [文档](https://www.imagemagick.org/script/download.php)。
1. 设置工具，以便在命令行上运行转换。
1. 要查看该工具是否安装正确，请在命令行 `convert -h` 上运行以下命令。

   它显示一个包含转换工具所有可能选项的帮助屏幕。

   >[!NOTE]
   >
   >在某些版本的Windows（例如Windows SE）中，转换命令可能无法运行，因为它与作为Windows安装一部分的本机转换实用程序相冲突。 在这种情况下，请提及用于将图像文件转换为缩略图的ImageMagick实用程序的完整路径。 For example, `"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`.

1. 要查看该工具是否运行正常，请向工作目录添加。jpg图像，并在命令行上运 `<image-name>.jpg -flip <image-name>-flipped.jpg` 行命令convert。

   翻转后的图像会添加到目录中。

然后，将命令行流程步骤添加到 **[!UICONTROL DAM 更新资产]**&#x200B;工作流：

1. 转到“工作 **[!UICONTROL 流]** ”控制台。
1. 在“模 **[!UICONTROL 型]** ”选项卡中，编 **[!UICONTROL 辑DAM更新资产模型]** 。
1. 按如下方式更改启 **[!UICONTROL 用Web的再现]** 步骤的设置：

   **参数**:

   `mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

1. 保存工作流。

要测试修改后的工作流，请向添加资产 `/content/dam`。

1. 在文件系统中，获取您选择的TIFF图像。 将其重命 `myImage.tiff` 名为并将其 `/content/dam`复制到，例如，使用WebDAV。
1. 例如， **[!UICONTROL 转到]** CQ5 DAM控制台 `http://localhost:4502/libs/wcm/core/content/damadmin.html`。
1. 打开资 **[!UICONTROL 源myImage.tiff]** ，验证已创建翻转的图像和三个缩略图。

#### 配置CommandLineProcess进程步骤 {#configuring-the-commandlineprocess-process-step}

本节介绍如何设置 [!UICONTROL CommandLineProcess] 的[!UICONTROL 进程参数]。

使用逗号分隔 [!UICONTROL 进程参数] ，但不要用空格开始它。

| 参数格式 | 描述 |
|---|---|
| mime:&lt;mime类型> | 可选参数。 如果资产的mime类型与其中一个参数相同，则应用该过程。 <br>可以定义多个MIME类型。 |
| tn:&lt;width>:&lt;height> | 可选参数。 该过程会创建缩略图，其尺寸在参数中定义。 <br>可以定义多个缩略图。 |
| cmd: &lt;命令> | 定义将执行的命令。 语法取决于命令行工具。 只能定义一个命令。 <br>以下变量可用于创建命令：<br>`${filename}`: 输入文件的名称，例如original.jpg <br> `${file}`: 输入文件的完整路径名，例如/tmp/cqdam0816.tmp/original.jpg <br> `${directory}`: 输入文件的目录，例如/tmp/cqdam0816.tmp <br>`${basename}`: 不带扩展名的输入文件的名称，例如原始文 <br>`${extension}`件： 输入文件的扩展名，例如jpg |

例如，如果ImageMagick安装在承载AEM服务器的磁盘上，并且如果您使用CommandLineProcess作为实施创建了一个进 [!UICONTROL 程步骤] ，以及将以下值作为进 [!UICONTROL 程参数]:

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

然后，当工作流运行时，该步骤仅应用于具有或 `image/gif` 作为 `mime:image/tiff` 原始图像 `mime-types`的资产，它会创建翻转后的原始图像，将其转换为JPG并创建具有尺寸的三个缩略图： 140x100、48x48和10x250。

使用以下 [!UICONTROL 流程参数] ，使用ImageMagick创建三个标准缩略图：

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

使用以下 [!UICONTROL 进程参数] ，使用ImageMagick创建启用Web的再现：

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>CommandLineProcess [!UICONTROL 步骤仅] 适用于资产(类型的节 `dam:Asset`点)或资产的后代。

>[!MORELIKETHIS]
>
>* [处理资产](assets-workflow.md)

