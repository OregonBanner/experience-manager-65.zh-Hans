---
title: 减轻AEM中的序列化问题
seo-title: 减轻AEM中的序列化问题
description: 了解如何减轻AEM中的序列化问题。
seo-description: 了解如何减轻AEM中的序列化问题。
uuid: c3989dc6-c728-40fd-bc47-f8427ed71a49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f3781d9a-421a-446e-8b49-40744b9ef58e
translation-type: tm+mt
source-git-commit: 3cbbad3ce9d93a353f48fc3206df989a8bf1991a
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 0%

---


# 缓解AEM{#mitigating-serialization-issues-in-aem}中的序列化问题

## 概述 {#overview}

Adobe的AEM团队一直与开放源项目[NotSoSerial](https://github.com/kantega/notsoserial)密切合作，以帮助缓解&#x200B;**CVE-2015-7501**&#x200B;中描述的漏洞。 NotSoSerial根据[Apache 2许可证](https://www.apache.org/licenses/LICENSE-2.0)授予许可，并包含根据其自己的[类似BSD的许可证](https://asm.ow2.org/license.html)授予许可的ASM代码。

此包中包含的代理jar是Adobe修改的NotSoSerial分发。

NotSoSerial是Java级别问题的Java级解决方案，不特定于AEM。 它将预检检查添加到尝试反序列化对象。 此检查将针对防火墙样式的允许列表和／或阻止列表测试类名。 由于默认阻止列表中类的数量有限，这不太可能影响您的系统或代码。

默认情况下，代理将针对当前已知的易受攻击类执行阻止列表检查。 此阻止列表旨在保护您免受当前使用此类漏洞的利用列表的侵害。

阻止列表和允许列表可按照本文[配置代理](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent)部分中的说明进行配置。

代理旨在帮助减轻最新已知的易受攻击类。 如果您的项目正在反序列化不受信任的数据，它仍可能易受拒绝服务攻击、内存不足攻击和未知的未来反序列化利用攻击。

Adobe正式支持Java 6、7和8，但我们了解NotSoSerial也支持Java 5。

## 安装代理{#installing-the-agent}

>[!NOTE]
>
>如果之前已安装AEM 6.1的序列化修补程序，请从java执行行中删除代理开始命令。

1. 安装&#x200B;**com.adobe.cq.cq-serialization-tester**&#x200B;捆绑包。

1. 转到位于`https://server:port/system/console/bundles`的Bundle Web控制台
1. 查找序列化捆绑并开始它。 这应动态自动加载NotSoSerial代理。

## 在应用程序服务器{#installing-the-agent-on-application-servers}上安装代理

AEM的应用程序服务器标准分发中不包含NotSoSerial代理。 但是，您可以从AEM jar分发中提取它并将其与应用程序服务器设置一起使用：

1. 首先，下载AEM quickstart文件并解压它：

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. 转到新解压的AEM quickstart的位置，并将`crx-quickstart/opt/notsoserial/`文件夹复制到AEM应用程序服务器安装的`crx-quickstart`文件夹。

1. 将`/opt`的所有权更改为运行服务器的用户：

   ```shell
   chown -R opt <user running the server>
   ```

1. 配置并检查代理是否已正确激活，如本文的下几节所示。

## 配置代理{#configuring-the-agent}

默认配置适用于大多数安装。 这包括已知远程执行易受攻击类的阻止列表和包的允许列表，其中可信任数据的反序列化应该相对安全。

防火墙配置是动态的，可以随时通过以下方式进行更改：

1. 转到位于`https://server:port/system/console/configMgr`的Web控制台
1. 搜索并单击&#x200B;**反序列化防火墙配置。**

   >[!NOTE]
   >
   >您也可以通过访问URL(网址为：
   >
   >* `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`


此配置包含允许列表、阻止列表和反序列化日志记录。

**允许列表**

在“允许列表”部分，这些是允许反序列化的类或包前缀。 请注意，如果要反序列化您自己的类，则需要将类或包添加到此允许列表。

**块列表**

在块列表部分中，不允许反序列化类。 这些类的初始集仅限于已发现易受远程执行攻击的类。 在允许列出任何条目之前应用阻止列表。

**诊断日志记录**

在诊断日志记录部分，可以选择在进行反序列化时要记录的多个选项。 它们仅在首次使用时登录，而在后续使用时不再登录。

**class-name-only**&#x200B;的默认值将通知正在反序列化的类。

您还可以设置&#x200B;**full-stack**&#x200B;选项，该选项将记录第一次反序列化尝试的java堆栈，以通知您反序列化的发生位置。 这对于从使用中查找和删除反序列化非常有用。

## 验证代理的激活{#verifying-the-agent-s-activation}

您可以通过浏览到以下URL验证反序列化代理的配置：

* `https://server:port/system/console/healthcheck?tags=deserialization`

访问URL后，将显示与代理相关的运行状况检查列表。 您可以通过验证运行状况检查是否已通过来确定代理是否已正确激活。 如果故障发生，您可能需要手动加载代理。

有关代理故障排除问题的详细信息，请参阅下面的[处理动态代理加载的错误](#handling-errors-with-dynamic-agent-loading)。

>[!NOTE]
>
>如果向允许列表添加`org.apache.commons.collections.functors`，运行状况检查将始终失败。

## 处理动态代理加载{#handling-errors-with-dynamic-agent-loading}时的错误

如果日志中显示错误，或验证步骤检测到加载代理时出现问题，则可能需要手动加载代理。 如果您使用的是JRE(Java运行时环境)而不是JDK（Java开发工具包），则还建议使用它，因为没有用于动态加载的工具。

要手动加载代理，请按照以下说明操作：

1. 修改CQ jar的JVM启动参数，添加以下选项：

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >这也需要使用-nofork CQ/AEM选项以及相应的JVM内存设置，因为在分类的JVM上不启用代理。

   >[!NOTE]
   >
   >NotSoSerial代理jar的Adobe分发位于AEM安装的`crx-quickstart/opt/notsoserial/`文件夹中。

1. 停止并重新启动JVM;

1. 按照[验证代理的激活符](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation)中所述的步骤再次验证代理的激活。

## 其他注意事项{#other-considerations}

如果您正在IBM JVM上运行，请查看有关[此位置](https://www.ibm.com/support/knowledgecenter/SSSTCZ_2.0.0/com.ibm.rt.doc.20/user/attachapi.html)的Java Attach API支持的文档。
