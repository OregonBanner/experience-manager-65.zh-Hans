---
title: OSGI捆绑套件
seo-title: OSGI捆绑套件
description: 管理OSGi捆绑套件的提示
seo-description: 管理OSGi捆绑套件的提示
uuid: 07af7089-a233-4e5b-928c-76ddc0af8839
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8d3374ac-51dd-4ff5-84c9-495c937ade12
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# OSGI捆绑套件{#osgi-bundles}

## 使用语义版本控制 {#use-semantic-versioning}

可在https://semver.org/上找到有关语义版本编号的商定最佳实践 [](https://semver.org/)。

## 不要在OSGi捆绑包中嵌入超出严格要求的类和jar {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

应将公用库分解为单独的包。 这将允许在您的捆绑包中重复使用它们。 将 *JAR打包到OSGI包中时* ，请务必检查联机源，以查看是否有人以前已经这样做。 查找现有捆绑包装的一些常见位置包括：Apache Felix、Apache Sling、Apache Geronimo、Apache serviceMix、Eclipse Bundle Recipes和SpringSource Enterprise Bundle Repository。

## 取决于最低需要的捆绑版本 {#depend-on-the-lowest-needed-bundle-versions}

对于POM文件中的编译时相关性，始终依赖于公开所需API的最低需求版本。 这将允许更高的向后兼容性，并使旧版本的后移修复更容易。

## 从OSGi包中导出最少的包集 {#export-a-minimal-set-of-packages-from-osgi-bundles}

一旦导出包，我们就为其他人创建了一个API供他们依赖。 确保尽可能少地导出，并确保导出的内容是API。 采用私有方法／类并将其公开要比采用以前导出的内容并使其成为私有更容易。

实施应始终放在单独的实 *施包* 。 默认情况下， *maven-bundle-plugin* 将导出项目中名称中没有 *impl* 的任何内容。

## 始终为导出的每个包显式定义语义版本 {#always-explicitly-define-a-semantic-version-for-each-package-exported}

这将允许您的API的消费者与您一起发展。 这样做时，请始终遵循语义版本控制最佳实践。 这样，您的API的消费者就可以知道新版本中需要哪些类型的更改。

## 包含公开的元类型信息 {#include-metatype-information-where-exposed}

通过指定有意义的元类型信息，可使您的服务和组件在Felix控制台中更易于理解。 SCR注释和属性列表位于： [https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html)。
