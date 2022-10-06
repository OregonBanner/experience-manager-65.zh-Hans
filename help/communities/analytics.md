---
title: 社区功能的Analytics配置
seo-title: Analytics Configuration for Communities Features
description: 为社区配置分析
seo-description: Configure analytics for Communities
uuid: 5a083645-9de6-4ecd-a94e-a40143f92edf
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e6fdaf56-402f-418d-96d8-e46bd3ad1e8c
docset: aem65
role: Admin
exl-id: 7d54928b-6512-4da9-a209-eb4488bf2b64
source-git-commit: 0f7d4aba0b8c79039918e1338007a4277a5030f2
workflow-type: tm+mt
source-wordcount: '2731'
ht-degree: 3%

---

# 社区功能的Analytics配置 {#analytics-configuration-for-communities-features}

## 概述 {#overview}

Adobe Analytics和Adobe Experience Manager(AEM)都是Adobe Marketing Cloud的解决方案。

可以为AEM Communities配置Adobe Analytics，以便成员与支持的社区功能交互时，事件会从中发送到生成报表的Adobe Analytics。

例如，当启用社区网站的成员查看分配给他们的视频资源时，资源播放器会将事件（包括视频心率数据）发送到Analytics。 从社区站点，管理员可以查看有关视频播放的各种报表。

此外，对于以下情况，需要进行分析：

* 在发布环境中：

   * 社区报告 [趋势](/help/communities/trends.md)
   * 允许网站访客按“查看次数最多”、“最活跃”、“最喜欢”进行排序
   * 查看UGC列表中的计数

* 在创作环境中：

   * 在 [成员管理控制台](/help/communities/members.md) （查看、帖子、关注、称赞）
   * 用于启用资源的趋势摘要、视频心率和视频设备 [报告](/help/communities/reports.md)

支持的社区功能包括：

* [支持资源](/help/communities/resources.md)
* [论坛](/help/communities/forum.md)
* [问题与解答](/help/communities/working-with-qna.md)
* [博客](/help/communities/blog-feature.md)
* [文件库](/help/communities/file-library.md)
* [日程表](/help/communities/calendar.md)

文档的此部分介绍如何将Analytics报表包与社区功能连接起来。 基本步骤包括：

1. [复制加密密钥](#replicate-the-crypto-key) 确保在所有AEM实例上正确进行加密/解密
1. 准备Adobe Analytics [报表包](#adobe-analytics-report-suite-for-video-reporting)
1. 创建AEM Analytics [云服务](#aem-analytics-cloud-service-configuration) 和 [框架](#aem-analytics-framework-configuration)

1. [启用Analytics](#enable-analytics-for-a-community-site) 用于社区站点
1. [**验证**](#verify-analytics-to-aem-variable-mapping) Analytics到AEM变量的映射
1. 识别 [主发布者](#primary-publisher)
1. [发布](#publish-community-site-and-analytics-cloud-service) 社区站点
1. 配置 [导入报表数据](#obtaining-reports-from-analytics) 从Adobe Analytics到社区站点

## 前提条件 {#prerequisites}

要配置Analytics for Communities功能，需要与您的客服专员合作来设置Adobe Analytics帐户和 [报表包](#adobe-analytics-report-suite-for-video-reporting). 建立后，应提供以下信息：

* **公司名称**

   与Adobe Analytics帐户关联的公司。

* **用户名**

   有权管理Analytics帐户的用户的登录用户名（应包括Web服务访问权限）。

* **密码**

   授权用户的登录密码。

* **Analytics数据中心**

   帐户的Analytics数据中心URL。

* **报表包**

   要使用的Analytics报表包的名称。

## Adobe Analytics用于视频报告的报表包 {#adobe-analytics-report-suite-for-video-reporting}

使用Adobe Marketing Cloud的 [报表包管理器](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/new-report-suite.html)，则可以配置Analytics报表包，以便允许社区站点提供社区功能的报表。

通过登录到 [Adobe Experience Cloud](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html) with [公司名称和用户名](/help/communities/analytics.md#prerequisites)，则可以将新报表包或现有报表包配置为：

* [11转化变量](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html) (eVar)

   * **`evar1`** 至 **`evar11`** 已启用

   * 可以重新调整（重命名）现有eVar的用途或创建新eVar以用于“社区”功能

* [7个成功事件](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/success-events/success-event.html) （事件）

   * **`event1`** 至 **`event7`** 已启用

   * 类型 **`Counter`**

      * 否 **`Counter (no subrelations)`**
   * 可以重新调整（重命名）现有事件的用途或创建新事件以用于“社区”功能


* [视频管理](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html)

   * 视频报告控制台

      * 启用 `Video Core`
      * 选择保存
   * 视频核心测量控制台

      * 选择 `Use Solution Variables`
      * 选择保存


如果使用 **新报表包**，请注意，新报表包可能只有4个evar和6个事件变量，而社区则需要11个evar和7个事件var。

如果使用 **现有报表包**，则可能需要 [修改变量映射](#modifying-analytics-variable-mapping) 在为社区站点激活Analytics框架之前，请执行以下操作：

有关专用于社区的变量的任何问题，请联系您的客户代表。

>[!CAUTION]
>
>**如果使用的现有报表包已在**
>
>* **`evar1`** 至 **`evar11`**
>
>* **`event1`** 至 **`event7`**
>
>**然后，在社区网站发布之前，** 通过移动在为社区站点启用AEM时自动映射到Analytics变量的Analytics变量，来恢复预先存在的映射至关重要。
>
>要恢复预先存在的映射并将AEM变量移动到其他Analytics变量，请参阅 [修改Analytics变量映射](#modifying-analytics-variable-mapping).
>
>如果不这样做，则可能会导致无法恢复的数据丢失。

### 视频心率分析 {#video-heartbeat-analytics}

当视频心率分析获得许可时， `Marketing Cloud Org Id` 分配。

要在 [配置Analytics报表包以进行视频报告](#adobe-analytics-report-suite-for-video-reporting):

* 创建 [Analytics云服务](#aem-analytics-cloud-service-configuration)
* 启用 [社区网站的分析](#enable-analytics-for-a-community-site)
* 关联 `Marketing Cloud Org Id` 和社区站点

的 `Marketing Cloud Org Id` 可在 [社区站点创建](/help/communities/sites-console.md#enablement) 或稍后 [修改](/help/communities/sites-console.md#modifying-site-properties) 社区站点属性。

![marketing-org-id](assets/marketing-org-id.png)

启用视频心率分析后，视频播放器的JavaScript(JS)代码会实例化视频心率库代码（同样位于JS中），该代码会处理每10秒向Analytics视频跟踪服务器发送视频状态更新的所有逻辑（不可配置），并最终将视频会话的累积报表发送到主Analytics服务器。

如果未启用，则从不实例化视频心率代码，并且只会将视频进度和恢复位置跟踪保留到SRP以进行报告。

## AEM Analytics Cloud服务配置 {#aem-analytics-cloud-service-configuration}

要使用创作实例上的标准UI创建新的Analytics集成，该集成将Adobe Analytics与AEM社区站点集成：

* 从全局导航： **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL Cloud Services]**
* 向下滚动到 **[!UICONTROL Adobe Analytics]**
* 选择 **[!UICONTROL 立即配置]** 或 **[!UICONTROL 显示配置]**

![云配置](assets/cloud-config1.png)

### 创建配置对话框 {#create-configuration-dialog}

* 选择 `[+]` 图标 **[!UICONTROL 可用配置]** 创建新配置

在创建配置对话框中，要输入的值标识配置。

![create-cloud-config](assets/cloud-config2.png)

* **标题**

   （必需）配置的显示标题。
例如，输入 *启用社区分析*

* **名称**

   （可选）如果未指定，则名称将默认为从标题派生的有效节点名称。
例如，输入 *社区*

* **模板**

   选择 `Adobe Analytics Configuration`

* 选择 **创建**

   * 启动配置页面并打开 `Analytics Settings` 对话框

### Analytics设置对话框 {#analytics-settings-dialog}

初始创建新Analytics配置时，会显示配置并显示一个用于输入Analytics设置的新对话框。 此对话框要求 [先决条件帐户信息](#prerequisites) 从客服专员那里获得。

![analytics-settings](assets/analytics-settings.png)

* **公司**

   与Adobe Analytics帐户关联的公司。

* **用户名**

   有权管理Analytics帐户的用户的登录用户名。

* **密码**

   授权用户的登录密码。

* **数据中心**

   选择托管报表包的Analytics数据中心。

* **不将跟踪标记添加到页面**

   保留为默认值（取消选中）。

* **使用 AppMeasurement**

   保留为默认值（取消选中）。

* **夜间不导入页面展示（创作）**

   保留为默认值（取消选中）。

* **夜间不导入页面展示（发布）**

   保留为默认值（取消选中）。

要保存设置，请执行以下操作：

* 选择 **连接到Analytics**

   * 如果不成功，

      * 验证条目不包含前导空格。
      * 尝试使用其他数据中心。

* 选择 **确定**.

   ![analytics-enablement-settings](assets/analytics-settings1.png)

### 创建框架 {#create-framework}

成功配置与Adobe Analytics的基本连接后，需要为社区站点创建或编辑框架。 该框架的用途是将社区功能(AEM)变量映射到Analytics（报表包）变量。

* 选择 `[+]` 图标 **[!UICONTROL 可用框架]** 创建新框架

   ![analytics-framework](assets/analytics-framework.png)

* **标题**

   （必需）框架的显示标题例如，输入 *启用社区框架*.

* **名称**

   （可选）如果未指定，则名称将默认为从标题派生的有效节点名称。
例如，输入 *社区*.

* *模板*

   选择 `Adobe Analytics Framework`.

* 选择&#x200B;**创建**。

创建Analytics框架会打开配置框架。

## AEM Analytics框架配置 {#aem-analytics-framework-configuration}

该框架的用途是将AEM变量映射到Analytics变量（eVar和事件）。 可用于映射的Analytics变量包括 [在报表包中定义](#adobe-analytics-report-suite-for-video-reporting).

![analytics-enablement-framework](assets/analytics-framework1.png)

### 选择报表包 {#select-report-suite}

选择为视频报告设置的报表包。

如果尚未创建或未正确设置报表包，请参阅上一部分：
[Adobe Analytics用于视频报告的报表包](#adobe-analytics-report-suite-for-video-reporting)

无需使用Sidekick，并且可以将其最小化，以便它不会妨碍对报表包设置的访问。

#### “报表包”对话框中的“添加项目” {#report-suites-dialog-before-and-after-selecting-add-item}

![报表包](assets/report-suite.png)

1. 选择 **添加项目+**.

   出现两个下拉框。

1. 选择 `Report suite.`

   可以选择与公司帐户关联的报表包。

1. 选择 **是** 在打开的对话框中：

   ```
   Load default server settings?
    Do you want to load the default server settings and overwrite current values in the Server section?
   ```

1. 选择 `Run Mode`.

1. 选择“**发布**”。

![analytics-framework2](assets/analytics-framework2.png)

Analytics云服务和框架现已完成。 在启用此Analytics服务的情况下创建社区站点后，将定义映射。

## 为社区站点启用Analytics {#enable-analytics-for-a-community-site}

### 为新社区站点启用 {#enable-for-new-community-site}

在 [创建新社区站点](/help/communities/sites-console.md):

* 在步骤3中，在 [“ANALYTICS”选项卡](/help/communities/sites-console.md#analytics):
   * 选择 **启用Analytics** 复选框。
   * 从下拉框中选择框架。

* （可选）返回到Analytics框架配置以调整变量映射。

### 为现有社区站点启用 {#enable-for-existing-community-site}

将Analytics云服务添加到 [现有社区站点](/help/communities/sites-console.md#modifying-site-properties):

* 导航到 **社区>站点** 控制台。
* 选择社区站点的编辑站点图标。
* 选择设置。
* 在Analytics部分中：
   * 选择 **启用Analytics** 复选框。
   * 从下拉框中选择框架。

* （可选）返回到Analytics框架配置以调整变量映射。

### 为自定义网站启用 {#enable-for-customized-sites}

为了使Analytics跟踪和导入功能对社区站点正常工作，使用 `scf-js-site-title` 类和href属性必须存在。 页面上只应存在一个此类元素，如未修改的中所示 `sitepage.hbs` 社区站点脚本。 的值 `siteUrl` 将作为 *网站路径*.

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

对于 **自定义社区网站** 覆盖 `sitepage.hbs` 脚本中，确保元素存在。 的 `siteUrl` 变量在提供给客户端之前，将在服务器上呈现时进行设置。

对于 **通用AEM网站** （包含社区组件），但不会使用 [站点创建向导](/help/communities/sites-console.md)，则需要添加元素。 href的值应该是网站的路径。 例如，如果网站路径为 `/content/my/company/en`，然后使用：

```xml
<div
    class="navbar-brand scf-js-site-title"
    href="/content/my/company/en.html"
    style="visibility: hidden;"
>
</div>
```

## Analytics for Communities功能 {#analytics-for-communities-features}

Analytics会自动用于多个社区功能。

创作环境的 [OSGi配置](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Component Configuration`，提供已用于Analytics的组件列表。 变量的自动映射由列出的组件决定。

如果创建了用于Analytics的新自定义组件，则应将这些组件添加到此已配置组件列表。

### 组件配置 {#component-configuration}

![component-configuration1](assets/component-configuration1.png)

>[!NOTE]
>
>日志组件用于实施博客功能。

### 将Analytics映射到AEM变量 {#mapped-analytics-to-aem-variables}

在启用Analytics并选择云配置框架后保存社区网站，AEM变量将自动映射到分别以evar1和event1开始的Analytics eVar和事件，并增加1。

如果使用现有的报表包来映射evar1到evar11以及event1到event7中的任何变量，则需要 [重新映射AEM变量](#modifying-analytics-variable-mapping) 并恢复原始映射。

以下示例显示了 [入门教程](/help/communities/getting-started-enablement.md):

![映射分析](assets/map-analytics1.png)

#### 随每个事件一起发送的eVar映射 {#map-of-evars-sent-with-each-event}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>启用<br /> 资源<br /> 类型</strong></td>
   <td><strong>网站<br /> 标题</strong></td>
   <td><strong>函数<br /> 类型</strong></td>
   <td><strong>组<br /> 标题</strong></td>
   <td><strong>组<br /> 路径</strong></td>
   <td><strong>UGC<br /> 类型</strong></td>
   <td><strong>UGC<br /> 标题</strong></td>
   <td><strong>用户<br /> （会员）</strong></td>
   <td><strong>UGC<br /> 路径</strong></td>
   <td><strong>网站<br /> 路径</strong></td>
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
   <td><strong>event1<br /> 资源播放</strong></td>
   <td><em>(某个)</em></td>
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
   <td><strong>event2<br /> SCFView</strong></td>
   <td><em>(某个)</em></td>
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
   <td><strong>event3<br /> SCFCreate(Post)</strong></td>
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
   <td><strong>event4<br /> SCFFollow</strong></td>
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
   <td><strong>event5<br /> SCFVoteUp</strong></td>
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
   <td><strong>event6<br /> SCFVoteDown</strong></td>
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
   <td><strong>event7<br /> SCFRate</strong></td>
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

**eVar值的示例：**

* *[MIME类型](https://www.iana.org/assignments/media-types)*:video/mp4
* *[社区网站标题](/help/communities/sites-console.md#step13asitetemplate)*:Geometrixx社区
* *[社区函数名称](/help/communities/functions.md)*:论坛
* *[社区组名称](/help/communities/creating-groups.md#creating-a-new-group)*:远足
* *社区组内容的路径*: `/content/sites/<site name>/en/groups/hiking`
* *[UGC组件resourceType](/help/communities/essentials.md)*: `social/forum/components/hbs/topic`
* *UGC组件标题*:徒步主题
* *login(authorizableId)*: `aaron.mcdonald@mailinator.com`
* *SRP到UGC的路径*: `/content/usergenerated/asi/.../forum/jmtz-topic3`
或 
*组件要遵循的路径*: `/content/sites/<site name>/en/jcr:content/content/primary/forum`

* *社区站点内容的路径*: `/content/sites/<site name>/en`

### 修改Analytics变量映射 {#modifying-analytics-variable-mapping}

为社区站点启用Analytics后，框架配置中会显示Analytics eVar和事件到AEM变量的映射。

启用Analytics后且发布社区网站之前，可以在框架中更改映射，方法是从左边栏中拖动所需的Analytics evar或事件，并将其拖放到映射表的相关行中。

要避免出现重复映射，请务必从行中删除替换的Analytics evar或事件，方法是将鼠标悬停在该evar上，然后选择Analytics变量元素右侧显示的“X”。

如果社区eVar和事件覆盖报表包中预先存在的映射，则为避免数据丢失，请将社区功能的AEM变量分配给其他Analytics eVar或事件，并恢复原始映射。

>[!CAUTION]
>
>在社区站点之前重新映射至关重要 [发布](#publishing-the-community-site) 启用Analytics后，则可能会丢失数据。

#### 示例步骤1:将Analytics evar14拖入映射表 {#example-step-dragging-analytics-evar-into-mapping-table}

![analytics-mapping-evar](assets/analytics-mapping-evar.png)

#### 示例步骤2:选择“x”以删除替换的evar11 {#example-step-selecting-x-to-remove-replaced-evar}

![analytics-mapping-evar1](assets/analytics-mapping-evar1.png)

#### 示例步骤3:AEM var eventdata.siteId已重新映射到Analytics evar14 {#example-step-aem-var-eventdata-siteid-remapped-to-analytics-evar}

![analytics-mapping-evar2](assets/analytics-mapping-evar2.png)

## 发布社区网站 {#publishing-the-community-site}

### 验证Analytics到AEM变量的映射 {#verify-analytics-to-aem-variable-mapping}

明智的做法是，在发布社区网站（该网站也发布Analytics云服务和框架）之前验证变量映射。

请参阅以下章节：

* [将Analytics映射到AEM变量](#mapped-analytics-to-aem-variables)
* [修改Analytics变量映射](#modifying-analytics-variable-mapping)

>[!CAUTION]
>
>**如果使用的现有报表包已在**
>
>* **`evar1`** 至 **`evar11`**
>
>* **`event1`** 至 **`event7`**
>
>**然后，在社区网站发布之前，** 重要的是要恢复预先存在的映射，并将自动映射的社区AEM变量（在为社区站点启用Analytics时）移动到其他Analytics变量。 此重新映射应在所有社区组件中保持一致。
>
>如果不这样做，则可能会导致无法恢复的数据丢失。

### 主发布者 {#primary-publisher}

当选择的部署是 [发布场](/help/communities/topologies.md#tarmk-publish-farm)，则必须将一个AEM发布实例标识为用于轮询Adobe Analytics以将报表数据写入的主发布者 [SRP](/help/communities/working-with-srp.md).

默认情况下， `AEM Communities Publisher Configuration` OSGi配置将其发布实例标识为主发布者，这样发布场中的所有发布实例都将自标识为主发布者。

因此，必须编辑所有辅助发布实例上的配置以取消选择 **主发布者** 复选框。

有关具体说明，请参阅 [部署社区](/help/communities/deploy-communities.md#primary-publisher).

>[!CAUTION]
>
>配置主发布者以阻止从多个发布实例进行轮询很重要。

### 复制加密密钥 {#replicate-the-crypto-key}

Adobe Analytics凭据已加密。 为了便于作者和发布者之间复制或传输加密的AEM凭据，所有Analytics实例必须共享相同的主加密密钥。

为此，请按照 [复制加密密钥](/help/communities/deploy-communities.md#replicate-the-crypto-key).

### 发布社区站点和Analytics Cloud服务 {#publish-community-site-and-analytics-cloud-service}

为社区站点启用Analytics云服务后，如有必要，还可以 [已调整Analytics到AEM变量的映射](#mapped-analytics-to-aem-variables)，则需要通过将配置复制到发布环境 [（重新）发布社区网站](/help/communities/sites-console.md#publishing-the-site).

## 从Analytics获取报表 {#obtaining-reports-from-analytics}

### 报表管理 {#report-management}

作者和主发布者的 [OSGi配置](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Report Management`，用于查询Analytics。

作者可查询实时报表。

在主发布者上，查询用于提供信息以准备报表导入器的分析数据导入。

查询间隔默认为10秒。

### 报表导入器 {#report-importer}

在发布启用了Analytics的社区网站后，即为主发布者的 [OSGi配置](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Report Importer`，则可以将其配置为为那些未在CRXDE中单独配置的配置设置默认轮询间隔。

轮询间隔控制向Adobe Analytics请求提取并保存到 [SRP](/help/communities/working-with-srp.md).

当数据可能被分类为“大数据”时，更频繁的轮询可能会给社区站点带来很大负载。

默认轮询 **导入间隔** 设置为12小时。

![report-importer](assets/report-importer.png)

### 组件报表自定义 {#component-report-customization}

目前，为了自定义要跟踪的量度，在存储库中创建节点，定义要为其生成该量度报表的时间段。

论坛主题目前是此自定义的唯一示例：

* 在主发布者上，使用管理权限登录。
* 导航到 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). 例如， [https://localhost:4503/crx/de](https://localhost:4503/crx/de).

* 在语言根的jcr:content节点下(例如 `/content/sites/engage/en/jcr:content),`导航到为Analytics报表配置的组件。
例如，**`analytics/reportConfigs/social_forum_components_hbs_topic`**

* 请注意创建的时间段：

   * `last30Days`
   * `last90Days`
   * `thisYear`

* 请注意 `total`节点。

   * 修改 **`interval`** 属性会覆盖报表导入器间隔。
   * 该值以秒为单位，设置为4小时(14400秒)。

![组件报表](assets/component-report.png)

## 在Analytics中管理用户数据 {#manage-user-data-in-analytics}

Adobe Analytics提供了用于访问、导出和删除用户数据的API。 有关更多信息，请参阅 [提交访问和删除请求](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-submit-access-delete.html).

## 资源 {#resources}

* Adobe Experience Cloud: [Analytics帮助和参考](https://experienceleague.adobe.com/docs/analytics.html)
* AEM: [与Adobe Analytics集成](/help/sites-administering/adobeanalytics.md)
* AEM: [Analytics与外部提供程序](/help/sites-administering/external-providers.md)
