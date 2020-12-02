---
title: 编码准则
seo-title: 编码准则
description: 社区开发人员指南、提示和技巧
seo-description: 社区开发人员指南、提示和技巧
uuid: 311ef4f7-7f2c-44c3-bcf2-f68713752623
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 244cd43c-a573-495d-b80c-b97ba9d19b75
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# 编码准则{#coding-guidelines}

## 准则、提示与技巧{#guidelines-tips-and-tricks}

与AEM Communities的合作已经从严重依赖Java服务器页面转变为灵活选择模板脚本语言，其中业务逻辑、样式和页面内容彼此不同。

使用用户生成的内容(UGC)的更大灵活性是通过SocialResourceProvider API实现的，这消除了对选择[SRP](srp.md)选项进行部署的感知的需要。

以下是AEM Communities开发人员的各种编码指南和最佳实践：

### 代码{#code}

* [使用SRP访问UGC](accessing-ugc-with-srp.md) -如何避免编写仅在JCR(JSRP)中存储UGC时才能使用的应用程序。
* [SocialUtils重构](socialutils.md) -用于替换SocialUtils的SRP的实用程序方法。
* [命名约定](naming-conventions.md) -自定义Java类的命名约定。

### 脚本 {#scripts}

* [侧传社区组件](sideloading.md) -如何在页面加载后动态添加组件。
* [富文本编辑器](rte.md) Essentials-如何自定义为发布内容向成员提供的富文本UI。

### IDE {#ide}

* [使用Maven for Communities](maven.md) -如何包含Communities API jar。
* [SocialUtils重构](socialutils.md) -用于替换SocialUtils的SRP的实用程序方法。

