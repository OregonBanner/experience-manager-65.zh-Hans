---
title: 如何以程式設計方式存取AEM JCR
seo-title: How to programmatically access the AEM JCR
description: 您可以以程式設計方式修改位於AEM存放庫(屬於Adobe Marketing Cloud的一部分)中的節點和屬性
seo-description: You can programmatically modify nodes and properties located within the AEM repository, which is part of the Adobe Marketing Cloud
uuid: 2051d03f-430a-4cae-8f6d-e5bc727d733f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 69f62a38-7991-4009-8db7-ee8fd35dc535
exl-id: fe946b9a-b29e-4aa5-b973-e2a652417a55
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 0%

---

# 如何以程式設計方式存取AEM JCR{#how-to-programmatically-access-the-aem-jcr}

您可以以程式設計方式修改位於Adobe CQ存放庫(屬於Adobe Marketing Cloud的一部分)中的節點和屬性。 若要存取CQ存放庫，請使用Java內容存放庫(JCR) API。 您可以使用Java JCR API對Adobe CQ存放庫中的內容執行建立、取代、更新和刪除(CRUD)操作。 如需Java JCR API的詳細資訊，請參閱 [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html).

>[!NOTE]
>
>這篇開發文章從外部Java應用程式修改了Adobe CQ JCR。 相反地，您可以使用JCR API從OSGi套件組合中修改JCR。 如需詳細資訊，請參閱 [將CQ資料儲存在Java內容存放庫中](https://helpx.adobe.com/experience-manager/using/persisting-cq-data-java-content1.html).

>[!NOTE]
>
>若要使用JCR API，請新增 `jackrabbit-standalone-2.4.0.jar` 檔案至您的Java應用程式的類別路徑。 您可以從Java JCR API網頁取得此JAR檔案，網址為 [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html).

>[!NOTE]
>
>若要瞭解如何使用JCR查詢API查詢Adobe CQ JCR，請參閱 [使用JCR API查詢Adobe Experience Manager資料](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html).

## 建立存放庫執行個體 {#create-a-repository-instance}

雖然有不同的方式可連線到存放庫並建立連線，但本開發文章會使用屬於的靜態方法 `org.apache.jackrabbit.commons.JcrUtils` 類別。 方法的名稱為 `getRepository`. 此方法會採用代表Adobe CQ伺服器URL的字串引數。 例如 `http://localhost:4503/crx/server`。

此 `getRepository`方法傳回 `Repository`例項，如下列程式碼範例所示。

```java
//Create a connection to the AEM JCR repository running on local host
Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");
```

## 建立工作階段執行個體 {#create-a-session-instance}

此 `Repository`執行個體代表CRX存放庫。 您使用 `Repository`執行個體以建立與存放庫的工作階段。 若要建立工作階段，請叫用 `Repository`執行個體的 `login`方法並傳遞 `javax.jcr.SimpleCredentials` 物件。 此 `login`方法傳回 `javax.jcr.Session` 執行個體。

您建立 `SimpleCredentials`物件，使用它的建構函式並傳遞下列字串值：

* 使用者名稱；
* 對應的密碼

傳遞第二個引數時，呼叫字串物件的 `toCharArray`方法。 下列程式碼會示範如何呼叫 `login`傳回「 」的方法 `javax.jcr.Sessioninstance`.

```java
//Create a Session instance
javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));
```

## 建立節點例項 {#create-a-node-instance}

使用 `Session`要建立的例項 `javax.jcr.Node` 執行個體。 A `Node`執行個體可讓您執行節點作業。 例如，您可以建立新節點。 若要建立代表根節點的節點，請叫用 `Session`執行個體的 `getRootNode` 方法，如下列程式碼行所示。

```java
//Create a Node
Node root = session.getRootNode();
```

一旦建立 `Node`例如，您可以執行建立其他節點及為其增加值等工作。 例如，下列程式碼會建立兩個節點，並將值新增至第二個節點。

```java
// Store content
Node day = adobe.addNode("day");
day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");
```

## 擷取節點值 {#retrieve-node-values}

若要擷取節點及其值，請叫用 `Node`執行個體的 `getNode`方法並傳遞代表完整路徑之字串值至節點。 請考量在上一個程式碼範例中建立的節點結構。 若要擷取日期節點，請指定adobe/day，如下列程式碼所示：

```java
// Retrieve content
Node node = root.getNode("adobe/day");
System.out.println(node.getPath());
System.out.println(node.getProperty("message").getString());
```

## 在Adobe CQ存放庫中建立節點 {#create-nodes-in-the-adobe-cq-repository}

以下Java程式碼範例代表連線至Adobe CQ的Java類別，會建立 `Session`例項，並新增節點。 節點會獲派資料值，然後節點的值及其路徑會寫入主控台。 當您完成工作階段時，請務必登出。

```java
/*
 * This Java Quick Start uses the jackrabbit-standalone-2.4.0.jar
 * file. See the previous section for the location of this JAR file
 */

import javax.jcr.Repository;
import javax.jcr.Session;
import javax.jcr.SimpleCredentials;
import javax.jcr.Node;

import org.apache.jackrabbit.commons.JcrUtils;
import org.apache.jackrabbit.core.TransientRepository;

public class GetRepository {

public static void main(String[] args) throws Exception {

try {

    //Create a connection to the CQ repository running on local host
    Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");

   //Create a Session
   javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));

  //Create a node that represents the root node
  Node root = session.getRootNode();

  // Store content
  Node adobe = root.addNode("adobe");
  Node day = adobe.addNode("day");
  day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");

  // Retrieve content
  Node node = root.getNode("adobe/day");
  System.out.println(node.getPath());
  System.out.println(node.getProperty("message").getString());

  // Save the session changes and log out
  session.save();
  session.logout();
  }
 catch(Exception e){
  e.printStackTrace();
  }
 }
}
```

執行完整程式碼範例並建立節點後，您便可以在以下位置檢視新節點： **[!UICONTROL CRXDE Lite]**，如下圖所示。

![chlimage_1-68](assets/chlimage_1-68a.png)
