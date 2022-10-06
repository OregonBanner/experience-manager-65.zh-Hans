---
title: OSGi包
seo-title: OSGI Bundles
description: 有关管理OSGi包的提示
seo-description: Tips for managing your OSGi bundles
uuid: 07af7089-a233-4e5b-928c-76ddc0af8839
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8d3374ac-51dd-4ff5-84c9-495c937ade12
exl-id: e18065c7-75b9-4b37-8294-cf94122a4dcf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# OSGi包{#osgi-bundles}

## 使用语义版本控制 {#use-semantic-versioning}

在上可找到语义版本编号的商定最佳实践 [https://semver.org/](https://semver.org/).

## 请勿嵌入OSGi包中严格需要的类和Jar {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

应将常用库划分为不同的包。 这样，它们便可在包中重复使用。 封装 *JAR* 在OSGi包中，确保检查在线源以查看是否有人以前已经这样做过。 查找现有包装器的一些常见位置包括：Apache Felix、Apache Sling、Apache Geronimo、Apache ServiceMix、Eclipse包方法和SpringSource企业包存储库。

## 取决于所需的最低包版本 {#depend-on-the-lowest-needed-bundle-versions}

对于POM文件中的编译时依赖项，始终取决于公开所需API所需的最低版本。 这样可提高向后兼容性，并更轻松地将补丁移入旧版本。

## 从OSGi包导出一组最小的包 {#export-a-minimal-set-of-packages-from-osgi-bundles}

导出资源包后，我们便立即为其他人员创建了一个API，供其他人员依赖。 确保尽可能少地导出，并确保要导出的内容是API。 采用私有方法/类并将其公开比采用先前导出的内容并将其公开容易得多。

实施应始终放在单独的 *impl* 包。 默认情况下， *maven-bundle-plugin* 将导出项目中没有 *impl* 以它的名称。

## 始终为导出的每个包显式定义语义版本 {#always-explicitly-define-a-semantic-version-for-each-package-exported}

这将允许您的API消费者与您一起进化。 这样做时，请始终遵循语义版本控制最佳实践。 这样，您的API消费者就可以知道新版本中预期会发生哪些类型的更改。

## 包括显示的元类型信息 {#include-metatype-information-where-exposed}

通过指定有意义的元类型信息，将使您的服务和组件在Felix控制台中更易于理解。 SCR注释和属性列表可在以下位置找到： [https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html).
