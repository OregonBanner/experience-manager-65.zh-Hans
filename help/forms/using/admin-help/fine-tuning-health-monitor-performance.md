---
title: 微调运行状况监视器性能
seo-title: Fine-tuning Health Monitor performance
description: 了解如何微调运行状况监视器性能
seo-description: Learn how to fine-tune Health Monitor performance
uuid: 770b10cb-065f-41b5-9594-a291e4311151
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b8f8bddc-0d38-4d5e-b33f-978f04bc16c6
exl-id: 41042e08-5e14-4809-89b7-16d98a72d1b4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 1%

---

# 微调运行状况监视器性能{#fine-tuning-health-monitor-performance}

收集填充运行状况监视器的系统统计信息对AEM Forms环境的性能有一些影响。 可以通过在应用程序服务器中设置下面列出的Java选项来控制此影响。

<table>
 <thead>
  <tr>
   <th><p>属性</p></th>
   <th><p>用途</p></th>
   <th><p>默认值</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>adobe.healthmonitor.enabled</p></td>
   <td><p>打开或关闭运行状况监视器线程</p></td>
   <td><p>true</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.statistics-enabled</p></td>
   <td><p>打开或关闭Gemfire缓存</p></td>
   <td><p>true</p></td>
  </tr>
  <tr>
   <td><p>adobe.healthmonitor.refresh-interval</p></td>
   <td><p>运行状况监控器线程收集统计信息之前的间隔（以毫秒为单位）</p></td>
   <td><p>10分钟（600,000毫秒）</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.multicast-port</p></td>
   <td><p>用于与分布式系统的其他成员通信的组播端口。 如果设置为0，则对成员发现和分发都禁用多播。 </p><p>注：为不同的分布式系统选择不同的多播地址和端口。 请勿仅使用不同的地址。</p></td>
   <td><p>无默认值。 有效值的范围为0到65535。</p></td>
  </tr>
  <tr>
   <td><p>statistics-sample-rate</p></td>
   <td><p>统计信息的采样速率（以毫秒为单位）。 只有在获取样本时，才会更新操作系统统计信息。</p></td>
   <td><p>600000</p></td>
  </tr>
  <tr>
   <td><p>adobe.workmanager.healthmonitor.enabled</p></td>
   <td><p>此属性启用或禁用Work Manager统计收集，如作业或工作项计数。</p></td>
   <td><p>true</p></td>
  </tr>
 </tbody>
</table>

## 将Java选项添加到JBoss {#add-java-options-to-jboss}

1. 停止JBoss应用程序服务器。
1. 打开 *[appserver根]*/bin/run.bat (Windows)或run.sh （Linux或UNIX），并根据需要添加任何Java选项。
1. 重新启动服务器。

## 将Java选项添加到WebLogic {#add-java-options-to-weblogic}

1. 键入https://以启动WebLogic管理控制台[主机名]： Web浏览器URL行中的“端口”/控制台。
1. 键入为WebLogic Server域创建的用户名和密码，然后单击更改中心下的日志，然后单击锁定和编辑。
1. 在“域结构”下，单击“环境”>“服务器”，然后在右窗格中，单击受控服务器名称。
1. 在下一个屏幕上，单击Configuration选项卡> Server Start选项卡。
1. 在“参数”框中，将所需的参数附加到当前内容的末尾。 例如，添加 —  `Dadobe.healthmonitor.enabled=false` 禁用Health Monitor。
1. 单击保存，然后单击激活更改。
1. 重新启动WebLogic托管服务器。

## 将Java选项添加到WebSphere {#add-java-options-to-websphere}

1. 在WebSphere管理控制台导航树中，对应用程序服务器执行以下操作：

   (WebSphere 6.x)单击“服务器”>“应用程序服务器”

   (WebSphere 7.x)单击服务器>服务器类型> WebSphere应用程序服务器

1. 在右窗格中，单击服务器名称。
1. 在“服务器基础架构”下，单击Java和表单工作流>进程定义。
1. 在“其他属性”下，单击“Java虚拟机”。
1. 在“通用JVM参数”框中，键入所需的参数。
1. 单击“确定”或“应用”，然后单击“直接保存到主控配置”。
