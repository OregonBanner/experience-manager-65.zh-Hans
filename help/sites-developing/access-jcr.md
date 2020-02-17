---
title: 如何以编程方式访问AEM JCR
seo-title: 如何以编程方式访问AEM JCR
description: 您可以有计划地修改位于AEM存储库（Adobe Marketing cloud的一部分）中的节点和属性
seo-description: 您可以有计划地修改位于AEM存储库（Adobe Marketing cloud的一部分）中的节点和属性
uuid: 2051d03f-430a-4cae-8f6d-e5bc727d733f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 69f62a38-7991-4009-8db7-ee8fd35dc535
translation-type: tm+mt
source-git-commit: 6d216e7521432468a01a29ad2879f8708110d970

---


# 如何以编程方式访问AEM JCR{#how-to-programmatically-access-the-aem-jcr}

您可以有计划地修改位于Adobe CQ存储库（Adobe Marketing cloud的一部分）中的节点和属性。 要访问CQ存储库，请使用Java内容存储库(JCR)API。 可以使用Java JCR API对位于Adobe CQ存储库中的内容执行创建、替换、更新和删除(CRUD)操作。 有关Java JCR API的详细信息，请参 [阅https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html)。

>[!NOTE]
>
>本开发文章从外部Java应用程序修改Adobe CQ JCR。 相反，您可以使用JCR API从OSGi包中修改JCR。 有关详细信息，请 [参阅在Java内容存储库中保持CQ数据](https://helpx.adobe.com/experience-manager/using/persisting-cq-data-java-content1.html)。

>[!NOTE]
>
>要使用JCR API，请将文 `jackrabbit-standalone-2.4.0.jar` 件添加到Java应用程序的类路径。 可从Java JCR API网页https://jackrabbit.apache.org/jcr/jcr-api.html获取此JAR文 [件](https://jackrabbit.apache.org/jcr/jcr-api.html)。

>[!NOTE]
>
>要了解如何使用JCR查询API查询Adobe CQ JCR，请参阅 [使用JCR API查询Adobe Experience Manager数据](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html)。

## 创建存储库实例 {#create-a-repository-instance}

虽然连接存储库和建立连接的方法不同，但本开发文章使用属于类的静态方 `org.apache.jackrabbit.commons.JcrUtils` 法。 方法的名称为 `getRepository`。 此方法采用一个表示Adobe CQ服务器URL的字符串参数。 For example `http://localhost:4503/crx/server`.

该方 `getRepository`法返回一 `Repository`个实例，如下面的代码示例所示。

```java
//Create a connection to the AEM JCR repository running on local host
Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");
```

## 创建会话实例 {#create-a-session-instance}

实 `Repository`例表示CRX存储库。 使用实例 `Repository`与存储库建立会话。 要创建会话，请调用实 `Repository`例的方 `login`法并传递对 `javax.jcr.SimpleCredentials` 象。 该方 `login`法返回一个 `javax.jcr.Session` 实例。

可使用对象 `SimpleCredentials`的构造函数并传递以下字符串值来创建对象：

* 用户名；
* 相应的密码

传递第二个参数时，调用String对象的方 `toCharArray`法。 以下代码显示如何调用 `login`返回的方法 `javax.jcr.Sessioninstance`。

```java
//Create a Session instance
javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));
```

## 创建节点实例 {#create-a-node-instance}

使用实 `Session`例创建实 `javax.jcr.Node` 例。 通过 `Node`实例可执行节点操作。 例如，您可以创建新节点。 要创建表示根节点的节点，请调 `Session`用实例的 `getRootNode` 方法，如下面的代码行所示。

```java
//Create a Node
Node root = session.getRootNode();
```

创建实例后， `Node`您可以执行创建其他节点和向其添加值等任务。 例如，下面的代码创建两个节点并将一个值添加到第二个节点。

```java
// Store content
Node day = adobe.addNode("day");
day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");
```

## 检索节点值 {#retrieve-node-values}

要检索节点及其值，请调用实 `Node`例的方 `getNode`法并将表示完全限定路径的字符串值传递给节点。 请考虑在上一个代码示例中创建的节点结构。 要检索日节点，请指定adobe/day，如以下代码所示：

```java
// Retrieve content
Node node = root.getNode("adobe/day");
System.out.println(node.getPath());
System.out.println(node.getProperty("message").getString());
```

## 在Adobe CQ存储库中创建节点 {#create-nodes-in-the-adobe-cq-repository}

以下Java代码示例表示连接到Adobe CQ、创建实例和添 `Session`加新节点的Java类。 为节点分配一个数据值，然后将节点的值及其路径写入控制台。 完成会话后，请务必注销。

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

运行完整的代码示例并创建节点后，您可以在 **[!UICONTROL CRXDE Lite中查看新节点]**，如下图所示。

![chlimage_1-68](assets/chlimage_1-68a.png)

