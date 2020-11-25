---
title: 社区分析配置功能
seo-title: 社区分析配置功能
description: 为社区配置分析
seo-description: 为社区配置分析
uuid: 5a083645-9de6-4ecd-a94e-a40143f92edf
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e6fdaf56-402f-418d-96d8-e46bd3ad1e8c
docset: aem65
translation-type: tm+mt
source-git-commit: ef57d53fc780bd222abbe994fc71e133ce8a77fc
workflow-type: tm+mt
source-wordcount: '2756'
ht-degree: 3%

---


# 社区分析配置功能 {#analytics-configuration-for-communities-features}

## 概述 {#overview}

Adobe Analytics和Adobe Experience Manager(AEM)都是Adobe Marketing Cloud的解决方案。

Adobe Analytics可以为AEM Communities配置，这样，当成员与支持的社区功能交互时，事件会发送到生成报告的Adobe Analytics。

例如，当启用社区站点的成员视图分配给他们的视频资源时，资源播放器会将事件发送到Analytics，包括视频心跳数据。 在社区站点中，管理员可以查看有关视频播放的各种报告。

此外，对于以下情况，分析是必需的：

* 在发布环境中：

   * 报告社区趋 [势](/help/communities/trends.md)
   * 允许网站访客按“查看次数最多”、“最活跃”、“最喜欢”进行排序
   * 视图计入UGC列表

* 在作者环境中：

   * 在成员管理控制台中显 [示参与数据](/help/communities/members.md) (视图、帖子、关注、喜欢)
   * 用于启用资源报告的趋势摘要、视频心跳和视频设 [备](/help/communities/reports.md)

支持的社区功能包括：

* [支持资源](/help/communities/resources.md)
* [论坛](/help/communities/forum.md)
* [问题与解答](/help/communities/working-with-qna.md)
* [博客](/help/communities/blog-feature.md)
* [文件库](/help/communities/file-library.md)
* [日历](/help/communities/calendar.md)

本文档的本节介绍如何将Analytics报表包与社区功能相连。 基本步骤为：

1. [复制加密密钥](#replicate-the-crypto-key) ，以确保在所有AEM实例上正确进行加密／解密
1. 准备一个Adobe Analytics [报告套件](#adobe-analytics-report-suite-for-video-reporting)
1. 创建AEM Analytics云 [服务和](#aem-analytics-cloud-service-configuration)[框架](#aem-analytics-framework-configuration)

1. [为社区](#enable-analytics-for-a-community-site) 站点启用Analytics
1. [**验证**](#verify-analytics-to-aem-variable-mapping) Analytics到AEM变量映射
1. 识别主 [发行商](#primary-publisher)
1. [发布](#publish-community-site-and-analytics-cloud-service) 社区站点
1. 配置 [将报告数据从Adobe Analytics](#obtaining-reports-from-analytics) (M)导入社区站点

## 前提条件 {#prerequisites}

要配置Analytics for Communities功能，必须与您的帐户代表合作来设置Adobe Analytics帐户和报 [告包](#adobe-analytics-report-suite-for-video-reporting)。 建立后，应提供以下信息：

* **公司名称**

   与Adobe Analytics帐户关联的公司。

* **用户名**

   已授权管理Analytics帐户的用户的登录用户名（应包括Web服务访问权限）。

* **密码**

   授权用户的登录密码。

* **Analytics数据中心**

   帐户的Analytics数据中心的URL。

* **报表包**

   要使用的Analytics报表包的名称。

## Adobe Analytics视频报告套件报告 {#adobe-analytics-report-suite-for-video-reporting}

使用Adobe Marketing Cloud的报 [告包管理器](https://docs.adobe.com/content/help/en/analytics/admin/manage-report-suites/new-report-suite/new-report-suite.html)，可以配置Analytics报告包，以便社区站点能够提供社区功能的报告。

通过使用 [公司](https://docs.adobe.com/content/help/en/analytics/analyze/analysis-workspace/home.html) 名和用户名登录 [到Adobe Experience Cloud,](/help/communities/analytics.md#prerequisites)可以配置新的或现有的报表包：

* [11转换变量](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html) (eVar)

   * **`evar1`** 启用 **`evar11`**

   * 可以重用（重命名）现有eVar或创建新eVar以用于Communities功能

* [7成功事件](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/success-events/success-event.html) (事件)

   * **`event1`** 启用 **`event7`**

   * 类型 **`Counter`**

      * 否 **`Counter (no subrelations)`**
   * 可以重用（重命名）现有事件或创建新的社区功能


* [视频管理](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html)

   * 视频报告控制台

      * 启用 `Video Core`
      * 选择保存
   * 视频核心测量控制台

      * 选择 `Use Solution Variables`
      * 选择保存


如果使用 **新的报表包**，请注意，新的报表包可能只有4个evar和6个事件变量，而社区需要11个evar和7个事件变量。

如果使用 **现有报表包**，则可能需要在 [为社区站点激活Analytics框架之前修](#modifying-analytics-variable-mapping) 改变量映射。

有关专用于社区的变量的任何疑虑，请与您的客户代表联系。

>[!CAUTION]
>
>**如果使用的现有报表包已经在**
>
>* **`evar1`** 至 **`evar11`**
   >
   >
* **`event1`** 至 **`event7`**
>
>
**然后，在发布社区站点之前** ，务必通过移动AEM变量来恢复先前存在的映射，当为社区站点启用分析时，这些变量会自动映射到Analytics变量。
>
>要恢复先前存在的映射并将AEM变量移动到其他Analytics变量，请参阅修改分析变 [量映射一节](#modifying-analytics-variable-mapping)。
>
>否则可能导致无法恢复的数据丢失。

### 视频心跳分析 {#video-heartbeat-analytics}

获得视频心跳分析许可后，将 `Marketing Cloud Org Id` 分配一个。

要在为视频报告配置 [Analytics报表包后启用视频心跳报告](#adobe-analytics-report-suite-for-video-reporting):

* 创建Analytics [云服务](#aem-analytics-cloud-service-configuration)
* 为社 [区站点启用分析](#enable-analytics-for-a-community-site)
* 将社区 `Marketing Cloud Org Id` 站点关联

可 `Marketing Cloud Org Id` 以在创建社区站点时输入 [该内容](/help/communities/sites-console.md#enablement) ，也可以在更 [晚时修改社](/help/communities/sites-console.md#modifying-site-properties) 区站点属性。 [](#aem-analytics-cloud-service-configuration)

![marketing-org-id](assets/marketing-org-id.png)

启用视频心跳分析后，视频播放器的JavaScript(JS)代码将实例化视频心跳库代码（也以JS为单位），该代码每10秒（不可配置）处理向Analytics视频跟踪服务器发送视频状态更新的所有逻辑，并最终向主Analytics服务器发送视频会话的累积报告。

如果未启用，则视频心跳代码从不被实例化，只有视频进度和恢复位置跟踪被保留到SRP以进行报告。

## AEMAnalytics Cloud服务配置 {#aem-analytics-cloud-service-configuration}

要创建新的Analytics集成，它使用创作实例上的标准UI将Adobe Analytics与AEM社区站点集成：

* 从全局导航： **[!UICONTROL “工具]** ”>“ **[!UICONTROL 部署]** ”> **[!UICONTROL Cloud Services]**
* 向下滚动到 **[!UICONTROL Adobe Analytics]**
* 选择 **[!UICONTROL 立即配置]** 或显 **[!UICONTROL 示配置]**

![云——配置](assets/cloud-config1.png)

### 创建配置对话框 {#create-configuration-dialog}

* 选择 `[+]` 可用配置旁 **[!UICONTROL 边的图标]** ，以创建新配置

在“创建配置”对话框中，要输入的值标识配置。

![create-cloud-config](assets/cloud-config2.png)

* **标题**

   （必需）配置的显示标题。
例如，输入 *Enablement Community Analytics*

* **名称**

   （可选）如果未指定，则名称将默认为从标题派生的有效节点名称。
For example, enter *communities*

* **模板**

   选择 `Adobe Analytics Configuration`

* Select **Create**

   * 启动配置页面并打开对 `Analytics Settings` 话框

### 分析设置对话框 {#analytics-settings-dialog}

初始创建新的Analytics配置会显示配置，并显示新对话框以输入Analytics设置。 此对话框要求从 [帐户代表处获](#prerequisites) 取必备帐户信息。

![analytics-settings](assets/analytics-settings.png)

* **公司**

   与Adobe Analytics帐户关联的公司。

* **用户名**

   已授权管理Analytics帐户的用户的登录用户名。

* **密码**

   授权用户的登录密码。

* **数据中心**

   选择承载报告包的Analytics数据中心。

* **不将跟踪标记添加到页面**

   保留为默认值（取消选择）。

* **使用 AppMeasurement**

   保留为默认值（取消选择）。

* **夜间不导入页面展示（创作）**

   保留为默认值（取消选择）。

* **夜间不导入页面展示（发布）**

   保留为默认值（取消选择）。

保存设置：

* 选择 **连接到分析**

   * 如果不成功，

      * 验证条目不包含前导空格。
      * 尝试其他数据中心。

* 选择 **确定**。

   ![analytics-enablement-settings](assets/analytics-settings1.png)

### 创建框架 {#create-framework}

成功配置与Adobe Analytics的基本连接后，必须为社区站点创建或编辑框架。 该框架的用途是将社区功能(AEM)变量映射到Analytics（报表包）变量。

* 选择 `[+]` 可用框架 **[!UICONTROL 旁边的图标]** ，以创建新框架

   ![analytics-framework](assets/analytics-framework.png)

* **标题**

   （必需）框架的显示标题例如，输入 *Enablement Community Framework*。

* **名称**

   （可选）如果未指定，则名称将默认为从标题派生的有效节点名称。
For example, enter *communities*.

* *模板*

   选择 `Adobe Analytics Framework`.

* 选择&#x200B;**创建**。

创建Analytics Framework会打开要配置的框架。

## AEM Analytics Framework配置 {#aem-analytics-framework-configuration}

该框架的用途是将AEM变量映射到Analytics变量(eVar和事件)。 可用于映射的Analytics变量 [在报表包中定义](#adobe-analytics-report-suite-for-video-reporting)。

![analytics-enablement-framework](assets/analytics-framework1.png)

### 选择报表包 {#select-report-suite}

选择已设置用于视频报告的报表包。

如果尚未创建或未正确设置报表包，请参阅上一节：[Adobe Analytics视频报告套件报告](#adobe-analytics-report-suite-for-video-reporting)

Sidekick不需要，并且可以最小化，以便它不会妨碍对报告包设置的访问。

#### 选择“添加项目”前后的“报表包”对话框 {#report-suites-dialog-before-and-after-selecting-add-item}

![report-suite](assets/report-suite.png)

1. 选择 **添加项目+**。

   出现两个下拉框。

1. 选择 `Report suite.`

   与公司帐户关联的报表包可供选择。

1. 在打 **开的对** 话框中选择“是”:

   ```
   Load default server settings?
    Do you want to load the default server settings and overwrite current values in the Server section?
   ```

1. 选择 `Run Mode`。

1. 选择“**发布**”。

![analytics-framework2](assets/analytics-framework2.png)

Analytic Cloud服务和框架现已完成。 在启用此Analytics服务的情况下创建社区站点后，将定义映射。

## 为社区站点启用分析 {#enable-analytics-for-a-community-site}

### 为新社区站点启用 {#enable-for-new-community-site}

要在创建新社区站点时添 [加Analytics云服务](/help/communities/sites-console.md):

* 在步骤3的“ANALYTICS”（分析） [选项卡下](/help/communities/sites-console.md#analytics):
   * 选中启 **用分析** 复选框。
   * 从下拉框中选择框架。

* （可选）返回到Analytics框架配置以调整变量映射。

### 为现有社区站点启用 {#enable-for-existing-community-site}

要将Analytics云服务添加到现有社 [区站点](/help/communities/sites-console.md#modifying-site-properties):

* 导航到“社 **区”>“站点** ”控制台。
* 选择社区站点的“编辑站点”图标。
* 选择设置。
* 在“分析”部分：
   * 选中启 **用分析** 复选框。
   * 从下拉框中选择框架。

* （可选）返回到Analytics框架配置以调整变量映射。

### 为自定义站点启用 {#enable-for-customized-sites}

要使Analytics跟踪和导入能够对社区站点正常工作，必须存在具有类和href属 `scf-js-site-title` 性的页面元素。 页面上只应存在一个此类元素，如社区站点的未修改 `sitepage.hbs` 脚本中的元素。 值被提取 `siteUrl` 并作为站点路径发送 *到Adobe Analytics*。

```xml
# present in default sitepage.hbs
# only one scf-js-site-title class should be included
# this example sets it to be hidden as it serves no visual purpose
<div
    class="navbar-brand scf-js-site-title"
    href="{{siteUrl}}.html"
    style="visibility: hidden;"
>
</div>
```

对于叠 **加脚本的自定** 义社区站 `sitepage.hbs` 点，请确保元素存在。 当在 `siteUrl` 服务器上呈现变量后，将设置变量，然后再提供给客户端。

对于包 **含Communities组件** 、但不是使用站点创建向导 [创建的通用AEM站点](/help/communities/sites-console.md)，必须添加元素。 href值应为站点的路径。 例如，如果站点路径为， `/content/my/company/en`则使用：

```xml
<div
    class="navbar-brand scf-js-site-title"
    href="/content/my/company/en.html"
    style="visibility: hidden;"
>
</div>
```

## 社区分析功能 {#analytics-for-communities-features}

Analytics可自动用于多个Communities功能。

作者环境 [的OSGi配](/help/sites-deploying/configuring-osgi.md)`AEM Communities Analytics Component Configuration`置提供了已用于Analytics分析的组件列表。 变量的自动映射由列出的组件决定。

如果创建了用于Analytics的新自定义组件，则应将这些组件添加到已配置组件的此列表。

### 组件配置 {#component-configuration}

![component-configuration1](assets/component-configuration1.png)

>[!NOTE]
>
>日志组件用于实现博客功能。

### 将分析映射到AEM变量 {#mapped-analytics-to-aem-variables}

在启用Analytics并选择云配置框架的情况下保存社区站点后，AEM变量将自动映射到以evar1和事件1开头的Analytics eVar和事件，并增加1。

如果使用现有报表包映射evar1到evar11以及事件1到事件7中的任何变量，则需要重 [新映射AEM变量](#modifying-analytics-variable-mapping) 并恢复原始映射。

下面是在学习入门教程之后默认 [映射的示例](/help/communities/getting-started-enablement.md):

![地图分析](assets/map-analytics1.png)

#### 随每个事件发送的eVar映射 {#map-of-evars-sent-with-each-event}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Enablement<br /> Resource<br /> Type</strong></td>
   <td><strong>站点标<br /> 题</strong></td>
   <td><strong>函数类<br /> 型</strong></td>
   <td><strong>组标题<br /></strong></td>
   <td><strong>Group<br /> Path</strong></td>
   <td><strong>UGC类<br /> 型</strong></td>
   <td><strong>UGC<br /> Title</strong></td>
   <td><strong>用户<br /> （会员）</strong></td>
   <td><strong>UGC路径<br /></strong></td>
   <td><strong>站点路径<br /> (Site Path)</strong></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><strong>eVar1</strong></td>
   <td><strong>eVar2</strong></td>
   <td><strong>eVar3</strong></td>
   <td><strong>eVar4</strong></td>
   <td><strong>eVar5</strong></td>
   <td><strong>eVar6</strong></td>
   <td><strong>eVar7</strong></td>
   <td><strong>eVar8</strong></td>
   <td><strong>eVar9</strong></td>
   <td><strong>eVar10</strong></td>
  </tr>
  <tr>
   <td><strong>事件<br /> 1资源播放</strong></td>
   <td><em>(a)</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>(i)</em></td>
   <td><em>-</em></td>
  </tr>
  <tr>
   <td><strong>事件<br /> 2 SCFView</strong></td>
   <td><em>(a)</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>(i)</em></td>
   <td><em>(j)</em></td>
  </tr>
  <tr>
   <td><strong>事件<br /> 3 SCFCreate（发布）</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>(i)</em></td>
   <td><em>(j)</em></td>
  </tr>
  <tr>
   <td><strong>事件<br /> 4 SCFFollow</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>(i)</em></td>
   <td><em>(j)</em></td>
  </tr>
  <tr>
   <td><strong>事件<br /> 5 SCFVoteUp</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>(i)</em></td>
   <td><em>(j)</em></td>
  </tr>
  <tr>
   <td><strong>事件6<br /> SCFVoteDown</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>(i)</em></td>
   <td><em>(j)</em></td>
  </tr>
  <tr>
   <td><strong>事件<br /> 7 SCFRate</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>(i)</em></td>
   <td><em>(j)</em></td>
  </tr>
 </tbody>
</table>

**eVar值示例：**

* *[MIME类型](https://www.iana.org/assignments/media-types)*:video/mp4
* *[社区站点标题](/help/communities/sites-console.md#step13asitetemplate)*:Geometrixx社区
* *[社区函数名称](/help/communities/functions.md)*:论坛
* *[社区组名称](/help/communities/creating-groups.md#creating-a-new-group)*:远足
* *社区组内容的路径*: `/content/sites/<site name>/en/groups/hiking`
* *[UGC组件资源类型](/help/communities/essentials.md)*: `social/forum/components/hbs/topic`
* *UGC组件标题*:远足主题
* *login(authorizableId)*: `aaron.mcdonald@mailinator.com`
* *UGC的SRP路径*: `/content/usergenerated/asi/.../forum/jmtz-topic3`
或 
*要遵循的组件路径*: `/content/sites/<site name>/en/jcr:content/content/primary/forum`

* *社区站点内容的路径*: `/content/sites/<site name>/en`

### 修改分析变量映射 {#modifying-analytics-variable-mapping}

在为社区站点启用Analytics后，可以从框架配置中看到Analytics eVar和事件到AEM变量的映射。

启用Analytics后，在发布社区站点之前，可以通过将所需的Analyticsevar或事件从左边栏拖放到映射表中的相关行，在框架中更改映射。

要避免重复映射，请务必将替换的Analyticsevar或事件从行中删除，方法是将指针悬停在该行上，然后选择显示在Analytics变量元素右侧的“X”。

如果Communities eVar和事件覆盖了报表包中先前存在的映射，则为避免数据丢失，请将Communities功能的AEM变量分配给其他Analytics eVar或事件，并恢复原始映射。

>[!CAUTION]
>
>在启用Analytics的情况下发布社区站点之前重 [新映射](#publishing-the-community-site) ，这一点很重要，否则可能会丢失数据。

#### 示例步骤1:将Analytics evar14拖入映射表 {#example-step-dragging-analytics-evar-into-mapping-table}

![analytics-mapping-evar](assets/analytics-mapping-evar.png)

#### 示例步骤2:选择“x”以删除已替换的evar11 {#example-step-selecting-x-to-remove-replaced-evar}

![analytics-mapping-evar1](assets/analytics-mapping-evar1.png)

#### 示例步骤3:AEM var eventdata.siteId重新映射到Analytics evar14 {#example-step-aem-var-eventdata-siteid-remapped-to-analytics-evar}

![analytics-mapping-evar2](assets/analytics-mapping-evar2.png)

## 发布社区站点 {#publishing-the-community-site}

### 验证分析到AEM变量映射 {#verify-analytics-to-aem-variable-mapping}

在发布社区站点之前验证变量映射是明智的，该站点也会发布Analytics云服务和框架。

请参阅以下部分：

* [将分析映射到AEM变量](#mapped-analytics-to-aem-variables)
* [修改分析变量映射](#modifying-analytics-variable-mapping)

>[!CAUTION]
>
>**如果使用的现有报表包已经在**
>
>* **`evar1`** 至 **`evar11`**
   >
   >
* **`event1`** 至 **`event7`**
>
>
**然后，在发布社区站点之前** ，务必恢复预先存在的映射并将自动映射的社区AEM变量（在为社区站点启用Analytics时）移动到其他Analytics变量。 此重新映射应在所有社区组件之间保持一致。
>
>否则可能导致无法恢复的数据丢失。

### 主发布者 {#primary-publisher}

当选择的部署是发 [布场](/help/communities/topologies.md#tarmk-publish-farm)，则必须将一个AEM发布实例标识为轮询Adobe Analytics以将报告数据写入SRP的主发 [布者](/help/communities/working-with-srp.md)。

默认情况下， `AEM Communities Publisher Configuration` OSGi配置将其发布实例标识为主发布者，这样发布场中的所有发布实例都将自标识为主发布者。

因此，必须编辑所有辅助发布实例上的配置以取消选中“主发 **布者** ”复选框。

有关具体说明，请参阅部署社区的主要发 [布者部分](/help/communities/deploy-communities.md#primary-publisher)。

>[!CAUTION]
>
>配置主发布者以阻止多个发布实例进行轮询很重要。

### 复制加密密钥 {#replicate-the-crypto-key}

Adobe Analytics的凭据已加密。 为了便于作者和发布者之间复制或传输加密的分析凭据，所有AEM实例必须共享相同的主加密密钥。

为此，请按照复制加密密钥 [中的说明操作](/help/communities/deploy-communities.md#replicate-the-crypto-key)。

### 发布社区站点和Analytics Cloud服务 {#publish-community-site-and-analytics-cloud-service}

为社区站点启用Analytics云服务后，并在必要时调整 [了Analytics到AEM变量的映射](#mapped-analytics-to-aem-variables)，有必要通过（重新）发布社区站点将配 [置复制到发布环境](/help/communities/sites-console.md#publishing-the-site)。

## 从Analytics获取报告 {#obtaining-reports-from-analytics}

### 报表管理 {#report-management}

作者和主发布者的 [OSGi配置](/help/sites-deploying/configuring-osgi.md)`AEM Communities Analytics Report Management`，用于查询分析。

作者可以查询实时报告。

在主发布者上，查询用于提供准备报表导入程序的分析数据导入的信息。

查询间隔默认为10秒。

### 报表导入程序 {#report-importer}

一旦发布了启用Analytics的社区站点，主发布者的 [OSGi配置](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Report Importer`就可以配置为为那些未在CRXDE中单独配置的配置设置默认轮询间隔。

轮询间隔控制向Adobe Analytics请求数据被提取并保存到SRP中的 [频率](/help/communities/working-with-srp.md)。

当数据可能被归类为“大数据”时，更频繁的民意测验可能会给社区站点带来很大负担。

默认轮询 **导入间隔** 设置为12小时。

![report-importer](assets/report-importer.png)

### 组件报表自定义 {#component-report-customization}

目前，为了自定义要跟踪的度量，在存储库中创建节点，该节点定义要为该度量生成报告的时间段。

论坛主题目前是此自定义的唯一示例：

* 在主发行商上，以管理权限登录。
* 导航到 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)。 例如， [https://localhost:4503/crx/de](https://localhost:4503/crx/de)。

* 在语言根的jcr:content节点下(例如，导 `/content/sites/engage/en/jcr:content),`航到为Analytics报告配置的组件。
例如，**`analytics/reportConfigs/social_forum_components_hbs_topic`**

* 注意创建的时间段：

   * `last30Days`
   * `last90Days`
   * `thisYear`

* 注意节 `total`点。

   * 修改属 **`interval`** 性将覆盖报表导入程序间隔。
   * 该值以秒为单位，并设置为4小时（14400秒）。

![component-report](assets/component-report.png)

## 在Analytics中管理用户数据 {#manage-user-data-in-analytics}

Adobe Analytics提供的API允许您访问、导出和删除用户数据。 有关详细信息，请参 [阅提交访问和删除请求](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-submit-access-delete.html)。

## 资源 {#resources}

* Adobe Experience Cloud: [分析帮助与参考](https://docs.adobe.com/content/help/en/analytics/landing/home.html)
* AEM: [Integrating with Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* AEM: [外部提供商的分析](/help/sites-administering/external-providers.md)
