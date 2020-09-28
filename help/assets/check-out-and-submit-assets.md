---
title: 签入和签出资产以进行编辑
description: 了解如何签出资产进行编辑，并在更改完成后将其签回。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---


# DAM中的登记和注销文 [!DNL Experience Manager] 件 {#check-in-and-check-out-files-in-assets}

[!DNL Adobe Experience Manager Assets] 允许您签出要编辑的资产，并在完成更改后重新将其签回。 注销资产后，只有您才能编辑、批注、发布、移动或删除资产。 签出资产会锁定资产。 在您将资产重新签入之前，其他用户无法对资产执行任何这些操作 [!DNL Assets]。 但是，他们仍可以更改锁定资产的元数据。

要能够签出／登录资产，您需要对资产具有写入权限。

此功能有助于防止其他用户覆盖作者所做的更改，在创作中，多个用户跨团队协作编辑工作流。

## 注销资产 {#checking-out-assets}

1. 从用 [!DNL Assets] 户界面中，选择要签出的资产。 您还可以选择多个资产进行注销。
1. 在工具栏中，单击 **[!UICONTROL 签出]**。
“检 **[!UICONTROL 出]** ”选项切换 **[!UICONTROL 为“检入]**”。
要验证其他用户是否可以编辑您注销的资产，请以其他用户身份登录。 签出的资产的缩略图上会显示锁定符号。

   ![chlimage_1-471](assets/chlimage_1-471.png)

   选择资产。 请注意，工具栏不会显示任何允许您编辑、批注、发布或删除资产的选项。

   ![chlimage_1-472](assets/chlimage_1-472.png)

   您可以单击 **[!UICONTROL 视图属性]** ，以编辑锁定资产的元数据。

1. 单击 **[!UICONTROL 编辑]** ，以在编辑模式下打开资产。

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. 编辑资产并保存更改。 例如，裁剪图像并保存。

   ![chlimage_1-474](assets/chlimage_1-474.png)

   您还可以选择对资产添加注释或发布。

1. 从界面中选择已编辑的 [!DNL Assets] 资产，然后单 **[!UICONTROL 击工]** 具栏中的签入。 修改后的资产已签入， [!DNL Assets] 可供其他用户编辑。

## 强制签入 {#forced-check-in}

管理员可以签入其他用户签出的资产。

1. 以管理员 [!DNL Assets] 身份登录。
1. 从用户 [!DNL Assets] 界面中，选择已由其他用户签出的一个或多个资产。

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. 在工具栏中，单击“ **[!UICONTROL 释放锁定]**”。 资产将签回，可供其他用户编辑。

## 最佳实践和限制 {#tips-limitations}

* 可以删除包含已签 *出的资* 源文件的文件夹。 删除文件夹之前，请确保用户未签出任何数字资产。

>[!MORELIKETHIS]
>
>* [了解Experience Manager桌面应用程序中的登记和注销](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#how-app-works2)
>* [了解资产登记和注销的视频教程](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/collaboration/checkin-checkout-technical-video-understand.html)

