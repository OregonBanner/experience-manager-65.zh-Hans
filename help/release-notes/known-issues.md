---
title: 已知问题
description: 针对Adobe Experience Manager6.5已知问题的发行说明
translation-type: tm+mt
source-git-commit: 8d60e064ab50f24016c049c8d5d0fceb784c99a3
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 46%

---


# 已知问题 {#known-issues}

此页面列出了于 2019 年 4 月发布的 Adobe Experience Manager 6.5 中存在的已知问题列表。

如果您需要了解有关已知问题的更多信息，请[联系支持人员](https://helpx.adobe.com/cn/support/experience-manager.html)。

## 平台 {#platform}

* 报告删除CRX快速启动及其内容的问题。

   在每个操作中，确保属性`htmllibmanager.fileSystemOutputCacheLocation`不是空字符串：

   1. 正在调用`/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`。
   2. 升级到AEM 6.5。
   3. 在AEM 6.5上执行“延迟内容迁移”。

   有一篇[知识库](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html)文章，提供进一步的详细信息以及解决此问题的解决方法。

* 如果将JDK 11与AEM 6.5实例一起使用，则部署某些包后，某些页面可能显示为空。 日志文件中显示以下错误消息：

   ```java
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

要解决此错误，请执行以下操作：

1. 停止AEM实例。 转到`<aem_server_path_on_server>crx-quickstart\conf`并打开`sling.properties`文件。 Adobe建议备份此文件。

1. 搜索 `org.osgi.framework.bootdelegation=`. 添加`jdk.internal.reflect,jdk.internal.reflect.*`属性，将结果显示为。

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. 保存文件并重新启动AEM实例。

## 资产 {#assets}

* **搜索：** 如果搜索字符串包含前导空格，则搜索不会产生任[何返回(OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **文件夹元数据架构**：添加选择按钮后，ID 和值字段未按预期呈现，且删除功能不起作用。(CQ-4261144)
* 重命名资产时，无法在资产名称中使用空格。(CQ-4266403)

## 表单 {#forms}

* 当AEM Forms安装在Linux操作系统上时，带硬件安全模块的数字签名不起作用。 (CQ-4266721)
* （仅限 WebSphere 上的 AEM Forms）如果您将&#x200B;**用户名**&#x200B;作为搜索条件搜索&#x200B;**管理员**，则 **Forms 工作流** > **任务搜索**&#x200B;选项不会返回任何结果。(CQ-4266457)

* AEM Forms无法将JPEG压缩的TIF和TIFF文件转换为PDF文档。 (CQ-4265972)
* **AEM Forms 迁移**&#x200B;页面上的 **AEM Forms 资产扫描程序**&#x200B;和&#x200B;**交互式通信迁移字符**&#x200B;选项不起作用。(CQ-4266572)

* （仅限JBoss 7）从先前版本升级到AEM 6.5Forms，且先前版本包含创建和使用默认提交或默认渲染进程副本的进程(.lca)，使用此类进程(.lca)的HTML5Forms将无法执行所需的操作。 (CQ-4243928)
* 在自适应表单中，当从规则编辑器调用表单数据模型服务以动态更新图像选项组件的值时，不会更新图像选项组件的值。(CQ-4254754)
* AEM Forms设计器安装程序需要32位版本的[Visual C++可再发行运行时包2012](https://support.microsoft.com/zh-cn/help/2977003/the-latest-supported-visual-c-downloads)和[Visual C++可再发行运行时包2013](https://support.microsoft.com/zh-cn/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package)。 确保在开始安装之前已安装上述可再发行运行时包。(CQ-4265668)

* PDF Generator不支持基于智能卡的身份验证。  当管理员在Windows服务器上启用组策略`Interactive Logon: Require Smart card`时，所有现有PDF Generator用户都将失效。

* 当自适应表单配置为动态更新组件的值并且通过调度程序访问托管表单的发布实例时，动态更新字段值的功能将停止工作。要解决此问题，请在发布实例中打开CRXDE，导航到`/libs/fd/af/runtime/clientlibs/guideChartReducer`，然后创建下面列出的属性。

   * 名称：allowProxy
   * 类型：布尔型
   * 值：true
   * 受保护：False
   * 必填：False
   * 多选：False
   * 自动创建：False

   该属性让运行时文件夹下的客户端库可以访问代理。(CQ-4268679)

* 启动AEM Forms时，将显示`SAX Security Manager could not be setup`警告。
