---
title: 使用JEE自定义DSC上的AEM Forms压缩和解压缩文件
description: 了解如何使用JEE自定义DSC上的AEM Forms压缩和解压缩文件
exl-id: 1b950d8f-6b54-452a-831b-f5644370691d
source-git-commit: f0dd1ac3ab9c17a8b331f5048d84ec97dd23924f
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 0%

---

# 在JEE自定义DSC中使用AEM Forms压缩和解压缩文件 {#compressing-decompressing-files}

## 必备知识 {#prerequisites}

在JEE流程管理、基本Java™编程和创建自定义组件方面使用AEM Forms的体验。

**其他必需的其他产品**

Java™编辑器，例如 [Eclipse](https://www.eclipse.org/) 或 [Netbeans IDE](https://netbeans.apache.org/)

## 用户级别 {#user-level}

中间

通过JEE上的AEM Forms，开发人员可以创建自定义DSC（文档服务容器），以创建扩充的开箱即用功能。 创建此类组件可插入JEE运行时环境的AEM Forms，并且符合预期目的。 本文介绍如何创建自定义ZIP服务，该服务可用于将文件列表压缩为.zip文件，并将.zip解压缩为文档列表。

## 创建自定义DSC组件 {#create-custom-dsc-component}

创建具有两个服务操作的自定义DSC组件，以压缩和解压缩文档列表。 此组件使用java.util.zip包进行压缩和解压缩。 请按照以下步骤创建自定义组件：

1. 将adobe-livecycle-client.jar文件添加到库中
1. 添加所需的图标
1. 创建公共类
1. 创建两个名为UnzipDocument和ZipDocuments的公共方法
1. 编写压缩和解压缩逻辑

可以在此处找到代码：

```java
/*
 * Custom DSC : ZIP Utility
 * Purpose: This is a LiveCycle ES2 custom component used to Compress & Decompress List of Documents
 * Author: Nithiyanandam Dharmadass
 * Organization: Ministry of Finance, Kingdom of Bahrain
 * Last modified Date: 18/Apr/2011
 */
package nith.lces2.dsc;

import java.util.zip.ZipEntry;
import java.util.zip.ZipInputStream;
import com.adobe.idp.Document;
import java.io.ByteArrayOutputStream;
import java.io.InputStream;
import java.util.ArrayList;
import java.util.List;
import java.util.zip.ZipOutputStream;

public class ZIPService {

    static final int BUFFER = 2048; // 2MB buffer size

    public java.util.List UnzipDocument(com.adobe.idp.Document zipDocument) throws Exception {
        ZipInputStream zis = new ZipInputStream(zipDocument.getInputStream());

        ZipEntry zipFile;

        List resultList = new ArrayList();

        while ((zipFile = zis.getNextEntry()) != null) {

            ByteArrayOutputStream byteArrayOutStream = new ByteArrayOutputStream();

            int count;  // an int variable to hold the number of bytes read from input stream
            byte data[] = new byte[BUFFER];
            while ((count = zis.read(data, 0, BUFFER)) != -1) {
                byteArrayOutStream.write(data, 0, count);   // write to byte array
            }

            com.adobe.idp.Document unzippedDoc = new Document(byteArrayOutStream.toByteArray());  // create an idp document
            unzippedDoc.setAttribute("file", zipFile.getName());
            unzippedDoc.setAttribute("wsfilename", zipFile.getName());  // update the wsfilename attribute
            resultList.add(unzippedDoc);
        }
        return resultList;  // List of uncompressed documents
    }

    public com.adobe.idp.Document ZipDocuments(java.util.List listOfDocuments,java.lang.String zipFileName) throws Exception {

        if (listOfDocuments == null || listOfDocuments.size() == 0) {
            return null;
        }

        ByteArrayOutputStream byteArrayOutStream = new ByteArrayOutputStream();
        ZipOutputStream zos = new ZipOutputStream(byteArrayOutStream);  // ZIP Output Stream

        for (int i = 0; i < listOfDocuments.size(); i++) {
            Document doc = (Document) listOfDocuments.get(i);
            InputStream docInputStream = doc.getInputStream();
            ZipEntry zipEntry = new ZipEntry(doc.getAttribute("file").toString());
            zos.putNextEntry(zipEntry);
            int count;
            byte data[] = new byte[BUFFER];
            while ((count = docInputStream.read(data, 0, BUFFER)) != -1) {
                zos.write(data, 0, count);  // Read document content and add to zip entry
            }
            zos.closeEntry();
        }
        zos.flush();
        zos.close();

        Document zippedDoc = new Document(byteArrayOutStream.toByteArray());
        if(zipFileName==null || zipFileName.equals(""))
        {
            zipFileName = "CompressedList.zip";
        }
        zippedDoc.setAttribute("file", zipFileName);
        return zippedDoc;
    }
}
```

## 创建组件.XML文件 {#create-component-xml-file}

必须在包的根文件夹中创建component.xml文件，该文件定义了服务操作及其参数。

component.xml文件如下所示：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<component xmlns="https://adobe.com/idp/dsc/component/document">
<!-- Unique id identifying this component -->
   <component-id>ZipService</component-id>

<!-- Version -->
   <version>1.0</version>

<!-- Start of the Service definition -->
   <services>
<!-- Unique name for service descriptor.
           The value is used as the default name for
           deployed services -->
      <service name="ZipService">
<!-- service implementation class definition -->
        <implementation-class>nith.lces2.dsc.ZIPService</implementation-class>

<!-- description -->
        <description>Compress or Decompress list of documents</description>

<!--  You can provide your own icons for a distinct look   -->
          <small-icon>icons/Zip_icon16.png</small-icon>
          <large-icon>icons/Zip_icon32.png</large-icon>


<!-- automatically deploys the service and starts it after installation -->
         <auto-deploy service-id="ZipService" />

         <operations>
<!-- method name in the interface setSmtpHost-->
            <operation name="UnzipDocument">
<!-- input parameters to the "send" method -->
              <input-parameter name="zipDocument" title="Input ZIP Document" type="com.adobe.idp.Document">
                    <hint>A ZIP File to be decompressed</hint>
                </input-parameter>
                <output-parameter name="resultList" title="Decompressed list of documents" type="java.util.List">
                    <hint>Decompressed ZIP list</hint>
                </output-parameter>
            </operation>
            <operation name="ZipDocuments">
<!-- input parameters to the "send" method -->
              <input-parameter name="listOfDocuments" title="List of Documents" type="java.util.List">
                    <hint>A list of documents to be Compressed</hint>
                </input-parameter>
                <input-parameter name="zipFileName" title="Result File Name" type="java.lang.String">
                    <hint>The name of compressed file (optional)</hint>
                </input-parameter>

                <output-parameter name="zippedDoc" title="Compressed Zip file" type="com.adobe.idp.Document">
                    <hint>Compressed ZIP File</hint>
                </output-parameter>
            </operation>
             </operations>
      </service>
   </services>
</component>
```

## 打包和部署组件 {#packaging-deploying-component}

1. 编译Java™项目并创建.JAR文件。
1. 通过Workbench将组件（.JAR文件）部署到JEE运行时的AEM Forms。
1. 从Workbench启动服务（请参阅下图）。

![流程设计](assets/process-design.jpg)

## 在工作流中使用ZIP服务 {#using-zip-service-in-workflows}

自定义服务的UnzipDocument操作现在可以接受文档变量作为输入，并返回文档变量列表作为输出。

![解压缩文档](assets/unzip-doc.jpg)

同样，自定义组件的ZipDocuments操作可以接受文档列表作为输入，将它们压缩为zip文件并返回压缩的文档。

![Zip文档](assets/zip-doc.jpg)

以下工作流编排说明如何解压缩给定的ZIP文件，将其压缩回另一个ZIP文件并返回输出（请参阅下图）。

![解压缩Zip工作流](assets/unzip-zip-process.jpg)

## 一些业务用例 {#business-use-cases}

您可以将此ZIP服务用于以下用例：

* 查找给定文件夹中的所有文件，并将文件作为压缩文档返回。

* 提供包含多个PDF文档的ZIP文件，在解压缩文档后可以扩展这些文档。 这需要AEM Forms on JEEReader扩展模块。

* 提供包含异类文档的ZIP文件，可使用生成PDF服务将异类文档解压缩并转换为PDF文档。

* 策略保护文档列表并作为ZIP文件返回。

* 允许用户将流程实例的所有附件下载为一个ZIP文件。
