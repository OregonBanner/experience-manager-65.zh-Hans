---
title: 网络注意事项和要求
description: 讨论设计 [!DNL Adobe Experience Manager Assets] 部署时的网络注意事项。
contentOwner: AG
role: 架构师、管理员
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 0%

---


# [!DNL Assets] 网络注意事项  {#assets-network-considerations}

了解网络与了解[!DNL Adobe Experience Manager Assets]同样重要。 网络可能影响上传、下载和用户体验。 绘制网络拓扑图有助于确定网络中的瓶颈点和次优化区域，您必须修复这些区域以提高网络性能和用户体验。

确保在网络图中包含以下内容：

* 从客户端设备（例如，计算机、移动设备和平板电脑）到网络的连接。
* 公司网络的拓扑。
* 从公司网络和[!DNL Experience Manager]环境上行到Internet。
* [!DNL Experience Manager]环境的拓扑。
* 定义[!DNL Experience Manager]网络接口的同时使用者。
* 已定义[!DNL Experience Manager]部署的工作流。

## 从客户端设备到公司网络的连接{#connectivity-from-the-client-device-to-the-corporate-network}

首先绘制单个客户端设备与公司网络之间的连接图。 在此阶段，识别共享资源，如WiFi连接，其中多个用户访问同一点或以太网交换机以上传和下载资源。

![chlimage_1-353](assets/chlimage_1-353.png)

客户端设备以各种方式连接到企业网络，如共享WiFi、以太网到共享交换机和VPN。 确定和了解此网络上的阻塞点对于[!DNL Assets]规划和修改网络非常重要。

在图的左上角，有三台设备被描述为共享一个48 Mbps WiFi接入点。 如果所有设备同时上传，则设备之间共享WiFi网络带宽。 与整个系统相比，用户可能在这个分割渠道上遇到三个客户的不同的阻塞点。

测量WiFi网络的真实速度是一个挑战，因为速度较慢的设备可能会影响接入点上的其他客户端。 如果您计划将WiFi用于资产交互，请同时从多个客户端执行速度测试以评估吞吐量。

图的左下角描述了通过独立渠道连接到公司网络的两个设备。 因此，每个设备的最低速度为10 Mbps和100 Mbps。

在右侧显示的计算机在VPN上有一个有限的上游，其速度为1 Mbps。 1Mbps连接的用户体验与1Gbps连接上的用户体验截然不同。 根据用户与之交互的资产的大小，其VPN上行链路可能不足以任务。

## 公司网络的拓扑{#topology-of-the-corporate-network}

![chlimage_1-354](assets/chlimage_1-354.png)

该图表显示公司网络内的上行链路速度高于通常使用的上行链路速度。 这些管道是共享资源。 如果共享交换机应处理50个客户端，它可能是一个阻塞点。 在初始图中，只有两台计算机共享特定连接。

## 从公司网络和[!DNL Experience Manager]环境{#uplink-to-the-internet-from-the-corporate-network-and-aem-environment}上行到因特网

![chlimage_1-355](assets/chlimage_1-355.png)

在Internet和VPC连接上考虑未知因素很重要，因为峰值负载或大规模提供商停机可能会损害互联网带宽。 一般而言，Internet连接可靠。 然而，它有时会引入一些障碍。

在从企业网络到互联网的上行链路上，可以使用带宽的其他服务。 了解资产的专用带宽或优先级带宽的多少非常重要。 例如，如果1 Gbps链路的利用率已经达到80%，则您最多只能为[!DNL Experience Manager Assets]分配20%的带宽。

企业防火墙和代理还可以通过多种不同的方式影响带宽。 此类设备可以使用服务质量、每个用户的带宽限制或每个主机的比特率限制来确定带宽优先级。 这些是要检查的重要要点，因为它们会显着影响[!DNL Assets]用户体验。

在此示例中，企业有10 Gbps上行链路。 它应该足够大，可以容纳多个客户。 此外，防火墙对主机速率的限制为10 Mbps。 此限制可能会将到单台主机的通信量限制为10 Mbps，即使到互联网的上行链路为10 Gbps。

这是最小的、面向客户端的瓶颈。 但是，您可以评估是否更改或配置负责此防火墙的网络操作组的允许列表。

从示例图中，您可以得出六个设备共享概念性的10Mbps渠道。 根据杠杆资产的规模，这可能不足以满足用户预期。

## [!DNL Experience Manager]环境{#topology-of-the-aem-environment}的拓扑

![chlimage_1-356](assets/chlimage_1-356.png)

设计[!DNL Experience Manager]环境的拓扑需要详细了解系统配置以及网络在用户环境内的连接方式。

示例方案包括一个包含五台服务器的发布场、一个S3二进制存储区和已配置的Dynamic Media。

调度程序与两个实体（外部世界和[!DNL Experience Manager]部署）共享100Mbps的连接。 对于同时上传和下载操作，应将此数字除以二。 连接的外部存储使用单独的连接。

[!DNL Experience Manager]部署与多个服务共享其1Gbps连接。 从网络拓扑的角度看，这等同于与不同服务共享单个渠道。

查看从客户端设备到[!DNL Experience Manager]部署的网络，最小的瓶颈似乎是10 Mbit企业防火墙限制。 您可以在[资产规模调整指南](assets-sizing-guide.md)中的大小调整计算器中使用这些值来确定用户体验。

## [!DNL Experience Manager]部署{#defined-workflows-of-the-aem-deployment}的已定义工作流

在考虑网络性能时，考虑系统中将发生的工作流和发布可能很重要。 此外，您使用的S3或其他网络连接存储和I/O请求会消耗网络带宽。 因此，即使在完全优化的网络中，性能也可能受到磁盘I/O的限制。

要简化资产摄取（尤其是上传大量资产时）的流程，请浏览资产工作流并了解有关其配置的更多信息。

在评估内部工作流拓扑时，您应分析以下内容：

* 编写资产的过程
* 工作流/事件在修改资产/元数据时触发
* 读取资产的过程

以下是需要考虑的一些项目：

* XMP元数据读/回
* 自动激活和复制
* 添加水印
* 子资产引入/页面提取
* 重叠工作流。

以下是资产工作流定义的客户示例。

![chlimage_1-357](assets/chlimage_1-357.png)
