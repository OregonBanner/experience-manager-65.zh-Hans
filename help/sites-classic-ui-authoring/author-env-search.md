---
title: 搜索
description: AEM 的创作环境提供了多种内容搜索机制，具体取决于资源类型。
uuid: 6dd3df4d-6040-4230-8373-fc028687b675
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 8d32960c-47c3-4e92-b02e-ad4d8fea7b2d
docset: aem65
exl-id: 1f46a57f-4966-4dd1-8c99-c0740718ae76
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 10%

---

# 搜索{#searching}

AEM 的创作环境提供了多种内容搜索机制，具体取决于资源类型。

>[!NOTE]
>
>在创作环境之外，还可以使用其他机制进行搜索，例如 [查询生成器](/help/sites-developing/querybuilder-api.md) 和 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

## 搜索基础知识 {#search-basics}

要访问搜索面板，请单击 **Search** 选项卡，该选项卡位于相应控制台的左窗格顶部。

![chlimage_1-101](assets/chlimage_1-101.png)

通过搜索面板，您可以搜索所有网站页面。 它包含用于以下各项的字段和小部件：

* **全文**：搜索指定的文本
* **修改于以下日期之后/之前**：仅搜索在特定日期之间更改的页面
* **模板**：仅搜索基于指定模板的页面
* **标记**：仅搜索具有指定标记的页面

>[!NOTE]
>
>当实例配置为时 [Lucene搜索](/help/sites-deploying/queries-and-indexing.md) 您可以在以下位置使用下列命令： **全文**：
>
>* [通配符](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Wildcard_Searches)
>* [布尔运算符](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boolean_operators)
>
>* [正则表达式](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Regexp_Searches)
>* [字段分组](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Field_Grouping)
>* [提升](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boosting_a_Term)
>

通过单击执行搜索 **Search** 位于窗格底部。 单击 **重置** 以清除搜索条件。

## 过滤器 {#filter}

在不同的位置，可以设置（和清除）过滤器以向下钻取并优化您的视图：

![chlimage_1-102](assets/chlimage_1-102.png)

## 查找和替换 {#find-and-replace}

在 **网站** 控制台a **查找并替换** 菜单选项允许您在网站的部分中搜索和替换字符串的多个实例。

1. 选择要执行查找和替换操作的根页面或文件夹。
1. 选择 **工具** 则 **查找并替换**：

   ![screen_shot_2012-02-15at120346pm](assets/screen_shot_2012-02-15at120346pm.png)

1. 此 **查找并替换** 对话框执行以下操作：

   * 确认查找操作应从何处开始的根路径
   * 定义要找到的术语
   * 定义应替换它的术语
   * 指示搜索是否应区分大小写
   * 指示是否只应找到全字（否则还会找到子字符串）

   点击 **预览** 列出搜索词的位置。 您可以选择/清除要替换的特定实例：

   ![screen_shot_2012-02-15at120719pm](assets/screen_shot_2012-02-15at120719pm.png)

1. 单击 **替换** 以实际替换所有实例。 系统将要求您确认该操作。

查找和替换servlet的默认范围包括以下属性：

* `jcr:title`
* `jcr:description`
* `jcr:text`
* `text`

可以使用Apache Felix Web管理控制台更改范围(例如，在 `https://localhost:4502/system/console/configMgr`)。 选择 `CQ WCM Find Replace Servlet (com.day.cq.wcm.core.impl.servlets.FindReplaceServlet)` 并根据需要配置作用域。

>[!NOTE]
>
>在标准AEM安装中，“查找和替换”使用Lucene进行搜索功能。
>
>Lucene索引长度最大为16k的字符串属性。 超出此范围的字符串将不会被搜索。
