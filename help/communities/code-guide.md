---
title: 编码准则
seo-title: Coding Guidelines
description: Communities开发人员指南、提示和技巧
seo-description: Communities developer guidelines, tips, and tricks
uuid: 311ef4f7-7f2c-44c3-bcf2-f68713752623
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 244cd43c-a573-495d-b80c-b97ba9d19b75
exl-id: a23aab83-1dfa-4d91-9b6b-6246a2103896
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# 编码准则 {#coding-guidelines}

## 准则、提示和技巧 {#guidelines-tips-and-tricks}

使用AEM Communities已从严重依赖Java Server Pages发展到灵活选择模板脚本语言，因为这种语言的业务逻辑、样式和页面内容彼此不同。

在使用用户生成的内容(UGC)方面更大的灵活性是通过SocialResourceProvider API，从而无需了解哪些 [SRP](srp.md) 已为部署选择了选项。

以下是AEM Communities开发人员的各种编码准则和最佳实践：

### 代码 {#code}

* [使用SRP访问UGC](accessing-ugc-with-srp.md)  — 如何避免编写仅当UGC存储在JCR (JSRP)中时才有效的应用程序。
* [SocialUtils重构](socialutils.md)  — 替换SocialUtils的SRP的实用程序方法。
* [命名约定](naming-conventions.md)  — 自定义Java类的命名约定。

### 脚本 {#scripts}

* [侧载社区组件](sideloading.md)  — 如何在页面加载后动态添加组件。
* [富文本编辑器Essentials](rte.md)  — 如何自定义提供给成员用于发布内容的富文本UI。

### IDE {#ide}

* [使用Maven for Communities](maven.md)  — 如何包含Communities API jar。
* [SocialUtils重构](socialutils.md)  — 替换SocialUtils的SRP的实用程序方法。
