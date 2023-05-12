---
title: 签入和签出 [!DNL Assets]
description: 了解如何签出要编辑的资产，并在更改完成后重新签入它们。
contentOwner: AG
role: User
feature: Asset Management
exl-id: 544ef73c-4e4b-433f-a173-fdf1c8f45d8e
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 2%

---

# 中的签入和签出文件 [!DNL Experience Manager] DAM {#check-in-and-check-out-files-in-assets}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/check-out-and-submit-assets.html?lang=en) |
| AEM 6.5 | 本文 |

[!DNL Adobe Experience Manager Assets] 允许您签出要编辑的资产，并在完成更改后重新签入它们。 签出资产后，只有您才能编辑、注释、发布、移动或删除资产。 签出资产会锁定资产。 在您将资产签回到 [!DNL Assets]. 但是，他们仍可以更改锁定资产的元数据。

要签出/签入资产，您需要对资产具有写入权限。

此功能有助于防止其他用户覆盖作者所做的更改，在作者所做的更改中，多个用户会跨团队协作进行编辑工作流。

## 签出资产 {#checking-out-assets}

1. 从 [!DNL Assets] 用户界面中，选择要签出的资产。 您还可以选择多个要签出的资产。
1. 在工具栏中，单击 **[!UICONTROL 结帐]**. 的 **[!UICONTROL 结帐]** 选项切换 **[!UICONTROL 签入]**.
要验证其他用户是否可以编辑您签出的资产，请以其他用户身份登录。 锁符号显示在您签出的资产的缩略图上。

   ![chlimage_1-471](assets/chlimage_1-471.png)

   选择资产。 请注意，工具栏不显示任何选项，允许您编辑、注释、发布或删除资产。

   ![chlimage_1-472](assets/chlimage_1-472.png)

   要编辑锁定资产的元数据，请单击 **[!UICONTROL 查看属性]**.

1. 单击 **[!UICONTROL 编辑]** 以在编辑模式下打开资产。

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. 编辑资产并保存更改。 例如，裁剪图像并保存。

   ![chlimage_1-474](assets/chlimage_1-474.png)

   您还可以选择在资产中添加批注或发布资产。

1. 从 [!DNL Assets] 界面，然后单击 **[!UICONTROL 签入]** 中。 已修改的资产将签入到 [!DNL Assets] 和可供其他用户编辑。

## 强制签入 {#forced-check-in}

管理员可以签入其他用户签出的资产。

1. 登录到 [!DNL Assets] 作为管理员。
1. 从 [!DNL Assets] 用户界面选择已由其他用户签出的一个或多个资产。

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. 在工具栏中，单击 **[!UICONTROL 释放锁]**. 资产会签回，以供其他用户编辑。

## 最佳实践和限制 {#tips-limitations}

* 可以删除 *文件夹* 包含已签出的资产文件。 在删除文件夹之前，请确保用户未签出任何数字资产。

>[!MORELIKETHIS]
>
>* [了解签入和签出 [!DNL Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#how-app-works2)
>* [了解签入和签出的视频教程 [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html)

