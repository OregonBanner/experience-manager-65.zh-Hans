---
title: OSGi包
seo-title: OSGi包
description: 有关管理OSGi包的提示
seo-description: 有关管理OSGi包的提示
uuid: 07af7089-a233-4e5b-928c-76ddc0af8839
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8d3374ac-51dd-4ff5-84c9-495c937ade12
exl-id: e18065c7-75b9-4b37-8294-cf94122a4dcf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---

# OSGi包{#osgi-bundles}

## 使用语义版本控制{#use-semantic-versioning}

可在[https://semver.org/](https://semver.org/)中找到有关语义版本编号的商定最佳实践。

## 不要嵌入比OSGi包{#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}中严格需要的类和Jar数量更多的内容

应将常用库划分为不同的包。 这样，它们便可在包中重复使用。 在OSGi包中封装&#x200B;*JAR*&#x200B;时，请确保检查联机源以查看以前是否有人已经这样做。 查找现有包装器的一些常见位置包括：Apache Felix、Apache Sling、Apache Geronimo、Apache ServiceMix、Eclipse包方法和SpringSource企业包存储库。

## 取决于所需的最低包版本{#depend-on-the-lowest-needed-bundle-versions}

对于POM文件中的编译时依赖项，始终取决于公开所需API所需的最低版本。 这样可提高向后兼容性，并更轻松地将补丁移入旧版本。

## 从OSGi包{#export-a-minimal-set-of-packages-from-osgi-bundles}导出最小的包集

导出资源包后，我们便立即为其他人员创建了一个API，供其他人员依赖。 确保尽可能少地导出，并确保要导出的内容是API。 采用私有方法/类并将其公开比采用先前导出的内容并将其公开容易得多。

实施应始终放在单独的&#x200B;*impl*&#x200B;包中。 默认情况下， *maven-bundle-plugin*&#x200B;将导出项目中名称中没有&#x200B;*impl*&#x200B;的任何内容。

## 始终为导出的{#always-explicitly-define-a-semantic-version-for-each-package-exported}的每个包显式定义语义版本

这将允许您的API消费者与您一起进化。 这样做时，请始终遵循语义版本控制最佳实践。 这样，您的API消费者就可以知道新版本中预期会发生哪些类型的更改。

## 包含{#include-metatype-information-where-exposed}公开的元类型信息

通过指定有意义的元类型信息，将使您的服务和组件在Felix控制台中更易于理解。 SCR注释和属性列表可在以下位置找到：[https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html)。
