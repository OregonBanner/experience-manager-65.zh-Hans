---
title: AEM Mobile- GDPR就绪性
seo-title: AEM Mobile- GDPR就绪性
description: 'null'
seo-description: 'null'
uuid: 817c434f-4b78-40f7-99d6-6efafdedb77e
contentOwner: trushton
discoiquuid: 9399dd3d-a485-4f53-a6f2-7b190da4235b
translation-type: tm+mt
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 1%

---


# AEM Mobile- GDPR就绪{#aem-mobile-gdpr-readiness}

>[!IMPORTANT]
>
>GDPR在以下各节中用作示例，但涵盖的详细信息适用于所有数据保护和隐私法规；例如GDPR、CCPA等。

## AEM MobileGDPR支持{#aem-mobile-gdpr-support}

AEM Mobile已准备好协助客户履行其GDPR合规义务。 AEM Mobile没有存储任何个人数据。 如果您已配置好，则可以使用您的Adobe ID登录Adobe Experience Mobile。

[https://aemmobile.adobe.com/signin/index.html](https://aemmobile.adobe.com/signin/index.html)

## Adobe Digital Publishing Suite {#adobe-digital-publishing-suite}

Adobe的数字出版产品(在AEM Mobile之前)支持Adobe的GDPR就绪性计划。 请参阅[https://www.adobe.com/privacy/general-data-protection-regulation.html](https://www.adobe.com/privacy/general-data-protection-regulation.html)。 以下将提供Digital Publishing Suite产品中有关支持GDPR相关功能的具体信息，包括如何与Adobe合作以发起GDPR请求。

为确保您不会将AEM Mobile与旧版Digital Publishing Suite产品混淆在一起，您可以在以下网址登录Digital Publishing Suite产品：

[https://digitalpublishing.acrobat.com/welcome.html](https://digitalpublishing.acrobat.com/welcome.html)

### 启动GDPR请求{#initiating-a-gdpr-request}

请联系Adobe客户关怀以发起Digital Publishing Suite的GDPR请求。

需要以下ID来查找客户数据。 收到的任何子集都表示其他ID不适用于此用户。

强制:

* 客户合同ID:*dpsc-contractId*

请至少提供以下1项：

* 最终用户的客户提供的OAuth ID（在客户的直接授权系统中使用的ID）:*dpsc-directEntitlementId*
* 对于Windows应用程序用户，最终用户的App Store ID:*dpsc-windowsAppStoreId*
* 最终用户与DPS应用程序交互时使用的电子邮件地址：*email*

### 常见问题解答(FAQ){#frequently-asked-questions-faq}

**Adobe是否会在启动DELETE请求时删除我的App Store购买？**

Adobe将删除其在App Store购买中包含的信息(订阅等) 但在App商店，购买仍将记录在案。 如果应用程序（最终用户）登录到App Store，则这些收据将再次被拾取并发送至Adobe，随后这些收据将被视为新购买，并由应用程序恢复以重新获得访问权。

**Adobe是否会在启动DELETE请求时删除客户提供的权利？**

Adobe将删除其拥有的客户额外直接权益津贴信息。 如果应用程序（最终用户）登录到客户使用的OAuth机制，它将向Adobe发送信息，服务将再次获取额外的权利。

**最终用户应该有哪些期望？**

由于将授权分配给应用程序的密钥作为查看器软件的一部分驻留在设备上，因此最终用户应卸载应用程序。 最终用户应意识到，如果他们重新安装App，则现有购买（与App Store用户关联）和直接授权许可（与客户的OAuth用户关联）仍将恢复。

**当应用程序在设备上的人员之间共享时会发生什么情况？**

Adobe几乎没有直接关联到特定用户的信息。 它使用随机创建的UUID关联数据，该UUID保存在应用程序的数据中，并在应用程序启动的每个请求中传递。 这意味着在同一设备上共享应用程序的最终用户将使用相同的UUID，且所有数据都将被认为是GDPR请求者所拥有。 对于访问和删除请求，DPSC将考虑将共享应用程序的人员视为一人。

**使用Analytics跟踪哪些个人数据？**

无. 正在跟踪数据，但数据位于应用程序级别（非个人）。 这包括启动项、崩溃、关闭、活动、购买或作品集叠加等事件。 不跟踪地理位置、名称、设备ID或IP地址。

**最终用户提供了其信息，但未找到任何信息。为什么不？**

随着Digital Publishing Suite产品的发展，服务实施发生了更改，更多数据被模糊化。 如果未使用用户提供的数据找到任何数据，则表示无法将用户数据跟踪回该人。

### 示例 {#example}

请联系Adobe客户服务部门以发起GDPR请求。

以下是Digital Publishing Suite GDPR请求的输入和结果输出的示例：

#### 输入：{#inputs}

```
dpsc-contractId = “12345-1234-12416234” 
directEntitlementId = “1234-1234-1234” 
windowsAppStoreId = “testWinAppStoreId” 
email = “test@what.com”
```

#### 输出{#outputs}

```
{

    "jobId": "test-1524750204384",

    "product": "DPSC",

    "action": "access",

    "userIDS": [

        {

        "namespace": "email",

        "value": "test@what.com"

        },

        {

        "namespace": "windowsAppStoreId",

        "value": "testWinAppStoreId"

        },

        {

        "namespace": "directEntitlementId",

        "value": "1234-1234-1234"

        }

    ],

    "receiptData": {

    "recordsFound": 6,

    "recordsAffected": 0,

    "tablesModified": 0,

    "subscriptionsFound": 24,

    "entitlementsFound": 24

    },

    "records": {

        "DPS_Stage_EntitlementUserDevices": [

        {

            "user_id": "testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "device_id": "appleStore:test1b16-f032-4d9c-9200-0d19999405c4",

            "account_id": "test@what.com"

        },

        {

            "user_id": "test967d-5179-4dc6-958c-facd9d94da38",

            "device_id": "appleStore:test3f07-d5aa-4b32-8fac-b2b690b7ccd7",

            "account_id": "test@what.com"

        },

        {

            "user_id": "test1838-6494-4e74-912c-1edf61581d0e",

            "device_id": "appleStore:test3813-f8cc-49ce-b021-50eb0814a3bb",

            "account_id": "1234-1234-1234"

        },

        {

            "user_id": "test5468-1a11-4e4c-be43-274181a9ef81",

            "device_id": "appleStore:testf082-2783-498d-ab62-b1b2e3eb67ae",

            "account_id": "1234-1234-1234"

        }

        ],

            "DPS_Stage_EntitlementUsers": [

        {

            "id": "store:test04a7-33a3-4b90-863d-79981ead0f19:appleStore",

            "part_id": "0",

            "alias_user_id": "testWinAppStoreId"

        },

        {

            "id": "internal:testd2da-0606-4444-87ef-0d5a1d4a121d:adobe",

            "part_id": "0",

            "user_id": "test@what.com"

        }

        ],

            "DPS_Stage_Subscriptions": [

        {

            "id": "appleStore:testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "account_id": "test3531-a209-4391-beb9-951c7822244e",

            "overflow": "test4e59-86a8-4b75-b699-77e980c287ab",

            "entitlement_count": "12"

        },

        {

            "id": "appleStore:test5468-1a11-4e4c-be43-274181a9ef81",

            "account_id": "test491b-379e-4d24-96ef-e481bf8d3062",

            "overflow": "test931b-7422-485d-85a5-134828187b6c",

            "entitlement_count": "12"

        }

        ],

            "DPS_Stage_Entitlements": [

        {

            "id": "samsungStore:testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "account_id": "test7332-60a0-42b8-a508-474668d83d2e",

            "overflow": "test9bc3-94d0-43cf-b132-0629868f7d9d",

            "entitlement_count": "12"

        },

        {

            "id": "appleStore:test5468-1a11-4e4c-be43-274181a9ef81",

            "account_id": "testf766-102a-460d-8f5a-42f7bb9d68b7",

            "overflow": "test4d96-2197-45a8-9caf-2aa2846b770c",

            "entitlement_count": "12"

        }

        ],

            "s3Buckets": {

            "name": "DPS-Entitlements-Overflow",

            "folder": "stage/",

            "overflows": {

            "subscriptions": [

            "test4e59-86a8-4b75-b699-77e980c287ab",

            "test931b-7422-485d-85a5-134828187b6c"

        ],

            "entitlements": [

            "test9bc3-94d0-43cf-b132-0629868f7d9d",

            "test4d96-2197-45a8-9caf-2aa2846b770c"

                ]

            }

        }

    }

}
```

