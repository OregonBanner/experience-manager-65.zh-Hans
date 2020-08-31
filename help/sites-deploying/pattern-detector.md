---
title: 利用模式检测器评估升级复杂度
seo-title: 利用模式检测器评估升级复杂度
description: 了解如何使用模式检测器来评估升级的复杂性。
seo-description: 了解如何使用模式检测器来评估升级的复杂性。
uuid: 84d0add9-3123-4188-9877-758911b1899f
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: b5607343-a13b-4520-a771-f1a555bfcc7b
docset: aem65
translation-type: tm+mt
source-git-commit: 9a4ae73c08657195da2741cccdb196bd7f7142c9
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 1%

---


# 利用模式检测器评估升级复杂度{#assessing-the-upgrade-complexity-with-the-pattern-detector}

## 概述 {#overview}

此功能允许您通过检测使用的模式检查现有AEM实例的可升级性：

1. 违反某些规则，在受升级影响或覆盖的区域执行
1. 使用AEM 6.x功能或AEM 6.5上不向后兼容的API，在升级后可能会中断。

这可作为对升级至AEM 6.5所涉发展工作的评估。

## 如何设置 {#how-to-set-up}

模式检测器作为一个软件包单独 [发布](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/compatpack/pd-all-aem65) ，它可处理任何源AEM版本（从6.1到6.5），目标是AEM 6.5升级。 可以使用包管理器 [安装它](/help/sites-administering/package-manager.md)。

## 使用方法 {#how-to-use}

>[!NOTE]
>
>图案检测器可以运行于任何环境，包括本地开发实例。 但是，为了：
>
>* 提高检测率
>* 避免业务关键型实例出现任何缓慢


>同时，建议在登台环境上 **运行它** ，这些在用户应用程序、内容和配置方面尽可能接近生产应用程序。
>
可以使用多种方法检查图案检测器输出：

* **通过Felix Inventory控制台：**

1. 通过浏览至https://serveraddress:serverport/system/console/configMgr，转到AEM Web *Console*
1. 选择 **状态——图案检测器** ，如下图所示：

   ![screeston-2018-2-5pattern-detector](assets/screenshot-2018-2-5pattern-detector.png)

* **通过基于反应文本或常规JSON界面**

* **通过反应式JSON行界面，**可在每行中生成单独的JSON文档。

下面介绍了这两种方法：

## 反应接口 {#reactive-interface}

该被动接口允许在检测到怀疑后立即处理违规报告。

输出当前位于2个URL下：

1. 纯文本界面
1. JSON界面

## 处理纯文本界面 {#handling-the-plain-text-interface}

输出中的信息将格式化为一系列事件条目。 有两个渠道-一个用于发布违规，另一个用于发布当前进度。

可以使用以下命令获取它们：

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep SUSPICION
```

输出将如下所示：

```
2018-02-13T14:18:32.071+01:00 [SUSPICION] The pattern=ECU/extraneous.content.usage was found by detector=ContentAccessDetector with id=a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f message="Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid". More info at=https://www.adobe.com/go/aem6_EC
```

可以使用以下命令过滤进 `grep` 度：

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep PROGRESS
```

这将导致以下输出：

```
2018-02-13T14:19:26.909+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=45780/16 MB items, found=0 suspicions so far in period=PT5.005S (throughput=34667 items/sec)
2018-02-13T14:19:31.904+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=106050/39 MB items, found=0 suspicions so far in period=PT10S (throughput=23378 items/sec)
2018-02-13T14:19:35.685+01:00 [PROGRESS] Finished in period=PT13.782
```

## 处理JSON界面 {#handling-the-json-interface}

同样，JSON发布后可 [使用jq](https://stedolan.github.io/jq/) 工具进行处理。

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == true)'
```

输出：

```
{
  "timestamp": "2018-02-13T14:20:18.894+01:00",
  "suspicion": true,
  "pattern": {
    "code": "ECU",
    "type": "extraneous.content.usage",
    "detective": "ContentAccessDetector",
    "moreInfo": "https://www.adobe.com/go/aem6_ECU"
  },
  "item": {
    "id": "a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f",
    "message": "Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid"
  }
}
```

进度每5秒报告一次，除标记为怀疑的邮件外，还可排除其他邮件来获取：

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == false)'
```

输出：

```
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:17.279+01:00",
  "type": "PROGRESS",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 57209,
    "itemsAnalysedSize": "26 MB",
    "suspicionsFound": 0
  },
  "progress": {
    "elapsedTime": "PT5.003S",
    "elapsedTimeMilliseconds": 5003,
    "itemsPerSecond": 36965
  }
}
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:22.276+01:00",
  "type": "PROGRESS",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 113194,
    "itemsAnalysedSize": "46 MB",
    "suspicionsFound": 0
  },
  "progress": {
    "elapsedTime": "PT10S",
    "elapsedTimeMilliseconds": 10000,
    "itemsPerSecond": 24092
  }
}
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:25.762+01:00",
  "type": "FINISHED",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 140744,
    "itemsAnalysedSize": "63 MB",
    "suspicionsFound": 1
  },
  "progress": {
    "elapsedTime": "PT13.486S",
    "elapsedTimeMilliseconds": 13486,
    "itemsPerSecond": 19907
  }
}
{
  "suspicion": false,
  "type": "SUMMARY",
  "suspicionsFound": 1,
  "totalTime": "PT13.487S"
}
```

>[!NOTE]
建议的方法是将卷起的整个输出保存到文件中，然后通过或过滤 `jq` 信息 `grep` 类型对其进行处理。

## 检测范围 {#scope}

当前模式检测器允许检查：

* OSGi捆绑了导出和导入不匹配
* Sling资源类型和超类型（带有搜索路径内容叠加）叠加用法
* Oak索引定义（兼容性）
* VLT包（超额使用）
* rep：用户节点兼容性（在OAuth配置上下文中）

>[!NOTE]
请注意，模式检测器会尝试准确预测升级警告。 但是，在某些情况下，它可能会产生误报。

