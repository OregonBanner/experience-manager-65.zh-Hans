---
title: 停用適用於JEE和OSGI之PDFG設定的UAC
description: 針對PDFG設定停用UAC的步驟
exl-id: 785b7bb4-7158-45ea-a1e5-eebf3dc3ebc3
source-git-commit: 2e9b9c40f54aa54a946e4320341ed4a760c56fd1
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 3%

---

# 無法在Windows Server上將Word或Excel檔案轉換為PDF {#unable-to-convert-word-excel-files-PDF}

## 问题 {#issue}

當使用者嘗試在Microsoft Windows Server上將Word或Excel檔案轉換為PDF時，會遇到以下錯誤：

*來自主要轉換器的錯誤訊息：ALC-PDG-015-003 — 系統無法開啟輸入檔案。 請再次提交您的檔案或連絡您的系統管理員。*


## 解决方案 {#solution}

執行以下步驟以解決問題：
1. 若要存取系統組態公用程式，請前往 **[!UICONTROL 開始>執行]** 然後輸入 **[!UICONTROL MSCONFIG]**.
1. 按一下 **[!UICONTROL 工具]** Tab鍵並向下捲動並選取 **[!UICONTROL 變更UAC設定]**. 按一下 **[!UICONTROL Launch]** 在新視窗中執行指令。
1. 將滑桿調整至永不通知層級。 完成後，關閉命令視窗並關閉「系統組態」視窗。
1. 確認UAC的登入設定設為0 （零）。 執行以下步驟以進行驗證：

   1. Microsoft®建議您在修改登入之前先備份登入。 如需詳細步驟，請參閱 [如何在Windows中備份及還原登入](https://support.microsoft.com/en-us/help/322756).
   1. 開啟Microsoft® Windows登入編輯器。 若要開啟登入編輯程式，請前往「開始>執行」，輸入regedit，然後按一下「確定」。
   1. 导航到 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`。請確定EnableLUA的值設為0 （零）。
   1. 確保值 **EnableLUA** 設為0 （零）。 如果值不是0，請將值變更為0。 关闭注册表编辑器。

1. 重新啟動電腦。

## 套用至 {#appliesto}

此解決方案適用於下列專案：
* JEE伺服器上的AEM Forms
* OSGi伺服器上的AEM Forms
