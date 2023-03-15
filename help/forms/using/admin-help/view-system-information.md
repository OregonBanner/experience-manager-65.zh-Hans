---
title: 查看系统信息
seo-title: View system information
description: 了解如何查看资源监控图表和有关运行AEM表单的服务器的信息。
seo-description: Learn how you can view resource monitoring charts and information about the server that is running AEM forms.
uuid: 983c1cc7-a8b3-48b2-a4c8-7b28a2e32537
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d51460d9-c96c-4661-b93e-e015427878ab
exl-id: 27a2e81c-47b0-4de8-95bd-7cb34b9450da
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# 查看系统信息 {#view-system-information}

“系统”选项卡显示资源监视图表和有关运行AEM表单的服务器的信息。 要访问此信息，请在管理控制台中单击页面右上角的运行状况监视器。 如果在群集环境中运行AEM表单，则显示的信息为从“服务器”列表中选择的节点的信息。

要将当前系统信息保存为属性文件，请单击“保存”。

“系统”选项卡的右侧窗格显示以下信息的图形表示：

* 作业和工作计数项
* 栈和已提交的栈使用情况
* 非栈和已提交的非栈使用情况

您可以沿时间轴拖动指针以获取特定时间点的值。

>[!NOTE]
>
>图形数据、服务器信息值和时钟时间每10分钟更新一次。 信息不会实时显示。

“系统”选项卡的左窗格显示有关服务器或节点的以下信息：

**虚拟机：** 服务器上的Java虚拟机(JVM)版本。

**虚拟机供应商：** JVM的制造商。

**虚拟机版本：** JVM版本号

**计算机名称：** 安装AEM forms的服务器的主机名。

**运行时间：** 服务器运行的时间，以小时和分钟为单位。

**即时编译器：** 正在使用的编译器的名称。

**编译时间：** 编译所花费的时间。

**实时线程数：** AEM Forms系统中当前存在的线程总数。

**峰值线程数：** 系统上记录的最大实时线程数。

**已加载类的数量：** 加载到JVM中的类数。

**已卸载类的数量：** 从JVM卸载的类数。

**最小栈：** 已使用的最小栈数量。

**最大栈：** 已使用的最大栈数量。

**操作系统名称：** AEM Forms服务器上运行的操作系统的名称。

**操作系统版本：** AEM forms服务器上运行的操作系统的版本号。

**操作系统拱门：** 运行JVM的操作系统体系结构。

**处理器数量：** 系统上的处理器数量。

**虚拟机参数：** JVM使用的参数。

**类路径：** JVM使用的类路径。

**库路径：** JVM使用的库路径。

**引导类路径：** JVM使用的引导类路径。

**应用程序服务器类型：** 用于运行AEM表单的应用程序服务器的类型。

**应用程序服务器版本：** 用于运行AEM表单的应用程序服务器的版本号。

**应用程序服务器供应商：** 用于运行AEM表单的应用程序服务器的制造商。

**安装日期：** 安装AEM表单的日期（格式为yyyy-mm-dd）。

**AEM Forms版本：** 已安装的AEM表单版本。

**修补程序版本：** AEM forms修补程序编号。

**数据库名称：** AEM表单使用的数据库类型。

**数据库版本：** AEM表单使用的数据库的版本号。

**数据库驱动器名称：** JVM用来连接到数据库的驱动程序的名称。

**数据库驱动程序版本：** JVM用来连接到数据库的驱动程序的版本。

此 **保存** 按钮可将此系统信息保存在属性文件中。
