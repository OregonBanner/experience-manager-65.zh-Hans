---
title: 如何在动态PDF forms中生成和使用哈希？
description: 在动态PDF forms中生成和使用哈希。
exl-id: 026f5686-39ea-4798-9d1f-031f15941060
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 0%

---

# 在动态PDF forms中生成和使用哈希 {#generate-work-with-hashes-dynamic-pdf-forms}

## 必备知识 {#prerequisite-knowledge}

您需要在JEE Designer上获得AEM Forms的某些使用体验，以及访问和调用脚本对象中的函数的功能。

## 用户级别 {#user-level}

开始

如果您希望在PDF表单中隐藏口令，并且不希望该口令以明文形式显示在源代码中或PDF文档的任何位置，了解如何生成并使用MD4、MD5、SHA-1和SHA-256哈希是关键。

其思想是通过生成唯一的哈希并将此哈希存储在PDF文档中来模糊密码。 此唯一哈希可以由不同的哈希函数生成，在本文中，将向您展示如何在PDF表单中生成哈希以及如何使用它们。

哈希函数将任意长度的长字符串（或消息）作为输入，并生成固定长度的字符串作为输出，有时称为消息摘要或数字指纹。

通过JEE Designer上的AEM Forms，您可以在脚本对象中作为JavaScript实施各种哈希函数，并在动态PDF文档中运行这些函数。 本文示例文件包含的示例PDF使用以下散列函数的开源实现：

* MD4和MD5 — 由Ronald Rivest设计

* SHA-1和SHA-256 — 由NIST定义

使用哈希的最大好处是，您不必通过比较明文字符串来直接比较密码；相反，您可以比较两个密码中的两个哈希。 由于两个不同的字符串不太可能具有相同的哈希，因此如果两个哈希相同，则可以假定比较的字符串（在本例中是密码）也相同。

>[!NOTE]
>
>MD4或MD5存在一些已知的安全问题（称为哈希冲突）。 由于这些散列碰撞和其他SHA-1攻击（包括彩虹表），我决定集中研究第二个样本中的SHA-256散列函数。 欲了解更多信息，请参见 [冲突](https://en.wikipedia.org/wiki/Hash_collision) 和 [彩虹表](https://en.wikipedia.org/wiki/Rainbow_table) 维基百科的页面。

## 检查脚本对象 {#examining-script-objects}

在JEE设计器的AEM Forms中打开两个提供的示例之一时，您可以在层级组件面板中找到四个脚本对象（请参阅下图）。

![变量](assets/variables.jpg)

要查看这些脚本对象中散列函数的JavaScript实现，请选择脚本对象并在脚本编辑器中浏览代码。 您可以看到以下每个哈希函数的实现方式：

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

正如您从该列表中看到的，对于散列的不同输出类型，有不同的函数可用。 您可以选择 `hex_` 对于十六进制数字， `b64_` 对于Base64编码输出，或者 `str_` 用于简单字符串编码。

根据您选择的哈希函数，哈希的长度会有所不同：

* MD4:128位
* MD5:128位
* SHA-1:160位
* SHA-256:256位

## 尝试示例PDF forms {#try-sample-pdf-forms}

本文中的示例文件包括两个PDF forms。 第一个示例允许您键入字符串，然后为该字符串生成MD4、MD5、SHA-1和SHA-256哈希值。 第二个示例是一个简单表单，如果输入了正确的密码，该表单会解锁文本字段。

### 示例1：生成哈希 {#generating-dashes}

请按照以下步骤尝试第一个示例：

1. 下载并解压缩示例文件后，在JEE Designer中使用AEM Forms打开hashing_forms_sample1.pdf。 或者，您可以使用Adobe Reader或Adobe Acrobat Professional打开并查看示例，但将无法看到源代码。
1. 在标记为的文本字段中 [!UICONTROL 清文本] 键入要经过哈希处理的密码或任何其他消息。
1. 单击四个按钮之一以生成MD4、MD5、SHA-1或SHA-256哈希值。 根据您按下的按钮，将调用生成十六进制输出的四个哈希函数之一，并对字符串或消息进行哈希处理。

哈希操作的结果显示在标记为的字段中 [!UICONTROL 哈希]. 哈希长度因您选择的哈希函数而异。

所有示例都使用十六进制数字作为输出类型。 您可以使用脚本编辑器修改示例，并将输出类型更改为Base64或简单字符串。

### 示例2：匹配密码 {#matching-passwords}

第二个示例演示了如何在后台比较哈希，而不必公开真正的密码。 您输入的密码将经过哈希处理。 真正的密码（存储在不可见的字段中）也经过哈希处理。 密码安全不是因为它不可见，而是因为它经过哈希处理。 由于不可能从散列值重构密码，因此以散列形式公开密码是安全的。 只对散列进行比较，而不是对明文格式的密码进行比较。 如果两个哈希相同，则可以假定密码相同。

请按照以下步骤尝试第二个示例：

1. 打开 `hashing_forms_sample2.pdf` AEM Forms的JEE设计器。 或者，您可以使用Adobe Reader或Adobe Acrobat Professional打开并查看示例，但将无法看到源代码。
1. 选择两个口令字段之一，标签为 [!UICONTROL 密码手册] 或 [!UICONTROL 密码女性] 并键入密码：
   1. 此人的密码为 `bob`
   1. 女人的密码是 `alice`
1. 当您将焦点移出密码字段或按Enter键时，系统会自动生成您输入的密码散列，并与后台存储的正确密码散列进行比较。 正确的散列密码存储在标记为的不可见文本字段中 `passwd_man_hashed` 和 `passwd_woman_hashed`. 如果键入该人的正确密码，则文本字段中标有 `Man 1` 和 `Man 2` 设置为可访问，以便您能够在其中键入文本。 同样的行为也适用于妇女的田地。
1. 或者，您可以单击标记为“删除密码”的按钮，这将禁用文本字段并更改其边框。

用于比较两个哈希值并启用文本字段的代码非常简单：

```xml
if (soHASHING_SHA256.hex_sha256(this.rawValue) == passwd_man_hashed.rawValue){
     VAL_man_1.access = "open";
     VAL_man_2.access = "open";
     VAL_man_1.borderColor = "0,255,0";
     VAL_man_2.borderColor = "0,255,0";
}
```

## 从这里前往何处 {#next-steps}

你在哪里需要这样的东西？ 考虑一个PDF表单，其中包含应仅由授权人员填写的字段。 通过使用密码保护这些字段（在Sample_2.pdf中无法以明文形式查看这些字段），您可以确保只有知道密码的用户才能访问这些字段。

我鼓励您继续探索这两个示例PDF文件。  您可以使用Sample_1.pdf生成新的哈希值，并使用生成的值更改Sample_2.pdf中使用的密码或哈希函数。  归因部分中列出的资源还提供有关哈希处理以及本文中使用的特定JavaScript实施的更多信息。

## 归因 {#attributions}

* [罗纳德·里韦斯特](https://en.wikipedia.org/wiki/Ron_Rivest)
* [NIST](https://csrc.nist.gov/projects/cryptographic-standards-and-guidelines)
* [哈希冲突](https://en.wikipedia.org/wiki/Hash_collision)
* [彩虹表](https://en.wikipedia.org/wiki/Rainbow_table)
* [JavaScript MD5项目主页](https://pajhome.org.uk/crypt/md5/)
* [jsSHA2项目主页](https://anmar.eu.org/projects/jssha2/)
