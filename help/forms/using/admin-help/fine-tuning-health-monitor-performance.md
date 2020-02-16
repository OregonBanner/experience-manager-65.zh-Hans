---
title: 微调运行状况监视器性能
seo-title: 微调运行状况监视器性能
description: 了解如何微调运行状况监视器性能
seo-description: 了解如何微调运行状况监视器性能
uuid: 770b10cb-065f-41b5-9594-a291e4311151
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b8f8bddc-0d38-4d5e-b33f-978f04bc16c6
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 微调运行状况监视器性能{#fine-tuning-health-monitor-performance}

收集填充运行状况监视器的系统统计信息会对AEM表单环境的性能产生一定影响。 可通过设置应用程序服务器中下面列出的Java选项来控制此影响。

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
   <td><p>打开或关闭健康监视器线程</p></td>
   <td><p>true</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.statistics已启用</p></td>
   <td><p>打开或关闭Gemfire缓存</p></td>
   <td><p>true</p></td>
  </tr>
  <tr>
   <td><p>adobe.healthmonitor.refresh_interval</p></td>
   <td><p>健康监视器线程收集统计信息的间隔（以毫秒为单位）</p></td>
   <td><p>10分钟（600,000毫秒）</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.multicast-port</p></td>
   <td><p>用于与分布式系统的其他成员通信的多播端口。 如果设置为零，则对于成员发现和分发都禁用多播。 </p><p>注意：为不同的分布式系统选择不同的多播地址和端口。 请勿仅使用不同的地址。</p></td>
   <td><p>无默认值。 有效值的范围是0到65535。</p></td>
  </tr>
  <tr>
   <td><p>统计采样率</p></td>
   <td><p>统计数据采样的速率（以毫秒为单位）。 操作系统统计信息仅在采取示例时更新。</p></td>
   <td><p>600000</p></td>
  </tr>
  <tr>
   <td><p>adobe.workmanager.healthmonitor.enabled</p></td>
   <td><p>此属性可启用或禁用“工作管理者”统计信息收集，如作业或工作项计数。</p></td>
   <td><p>true</p></td>
  </tr>
 </tbody>
</table>

## 向JBoss添加Java选项 {#add-java-options-to-jboss}

1. 停止JBoss应用程序服务器。
1. 在编 *[辑器中打]*&#x200B;开appserver root /bin/run.bat(Windows)或run.sh（Linux或UNIX），并根据需要添加任何Java选项。
1. 重新启动服务器。

## 将Java选项添加到WebLogic {#add-java-options-to-weblogic}

1. 通过在Web浏览器的URL行中键入https://[主机名]:[port]/console，启动WebLogic管理控制台。
1. 键入您为WebLogic服务器域创建的用户名和密码，然后单击“更改中心”下的“日志”，然后单击“锁定并编辑”。
1. 在“域结构”下，单击“环境”>“服务器”，在右侧窗格中单击受控服务器名称。
1. 在下一个屏幕上，单击“配置”选项卡>“服务器开始”选项卡。
1. 在“参数”框中，将所需的参数追加到当前内容的末尾。 例如，添加——禁 `Dadobe.healthmonitor.enabled=false` 用健康监视器。
1. 单击保存，然后单击激活更改。
1. 重新启动WebLogic托管服务器。

## 将Java选项添加到WebSphere {#add-java-options-to-websphere}

1. 在WebSphere管理控制台导航树中，为应用程序服务器执行以下操作：

   (WebSphere 6.x)单击“服务器”>“应用程序服务器”

   (WebSphere 7.x)单击“服务器”>“服务器类型”>“WebSphere应用程序服务器”

1. 在右窗格中，单击服务器名称。
1. 在“服务器基础结构”下，单击“Java”和“表单工作流”>“进程定义”。
1. 在“其他属性”下，单击“Java虚拟机”。
1. 在“通用JVM参数”框中，键入所需的参数。
1. 单击“确定”或“应用”，然后单击“直接保存到主配置”。

