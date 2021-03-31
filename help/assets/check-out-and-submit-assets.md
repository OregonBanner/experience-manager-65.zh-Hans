---
title: 在 [!DNL Assets]中签入和签出文件
description: 了解如何签出要编辑的资产，并在更改完成后重新签入。
contentOwner: AG
role: 商务从业人员
feature: 资产管理
translation-type: tm+mt
source-git-commit: ad0672c345262712e51e821fa4e050b505063ac4
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---


# [!DNL Experience Manager] DAM {#check-in-and-check-out-files-in-assets}中的签入和签出文件

[!DNL Adobe Experience Manager Assets] 允许您签出要编辑的资产，并在完成更改后重新签入。注销资产后，只有您才能编辑、批注、发布、移动或删除资产。 签出资产会锁定资产。 在您将资产签回[!DNL Assets]之前，其他用户无法对资产执行任何这些操作。 但是，他们仍然可以更改锁定资产的元数据。

要能够签出/登录资产，您需要对资产具有写权限。

此功能有助于防止其他用户覆盖作者所做的更改，在作者中，多个用户跨团队协作编辑工作流。

## 签出资产{#checking-out-assets}

1. 从[!DNL Assets]用户界面中，选择要签出的资产。 您还可以选择要签出的多个资产。
1. 在工具栏中，单击&#x200B;**[!UICONTROL 结帐]**。 **[!UICONTROL Checkout]**&#x200B;选项切换为&#x200B;**[!UICONTROL Checkin]**。
要验证其他用户是否可以编辑您注销的资产，请以其他用户身份登录。 您签出的资产的缩略图上会显示锁定符号。

   ![chlimage_1-471](assets/chlimage_1-471.png)

   选择资产。 请注意，工具栏不会显示任何允许您编辑、注释、发布或删除资产的选项。

   ![chlimage_1-472](assets/chlimage_1-472.png)

   要编辑锁定资产的元数据，请单击&#x200B;**[!UICONTROL 视图属性]**。

1. 单击&#x200B;**[!UICONTROL 编辑]**&#x200B;以在编辑模式下打开资产。

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. 编辑资产并保存更改。 例如，裁剪图像并保存。

   ![chlimage_1-474](assets/chlimage_1-474.png)

   您还可以选择对资产添加注释或发布。

1. 从[!DNL Assets]界面中选择已编辑的资产，然后单击工具栏中的&#x200B;**[!UICONTROL 签入]**。 已修改的资产已签入[!DNL Assets]，可供其他用户编辑。

## 强制签入{#forced-check-in}

管理员可以签入其他用户签出的资产。

1. 以管理员身份登录到[!DNL Assets]。
1. 从[!DNL Assets]用户界面中，选择已被其他用户签出的一个或多个资产。

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. 在工具栏中，单击&#x200B;**[!UICONTROL 释放锁]**。 资产会签回并可供其他用户编辑。

## 最佳实践和限制{#tips-limitations}

* 可以删除包含已签出资源文件的&#x200B;*文件夹*。 在删除文件夹之前，请确保用户未签出任何数字资产。

>[!MORELIKETHIS]
>
>* [了解登记和注销Indesktop应 [!DNL Experience Manager] 用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=en#how-app-works2)
>* [了解签入和签出的视频教程 [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html)

