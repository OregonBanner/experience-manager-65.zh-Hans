---
title: OSGi包
seo-title: OSGI Bundles
description: 管理OSGi捆绑包的提示
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

有关语义版本编号的公认最佳实践，请访问 [https://semver.org/](https://semver.org/).

## 嵌入的类和jar数量不要超过OSGi捆绑包中严格需要的数量 {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

应将通用库分解为单独的包。 这将允许它们在您的捆绑包中重复使用。 包装时 *JAR* 在OSGI包中，确保检查在线源，以查看是否有人以前已经这样做过。 查找现有捆绑包的一些常见位置包括：Apache Felix、Apache Sling、Apache Geronimo、Apache ServiceMix、Eclipse捆绑包方法和SpringSource企业捆绑包存储库。

## 取决于所需的最低捆绑包版本 {#depend-on-the-lowest-needed-bundle-versions}

对于POM文件中的编译时间依赖关系，始终依赖于公开所需API的最低版本。 这样可以实现更高的向后兼容性，并简化对旧版本的反向移植修复。

## 从OSGi捆绑包导出最小包集 {#export-a-minimal-set-of-packages-from-osgi-bundles}

导出资源包后，我们即创建了供其他人依赖的API。 确保导出尽可能少的内容，并确保要导出的内容是API。 获取私有方法/类并将其公开，比获取之前导出的内容并将其设为私有要容易得多。

实施应始终放在单独的 *实作* 包。 默认情况下， *maven-bundle-plugin* 将导出项目中不包含以下项的任何内容 *实作* 以它的名义。

## 始终为导出的每个包显式定义语义版本 {#always-explicitly-define-a-semantic-version-for-each-package-exported}

这将允许您API的消费者与您一起发展。 在执行此操作时，请始终遵循语义版本控制最佳实践。 这使您的API使用者能够知道新版本中预期的更改类型。

## 包括所公开的元类型信息 {#include-metatype-information-where-exposed}

通过指定有意义的元类型信息，可使您的服务和组件在Felix控制台中更易于理解。 SCR注释和属性列表可在以下位置找到： [https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html).
