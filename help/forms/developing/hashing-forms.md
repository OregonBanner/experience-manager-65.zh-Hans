---
title: 如何在动态PDF forms中生成和处理哈希？
description: 在动态PDF forms中生成和使用哈希
source-git-commit: 730ae7cd6cd04eb6377b37eafe29db597e93cce3
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 0%

---

# 在动态PDF forms中生成和使用哈希 {#generate-work-with-hashes-dynamic-pdf-forms}


## 先决知识 {#prerequisite-knowledge}

需要在JEE Designer上获得一些使用AEM Forms的体验，以及在脚本对象中访问和调用函数的功能也是必需的。

## 用户级别 {#user-level}

开始

当您希望隐藏PDF表单中的密码，而不希望在源代码或PDF文档的其他位置中以明文形式显示密码时，知道如何生成和使用MD4、MD5、SHA-1和SHA-256哈希是关键。

其思想是通过生成唯一的哈希来模糊密码，并将此哈希存储在PDF文档中。 此唯一的哈希函数可以由不同的哈希函数生成，在本文中，我将向您展示如何在PDF表单中生成它们以及如何使用它们。

散列函数将任意长度的长字符串（或消息）作为输入，并生成固定长度的字符串作为输出，有时称为消息摘要或数字指纹。

AEM Forms on JEE Designer允许您在脚本对象中作为JavaScript实施不同的哈希函数，并在动态PDF文档中运行它们。 本文示例文件中包含的示例PDF使用以下哈希函数的开源实施：

* MD4和MD5 — 由Ronald Rivest设计

* SHA-1和SHA-256 — 由NIST定义

使用哈希的最大好处是，您不必通过比较明文字符串来直接比较密码；相反，您可以比较两个密码的两个哈希。 由于两个不同的字符串不太可能具有相同的哈希，因此，如果两个哈希都相同，则您可以假定比较的字符串（在本例中为密码）也相同。

>[!NOTE]
>
>MD4或MD5存在一些众所周知的安全问题（称为哈希冲突）。 由于这些哈希冲突和其他SHA-1哈克（包括彩虹表），我决定在第二个示例中集中讨论SHA-256哈希函数。  有关详细信息，请参阅Wikipedia的[Collision](https://en.wikipedia.org/wiki/Hash_collision)和[彩虹表](https://en.wikipedia.org/wiki/Rainbow_table)页。

## 检查脚本对象 {#examining-script-objects}

在JEE Designer的AEM Forms中打开提供的两个示例中的一个时，您将在“层次结构”面板中找到四个脚本对象（请参阅下图）。

![变量](assets/variables.jpg)

要查看这些脚本对象中哈希函数的JavaScript实现，请选择脚本对象，然后在脚本编辑器中浏览代码。  您可以查看以下每个哈希函数的实施方式：

* soHASHING_MD4.hex_md4()
* soHASHING_MD4.b64_md4()
* soHASHING_MD4.str_md4()
* soHASHING_MD5.hex_md5()
* soHASHING_MD5.b64_md5()
* soHASHING_MD5.str_md5()
* soHASHING_SHA1.hex_sha1()
* soHASHING_SHA1.b64_sha1()
* soHASHING_SHA1.str_sha1()
* soHASHING_SHA256.hex_sha256()
* soHASHING_SHA256.b64_sha256()
* soHASHING_SHA256.str_sha256()

正如您从此列表中所看到的，哈希的不同输出类型有不同的可用函数。 您可以选择`hex_`表示十六进制数字，`b64_`表示Base64编码输出，或`str_`表示简单字符串编码。

根据您选择的哈希函数，哈希的长度将有所不同：

* MD4:128位
* MD5:128位
* SHA-1:160位
* SHA-256:256位

## 尝试示例PDF forms {#try-sample-pdf-forms}

本文的示例文件包括两个PDF forms。 第一个示例允许您键入字符串，然后为字符串生成MD4、MD5、SHA-1和SHA-256哈希值。  第二个示例是一个简单的表单，在输入正确的密码时会解锁文本字段。

### 示例1: 生成哈希 {#generating-dashes}

请按照以下步骤尝试第一个示例：

1. 下载并解压缩示例文件后，在JEE Designer上使用AEM Forms打开hashing_forms_sample1.pdf。 或者，您也可以使用Adobe Reader或Adobe Acrobat Professional打开和查看示例，但是您将看不到源代码。
1. 在标有[!UICONTROL clear text]的文本字段中，键入密码或任何其他要经过哈希处理的消息。
1. 单击四个按钮中的一个按钮以生成MD4、MD5、SHA-1或SHA-256哈希。 根据您按下的按钮，将调用产生十六进制输出的四个哈希函数之一，并对字符串或消息进行哈希处理。

哈希运算的结果显示在标有[!UICONTROL hash]的字段中。 哈希的长度将因您选择的哈希函数而异。

所有示例都使用十六进制数字作为输出类型。 您可以使用脚本编辑器来修改示例，并将输出类型更改为Base64或简单字符串。

### 示例2: 匹配密码 {#matching-passwords}

第二个示例演示了如何在后台比较哈希，而无需公开真实密码。 您输入的密码经过哈希处理。 存储在不可见字段中的真实密码也经过哈希处理。 密码是安全的，不是因为它不可见，而是因为它已经过哈希处理。 由于无法从哈希值重建密码，因此以哈希形式公开密码是安全的。 只在哈希之间进行比较，而不是在明文的密码之间进行比较。 如果两个哈希都相同，则可以假定密码相同。

请按照以下步骤尝试第二个示例：

1. 在JEE Designer上使用AEM Forms打开`hashing_forms_sample2.pdf`。 或者，您也可以使用Adobe Reader或Adobe Acrobat Professional打开和查看示例，但是您将看不到源代码。
1. 选择标有[!UICONTROL Password MAN]或[!UICONTROL Password WOMAN]的两个密码字段之一，然后键入密码：
   1. 该人的密码为`bob`
   1. 女子的密码是`alice`
1. 当您将焦点移出密码字段或按Enter键时，系统会自动生成您输入的密码的哈希值，并将其与后台存储的正确密码的哈希值进行比较。 正确且经过哈希处理的密码存储在标有`passwd_man_hashed`和`passwd_woman_hashed`的不可见文本字段中。 如果为人键入正确的密码，则标记为`Man 1`和`Man 2`的文本字段将可供访问，以便您在其中键入文本。 同样的行为也适用于妇女的田地。
1. 或者，您也可以单击标有“删除密码”的按钮，以禁用文本字段并更改其边框。

用于比较两个哈希值并启用文本字段的代码非常简单：

```xml
if (soHASHING_SHA256.hex_sha256(this.rawValue) == passwd_man_hashed.rawValue){
     VAL_man_1.access = "open";
     VAL_man_2.access = "open";
     VAL_man_1.borderColor = "0,255,0";
     VAL_man_2.borderColor = "0,255,0";
}
```

## 从这里出发 {#next-steps}

你在哪里需要这样的东西？ 请考虑使用PDF表单，其中包含的字段只应由授权个人填写。 通过使用密码保护这些字段（与Sample_2.pdf中一样，该密码在文档中的任意位置都无法以明文显示），可以确保这些字段仅供知道密码的用户访问。

我建议您继续浏览两个PDF示例文件。  您可以使用Sample_1.pdf生成新的哈希值，并使用生成的值更改Sample_2.pdf中使用的密码或哈希函数。  “归因”部分中列出的资源还提供了有关哈希处理以及本文中使用的特定JavaScript实施的其他信息。

## 归因 {#attributions}

* [罗纳德·里韦斯特](https://en.wikipedia.org/wiki/Ron_Rivest)
* [NIST](https://csrc.nist.gov/projects/cryptographic-standards-and-guidelines)
* [哈希冲突](https://en.wikipedia.org/wiki/Hash_collision)
* [彩虹表](https://en.wikipedia.org/wiki/Rainbow_table)
* [JavaScript MD5项目主页](http://pajhome.org.uk/crypt/md5/)
* [jsSHA2项目主页](https://anmar.eu.org/projects/jssha2/)


