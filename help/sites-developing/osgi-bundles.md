---
title: OSGI捆绑
seo-title: OSGI捆绑
description: 管理OSGi捆绑包的提示
seo-description: 管理OSGi捆绑包的提示
uuid: 07af7089-a233-4e5b-928c-76ddc0af8839
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8d3374ac-51dd-4ff5-84c9-495c937ade12
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---


# OSGI捆绑{#osgi-bundles}

## 使用语义版本控制{#use-semantic-versioning}

可在[https://semver.org/](https://semver.org/)找到语义版本编号的一致最佳实践。

## 不要嵌入比OSGi捆绑{#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}中严格需要的更多类和jar

应将公用库分解为单独的包。 这将允许在您的捆绑包中重复使用它们。 将&#x200B;*JAR*&#x200B;打包到OSGI包中时，请确保检查联机源，看看是否有人以前已经这样做过。 查找现有捆绑包装的一些常见位置是：Apache Felix、Apache Sling、Apache Geronimo、Apache ServiceMix、Eclipse Bundle Recipes和SpringSource Enterprise Bundle Repository。

## 取决于所需的最低捆绑版本{#depend-on-the-lowest-needed-bundle-versions}

对于POM文件中的编译时相关性，始终依赖于公开所需API的最低需要版本。 这将允许更高的向后兼容性，并使旧版本的后移修复更容易。

## 从OSGi包{#export-a-minimal-set-of-packages-from-osgi-bundles}导出最少的包集

一旦导出了包，我们就为其他人创建了一个API。 确保尽可能少地导出，并确保所导出的是API。 采用私有方法／类并将其公开要比采用以前导出的内容并将其公开容易得多。

应始终将实现放置在单独的&#x200B;*impl*&#x200B;包中。 默认情况下，*maven-bundle-plugin*&#x200B;将导出项目中名称中没有&#x200B;*impl*&#x200B;的任何内容。

## 始终为导出的{#always-explicitly-define-a-semantic-version-for-each-package-exported}的每个包显式定义语义版本

这将允许您的API的消费者与您一同发展。 这样做时，请始终遵循语义版本控制最佳实践。 这将使您的API的消费者了解新版本中需要哪些类型的更改。

## 包含显示{#include-metatype-information-where-exposed}的元类型信息

通过指定有意义的元类型信息，您的服务和组件在Felix控制台中更易于理解。 SCR注释和属性的列表可在以下位置找到：[https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html)。
