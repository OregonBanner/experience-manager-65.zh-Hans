---
title: 请求分析脚本
seo-title: 请求分析脚本
description: 生成请求分析脚本以简化对access.log文件的分析，生成可读报告供以后处理
seo-description: 生成请求分析脚本以简化对access.log文件的分析，生成可读报告供以后处理
uuid: 24eff3c6-5748-46f3-a30c-4a3a6427ce1d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 1b5e0ccf-4157-45e3-8caf-1d6739d7d9d2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 请求分析脚本{#request-analysis-script}

## 下载 {#download}

此脚本可简化对生成可读报告的文 `access.log` 件的分析，以便日后处理。

[获取文件](assets/analyse-access.sh)

## 描述 {#description}

此脚本可简化对生成可读报告的文 `access.log` 件的分析，以便日后处理。

它生成总的请求编号、GET与POST、随时间的请求分发等。

输出采用Markdown语法，因此使用pandoc等工具将其转换为PDF或在浏览器中显示它并带有Markdown查看器等增效工具。

它可以分析命令行上提供的自定义路径。

从告诉您如何运行该注释的文件中获取注释：

分析CQ外 `access.log` 推各种信息并在上生成Markdown输出 `stdout`。

## 使用情况 {#usage}

`./analyse-access.sh access.log.2013-&ast;`

您可以提供其他自定义路径以在命令行上进行分析

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

可以通过简单的管道保存输出

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
