---
title: We.Gov参考网站演练
seo-title: We.Gov参考网站演练
description: 使用虚构的用户和用户组使用We.Gov演示包执行AEM Forms任务。
seo-description: 使用虚构的用户和用户组使用We.Gov演示包执行AEM Forms任务。
uuid: 797e301a-36ed-4bae-9ea8-ee77285c786d
contentOwner: anujkapo
discoiquuid: ddb3778b-be06-4cde-bc6e-0994efa42b18
docset: aem65
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# We.Gov参考网站演练{#we-gov-reference-site-walkthrough}

## Pre-requisites {#pre-requisites}

按照设置和配置We.Gov参考 [站点中所述设置参考站点](../../forms/using/forms-install-configure-gov-reference-site.md)。

## 用户案例 {#user-story}

* AEM Forms

   * 数据捕获
   * 数据集成(MS Dynamics)
   * Adobe Sign

* 工作流
* 客户通信

   * 打印渠道
   * Web 渠道

* Adobe Analytics

### Fictitious users and groups {#fictitious-users-and-groups}

We.Gov演示包随附以下内置虚拟用户：

* **谭雅**:符合政府机构服务条件的公民

![虚拟用户](/help/forms/using/assets/aya_tan_new.png)

* **乔治·朗**:We.Gov机构业务分析员

![虚拟用户](/help/forms/using/assets/george_lang.png)

* **卡米拉·桑托斯**:We.Gov代理CX主管

![虚拟用户](/help/forms/using/assets/camila_santos.png)

还包括以下组：

* **We.Gov Forms用户**

   * George Lang（成员）
   * 卡米拉·桑托斯（成员）

* **We.Gov用户**

   * George Lang（成员）
   * 卡米拉·桑托斯（成员）
   * 谭雅雅（委员）

### 演示概述术语图例 {#demo-overview-terms-legend}

1. **模拟**:AEM演示中定义的用户和用户组。
1. **按钮**:用于导航的彩色矩形或带圆圈的箭头。
1. **单击**:执行用户案例中的操作。
1. **链接**:位于We.Gov站点的主菜单顶部。
1. **用户说明**:浏览用户故事时要遵循的一组数字步骤。
1. **Forms Portal**: *https://&lt;aemserver>:&lt;port>/content/we-gov/formsportal.html*
1. **移动视图**:We.Gov用户使用重新调整大小的浏览器复制移动视图。
1. **桌面视图**:We.gov用户在笔记本或台式机上视图演示。
1. **预编剧表单**:We.Gov网站主页上的表单。
1. **自适应表单**:We.gov演示的注册申请表。

   *https://&lt;aemserver>:&lt;port>/content/forms/af/adobe-gov-forms/enrollment-application-for-health-benefits.html*

1. **Adobe We.Gov网站**: *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. **Adobe收件箱**:位于AEM后端中的 [顶部菜单栏](assets/bell.svg) “贝尔”图标。

   *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. **电子邮件客户端**:视图电子邮件的首选方式(Gmail、Outlook)
1. **CTA**:行动动员
1. **导航**:在浏览器页面上查找特定的参考点。

## 移动视图演示 {#mobile-view-demo}

**此部分必须在演示之前执行。**

**用户说明：**

1. 导航到： *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. 登录方式：

   1. **用户**:aya.tan
   1. **密码**:口令

1. 重新调整浏览器窗口的大小或使用浏览器的模拟器复制移动设备的大小。

### Aya用户案例（We.Gov网站） {#aya-user-story-we-gov-website}

![虚拟用户](/help/forms/using/assets/aya_tan_new-1.png)

**本节**:阿亚是公民。 她从朋友那里得知，她可能有资格从政府机构获得服务。 Aya从她的手机导航到We.Gov网站，进一步了解她有资格获得的服务。

### Aya用户案例（We.Gov前屏幕） {#aya-user-story-we-gov-pre-screener}

Aya回答了几个问题，通过在手机上填写一份简短的自适应表格来确认她的资格。

**用户说明：**

1. 在每个下拉字段中进行选择。

   >[!NOTE]
   >
   >如果用户年收入超过200,000美元，则他们没有资格。

1. 单击“我&#x200B;**是否有资格？**” 按钮.
1. 单击“立&#x200B;**即应用**”按钮以继续。

   ![立即应用链接](/help/forms/using/assets/apply_now_link.png)

### Aya用户案例（We.Gov自适应表单） {#aya-user-story-we-gov-adaptive-form}

Aya发现她符合条件，开始填写她的应用程序，在她的移动设备上请求服务。

Aya需要在家查看一些文档，然后才能完成服务请求申请。 她保存并退出应用程序。

**用户说明：**

1. 填写“基本信息”字段，其中包括必填字段和下拉列表：

   1. 基本信息

      1. 名字
      1. 中间名
      1. 姓氏
      1. 首选名称
      1. DOB
      1. 性别
   1. 联系信息

      1. 街道地址
      1. 城市
      1. 电话号码
      1. 邮政编码
      1. 电子邮件
      1. 状态
   1. 军事地位

      1. 家庭状态



1. 使用以下动 **态逻辑** ，使用“系列状态”下拉菜单演 **示动态功能** :

   1. **单个**:显示外观面板的下一个
   1. **已婚**:显示婚姻相关面板
   1. **离婚**:显示外观面板的下一个
   1. **丧偶**:显示外观面板的下一个
   1. **你有孩子吗？**:（是／否）用于显示子依赖面板的单选按钮。

      1. （添加／删除）按钮，以添加／删除多个子从属面板。

1. 单击灰色菜单栏中的向右箭头。
1. 单击底部的“保存”按钮。

   ![自适应表单详细信息](/help/forms/using/assets/adaptive_form.png)

## 桌面演示 {#desktop-demo}

**本节：** 回到家里，Aya找到了她需要的信息，并从她的桌面恢复该应用程序。 Aya导航到在线表单门户以恢复其应用程序。 借助一些简单的自定义功能，机构还可以自动生成链接并通过电子邮件发送以恢复应用程序。

### Aya用户案例（续自适应表单） {#aya-user-story-continued-adaptive-form}

**用户说明：**

1. 导航到 *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. 在导航栏中，单击“在&#x200B;**线服务**”。
1. 从“Draft Forms”（草稿表单）面板中，选择现有的“Enjorning Application For Health Benefits”（健康福利登记申请）。

   ![健康福利的注册申请](/help/forms/using/assets/enrollment_application.png)

   外观和感觉都一样，她无需重新输入任何数据。

   **用户说明：**

1. 单击右侧的“圈子CTA”以移至下一节。

   ![右圆CTA](/help/forms/using/assets/right_circle_cta_new.png)

   表单会填充到Aya最后一个条目的点。 Aya已输入了她的所有信息并准备提交。

   ![提交自适应表单](/help/forms/using/assets/submit_adaptive_form.png)

   提交后，Aya会收到一封电子邮件，该电子邮件将打开并准备使用Adobe Sign进行电子签名。

**用户说明：**

1. 提交后，将显示感谢页面。
1. 导航到您的电子邮件客户端并查找Adobe Sign电子邮件。
1. 单击指向Adobe Sign的链接。

   ![Adobe sign链接](/help/forms/using/assets/adobe_sign_link.png)

**用户说明：**

1. 选中“我&#x200B;**同意**”框。
1. 单击“**接受**”。
1. 滚动到审阅文档的底部。
1. 单击高亮显示的黄色选项卡以签署文档。

   ![签署文档](/help/forms/using/assets/sign_document_new.png)![签署测试文档](/help/forms/using/assets/sign_test_document.png)

## 政府代理(George) {#government-agent-george}

![政府代理乔治](/help/forms/using/assets/george_lang-1.png)

**本节：** 乔治是政府机构的业务分析师，Aya是向其请求服务。 George有一个仪表板，在该环境中他可以查看分配给他的所有服务请求应用程序以供审阅。

### George User Story（AEM收件箱） {#george-user-story-aem-inbox}

**用户说明：**

1. 导航到 *https://&lt;aemserver>:&lt;port>/aem/start.html*
1. 单击用户图标（右上角），然后使用“**Sign Out**”（注销）或“**Impersonate as**”（模拟为）菜单选项（如果您当前已与管理用户登录）。

   1. 登录方式：

      1. **用户：** george.lang
      1. **密码：** 口令
   1. 或模拟：

      1. 在“模&#x200B;**拟为**”字段中键&#x200B;**入“George**”。

      1. 单击“确定”以模拟。


1. 从右上角，单击通知（铃）图标。
1. 单击“**全部视图**”导航到收件箱。
1. 从收件箱中，打开最新的“**Health Benefits Application Review**”任务。

   ![健康效益应用审查](/help/forms/using/assets/health_benefits.png)

### George User Story（AEM收件箱和MS Dynamics） {#george-user-story-aem-inbox-and-ms-dynamics}

由于集成了数据并实现了自动工作流,Aya的应用程序以及在提交数据时自动生成的CRM记录也随之出现。

**用户说明：**

1. 打开并检查只读自适应表单。
1. 单击“**Open MS Dynamics**”按钮，在新窗口中打开MS Dynamics记录。
1. 在CRM中，您可以看到所有信息都可以更新

   1. （可选）在Dynamics中直接添加一些审阅备注。

1. 关闭并返回AEM收件箱。

   ![MS Dynamics记录](/help/forms/using/assets/ms_dynamics.png)

### George User Story（返回AEM收件箱） {#george-user-story-back-to-aem-inbox}

George批准了Aya的应用程序，并且由于现有的自动工作流程，确认电子邮件也会发送到Aya。

**用户说明：**

1. 导航到左上角，然后单击“批准&#x200B;****”以批准此应用程序。
1. 在该模式中，您可以为CX潜在客户留言。
1. 单击完成。
1. （公民角色）打开电子邮件客户端，视图发送给Aya的电子邮件。

   ![视图发送到Aya的电子邮件](/help/forms/using/assets/email_client.png)

## CX潜在客户(Camila) {#cx-lead-camila}

![Camila（CX潜在客户）](/help/forms/using/assets/camila_santos-1.png)

**本节：** Camila CX Lead与Aya建立了欢迎电话联系，以说明如何利用她获得批准的政府服务。

### Camila用户案例（AEM收件箱和MS Dynamics） {#camila-user-story-aem-inbox-ms-dynamics}

**用户说明：**

1. 导航到 *https://&lt;aemserver>:&lt;port>/aem/start.html*
1. 单击用户图标（右上角），然后使用“**Sign Out**”（注销）或“**Impersonate as**”（模拟为）菜单选项（如果您当前已与管理用户登录）。

   1. 登录方式：

      1. **用户**:卡米拉·桑托斯
      1. **密码**:口令
   1. 或模拟：

      1. 在“模&#x200B;**拟为**”字段中键&#x200B;**入“Camila**”。

      1. 单击“确定”以模拟。


1. 从右上角，单击通知（铃）图标。
1. 单击“**全部视图**”导航到收件箱。
1. 从收件箱中，打开最新的“新联&#x200B;**系人批准**”任务。

   ![新的联系人批准](/help/forms/using/assets/new_contact_approval.png)

   **用户说明：**

1. 打开并检查只读自适应表单。
1. 单击“**Open MS Dynamics**”按钮，在新窗口中打开MS Dynamics记录。
1. 在CRM中，您可以看到所有信息都可以更新

   1. （可选）直接在Dynamics中添加新的调用活动。
   1. 打开“**活动**”部分。
   1. 单击“新&#x200B;**电话呼叫**”选项。
   1. 添加电话呼叫详细信息。
   1. 保存并关闭窗口。

1. 返回AEM，导航到左上角，然后单击“提&#x200B;**交**”以提交应用程序。
1. 在该模式中，您可以留言。
1. 单击完成。

   ![活动选项卡](/help/forms/using/assets/activities_tab.png)![确认新联系人](/help/forms/using/assets/confirm_new_contact.png)

## 欢迎凯特市民（阿亚） {#welcome-kit-citizen-aya}

**本节：** Aya收到一封电子邮件，其中包含一个指向交互式通信的链接，该链接概括了Aya的优点，还包括要填写的表单字段。 附加PDF优势声明并链接到邮件中的交互式通信函（与交互式通信具有相同的主题／品牌）。

### Aya用户案例（电子邮件客户端） {#aya-user-story-email-client}

**用户说明：**

1. 找到并打开欢迎工具包电子邮件。
1. 滚动到页面底部的PDF附件。
1. 单击以打开PDF附件。
1. 在电子邮件客户端中向上滚动，然后单击“**在线视图欢迎工具包**”。

   1. 这将打开同一渠道的Web文档版。

1. 要直接快速参考PDF，请执行以下操作：

   *https://&lt;aemserver>:&lt;port>/aem/formdetails.html/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook*

1. 要直接快速参考IC:

   *https://&lt;aemserver>:&lt;port>/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook/jcr:content?渠道=web&amp;mode=disabled*

   ![Welcome Benefits Handbook](/help/forms/using/assets/welcome_benefits_handbook.png) ![Interactive Communication Link](/help/forms/using/assets/interactive_communication.png)

## 续订提醒市民(Aya) {#renewal-reminder-citizen-aya}

**本节：** 卡米拉还计划了一年后的沟通提醒。 （自动／执行和通过电子邮件发送的工作流步骤）。

### Aya用户案例（电子邮件客户端） {#aya-user-story-email-client-1}

**用户说明：**

1. 导航到您的电子邮件客户端。
1. 找到并打开续订提醒电子邮件。
1. 单击“提交&#x200B;**新应用程序**”按钮以打开自适应表单。

   1. 此部分有意留空以支持阶段2中的数据预填充。
   ![续订提醒电子邮件](/help/forms/using/assets/renewal_reminder_email.png)

## Analytics CX Lead(Camila) {#analytics-cx-lead-camila}

**本节：** 卡米拉导航到仪表板，她可以在此处查看机构KPI的各个方面，如开始填写服务请求表并放弃的公民百分比、从请求提交到批准／拒绝响应的平均时间长度以及她发送给公民的福利手册的参与统计数据。

### Camila评论网站报告(We.Gov Adobe Analytics) {#camila-reviews-sites-reporting-we-gov-adobe-analytics}

1. 导航到 *https://&lt;aemserver>:&lt;port>/sites.html/content*
1. 选择“**AEM Forms We.Gov Site**”以视图网站页面。
1. 选择其中一个网站页面（例如“主页”），然后选择“**Analytics &amp; Recommendations**”。

   ![分析和推荐](/help/forms/using/assets/analytics_recommendation.jpg)

1. 在此页上，您将看到从Adobe Analytics获取的与AEM站点页面相关的信息(注意：设计时，此信息会从Adobe Analytics中定期刷新，不会实时显示)。

   ![Adobe Analytics关键指标](/help/forms/using/assets/analytics_key_metrics.jpg)

1. 返回页面视图页面（在步骤3.中访问），您还可以通过将显示设置更改为“视图视图”中的视图项来列表页面&#x200B;**视图**。
1. 找到“**视图**”下拉菜单并选择“**列表视图**”。

   ![列表视图下拉菜单中的视图](/help/forms/using/assets/list_view_view_dropdown.jpg)

1. 从同一菜单中，选择“**视图设置**”，然后从“**Analytics**”部分选择要显示的列。

   ![配置列的显示](/help/forms/using/assets/view_setting_analytics.jpg)

1. 单击“**更新**”以使新列可用。

   ![使新列可用](/help/forms/using/assets/new_columns_available.jpg)

### Camila评论表单报告(We.Gov Adobe Analytics) {#camila-reviews-forms-reporting-we-gov-adobe-analytics}

1. 导航至

   *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. 选择“健康&#x200B;**益处登记申请**”自适应表单并选择“分&#x200B;**析报告**”选项。

   ![健康福利的注册申请](/help/forms/using/assets/analytics_report_benefits.jpg)

1. 等待页面加载，并视图Analytics报告数据。

   ![分析报告数据](/help/forms/using/assets/analytics_report_data_updated.jpg)

