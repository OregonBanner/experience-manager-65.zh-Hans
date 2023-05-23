---
title: 與Adobe Target整合的必要條件
seo-title: Prerequisites for Integrating with Adobe Target
description: 瞭解與Adobe Target整合的先決條件。
seo-description: Find out about the prerequisites for integrating with Adobe Target.
uuid: 55d87a96-5fe7-4f7e-93c1-fdf7fbb7c971
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: ae4a6e97-c0d7-472d-a25f-b89b1abf4df3
docset: aem65
exl-id: 30813c44-51ac-4e6e-8ee6-4e8baacb1ff9
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 7%

---

# 與Adobe Target整合的必要條件{#prerequisites-for-integrating-with-adobe-target}

作為 [AEM與Adobe Target的整合](/help/sites-administering/target.md)，您必須向Adobe Target註冊、設定復寫代理程式，並在發佈節點上保護活動設定。

## 向Adobe Target註冊 {#registering-with-adobe-target}

若要將AEM與Adobe Target整合，您必須具備有效的Adobe Target帳戶。 此帳戶必須具有 **核准者** 至少需要層級許可權。 註冊Adobe Target時，您會收到使用者端代碼。 您需要使用者端代碼以及Adobe Target登入名稱和密碼，才能將AEM連線至Adobe Target。

使用者端代碼會在呼叫Adobe Target伺服器時識別Adobe Target客戶帳戶。

>[!NOTE]
>
>您的帳戶也必須由Target團隊啟用，才能使用整合。
>
>如果不是這種情況，請聯絡 [Adobe客戶服務](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html).

## 啟用目標復寫代理 {#enabling-the-target-replication-agent}

測試和目標 [復寫代理](/help/sites-deploying/replication.md) 必須在作者執行個體上啟用。 請注意，如果您使用 [nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) 執行模式以安裝AEM。 如需保護生產環境的詳細資訊，請參閱 [安全性檢查清單](/help/sites-administering/security-checklist.md).

1. 在AEM首頁上，按一下或點選 **工具** > **部署** > **復寫**.
1. 按一下或點選 **作者上的代理**.
1. 按一下或點選 **Test and Target (test and target)** 復寫代理程式，然後按一下或點選 **編輯**.
1. 選取「已啟用」選項，然後按一下或點選 **確定**.

   >[!NOTE]
   >
   >當您設定Test and Target復寫代理程式時，請在 **傳輸** 索引標籤中，URI預設會設定為 **tnt:///**. 請勿將此URI取代為 **https://admin.testandtarget.omniture.com**.
   >
   >請注意，如果您嘗試透過測試連線 **tnt:///**，會擲回錯誤。 這是預期行為，因為此URI僅供內部使用，不應與搭配使用 **測試連線**.

## 保護活動設定節點 {#securing-the-activity-settings-node}

您必须确保发布实例中的活动设置节点 **cq:ActivitySettings** 安全，以使其不可由普通用户访问。该活动设置节点应当只能由负责将活动同步到 Adobe Target 的服务访问。

此 **cq：ActivitySettings** 節點可在CRXDE lite中使用，位於 `/content/campaigns/*nameofbrand*`* *在活動jcr：content節點下；* *例如 `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`. 此節點僅在您鎖定元件目標後建立。

此 **cq：ActivitySettings** 活動jcr：content下的節點受以下ACL保護：

* 拒絕所有人的所有
* 允許「target-activity-authors」的jcr：read，rep：write （author是此群組的成員）
* 允許「targetservice」的jcr：read，rep：write

這些設定可確保一般使用者無權存取節點屬性。 在製作和發佈上使用相同的ACL。 另請參閱 [使用者管理與安全性](/help/sites-administering/security.md) 以取得詳細資訊。

## 設定AEM連結外部化器 {#configuring-the-aem-link-externalizer}

在Adobe Target中編輯活動時，URL會指向 **localhost** 除非您變更AEM作者節點上的URL。 如果您希望匯出的內容指向特定的，可以設定AEM Link Externalizer *發佈* 網域。

>[!NOTE]
>
>另請參閱 [新增雲端設定](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration).

若要設定AEM外部化程式：

>[!NOTE]
>
>如需詳細資訊，請參閱 [將URL外部化](/help/sites-developing/externalizer.md).

1. 導覽至OSGi Web主控台，網址為 **https://&lt;server>：&lt;port>/system/console/configMgr。**
1. 尋找 **Day CQ連結外部化器** 並輸入作者節點的網域。

   ![chlimage_1-120](assets/aem-externalizer-01.png)
