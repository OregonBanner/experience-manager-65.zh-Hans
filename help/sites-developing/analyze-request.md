---
title: 请求分析脚本
seo-title: Request Analysis Script
description: 制作request analysis脚本是为了便于分析access.log文件，从而生成可读报告供以后处理
seo-description: The request analysis script is made to ease the analysis of the access.log files producing a readable report for later processing
uuid: 24eff3c6-5748-46f3-a30c-4a3a6427ce1d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 1b5e0ccf-4157-45e3-8caf-1d6739d7d9d2
exl-id: e14a9cda-890f-46b7-9433-1b52eb91eae3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 2%

---

# 请求分析脚本{#request-analysis-script}

## 下载 {#download}

编写此脚本是为了便于分析 `access.log` 生成可读报告以供以后处理的文件。

[获取文件](assets/analyse-access.sh)

## 描述 {#description}

编写此脚本是为了便于分析 `access.log` 生成可读报告以供以后处理的文件。

它可以生成整体请求数、GET与POST、请求随时间推移的分布等等。

输出采用Markdown语法，因此将输出转换为使用pandoc等PDF或使用Markdown查看器等插件在浏览器中显示的工具会更容易。

它可以分析命令行上提供的自定义路径。

从文件中指明如何运行该程序的注释获取：

分析CQ `access.log` 推断各种信息并生成Markdown输出 `stdout`.

## 用途 {#usage}

`./analyse-access.sh access.log.2013-&ast;`

您可以在命令行中提供其他要分析的自定义路径

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

可通过简单管道保存输出

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
