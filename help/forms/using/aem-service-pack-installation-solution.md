---
title: 安装最新的6.5.15.0 Service Pack后，CRX/bundle和“启动页面”服务出现不可用错误
description: 安装最新的6.5.15.0 Service Pack后，CRX/bundle和“启动页面”服务出现不可用错误
source-git-commit: 974796a6b9e921f8c2f40d72a4764eb9f4d8b92b
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 2%

---


# 安装AEM(6.5.15.0)Service Pack后出现服务不可用错误 {#steps-to-resolve-error-after-installing-service-pack}

## 带有 OS 剪贴板 {#issue}

安装 [AEM 6.5.15.0 service pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)，则出现错误为：
* 错误 [FelixDispatchQueue] org.apache.sling.scripting.console FrameworkEvent错误(org.osgi.framework.BundleException:无法解析org.apache.sling.scripting.console

安装AEM 6.5.15.0 Service Pack后，CRX/bundle和起始页显示服务不可用错误。

## 应用到 {#applies-to}

此解决方案适用于：
* AEM Forms在所有JEE服务器上，但JBoss EAP 7.4.0上运行的服务器除外

## 解决方案 {#solution}

>[!NOTE]
>
>故障排除步骤适用于除JBoss EAP 7.4之外的所有应用程序服务器。

安装后 [AEM 6.5.15.0 service pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)，如果CRX/bundle和启动页显示服务不可用错误，请执行以下步骤：

1. 停止应用程序服务器。
1. 导航到 `[aem-forms root]\crx-repository\launchpad\felix\bundle52`。
1. 找到 `bundle.info` 文件。
1. 打开 `bundle.info` 文件，并将包名称搜索为 `org.apache.felix.http.bridge`.

   >[!NOTE]
   >
   >如果 `bundle.info` 在 `bundle52` 不包含 `org.apache.felix.http.bridge` 包，检查包号中位于 `org.apache.felix.http.bridge`. 然后，导航到 [aem-forms根]\crx-repository\launchpad\felix\bundle[x] 并在此位置执行后续步骤。

1. 导航至 URL: `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`.
1. 搜索 `bundle.jar` 并重命名 `bundle.jar` to `bundle.jar.bak`.
1. 复制 `Bundle for AEM 6.5 Forms on JEE Service Pack 15` 从这个位置 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bundle.jar).
1. 启动应用程序服务器，等待日志稳定并检查包状态。
1. 所有包都处于活动状态后，请安装 [JEE Service Pack 15上AEM 6.5 Forms的片段](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) 从 `system/console/bundles` 等待应用服务器稳定。
1. 停止应用程序服务器。
1. 导航到 `[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1` 并删除 `bundle.jar`.
1. 重命名 `bundle.jar.bak` 到 `bundle.jar`.
1. 启动应用程序服务器。