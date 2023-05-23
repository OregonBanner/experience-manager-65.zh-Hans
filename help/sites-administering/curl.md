---
title: 搭配AEM使用cURL
seo-title: Using cURL with AEM
description: 瞭解如何搭配AEM使用cURL。
seo-description: Learn how to use cURL with AEM.
uuid: 771b9acc-ff3a-41c9-9fee-7e5d2183f311
contentOwner: Silviu Raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: d4ceb82e-2889-4507-af22-b051af83be38
exl-id: e3f018e6-563e-456f-99d5-d232f1a4aa55
source-git-commit: fafcf5f9ec64f147447300b02afbc0590d0c5e22
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 2%

---

# 搭配AEM使用cURL{#using-curl-with-aem}

管理員通常需要自動化或簡化任何系統內的常見工作。 例如，在AEM中，管理使用者、安裝套件和管理OSGi套件組合是通常必須完成的任務。

由於AEM建置所根據之Sling架構的RESTful性質，大部分工作都可透過URL呼叫來完成。 cURL可用來執行這類URL呼叫，可做為AEM管理員的實用工具。

## 什麼是cURL {#what-is-curl}

cURL是用來執行URL操作的開放原始碼命令列工具。 它支援廣泛的網際網路通訊協定，包括HTTP、HTTPS、FTP、FTPS、SCP、SFTP、TFTP、LDAP、DAP、DICT、TELNET、FILE、IMAP、POP3、SMTP和RTSP。

cURL是建立良好且廣泛使用的工具，用於使用URL語法取得或傳送資料，最初於1997年發行。 名稱cURL原本的意思是「參閱URL」。

由於AEM建置所依據的Sling架構具有RESTful性質，因此大部分工作可以簡化為URL呼叫，而透過cURL執行。 [內容操控任務](/help/sites-administering/curl.md#common-content-manipulation-aem-curl-commands) 例如啟用頁面、開始工作流程以及 [作業任務](/help/sites-administering/curl.md#common-operational-aem-curl-commands) 例如套件管理及管理使用者等，都可以使用cURL來自動化。 此外，您可以 [建立您自己的cURL](/help/sites-administering/curl.md#building-a-curl-ready-aem-command) 適用於AEM中大部分工作的命令。

>[!NOTE]
>
>透過cURL執行的任何AEM命令都必須像任何使用者一樣獲得AEM的授權。 使用cURL執行AEM命令時，會考量所有ACL和存取許可權。

## 正在下載cURL {#downloading-curl}

cURL是macOS的標準部分，並且有些Linux障礙。 不過，它適用於大多數的作業系統。 您可在以下網址找到最新下載內容： [https://curl.haxx.se/download.html](https://curl.haxx.se/download.html).

cURL的來源存放庫也可以在GitHub上找到。

## 建置cURL就緒的AEM命令 {#building-a-curl-ready-aem-command}

cURL命令可建置供AEM中的大部分作業使用，例如觸發工作流程、檢查OSGi設定、觸發JMX命令、建立復寫代理程式等。

若要尋找特定操作所需的確切命令，您必須在執行AEM命令時，使用瀏覽器中的開發人員工具來擷取對伺服器的POST呼叫。

以下步驟說明如何在Chrome瀏覽器中建立新頁面，以作為範例。

1. 準備您要在AEM中叫用的動作。 在此案例中，我們已將推進至 **建立頁面** 精靈，但尚未點按 **建立**.

   ![chlimage_1-66](assets/chlimage_1-66a.png)

1. 啟動開發人員工具並選取 **網路** 標籤。 按一下 **保留記錄** 選項。

   ![chlimage_1-67](assets/chlimage_1-67a.png)

1. 按一下 **建立** 在 **建立頁面** 精靈以實際建立工作流程。
1. 以滑鼠右鍵按一下產生的POST動作，然後選取 **複製** -> **復製為cURL**.

   ![chlimage_1-68](assets/chlimage_1-68a.png)

1. 將cURL命令複製到文字編輯器，並從命令中移除所有標題，其開頭為 `-H` （下圖以藍色顯示）並新增適當的驗證引數，例如 `-u <user>:<password>`.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. 透過命令列執行cURL命令並檢視回應。

   ![chlimage_1-70](assets/chlimage_1-70a.png)

## 常用操作AEM cURL命令 {#common-operational-aem-curl-commands}

以下是常見管理和操作任務的AEM cURL命令清單。

>[!NOTE]
>
>以下範例假設AEM執行於 `localhost` 在連線埠上 `4502` 和使用使用者 `admin` 使用密碼 `admin`. 額外的命令預留位置會設定在尖括弧中。

### 封裝管理 {#package-management}

#### 列出所有已安裝的套件

```shell
curl -u <user>:<password> http://<host>:<port>/crx/packmgr/service.jsp?cmd=ls
```

#### 建立套裝 {#create-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=create -d packageName=<name> -d groupName=<name>
```

#### 預覽套件 {#preview-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=preview
```

#### 列出封裝內容 {#list-package-content}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/console.html/etc/packages/mycontent.zip?cmd=contents
```

#### 建置套件 {#build-a-package}

```shell
curl -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=build
```

#### 將封裝折行 {#rewrap-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=rewrap
```

#### 重新命名套裝 {#rename-a-package}

```shell
curl -u <user>:<password> -X POST -Fname=<New Name> http://localhost:4502/etc/packages/<Group Name>/<Package Name>.zip/jcr:content/vlt:definition
```

#### 上傳套裝 {#upload-a-package}

```shell
curl -u <user>:<password> -F cmd=upload -F force=true -F package=@test.zip http://localhost:4502/crx/packmgr/service/.json
```

#### 安裝套裝 {#install-a-package}

```shell
curl -u <user>:<password> -F cmd=install http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### 解除安裝套裝 {#uninstall-a-package}

```shell
curl -u <user>:<password> -F cmd=uninstall http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### 刪除套裝 {#delete-a-package}

```shell
curl -u <user>:<password> -F cmd=delete http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### 下載套件 {#download-a-package}

```shell
curl -u <user>:<password> http://localhost:4502/etc/packages/my_packages/test.zip
```

#### 復寫封裝 {#replicate-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip?cmd=replicate
```

### 用户管理 {#user-management}

#### 建立新使用者 {#create-a-new-user}

```shell
curl -u <user>:<password> -FcreateUser= -FauthorizableId=hashim -Frep:password=hashim http://localhost:4502/libs/granite/security/post/authorizables
```

#### 建立新群組 {#create-a-new-group}

```shell
curl -u <user>:<password> -FcreateGroup=group1 -FauthorizableId=testGroup1 http://localhost:4502/libs/granite/security/post/authorizables
```

#### 將屬性新增至現有使用者 {#add-a-property-to-an-existing-user}

```shell
curl -u <user>:<password> -Fprofile/age=25 http://localhost:4502/home/users/h/hashim.rw.html
```

#### 使用設定檔建立使用者 {#create-a-user-with-a-profile}

```shell
curl -u <user>:<password> -FcreateUser=testuser -FauthorizableId=hashimkhan -Frep:password=hashimkhan -Fprofile/gender=male http://localhost:4502/libs/granite/security/post/authorizables
```

#### 建立新使用者作為群組成員 {#create-a-new-user-as-a-member-of-a-group}

```shell
curl -u <user>:<password> -FcreateUser=testuser -FauthorizableId=testuser -Frep:password=abc123 -Fmembership=contributor http://localhost:4502/libs/granite/security/post/authorizables
```

#### 新增使用者至群組 {#add-a-user-to-a-group}

```shell
curl -u <user>:<password> -FaddMembers=testuser1 http://localhost:4502/home/groups/t/testGroup.rw.html
```

#### 從群組移除使用者 {#remove-a-user-from-a-group}

```shell
curl -u <user>:<password> -FremoveMembers=testuser1 http://localhost:4502/home/groups/t/testGroup.rw.html
```

#### 設定使用者的群組成員資格 {#set-a-user-s-group-membership}

```shell
curl -u <user>:<password> -Fmembership=contributor -Fmembership=testgroup http://localhost:4502/home/users/t/testuser.rw.html
```

#### 刪除使用者 {#delete-a-user}

```shell
curl -u <user>:<password> -FdeleteAuthorizable= http://localhost:4502/home/users/t/testuser
```

#### 刪除群組 {#delete-a-group}

```shell
curl -u <user>:<password> -FdeleteAuthorizable= http://localhost:4502/home/groups/t/testGroup
```

### 备份 {#backup}

另請參閱 [備份與還原](/help/sites-administering/backup-and-restore.md#automating-aem-online-backup) 以取得詳細資訊。

### osgi {#osgi}

#### 啟動套件組合 {#starting-a-bundle}

```shell
curl -u <user>:<password> -Faction=start http://localhost:4502/system/console/bundles/<bundle-name>
```

#### 停止套件組合 {#stopping-a-bundle}

```shell
curl -u <user>:<password> -Faction=stop http://localhost:4502/system/console/bundles/<bundle-name>
```

### Dispatcher {#dispatcher}

#### 使快取失效 {#invalidate-the-cache}

```shell
curl -H "CQ-Action: Activate" -H "CQ-Handle: /content/test-site/" -H "CQ-Path: /content/test-site/" -H "Content-Length: 0" -H "Content-Type: application/octet-stream" http://localhost:4502/dispatcher/invalidate.cache
```

#### 收回快取 {#evict-the-cache}

```shell
curl -H "CQ-Action: Deactivate" -H "CQ-Handle: /content/test-site/" -H "CQ-Path: /content/test-site/" -H "Content-Length: 0" -H "Content-Type: application/octet-stream" http://localhost:4502/dispatcher/invalidate.cache
```

### 复制代理 {#replication-agent}

#### 檢查代理程式的狀態 {#check-the-status-of-an-agent}

```shell
curl -u <user>:<password> "http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json?agent=publish"
http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json?agent=publish
```

#### 刪除代理程式 {#delete-an-agent}

```shell
curl -X DELETE http://localhost:4502/etc/replication/agents.author/replication99 -u <user>:<password>
```

#### 建立代理程式 {#create-an-agent}

```shell
curl -u <user>:<password> -F "jcr:primaryType=cq:Page" -F "jcr:content/jcr:title=new-replication" -F "jcr:content/sling:resourceType=/libs/cq/replication/components/agent" -F "jcr:content/template=/libs/cq/replication/templates/agent" -F "jcr:content/transportUri=http://localhost:4503/bin/receive?sling:authRequestLogin=1" -F "jcr:content/transportUser=admin" -F "jcr:content/transportPassword={DES}8aadb625ced91ac483390ebc10640cdf"http://localhost:4502/etc/replication/agents.author/replication99
```

#### 暫停代理程式 {#pause-an-agent}

```shell
curl -u <user>:<password> -F "cmd=pause" -F "name=publish"  http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json
```

#### 清除代理程式佇列 {#clear-an-agent-queue}

```shell
curl -u <user>:<password> -F "cmd=clear" -F "name=publish"  http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json
```

### 社区 {#communities}

#### 指派和撤銷徽章 {#assign-and-revoke-badges}

另請參閱 [社群評分和預算](/help/communities/implementing-scoring.md#assign-and-revoke-badges) 以取得詳細資訊。

另請參閱 [評分和徽章要點](/help/communities/configure-scoring.md#example-setup) 以取得詳細資訊。

#### MSRP重新索引 {#msrp-reindexing}

另請參閱 [MSRP - MongoDB儲存資源提供者](/help/communities/msrp.md#running-msrp-reindex-tool-using-curl-command) 以取得詳細資訊。

### 安全性 {#security}

#### 啟用和停用CRX DE Lite {#enabling-and-disabling-crx-de-lite}

另請參閱 [在AEM中啟用CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md) 以取得詳細資訊。

### 数据存储垃圾收集 {#data-store-garbage-collection}

另請參閱 [資料存放區垃圾收集](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection) 以取得詳細資訊。

### Analytics與Target整合 {#analytics-and-target-integration}

另請參閱 [選擇使用Adobe Analytics和Adobe Target](/help/sites-administering/opt-in.md#configuring-the-setup-and-provisioning-via-script) 以取得詳細資訊。

### 單一登入 {#single-sign-on}

#### 傳送測試標題 {#send-test-header}

另請參閱 [單一登入](/help/sites-deploying/single-sign-on.md) 以取得詳細資訊。

## 常見的Content Manipulation AEM cURL命令 {#common-content-manipulation-aem-curl-commands}

以下是內容操控的AEM cURL命令清單。

>[!NOTE]
>
>以下範例假設AEM執行於 `localhost` 在連線埠上 `4502` 和使用使用者 `admin` 使用密碼 `admin`. 額外的命令預留位置會設定在尖括弧中。

### 頁面管理 {#page-management}

#### 頁面啟用 {#page-activation}

```shell
curl -u <user>:<password> -X POST -F path="/content/path/to/page" -F cmd="activate" http://localhost:4502/bin/replicate.json
```

#### 頁面停用 {#page-deactivation}

```shell
curl -u <user>:<password> -X POST -F path="/content/path/to/page" -F cmd="deactivate" http://localhost:4502/bin/replicate.json
```

#### 樹啟動 {#tree-activation}

```shell
curl -u <user>:<password> -F cmd=activate -F ignoredeactivated=true -F onlymodified=true -F path=/content/geometrixx http://localhost:4502/etc/replication/treeactivation.html
```

#### 锁定页面 {#lock-page}

```shell
curl -u <user>:<password> -X POST -F cmd="lockPage" -F path="/content/path/to/page" -F "_charset_"="utf-8" http://localhost:4502/bin/wcmcommand
```

#### 解锁页面 {#unlock-page}

```shell
curl -u <user>:<password> -X POST -F cmd="unlockPage" -F path="/content/path/to/page" -F "_charset_"="utf-8" http://localhost:4502/bin/wcmcommand
```

#### 复制页面 {#copy-page}

```shell
curl -u <user>:<password> -F cmd=copyPage -F destParentPath=/path/to/destination/parent -F srcPath=/path/to/source/location http://localhost:4502/bin/wcmcommand
```

### 工作流 {#workflows}

另請參閱 [以程式設計方式與工作流程互動](/help/sites-developing/workflows-program-interaction.md) 以取得詳細資訊。

### Sling內容 {#sling-content}

#### 建立資料夾 {#create-a-folder}

```shell
curl -u <user>:<password> -F jcr:primaryType=sling:Folder http://localhost:4502/etc/test
```

#### 刪除節點 {#delete-a-node}

```shell
curl -u <user>:<password> -F :operation=delete http://localhost:4502/etc/test/test.properties
```

#### 移動節點 {#move-a-node}

```shell
curl -u <user>:<password> -F":operation=move" -F":applyTo=/sourceurl"  -F":dest=/target/parenturl/" https://localhost:4502/content
```

#### 複製節點 {#copy-a-node}

```shell
curl -u <user>:<password> -F":operation=copy" -F":applyTo=/sourceurl"  -F":dest=/target/parenturl/" https://localhost:4502/content
```

#### 使用Sling PostServlet上傳檔案 {#upload-files-using-sling-postservlet}

```shell
curl -u <user>:<password> -F"*=@test.properties"  http://localhost:4502/etc/test
```

#### 使用Sling PostServlet並指定節點名稱上傳檔案 {#upload-files-using-sling-postservlet-and-specifying-node-name}

```shell
curl -u <user>:<password> -F"test2.properties=@test.properties"  http://localhost:4502/etc/test
```

#### 上載指定內容型別的檔案 {#upload-files-specifying-a-content-type}

```shell
curl -u <user>:<password> -F "*=@test.properties;type=text/plain" http://localhost:4502/etc/test
```

### 資產操控 {#asset-manipulation}

另請參閱 [Assets HTTP API](/help/assets/mac-api-assets.md) 以取得詳細資訊。
