---
title: 登记和注销数字资产以进行编辑
description: 了解如何在更改完成后注销要编辑的资产并重新登记。
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# AEM DAM中的登记和注销文件 {#check-in-and-check-out-files-in-assets}

Adobe Experience Manager(AEM)资产可让您签出资产进行编辑，并在完成更改后将其签回。 注销资产后，只有您才能编辑、批注、发布、移动或删除资产。 注销资产会锁定资产。 在您将资产签回AEM资产之前，其他用户无法对资产执行任何这些操作。 但是，他们仍然可以更改锁定资产的元数据。

要能够注销／登录资产，您需要对资产具有写入权限。

此功能有助于防止其他用户覆盖作者所做的更改，在创作中，多个用户跨团队协作编辑工作流。

## 注销资产 {#checking-out-assets}

1. 从资产UI中，选择要注销的资产。 您还可以选择多个资产以注销。
1. 在工具栏中，单击 **[!UICONTROL 结帐]**。
“检 **[!UICONTROL 出]** ”(Checkout **[!UICONTROL )选项切换]**为“检入”(Checkin)。
要验证其他用户是否可以编辑您注销的资产，请以其他用户身份登录。 注销的资产的缩略图上会显示锁定符号。

   ![chlimage_1-471](assets/chlimage_1-471.png)

   选择资产。 请注意，工具栏不显示任何允许您编辑、注释、发布或删除资产的选项。

   ![chlimage_1-472](assets/chlimage_1-472.png)

   您可以单击 **[!UICONTROL 视图属性]** ，以编辑锁定资产的元数据。

1. 单击 **[!UICONTROL 编辑]** ，以在编辑模式下打开资产。

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. 编辑资产并保存更改。 例如，裁剪图像并保存。

   ![chlimage_1-474](assets/chlimage_1-474.png)

   您还可以选择对资产添加注释或发布资产。

1. 从界面中选择已编辑的资 [!DNL Assets] 产，然后单击工 **[!UICONTROL 具栏中的]** “签入”。 修改后的资产会登记到AEM资产，可供其他用户编辑。

## 强制登记 {#forced-check-in}

管理员可以登记其他用户注销的资产。

1. 以管理员身份登录到AEM资产。
1. 从资产UI中，选择一个或多个已由其他用户注销的资产。

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. 在工具栏中，单击释 **[!UICONTROL 放锁定]**。 资产将重新登记，可供其他用户编辑。

>[!MORELIKETHIS]
>
>* [了解AEM桌面应用程序中的登记和注销](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#how-app-works2)
>* [了解AEM资产中登记和注销的视频教程](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/collaboration/checkin-checkout-technical-video-understand.html)

