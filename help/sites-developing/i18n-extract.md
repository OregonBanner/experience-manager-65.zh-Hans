---
title: 提取字符串以进行翻译
seo-title: 提取字符串以进行翻译
description: 使用xgettext-maven-plugin从源代码中提取需要翻译的字符串
seo-description: 使用xgettext-maven-plugin从源代码中提取需要翻译的字符串
uuid: 2c586ecb-8494-4f8f-b31a-1ed73644d611
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: 034f70f1-fbd2-4f6b-b07a-5758f0461a5b
exl-id: 4acc5f7f-0bcb-4b5a-8531-52e146cffeae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# 提取字符串以翻译{#extracting-strings-for-translating}

使用xgettext-maven-plugin从需要翻译的源代码中提取字符串。 Maven插件会将字符串提取到您发送以进行翻译的XLIFF文件。 字符串将从以下位置提取：

* Java源文件
* Javascript源文件
* SVN资源（JCR节点）的XML表示

## 配置字符串提取{#configuring-string-extraction}

配置xgettext-maven-plugin工具如何为您的项目提取字符串。

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

| 区域 | 描述 |
|---|---|
| /filter | 标识要解析的文件。 |
| /parsers/vaultxml | 配置对保管库文件的解析。 标识包含外部字符串和本地化提示的JCR节点。 还标识要忽略的JCR节点。 |
| /parsers/javascript | 标识将字符串外部化的Javascript函数。 您无需更改此部分。 |
| /parsers/regexp | 配置对Java、JSP和ExtJS模板文件的解析。 您无需更改此部分。 |
| /potents | 用于检测要国际化的字符串的公式。 |

### 标识要解析的文件{#identifying-the-files-to-parse}

i18n.any文件的/filter部分标识xgettext-maven-plugin工具解析的文件。 添加多个包含和排除规则，以分别标识已解析和忽略的文件。 您应包括所有文件，然后排除您不想解析的文件。 通常，您会排除不对UI做出贡献的文件类型，或者排除定义UI但未翻译的文件。 包含和排除规则的格式如下：

```
{ /include "pattern" }
{ /exclude "pattern" }
```

规则的模式部分用于匹配要包含或排除的文件的名称。 模式前缀指示您是匹配JCR节点（其在Vault中的表示形式）还是文件系统。

| 前缀 | 效果 |
|---|---|
| / | 指示JCR路径。 因此，此前缀匹配jcr_root目录下的文件。 |
| &amp;ast; | 指示文件系统上的常规文件。 |
| 无 | 没有前缀或以文件夹或文件名开头的模式表示文件系统上的常规文件。 |

在模式中使用时，/字符表示子目录和&amp;ast;字符与全部匹配。 下表列出了几个示例规则。

<table>
 <tbody>
  <tr>
   <th>示例规则</th>
   <th>效果</th>
  </tr>
  <tr>
   <td><code>{ /include "*" }</code></td>
   <td>包含所有文件。</td>
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
   <td><p>排除/content节点下的所有文件。</p> <p>包括/content/catalogs/geometrixx/templatepages节点。</p> <p>包括/content/catalogs/geometrixx/templatepages的所有子节点。</p> </td>
  </tr>
 </tbody>
</table>

### 提取字符串{#extracting-the-strings}

无POM:

```shell
mvn -N com.adobe.granite.maven:xgettext-maven-plugin:1.2.2:extract  -Dxgettext.verbose=true -Dxgettext.target=out -Dxgettext.rules=i18n.any -Dxgettext.root=.
```

使用POM:将此项添加到POM:

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

### 输出文件{#output-files}

* `raw.xliff`:提取字符串
* `warn.log`:警告（如果有），如果API `CQ.I18n.getMessage()` 使用不正确。这些操作始终需要修复，然后重新运行。

* `parserwarn.log`:解析器警告（如果有），例如js解析器问题
* `potentials.xliff`:未提取的“潜在”候选项，但可能是需要翻译的人类可读字符串（可以忽略，仍会产生大量误报）
* `strings.xliff`:扁平xliff文件，将导入ALF中
* `backrefs.txt`:允许快速查找给定字符串的源代码位置
