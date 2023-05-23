---
title: 取得含附件的電子郵件的其他步驟
description: 取得含附件的電子郵件的其他步驟
exl-id: 0d0713fb-d95a-4a95-91ef-9cdaea30e343
source-git-commit: 2e9b9c40f54aa54a946e4320341ed4a760c56fd1
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# 無法取得JEE平台上AEM Forms的電子郵件（含附件）{#unable-to-get-email-with-attachments}

此問題適用於以下版本：
* Experience Manager6.5 Forms

## 问题 {#issue}

使用者無法執行操作，例如透過電子郵件傳送PDF或包含附件的提交設定。

## 解决方案 {#solution}

1. 將jar下載為 [java.mail-1.0.jar](/help/forms/using/java.mail-1.0.jar) 並解壓縮下載的jar檔案以取得資訊清單檔案。

1. 使用資訊清單檔案： `java.mail-1.0.jar` 從步驟1擷取以建立新的自訂jar檔案，例如 `java.mail-1.5.jar`.

1. 開啟資訊清單檔案並取代所有出現的 `1.5.0` 替換為 `1.5.6` 和 `Bundle-Version: 1.0` 替換為 `Bundle-Version:1.5`

1. 建立新的自訂jar (`java.mail-1.5.jar`)檔案，使用下列指令於 `C:\Adobe\Adobe_Experience_Manager_Forms\java\jdk\bin` 資料夾為：
   `jar -cfm java.mail-1.5.jar manifest.mf`

   在上述命令中， *manifest.mf* 是資訊清單檔案的名稱，並且 *java.mail-1.5.jar* 是在執行上述命令後建立的檔案名稱。

1. 下載 [javax.mail-1.5.6.redhat-1.jar](https://mvnrepository.com/artifact/com.sun.mail/javax.mail/1.5.6.redhat-1).

1. 導覽至 `http://<server name>:<port>/lc/system/console/bundles`並刪除名稱為的組合 `JavaMail API (com.sun.mail.javax.mail) version 1.6.2`.

1. 安裝 `java.mail-1.5.jar` 取得自步驟3。  此步驟會重新啟動JEE部署的sling屬性。 等候已安裝的套件組合在 `http://<server name>:<port>/lc/system/console/bundles` 將狀態顯示為 **作用中**.

   >注意：如果是，狀態仍為 **非作用中**，重新啟動   **Jboss** 從 **服務主控台**.


1. 安裝 `javax.mail-1.5.6.redhat-1.jar`使用步驟5下載的檔案。

1. 停止 **Jboss** 從 **服務主控台** 並將下列屬性附加至 **Sling.properties** 檔案：
   * `org.osgi.framework.system.packages.extra=javax.activation; version\=1.2.0`
   * `sling.bootdelegation.activation=javax.activation.*`

1. 重新啟動 **Jboss**.
