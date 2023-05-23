---
title: 擷取要轉譯的字串
seo-title: Extracting Strings for Translating
description: 使用xgettext-maven-plugin從您的原始程式碼中擷取需要翻譯的字串
seo-description: Use xgettext-maven-plugin to extract strings from your source code that need translating
uuid: 2c586ecb-8494-4f8f-b31a-1ed73644d611
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: 034f70f1-fbd2-4f6b-b07a-5758f0461a5b
exl-id: 4acc5f7f-0bcb-4b5a-8531-52e146cffeae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---

# 擷取要轉譯的字串{#extracting-strings-for-translating}

使用xgettext-maven-plugin從您的原始程式碼中擷取需要翻譯的字串。 Maven外掛程式會將字串擷取至您傳送的XLIFF檔案進行翻譯。 字串會從下列位置擷取：

* Java來源檔案
* Javascript來源檔案
* SVN資源（JCR節點）的XML表示法

## 設定字串擷取 {#configuring-string-extraction}

設定xgettext-maven-plugin工具如何為您的專案擷取字串。

```xml
/filter { }
/parsers {
   /vaultxml { }
   /javascript { }
   /regexp {
      /files {
         /java { }
         /jsp { }
         /extjstemplate { }
      }
   }
}
/potentials { }
```

| 分区 | 描述 |
|---|---|
| /filter | 識別要剖析的檔案。 |
| /parsers/vaultxml | 設定儲存庫檔案的剖析。 識別包含外部化字串和本地化提示的JCR節點。 也會識別要忽略的JCR節點。 |
| /parsers/javascript | 識別可將字串外部化的Javascript函式。 您不需要變更此區段。 |
| /parsers/regexp | 設定剖析Java、JSP和ExtJS範本檔案。 您不需要變更此區段。 |
| /潛能 | 偵測要國際化的字串的公式。 |

### 識別要剖析的檔案 {#identifying-the-files-to-parse}

i18n.any檔案的/filter區段會識別xgettext-maven-plugin工具剖析的檔案。 新增數個包含和排除規則，分別識別已剖析和忽略的檔案。 您應該包含所有檔案，然後排除不想剖析的檔案。 通常，您會排除不貢獻UI的檔案型別，或定義UI但未翻譯的檔案。 包含和排除規則的格式如下：

```
{ /include "pattern" }
{ /exclude "pattern" }
```

規則的陣列部分用於比對要包含或排除的檔案名稱。 陣列首碼表示您是匹配JCR節點（其在儲存庫中表示）還是檔案系統。

| 前缀 | 效果 |
|---|---|
| / | 表示JCR路徑。 因此，此首碼會比對jcr_root目錄下的檔案。 |
| &amp;ast； | 表示檔案系統上的一般檔案。 |
| 无 | 無首碼或以資料夾或檔案名稱開頭的模式表示檔案系統上的一般檔案。 |

當在模式中使用時，/字元表示子目錄，而&amp;ast；字元符合全部。 下表列出數個規則範例。

<table>
 <tbody>
  <tr>
   <th>規則範例</th>
   <th>效果</th>
  </tr>
  <tr>
   <td><code>{ /include "*" }</code></td>
   <td>包含所有檔案。</td>
  </tr>
  <tr>
   <td><code>{ /exclude "*.pdf" }</code></td>
   <td>排除所有PDF檔案。</td>
  </tr>
  <tr>
   <td><code> { /exclude "*/pom.xml" }</code></td>
   <td>排除POM檔案。</td>
  </tr>
  <tr>
   <td><code class="code">{ /exclude "/content/*" }
      { /include "/content/catalogs/geometrixx/templatepages" }
      { /include "/content/catalogs/geometrixx/templatepages/*" }</code></td>
   <td><p>排除/content節點下的所有檔案。</p> <p>包含/content/catalogs/geometrixx/templatepages節點。</p> <p>包含/content/catalogs/geometrixx/templatepages的所有子節點。</p> </td>
  </tr>
 </tbody>
</table>

### 擷取字串  {#extracting-the-strings}

無POM：

```shell
mvn -N com.adobe.granite.maven:xgettext-maven-plugin:1.2.2:extract  -Dxgettext.verbose=true -Dxgettext.target=out -Dxgettext.rules=i18n.any -Dxgettext.root=.
```

使用POM：將此專案新增至POM：

```xml
<build>
    <plugins>
        <plugin>
            <groupId>com.adobe.granite.maven</groupId>
            <artifactId>xgettext-maven-plugin</artifactId>
            <version>1.1</version>
            <configuration>
                <rules>i18n.any</rules>
                <root>jcr_root</root>
                <xliff>cq.xliff</xliff>
                <verbose>true</verbose>
            </configuration>
        </plugin>
    </plugins>
</build>
```

命令：

```shell
mvn xgettext:extract
```

### 輸出檔案 {#output-files}

* `raw.xliff`：擷取的字串
* `warn.log`：警告（若有的話） `CQ.I18n.getMessage()` API使用不正確。 這些一律需要修正，然後再重新執行。

* `parserwarn.log`：剖析器警告（如有），例如js剖析器問題
* `potentials.xliff`：未擷取的「潛在」候選項，但可能是需要翻譯的可讀取字串（可以忽略，仍會產生大量誤判）
* `strings.xliff`：平面化的xliff檔案，將匯入ALF中
* `backrefs.txt`：可讓您快速查詢指定字串的原始程式碼位置
