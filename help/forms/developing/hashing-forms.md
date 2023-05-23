---
title: 如何在動態PDF forms中產生及使用雜湊？
description: 在動態PDF forms中產生及使用雜湊
exl-id: 026f5686-39ea-4798-9d1f-031f15941060
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 0%

---

# 在動態PDF forms中產生及使用雜湊 {#generate-work-with-hashes-dynamic-pdf-forms}


## 必備條件知識 {#prerequisite-knowledge}

您需要在JEE Designer上使用AEM Forms的一些體驗，以及存取和呼叫指令碼物件中函式的能力。

## 使用者層級 {#user-level}

開始

如果您想要在PDF表單中隱藏密碼，並且不想在原始程式碼中或PDF檔案中的其他任何位置以純文字顯示，瞭解如何產生和使用MD4、MD5、SHA-1和SHA-256雜湊是關鍵。

其想法是產生唯一的雜湊並將此雜湊儲存在PDF檔案中，以模糊化密碼。 這個唯一的雜湊可以由不同的雜湊函式產生，在本文中，我將說明如何在PDF表單內產生雜湊以及如何使用雜湊。

雜湊函式會以任何長度的長字串（或訊息）作為輸入，並產生固定長度的字串作為輸出，有時稱為訊息摘要或數位指紋。

JEE Designer上的AEM Forms可讓您在指令碼物件中以JavaScript實施不同的雜湊函式，並在動態PDF檔案中執行這些函式。 本文範例檔案包含的範例PDF會使用下列雜湊函式的開放原始碼實作：

* MD4和MD5 — 由Ronald Rivest設計

* SHA-1和SHA-256 — 由NIST定義

使用雜湊的最大優點，是您不需要透過比較純文字字串來直接比較密碼；而是可以比較兩個密碼的兩種雜湊。 由於兩個不同的字串不太可能有相同的雜湊，因此如果兩個雜湊都相同，您可以假設比較的字串（在此例中是密碼）也相同。

>[!NOTE]
>
>MD4或MD5有一些眾所周知的安全性問題（稱為雜湊碰撞）。 由於這些雜湊碰撞和其他SHA-1雜湊（包括彩虹表格），我決定集中在第二個範例的SHA-256雜湊函式上。  如需詳細資訊，請參閱 [衝突](https://en.wikipedia.org/wiki/Hash_collision) 和 [彩虹表](https://en.wikipedia.org/wiki/Rainbow_table) 來自Wikipedia的頁面。

## 檢查指令碼物件 {#examining-script-objects}

當您在JEE設計工具的AEM Forms中開啟兩個提供的範例之一時，您會在「階層」浮動視窗中找到四個指令碼物件（請參閱下圖）。

![变量](assets/variables.jpg)

若要檢視這些指令碼物件中雜湊函式的JavaScript實作，請選取指令碼物件，並在指令碼編輯器中探索程式碼。  您可以檢視下列各個雜湊函式的實作方式：

* soHASHING_MD4.hex_md4()
* soHASHING_MD4.b64_md4()
* soHASHING_MD4.str_md4()
* soHASHING_MD5.hex_md5()
* soHASHING_MD5.b64_md5()
* soHASHING_MD5.str_md5()
* soHASHING_SHA1.hex_sha1()
* soHASHING_SHA1.b64_sha1( )
* soHASHING_SHA1.str_sha1( )
* soHASHING_SHA256.hex_sha256()
* soHASHING_SHA256.b64_sha256()
* soHASHING_SHA256.str_sha256()

從這個清單中可以看到，不同的雜湊輸出型別有不同的可用函式。 您可以選擇 `hex_` 對於十六進位數字， `b64_` Base64編碼輸出，或 `str_` 用於簡單字串編碼。

根據您選擇的雜湊函式，雜湊長度會有所不同：

* MD4:128位元
* MD5:128位元
* SHA-1： 160位元
* SHA-256： 256位元

## 正在嘗試範例PDF forms {#try-sample-pdf-forms}

本文範例檔案包含兩個PDF forms。 第一個範例可讓您輸入字串，然後產生字串的MD4、MD5、SHA-1和SHA-256雜湊值。  第二個範例是簡單的表單，如果輸入正確的密碼，它會解除鎖定文字欄位。

### 範例1：產生雜湊 {#generating-dashes}

請依照下列步驟嘗試第一個範例：

1. 下載並解壓縮範例檔案後，在JEE Designer上使用AEM Forms開啟hashing_forms_sample1.pdf。 或者，您可以使用Adobe Reader或Adobe Acrobat Professional來開啟和檢視範例，但將無法看到原始程式碼。
1. 在標示為的文字欄位中 [!UICONTROL 清除文字] 輸入密碼或任何其他要雜湊處理的訊息。
1. 按一下四個按鈕之一，產生MD4、MD5、SHA-1或SHA-256雜湊。 根據您按下的按鈕，會產生十六進位輸出的四個雜湊函式之一會被呼叫，而您的字串或訊息會經過雜湊處理。

雜湊作業的結果會顯示在標示為的欄位中 [!UICONTROL 雜湊]. 雜湊的長度會依您選擇的雜湊函式而有所不同。

所有範例都使用十六進位數字作為輸出型別。 您可以使用指令碼編輯器來修改範例，並將輸出型別變更為Base64或簡單字串。

### 範例2：相符的密碼 {#matching-passwords}

第二個範例示範如何在背景比較雜湊，而不需要揭露真正的密碼。 您輸入的密碼會經過雜湊處理。 實際密碼（儲存在隱藏的欄位中）也會經過雜湊處理。 密碼安全並非因為不可見，而是因為經過雜湊處理。 因為無法從雜湊值重新建構密碼，所以以雜湊形式公開密碼是安全的。 比較只會在雜湊之間進行，而不會在純文字的密碼之間進行。 如果兩個雜湊相同，您可以假設密碼相同。

請依照下列步驟，嘗試第二個範例：

1. 開啟 `hashing_forms_sample2.pdf` 與AEM Forms on JEE Designer搭配使用。 或者，您可以使用Adobe Reader或Adobe Acrobat Professional來開啟和檢視範例，但將無法看到原始程式碼。
1. 選擇兩個標示為的密碼欄位之一 [!UICONTROL 密碼手冊] 或 [!UICONTROL 密碼女人] 並輸入密碼：
   1. 此人的密碼為 `bob`
   1. 該女人的密碼為 `alice`
1. 當您將焦點移出密碼欄位或按下Enter鍵時，系統會自動產生您輸入的密碼雜湊，並與背景中儲存的正確密碼雜湊進行比較。 正確的雜湊密碼會儲存在標示為的隱藏文字欄位中 `passwd_man_hashed` 和 `passwd_woman_hashed`. 如果您為使用者輸入正確的密碼，則標示為的文字欄位 `Man 1` 和 `Man 2` 設為可存取，以便您在其中輸入文字。 女性的欄位也存在相同行為。
1. 或者，您可以按一下標示為「刪除密碼」的按鈕，以停用文字欄位並變更其邊框。

比較這兩個雜湊值並啟用文字欄位的程式碼很簡單：

```xml
if (soHASHING_SHA256.hex_sha256(this.rawValue) == passwd_man_hashed.rawValue){
     VAL_man_1.access = "open";
     VAL_man_2.access = "open";
     VAL_man_1.borderColor = "0,255,0";
     VAL_man_2.borderColor = "0,255,0";
}
```

## 從這裡前往何處 {#next-steps}

您哪裡需要這樣的資訊？ 假設有一個PDF表單，其中包含只有授權個人才能填寫的欄位。 透過使用密碼保護這些欄位（在檔案中任何位置都看不到明文，例如Sample_2.pdf），您可以確保這些欄位只有知道密碼的使用者才能存取。

我鼓勵您繼續探索這兩個範例PDF檔案。  您可以使用Sample_1.pdf產生新的雜湊值，並使用產生的值來變更Sample_2.pdf中使用的密碼或雜湊函式。  「歸因」區段中列出的資源也會提供雜湊和本文中所使用的特定JavaScript實作的其他資訊。

## 歸因 {#attributions}

* [Ronald Rivest](https://en.wikipedia.org/wiki/Ron_Rivest)
* [NIST](https://csrc.nist.gov/projects/cryptographic-standards-and-guidelines)
* [雜湊碰撞](https://en.wikipedia.org/wiki/Hash_collision)
* [彩虹表](https://en.wikipedia.org/wiki/Rainbow_table)
* [javascript MD5專案首頁](https://pajhome.org.uk/crypt/md5/)
* [jssha2專案首頁](https://anmar.eu.org/projects/jssha2/)
