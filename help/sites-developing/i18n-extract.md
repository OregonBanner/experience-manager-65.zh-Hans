---
title: 提取字符串以进行翻译
seo-title: Extracting Strings for Translating
description: 使用xgettext-maven-plugin从源代码中提取需要翻译的字符串
seo-description: Use xgettext-maven-plugin to extract strings from your source code that need translating
uuid: 2c586ecb-8494-4f8f-b31a-1ed73644d611
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: 034f70f1-fbd2-4f6b-b07a-5758f0461a5b
exl-id: 4acc5f7f-0bcb-4b5a-8531-52e146cffeae
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---

# 提取字符串以进行翻译{#extracting-strings-for-translating}

使用xgettext-maven-plugin从源代码中提取需要翻译的字符串。 Maven插件会将字符串提取到您发送的XLIFF文件中进行翻译。 将从以下位置提取字符串：

* Java源文件
* JavaScript源文件
* SVN资源（JCR节点）的XML表示形式

## 配置字符串提取 {#configuring-string-extraction}

配置xgettext-maven-plugin工具如何提取项目的字符串。

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
| /filter | 标识要解析的文件。 |
| /parsers/vaultxml | 配置保险库文件的解析。 标识包含外部化字符串和本地化提示的JCR节点。 还会标识要忽略的JCR节点。 |
| /parsers/javascript | 标识用于将字符串外部化的JavaScript函数。 您无需更改此分区。 |
| /parsers/regexp | 配置Java、JSP和ExtJS模板文件的解析。 您无需更改此分区。 |
| /潜能 | 检测要国际化的字符串的公式。 |

### 标识要解析的文件 {#identifying-the-files-to-parse}

i18n.any文件的/filter部分标识xgettext-maven-plugin工具解析的文件。 添加多个包含和排除规则，分别标识被解析和忽略的文件。 您应该包含所有文件，然后排除不想分析的文件。 通常，会排除不属于UI的文件类型，或定义UI但未翻译的文件。 包含和排除规则的格式如下：

```
{ /include "pattern" }
{ /exclude "pattern" }
```

规则的模式部分用于匹配要包含或排除的文件名。 模式前缀指示您是匹配JCR节点（它在电子仓库中的表示形式）还是文件系统。

| 前缀 | 效果 |
|---|---|
| / | 指示JCR路径。 因此，该前缀与jcr_root目录下的文件匹配。 |
| &amp;ast； | 指示文件系统中的常规文件。 |
| 无 | 无前缀或以文件夹或文件名开头的模式表示文件系统中的常规文件。 |

在模式中使用时，/字符表示子目录，&amp;ast；字符与所有匹配。 下表列出了几个规则示例。

<table>
 <tbody>
  <tr>
   <th>示例规则</th>
   <th>效果</th>
  </tr>
  <tr>
   <td><code>{ /include "*" }</code></td>
   <td>包括所有文件。</td>
  </tr>
  <tr>
   <td><code>{ /exclude "*.pdf" }</code></td>
   <td>排除所有PDF文件。</td>
  </tr>
  <tr>
   <td><code> { /exclude "*/pom.xml" }</code></td>
   <td>排除POM文件。</td>
  </tr>
  <tr>
   <td><code class="code">{ /exclude "/content/*" }
      { /include "/content/catalogs/geometrixx/templatepages" }
      { /include "/content/catalogs/geometrixx/templatepages/*" }</code></td>
   <td><p>排除/content节点下的所有文件。</p> <p>包含/content/catalogs/geometrixx/templatepages节点。</p> <p>包含/content/catalogs/geometrixx/templatepages的所有子节点。</p> </td>
  </tr>
 </tbody>
</table>

### 提取字符串  {#extracting-the-strings}

无POM：

```shell
mvn -N com.adobe.granite.maven:xgettext-maven-plugin:1.2.2:extract  -Dxgettext.verbose=true -Dxgettext.target=out -Dxgettext.rules=i18n.any -Dxgettext.root=.
```

使用POM：将此项添加到POM：

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

### 输出文件 {#output-files}

* `raw.xliff`：提取的字符串
* `warn.log`：警告（如果有），如果 `CQ.I18n.getMessage()` API使用不正确。 它们始终需要修复，然后再重新运行。

* `parserwarn.log`：解析器警告（如果有），例如js解析器问题
* `potentials.xliff`：未提取的“潜在”候选项，这些候选项可能是人类可读的字符串，需要翻译（可以忽略，但仍会生成大量误报）
* `strings.xliff`：拼合的xliff文件，将导入ALF
* `backrefs.txt`：允许快速查找给定字符串的源代码位置
