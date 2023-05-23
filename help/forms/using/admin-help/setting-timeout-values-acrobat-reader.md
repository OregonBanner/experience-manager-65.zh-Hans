---
title: 設定與Acrobat Reader DC擴充功能搭配使用的逾時值
seo-title: Setting timeout values for use with Acrobat Reader DC extensions
description: 瞭解如何設定逾時值以與Acrobat Reader DC擴充功能搭配使用。
seo-description: Learn how to set timeout values for use with Acrobat Reader DC extensions.
uuid: d6d072a0-0a30-417a-98b1-df8b4ff8f911
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a9aeeb89-45e9-4d5d-aa25-8145c89b64f2
exl-id: 0a55aab3-14a3-41ad-8533-dc2cd116a848
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# 設定與Acrobat Reader DC擴充功能搭配使用的逾時值  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

使用Acrobat Reader DC擴充功能中的許多PDF檔案時，請確定已適當設定下列逾時值，以防止工作逾時及失敗：

**檔案處置逾時**

此值可在管理控制檯中設定。 按一下「設定」>「核心系統設定」>「設定」，並指定「預設檔案處置逾時」的值。

**使用者管理員AEM表單逾時：** 您可以編輯config.xml檔案來設定此值。 在管理控制檯中，按一下「設定」>「使用者管理」>「組態」>「匯入和匯出組態檔」，然後按一下「匯出」。 開啟匯出的config.xml檔案並編輯下列行：

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

儲存config.xml檔案，然後將其匯入回管理主控台。

**應用程式伺服器工作階段逾時：** 此值可在應用程式伺服器上設定。 如需詳細資訊，請參閱應用程式伺服器隨附的檔案。
