---
title: 尽管AEM Forms尚未启动，但正在执行多项服务。
description: 即使AEM Forms尚未完全启动，它仍会处理多项服务。
source-git-commit: 6b24067c1808475044a612f21d5d4d2793c13e17
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 4%

---

# 尽管AEM Forms未完全启动，但仍执行多项服务{#steps-to-resolve-error-after-installing-service-pack}


## 问题 {#issue}

当用户重新启动AEM Forms时，当前调用过程仍会继续进行，例如渲染PDF文档等。 这会导致AEM Forms服务器的重新启动无法正确启动。

## 应用到 {#applies-to}

该解决方案适用于JEE服务器上的AEM Forms和OSGi服务器上的AEM Forms 。

## 解决方案 {#solution}

要解决此问题，用户需添加一个参数 `Dcom.adobe.livecycle.dsc.deferServiceStart=true` 到 [批处理文件](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/command-line-start-and-stop.html#windows-platform-start-bat-script-example) 在服务器启动期间。





