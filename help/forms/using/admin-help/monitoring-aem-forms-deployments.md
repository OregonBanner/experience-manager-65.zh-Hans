---
title: 监视AEM表单部署
seo-title: 监视AEM表单部署
description: 您可以从系统级和内部级监控AEM表单部署。 通过此文档进一步了解如何监视AEM表单部署。
seo-description: 您可以从系统级和内部级监控AEM表单部署。 通过此文档进一步了解如何监视AEM表单部署。
uuid: 032b7a93-3069-4ad5-a8c6-4c160f290669
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b3e7bca0-5aaf-4f28-bddb-fd7e8ed72ee8
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# 监视AEM表单部署 {#monitoring-aem-forms-deployments}

您可以从系统级和内部级监控AEM表单部署。 您可以使用专门的管理工具（如HP OpenView、IBM Tivoli和CA UniCenter）以及名为JConsole的第三方JMX监 *视器* ，专门监视Java活动。 实施监控战略可提高AEM表单部署的可用性、可靠性和性能。

有关监视AEM表单部署的更多信息，请参 [阅用于监视AEM表单部署的技术指南](https://www.adobe.com/devnet/livecycle/pdfs/lc_monitoring_wp_ue.pdf)。

## 使用MBean进行监视 {#monitoring-using-mbeans}

AEM表单提供两个注册的MBean，它们提供导航和统计信息。 这些是支持集成和检查的唯一MBean:

* **服务统计：** 此MBean提供有关服务名称及其版本的信息。
* **操作统计：** 此MBean提供每个表单服务器服务的统计信息。 管理员可在此处获取有关特定服务的信息，如调用时间、错误数等。

### ServiceStatisticMbean公共接口 {#servicestatisticmbean-public-interfaces}

ServiceStatistic MBean的这些公共接口可用于测试目的：

```java
 public String getServiceId();
 public int getMajorVersion();
 public int getMinorVersion();
```

### OperationStatisticMbean公共接口 {#operationstatisticmbean-public-interfaces}

OperationStatistic MBean的这些公共接口可用于测试目的：

```java
 // InvocationCount: The number of times the method is invoked.
 public long getInvocationCount();
 // InvocationStartTime: The time at which the method started to execute.
 public long getInvocationStartTime();
 // InvocationEndTime: The time at which the method finished execution.
 public long getInvocationEndTime();
 // InvocationTime: The time taken for the execution of the method.
 public long getInvocationTime();
 // LastSamplingDateTime: Convert InvocationStartTime to a formatted string
 public String getLastSamplingDateTime();
 // MaxInvocationTime: The maximum time taken for the execution of the method.
 public long getMaxInvocationTime();
 // MinInvocationTime: The minimum time taken for the execution of the method.
 public long getMinInvocationTime();
 // AverageInvocationTime: the averege execution time taken for the execution of the method.
 public double getAverageInvocationTime();
 // ExceptionCount: The number of times the method has thrown an Exception.
 public long getExceptionCount();
 // ExceptionMessage: The message of the last exception occurred.
 public String getExeptionMessage();
 public void setExceptionMessage(String errorMessage);
```

### MBean树和操作统计 {#mbean-tree-operation-statistics}

使用JMX控制台(JConsole)，可以使用OperationStatistic MBean中的统计信息。 这些统计信息是MBean的属性，可以在以下层次树下导航：

**MBean树**

**Adobe域名：** 取决于应用程序服务器。 如果应用程序服务器未定义域，则默认为adobe.com。

**服务类型：** AdobeService是用于列表所有服务的名称。

**AdobeServiceName:** 服务名称或服务ID。

**版本：** 服务的版本。

**操作统计**

**调用时间：** 执行方法所花费的时间。 这不包括请求序列化、从客户端传输到服务器以及反序列化的时间。

**调用计数：** 调用服务的次数。

**平均调用时间：** 服务器启动后执行的所有调用的平均时间。

**最大调用时间：** 自服务器启动以来执行的最长调用的持续时间。

**最小调用时间：** 自服务器启动以来执行的最短调用的持续时间。

**异常计数：** 导致失败的调用数。

**异常消息：** 发生的最后一个异常的错误消息。

**上次采样日期时间：** 上次调用的日期。

**时间单位：** 默认值为毫秒。

要启用JMX监控，应用程序服务器通常需要一些配置。 有关具体信息，请参阅应用程序服务器文档。

### 如何设置开放式JMX访问的示例 {#examples-of-how-to-set-up-open-jmx-access}

**JBoss 4.0.3/4.2.0 —— 配置JVM启动**

要从JConsole视图MBean，请配置JBoss应用程序服务器的JVM启动参数。 确保从run.bat/sh文件启动JBoss。

1. 编辑位于InstallJBoss/bin下的run.bat文件。
1. 找到JAVA_OPTS行并添加以下内容：

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

**WebLogic 9.2 /10 —— 配置JVM启动**

1. 编辑位于下方的startWebLogic.bat文件 `[WebLogic home]/user_projects/domains/Adobe_Live_Cycle/bin`。
1. 找到JAVA_OPTS行并添加以下内容：

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

1. 重新启动WebLogic。

>[!NOTE]
>
>对于WebLogic，您可以使用远程或IIOP访问MBean。

**远程访问MBean**

1. 启动JConsole进行新连接，然后单击“远程”选项卡。
1. 输入主机名和端口(9088，在JVM的开始选项中指定的编号)。

**Websphere 6.1 —— 配置JVM启动**

1. 在管理控制台（应用程序服务器> server1 >进程定义> JVM）上，将以下代码行添加到“通用JVM参数”字段中：

   ```shell
    -Djavax.management.builder.initial= -Dcom.sun.management.jmxremote
   ```

1. 在/opt/IBM/WebSphere/AppServer/java/jre/lib/management/management.properties文件(或&lt;Your Websphere JRE>/ lib/management/management.properties)中添加或取消以下三行注释：

   ```shell
    com.sun.management.jmxremote.port=9999 //any port you like, but make sure you use this port when you connect
    com.sun.management.jmxremote.authenticate=false
    com.sun.management.jmxremote.ssl=false
   ```

1. 重新启动WebSphere。

