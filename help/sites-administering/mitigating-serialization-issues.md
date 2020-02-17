---
title: 缓解AEM中的序列化问题
seo-title: 缓解AEM中的序列化问题
description: 了解如何在AEM中缓解序列化问题。
seo-description: 了解如何在AEM中缓解序列化问题。
uuid: c3989dc6-c728-40fd-bc47-f8427ed71a49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f3781d9a-421a-446e-8b49-40744b9ef58e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 缓解AEM中的序列化问题{#mitigating-serialization-issues-in-aem}

## 概述 {#overview}

Adobe的AEM团队一直与开放源项目 [NotSoSerial](https://github.com/kantega/notsoserial) 密切合作，以帮助缓解 **CVE-2015-7501中描述的漏洞**。 NotSoSerial根据 [Apache 2许可证授予许可](https://www.apache.org/licenses/LICENSE-2.0) ，并包括根据其自己的类似 [BSD的许可证授予许可的ASM代码](https://asm.ow2.org/license.html)。

此包中包含的代理jar是Adobe修改的NotSoSerial分发。

NotSoSerial是Java级别问题的Java级别解决方案，不特定于AEM。 它将预检检查添加到尝试反序列化对象。 此检查将针对防火墙样式的白名单和／或黑名单测试类名称。 由于默认黑名单中类的数量有限，这不太可能对您的系统或代码产生影响。

默认情况下，代理将针对当前已知的易受攻击类执行黑名单检查。 此黑名单旨在保护您免受使用此类漏洞的当前漏洞利用列表的侵害。

可以按照本文配置代理部分中的说明配置黑 [名单和白名单](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent) 。

该代理旨在帮助减轻最新的已知易受攻击类。 如果您的项目正在反序列化不受信任的数据，它仍可能易受拒绝服务攻击、内存不足攻击和未知的未来反序列化利用攻击。

Adobe正式支持Java 6、7和8，但我们了解NotSoSerial也支持Java 5。

## 安装代理 {#installing-the-agent}

>[!NOTE]
>
>如果您之前已安装AEM 6.1的序列化修补程序，请从java执行行中删除代理启动命令。

1. 安装com.adobe.cq.cq- **serialization-tester包** 。

1. 转到Bundle Web Console，网址为 `https://server:port/system/console/bundles`
1. 查找序列化捆绑并启动它。 这应动态地自动加载NotSoSerial代理。

## 在应用程序服务器上安装代理 {#installing-the-agent-on-application-servers}

NotSoSerial代理不包括在AEM的应用程序服务器的标准分发中。 但是，您可以从AEM jar分发中提取它，并将其与应用程序服务器设置一起使用：

1. 首先，下载AEM快速入门文件并将其解压：

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. 转到新解压缩的AEM快速启动程序的位置，并将该文 `crx-quickstart/opt/notsoserial/` 件夹复制到AEM应用程 `crx-quickstart` 序服务器安装的文件夹中。

1. 将服务器的所 `/opt` 有权更改为运行服务器的用户：

   ```shell
   chown -R opt <user running the server>
   ```

1. 配置并检查代理是否已正确激活，如本文的下几节所示。

## 配置代理 {#configuring-the-agent}

默认配置适用于大多数安装。 这包括已知远程执行易受攻击类的黑名单和包的白名单，其中可信数据的反序列化应该相对安全。

防火墙配置是动态的，可以通过以下方式随时更改：

1. 转到Web控制台，网址为 `https://server:port/system/console/configMgr`
1. 搜索并单击反序列化 **防火墙配置。**

   >[!NOTE]
   >
   >您还可以通过访问位于以下网址的URL直接访问配置页面：
   >
   >* `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`


此配置包含白名单、黑名单和反序列化日志记录。

**白名单**

在白名单部分，这些是允许反序列化的类或包前缀。 请注意，如果要反序列化您自己的类，您需要将类或包添加到此白名单中。

**黑名单**

在黑名单部分中，不允许反序列化类。 这些类的初始集仅限于发现容易受到远程执行攻击的类。 黑名单在列入白名单的条目之前应用。

**诊断记录**

在诊断日志记录部分，可以选择在进行反序列化时要记录的多个选项。 这些只在首次使用时记录，而不在后续使用中重新记录。

仅class- **name-only的默认值** ，将通知您正在进行反序列化的类。

您还可以设置完 **整堆栈选项** ，该选项将记录第一次反序列化尝试的Java堆栈，以通知您反序列化的发生位置。 这对于查找和从使用中删除反序列化非常有用。

## 验证代理的激活 {#verifying-the-agent-s-activation}

您可以通过浏览到以下URL验证反序列化代理的配置：

* `https://server:port/system/console/healthcheck?tags=deserialization`

访问URL后，将显示与代理相关的运行状况检查列表。 您可以通过验证运行状况检查是否通过来确定代理是否已正确激活。 如果故障发生，您可能需要手动加载代理。

有关对代理问题进行故障诊断的更多信息，请参 [阅以下处理Dynamic Agent加载错误](#handling-errors-with-dynamic-agent-loading) 。

>[!NOTE]
>
>如果添加 `org.apache.commons.collections.functors` 到白名单，则运行状况检查将始终失败。

## 处理动态代理加载时的错误 {#handling-errors-with-dynamic-agent-loading}

如果日志中显示了错误，或验证步骤检测到加载代理时出现问题，则可能需要手动加载代理。 如果您使用JRE（Java运行时环境）而不是JDK（Java开发工具包），则还建议使用该工具，因为用于动态加载的工具不可用。

要手动加载代理，请按照以下说明操作：

1. 修改CQ jar的JVM启动参数，添加以下选项：

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >这也需要使用-nofork CQ/AEM选项以及相应的JVM内存设置，因为分组的JVM上不会启用代理。

   >[!NOTE]
   >
   >可以在AEM安装的文件夹中找到NotSoSerial代理程 `crx-quickstart/opt/notsoserial/` 序jar的Adobe分发。

1. 停止并重新启动JVM;

1. 按照上述验证代理激活中所述的步骤再 [次验证代理激活](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation)。

## 其他注意事项 {#other-considerations}

如果您正在IBM JVM上运行，请查看此位置有关Java Attach API支持的 [文档](https://www.ibm.com/support/knowledgecenter/SSSTCZ_2.0.0/com.ibm.rt.doc.20/user/attachapi.html)。

