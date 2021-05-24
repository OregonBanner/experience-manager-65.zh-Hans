---
title: 在AEM中缓解序列化问题
seo-title: 在AEM中缓解序列化问题
description: 了解如何在AEM中缓解序列化问题。
seo-description: 了解如何在AEM中缓解序列化问题。
uuid: c3989dc6-c728-40fd-bc47-f8427ed71a49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f3781d9a-421a-446e-8b49-40744b9ef58e
exl-id: 01e9ab67-15e2-4bc4-9b8f-0c84bcd56862
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 0%

---

# 缓解AEM{#mitigating-serialization-issues-in-aem}中的序列化问题

## 概述 {#overview}

Adobe的AEM团队一直在与开源项目[NotSoSerial](https://github.com/kantega/notsoserial)密切合作，协助缓解&#x200B;**CVE-2015-7501**&#x200B;中描述的漏洞。 NotSoSerial根据[Apache 2许可证](https://www.apache.org/licenses/LICENSE-2.0)授权，并包含根据其自己的[类BSD许可证](https://asm.ow2.org/license.html)授权的ASM代码。

此包中包含的代理jar是Adobe修改的NotSoSerial分发。

NotSoSerial是Java级别问题的Java级解决方案，并不特定于AEM。 它会在尝试反序列化对象时添加预检检查。 此检查将针对防火墙样式的允许列表和/或阻止列表测试类名称。 由于默认阻止列表中类的数量有限，因此不太可能对系统或代码造成影响。

默认情况下，代理将针对当前已知的易受攻击类执行阻止列表检查。 此阻止列表旨在保护您免受使用此类型漏洞的当前漏洞攻击列表的攻击。

阻止列表和允许列表可按照本文[配置代理](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent)部分中的说明进行配置。

代理旨在帮助缓解最新已知的易受攻击类。 如果您的项目正在反序列化不可信的数据，它仍可能容易受到拒绝服务攻击、内存不足攻击和未知的未来反序列化攻击。

Adobe正式支持Java 6、7和8，但我们的理解是NotSoSerial也支持Java 5。

## 安装代理{#installing-the-agent}

>[!NOTE]
>
>如果您之前已安装AEM 6.1的序列化修补程序，请从java执行行中删除代理启动命令。

1. 安装&#x200B;**com.adobe.cq.cq-serialization-tester**&#x200B;包。

1. 转到`https://server:port/system/console/bundles`的“捆绑Web控制台”
1. 查找序列化包并启动它。 这应会动态自动加载NotSoSerial代理。

## 在应用程序服务器上安装代理{#installing-the-agent-on-application-servers}

NotSoSerial代理未包含在应用程序服务器的AEM标准分发中。 但是，您可以从AEM jar分发中提取它，并将其用于应用程序服务器设置：

1. 首先，下载AEM快速入门文件并将其解压缩：

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. 转到新解压缩的AEM快速启动文件的位置，然后将`crx-quickstart/opt/notsoserial/`文件夹复制到AEM应用程序服务器安装的`crx-quickstart`文件夹中。

1. 将`/opt`的所有权更改为运行服务器的用户：

   ```shell
   chown -R opt <user running the server>
   ```

1. 配置并检查代理是否已正确激活，如本文的以下部分所示。

## 配置代理{#configuring-the-agent}

默认配置适用于大多数安装。 这包括已知远程执行易受攻击类的阻止列表，以及包的允许列表，其中可信数据的反序列化应该相对安全。

防火墙配置是动态的，可随时通过以下方式进行更改：

1. 转到位于`https://server:port/system/console/configMgr`的Web控制台
1. 搜索并单击&#x200B;**反序列化防火墙配置。**

   >[!NOTE]
   >
   >您还可以通过访问以下URL直接访问配置页面：
   >
   >* `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`


此配置包含允许列表、阻止列表和反序列化日志记录。

**允许列表**

在允许列表部分中，这些是允许反序列化的类或包前缀。 请务必注意，如果您正在反序列化自己的类，则需要将类或包添加到此允许列表。

**阻止列表**

在块列表部分中，是不允许反序列化的类。 这些类的初始集仅限于发现容易遭受远程执行攻击的类。 阻止列表在任何允许列出的条目之前应用。

**诊断日志记录**

在诊断日志记录的部分中，您可以选择在发生反序列化时进行日志记录的多个选项。 这些用户仅在首次使用时登录，而不会在后续使用时再次登录。

**class-name-only**&#x200B;的默认值将通知您正在反序列化的类。

您还可以设置&#x200B;**full-stack**&#x200B;选项，该选项将记录第一次反序列化尝试的Java堆栈，以通知您反序列化的发生位置。 这可用于查找和删除使用中的反序列化。

## 验证代理的激活{#verifying-the-agent-s-activation}

您可以通过浏览到以下URL来验证反序列化代理的配置：

* `https://server:port/system/console/healthcheck?tags=deserialization`

访问URL后，将显示与代理相关的运行状况检查列表。 您可以通过验证运行状况检查是否已通过来确定是否正确激活了代理。 如果失败，您可能需要手动加载代理。

有关对代理问题进行故障诊断的详细信息，请参阅下面的[处理Dynamic Agent加载的错误](#handling-errors-with-dynamic-agent-loading)。

>[!NOTE]
>
>如果将`org.apache.commons.collections.functors`添加到允许列表，则运行状况检查将始终失败。

## 处理加载{#handling-errors-with-dynamic-agent-loading}动态代理时出现的错误

如果日志中显示错误或验证步骤检测到加载代理时出现问题，则可能需要手动加载代理。 如果您使用的是JRE（Java运行时环境）而不是JDK（Java开发工具包），则也建议使用此工具，因为没有用于动态加载的工具。

要手动加载代理，请按照以下说明操作：

1. 修改CQ jar的JVM启动参数，并添加以下选项：

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >这还需要使用 — nofork CQ/AEM选项以及相应的JVM内存设置，因为不会在分支JVM上启用代理。

   >[!NOTE]
   >
   >NotSoSerial代理jar的Adobe分发位于AEM安装的`crx-quickstart/opt/notsoserial/`文件夹中。

1. 停止并重新启动JVM;

1. 按照上述步骤（[验证代理的激活](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation)）再次验证代理的激活。

## 其他注意事项{#other-considerations}

如果您在IBM JVM上运行，请查阅有关[此位置](https://www.ibm.com/support/knowledgecenter/SSSTCZ_2.0.0/com.ibm.rt.doc.20/user/attachapi.html)支持Java Attach API的文档。
