---
title: 在AEM中缓解序列化问题
seo-title: Mitigating serialization issues in AEM
description: 了解如何在AEM中缓解序列化问题。
seo-description: Learn how to mitigate serialization issues in AEM.
uuid: c3989dc6-c728-40fd-bc47-f8427ed71a49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f3781d9a-421a-446e-8b49-40744b9ef58e
exl-id: 01e9ab67-15e2-4bc4-9b8f-0c84bcd56862
source-git-commit: 614c4c88f3f09feb5a400ade9f45f634ac4fbcd5
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---

# 在AEM中缓解序列化问题{#mitigating-serialization-issues-in-aem}

## 概述 {#overview}

Adobe的AEM团队与开源项目密切合作 [NotSoSerial](https://github.com/kantega/notsoserial) 以帮助缓解 **CVE-2015-7501**. NotSoSerial是在 [Apache 2许可证](https://www.apache.org/licenses/LICENSE-2.0) 并包含根据其自己的 [类似BSD的许可证](https://asm.ow2.io/).

此包中包含的代理jar是Adobe修改的NotSoSerial分发。

NotSoSerial是Java™级解决Java™级问题的Java级解决方案，并非特定于AEM。 它会在尝试反序列化对象时添加预检检查。 此检查会针对防火墙样式的或允许列表，或阻止列表者同时测试类名称。 由于默认中类数有限阻止列表，因此此测试不太可能对系统或代码产生影响。

默认情况下，代理会针对当前阻止列表已知的易受攻击类执行检查。 本阻止列表旨在保护您免受使用此类型漏洞的当前漏洞攻击列表的攻击。

可以阻止列表按照允许列表 [配置代理](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent) 本文章的章节。

代理旨在帮助缓解最新已知的易受攻击类。 如果您的项目正在反序列化不可信的数据，它仍可能容易受到拒绝服务攻击、内存不足攻击和未知的未来反序列化攻击。

Adobe正式支持Java™ 6、7和8。 但是，Adobe的理解是NotSoSerial也支持Java™ 5。

## 安装代理 {#installing-the-agent}

>[!NOTE]
>
>如果您之前已安装AEM 6.1的序列化修补程序，请从Java™运行行中删除代理启动命令。

1. 安装 **com.adobe.cq.cq-serialization-tester** 捆绑。

1. 转到“捆绑Web控制台”(位于 `https://server:port/system/console/bundles`
1. 查找序列化包并启动它。 这样做会动态自动加载NotSoSerial代理。

## 在应用程序服务器上安装代理 {#installing-the-agent-on-application-servers}

NotSoSerial代理未包含在应用程序服务器的AEM标准分发中。 但是，您可以从AEM jar分发中提取它，并将其用于应用程序服务器设置：

1. 首先，下载AEM快速入门文件并将其解压缩：

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. 转到新解压缩的AEM快速启动程序的位置，然后复制 `crx-quickstart/opt/notsoserial/` 文件夹 `crx-quickstart` AEM应用程序服务器安装的文件夹。

1. 更改 `/opt` 对运行服务器的用户：

   ```shell
   chown -R opt <user running the server>
   ```

1. 配置并检查代理是否已正确激活，如本文的以下部分所示。

## 配置代理 {#configuring-the-agent}

默认配置适用于大多数安装。 此配置包阻止列表括已知远程运行易受攻击类的，以及允许列表可信数据反序列化安全的包的。

防火墙配置是动态的，可随时通过以下方式进行更改：

1. 转到Web控制台(位于 `https://server:port/system/console/configMgr`
1. 搜索并单击 **反序列化防火墙配置。**

   >[!NOTE]
   您还可以通过访问以下URL直接访问配置页面：
   * `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`


此配置包含、允许列表和阻止列表反序列化日志记录。

**允许列表**

在允许列表部分中，这些列表是允许反序列化的类或包前缀。 如果要反序列化您自己的类，请将类或包添加到此允许列表。

**阻止列表**

在块列表部分中，是不允许反序列化的类。 这些类的初始集仅限于发现容易遭受远程执行攻击的类。 应用该阻止列表后，任何允许列出的条目都将生效。

**诊断日志记录**

在诊断日志记录部分，您可以选择多个选项，以在发生反序列化时进行记录。 这些选项仅在首次使用时记录，而不会在后续使用时重新记录。

默认 **class-name-only** 会通知您正在反序列化的类。

您还可以设置 **全栈** 该选项记录第一次反序列化尝试的Java™堆栈，以通知您反序列化的发生位置。 此选项对于从使用中查找和删除反序列化非常有用。

## 验证代理的激活 {#verifying-the-agent-s-activation}

您可以通过浏览到以下URL来验证反序列化代理的配置：

* `https://server:port/system/console/healthcheck?tags=deserialization`

访问URL后，将显示与代理相关的运行状况检查列表。 您可以通过验证运行状况检查是否已通过来确定是否正确激活了代理。 如果失败，必须手动加载代理。

有关对代理问题进行故障诊断的详细信息，请参阅 [处理Dynamic Agent加载时的错误](#handling-errors-with-dynamic-agent-loading) 下。

>[!NOTE]
如果添加 `org.apache.commons.collections.functors` 对于允许列表，运行状况检查始终失败。

## 处理动态代理加载时的错误 {#handling-errors-with-dynamic-agent-loading}

如果日志中显示错误或验证步骤检测到加载代理时出现问题，请手动加载代理。 如果您使用JRE(Java™运行时环境)而不是JDK(Java™ Development Toolkit)，则还建议使用此工作流，因为没有用于动态加载的工具。

要手动加载代理，请执行以下操作：

1. 编辑CQ jar的JVM启动参数，并添加以下选项：

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   要求您也使用 — nofork CQ/AEM选项以及相应的JVM内存设置，因为分支的JVM上未启用代理。

   >[!NOTE]
   NotSoSerial代理jar的Adobe分发可在 `crx-quickstart/opt/notsoserial/` 文件夹。

1. 停止并重新启动JVM;

1. 按照 [验证代理的激活](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation).

## 其他注意事项 {#other-considerations}

如果您是在IBM® JVM上运行，请查阅有关Java™ Attach API支持的文档，网址为 [此位置](https://www.ibm.com/docs/en/sdk-java-technology/8?topic=documentation-java-attach-api).
