---
title: 安装最新的6.5.15.0 Service Pack后，出现CRX/捆绑包和起始页服务不可用错误
description: 安装最新的6.5.15.0 Service Pack后，出现CRX/捆绑包和起始页服务不可用错误
exl-id: dfe015a3-3a24-41c5-aede-8e086851d62b
source-git-commit: e961f0c7107b4eacb0d5e50565cb64f5fa30e265
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 2%

---

# 安装AEM (6.5.15.0) Service Pack后出现“服务不可用”错误 {#steps-to-resolve-error-after-installing-service-pack}

## 带有 OS 剪贴板 {#issue}

安装后 [AEM 6.5.15.0 service pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)，错误发生如下：
* 错误 [FelixDispatchQueue] org.apache.sling.scripting.console框架事件错误(org.osgi.framework.BundleException：无法解析org.apache.sling.scripting.console

安装AEM 6.5.15.0 Service Pack后，CRX/捆绑包和起始页显示服务不可用错误。

## 应用到 {#applies-to}

此解决方案适用于：
* 所有JEE服务器（在JBoss EAP 7.4.0上运行的除外）上的AEM Forms

## 解决方案 {#solution}

>[!NOTE]
>
>故障排除步骤适用于除JBoss EAP 7.4之外的所有应用程序服务器。

安装后 [AEM 6.5.15.0 service pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)，如果CRX/捆绑包和起始页显示服务不可用错误，请执行以下步骤：

1. 停止应用程序服务器。
1. 导航到 `[aem-forms root]\crx-repository\launchpad\felix\bundle52`。
1. 找到 `bundle.info` 文件。
1. 打开 `bundle.info` 文件，并将包名称搜索为 `org.apache.felix.http.bridge`.

   >[!NOTE]
   >
   >如果 `bundle.info` 下 `bundle52` 不包含 `org.apache.felix.http.bridge` 捆绑，检查 `org.apache.felix.http.bridge`. 然后导航到 [aem-forms根]\crx-repository\launchpad\felix\bundle[x] 并在此位置执行后续步骤。

1. 导航至 URL: `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`.
1. 搜索 `bundle.jar` 并重命名 `bundle.jar` 到 `bundle.jar.bak`.
1. 复制 `Bundle for AEM 6.5 Forms on JEE Service Pack 15` 在此位置，从 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bundle.jar).
1. 启动应用程序服务器，等待日志稳定并检查捆绑包状态。
1. 一旦所有捆绑包都处于活动状态，请安装 [JEE Service Pack 15上的AEM 6.5 Forms片段](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) 从 `system/console/bundles` 并等待应用程序服务器稳定下来。
1. 停止应用程序服务器。
1. 导航到 `[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1` 并删除 `bundle.jar`.
1. 重命名 `bundle.jar.bak` 到 `bundle.jar`.
1. 启动应用程序服务器。
