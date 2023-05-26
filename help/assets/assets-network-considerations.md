---
title: 网络注意事项和要求
description: 讨论设计应用程序时的网络注意事项 [!DNL Adobe Experience Manager Assets] 部署。
contentOwner: AG
role: Architect, Admin
feature: Developer Tools
exl-id: 1313842c-18b1-4727-ba63-b454d0f5a2cc
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# [!DNL Assets] 网络注意事项 {#assets-network-considerations}

了解您的网络与了解一样重要 [!DNL Adobe Experience Manager Assets]. 网络可能会影响上传、下载和用户体验。 绘制网络拓扑图有助于识别网络中的瓶颈点和子优化区域，您必须修复这些区域才能提高网络性能和改善用户体验。

确保网络图中包含以下内容：

* 从客户端设备（例如，计算机、移动设备和平板电脑）到网络的连接。
* 公司网络的拓扑。
* 从公司网络和 [!DNL Experience Manager] 环境。
* 的拓扑 [!DNL Experience Manager] 环境。
* 定义的同时使用者 [!DNL Experience Manager] 网络接口。
* 已定义的工作流 [!DNL Experience Manager] 部署。

## 从客户端设备到公司网络的连接 {#connectivity-from-the-client-device-to-the-corporate-network}

首先绘制单个客户端设备与公司网络之间的连接图。 在此阶段，确定多个用户访问同一点或以太网交换机以上传和下载资产的共享资源，例如WiFi连接。

![chlimage_1-353](assets/chlimage_1-353.png)

客户端设备通过各种方式连接到公司网络，例如共享WiFi、到共享交换机的以太网和VPN。 识别和了解此网络上的瓶颈点对于以下方面很重要 [!DNL Assets] 规划和修改网络。

图左上角将三个设备描述为共享48 Mbps WiFi接入点。 如果所有设备同时上传，则设备之间共享WiFi网络带宽。 与系统整体相比，用户可能在这个划分的信道上遇到三个客户端的不同阻塞点。

测量WiFi网络的真实速度是一项挑战，因为速度慢的设备可能会影响接入点上的其他客户端。 如果您计划使用WiFi进行资产交互，请同时从多个客户端执行速度测试以评估吞吐量。

该图的左下角显示了通过独立通道连接到公司网络的两个设备。 因此，每个设备的最低速度可以是10 Mbps和100 Mbps。

右侧显示的计算机通过速度为1 Mbps的VPN有限地上游到公司网络。 1Mbps连接的用户体验与1Gbps连接的用户体验大不相同。 根据用户与之交互的资产大小，他们的VPN上行链路可能不足以完成任务。

## 公司网络的拓扑 {#topology-of-the-corporate-network}

![chlimage_1-354](assets/chlimage_1-354.png)

该图显示了公司网络内比一般使用的上行链路速度更快的上行链路速度。 这些管道是共享资源。 如果共享交换机需要处理50个客户端，则它可能是瓶颈。 在初始图表中，只有两台计算机共享特定连接。

## 从公司网络和 [!DNL Experience Manager] 环境 {#uplink-to-the-internet-from-the-corporate-network-and-aem-environment}

![chlimage_1-355](assets/chlimage_1-355.png)

请务必考虑Internet和VPC连接上的未知因素，因为因特网的带宽可能因峰值负载或大规模提供商中断而受损。 通常，Internet连接是可靠的。 但是，它有时可能会引入瓶颈。

在从公司网络到Internet的上行链路上，可以使用带宽进行其他服务。 了解多少带宽可以专用于资产或排定其优先顺序非常重要。 例如，如果1 Gbps链路的利用率已经达到80% ，则您最多只能为分配20%的带宽 [!DNL Experience Manager Assets].

企业防火墙和代理还可以通过多种不同的方式调整带宽。 此类设备可以使用服务质量、每个用户的带宽限制或每个主机的比特率限制来排定带宽优先级。 这些是需要检查的重要瓶颈，因为它们可以产生重大影响 [!DNL Assets] 用户体验。

在此示例中，企业具有10 Gbps的上行链路。 它应该足够大，可容纳多个客户。 此外，防火墙还设置了10 Mbps的主机速率限制。 即使到Internet的上行链路速度为10 Gbps，此限制也可能将单台主机的通信量限制为10 Mbps。

这是最小的面向客户的瓶颈。 但是，您可以通过负责此防火墙的网络操作组评估更改或配置允许列表。

从示例图中，您可以得出以下结论：六台设备共享一个10Mbps的概念信道。 根据利用的资产规模，这可能不足以满足用户期望。

## 的拓扑 [!DNL Experience Manager] 环境 {#topology-of-the-aem-environment}

![chlimage_1-356](assets/chlimage_1-356.png)

设计拓扑结构 [!DNL Experience Manager] 环境要求详细了解系统配置以及用户环境中网络连接的方式。

此示例场景包含一个发布场，其中配置了五台服务器、一个S3二进制存储区以及一个Dynamic Media。

Dispatcher与两个实体(外部世界和 [!DNL Experience Manager] 部署。 对于同时上载和下载操作，应将此数字除以2。 连接的外部存储使用单独的连接。

此 [!DNL Experience Manager] 部署与多个服务共享1Gbps连接。 从网络拓扑的角度来看，它等同于使用不同的服务共享单个信道。

检查从客户端设备到 [!DNL Experience Manager] 部署时，最小的瓶颈似乎是10 Mbit企业防火墙限制。 您可以在的大小计算器中使用以下值： [Assets大小调整指南](assets-sizing-guide.md) 以确定用户体验。

## 已定义的工作流 [!DNL Experience Manager] 部署 {#defined-workflows-of-the-aem-deployment}

在考虑网络性能时，可能必须考虑系统中将发生的工作流和发布。 此外，您使用和I/O请求的S3或其他网络连接存储占用了网络带宽。 因此，即使在完全优化的网络中，性能也可能受到磁盘I/O的限制。

要简化资产摄取流程（特别是在上传大量资产时），请探索资产工作流并详细了解其配置。

在评估内部工作流拓扑时，应分析以下内容：

* 编写资产的过程
* 修改资产/元数据时触发的工作流/事件
* 读取资产的过程

以下是需要考虑的一些项目：

* XMP元数据读/写
* 自动激活和复制
* 水印
* 子资产提取/页面提取
* 重叠的工作流。

以下是定义资产工作流的客户示例。

![chlimage_1-357](assets/chlimage_1-357.png)
