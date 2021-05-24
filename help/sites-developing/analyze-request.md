---
title: 请求分析脚本
seo-title: 请求分析脚本
description: 请求分析脚本的编写，旨在简化对access.log文件的分析，生成可读报告供以后处理
seo-description: 请求分析脚本的编写，旨在简化对access.log文件的分析，生成可读报告供以后处理
uuid: 24eff3c6-5748-46f3-a30c-4a3a6427ce1d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 1b5e0ccf-4157-45e3-8caf-1d6739d7d9d2
exl-id: e14a9cda-890f-46b7-9433-1b52eb91eae3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 2%

---

# 请求分析脚本{#request-analysis-script}

## 下载 {#download}

此脚本旨在简化对`access.log`文件的分析，这些文件会生成可读报告以供日后处理。

[获取文件](assets/analyse-access.sh)

## 描述 {#description}

此脚本旨在简化对`access.log`文件的分析，这些文件会生成可读报告以供日后处理。

它会生成总的请求数、GET与POST、随时间推移的请求分发等。

输出采用Markdown语法，因此使用pandoc等工具将其转换为PDF，或在带有Markdown查看器等插件的浏览器中显示将会更轻松。

它可以分析命令行上提供的自定义路径。

从告诉您如何运行该注释的文件中获取注释：

分析CQ `access.log`外推各种信息并在`stdout`上生成Markdown输出。

## 使用 {#usage}

`./analyse-access.sh access.log.2013-&ast;`

您可以提供其他自定义路径以在命令行上进行分析

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

可以通过简单的管道保存输出

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
