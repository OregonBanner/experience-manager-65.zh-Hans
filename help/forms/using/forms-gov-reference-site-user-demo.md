---
title: We.Gov和We.Finance参考站点演练
seo-title: We.Gov和We.Finance参考站点演练
description: 使用虚构的用户和组，通过We.Gov和We.Finance演示包来执行AEM Forms任务。
seo-description: 使用虚构的用户和组，通过We.Gov和We.Finance演示包来执行AEM Forms任务。
uuid: 797e301a-36ed-4bae-9ea8-ee77285c786d
contentOwner: anujkapo
discoiquuid: ddb3778b-be06-4cde-bc6e-0994efa42b18
docset: aem65
exl-id: 288d5459-bc69-4328-b6c9-4b4960bf4977
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2548'
ht-degree: 1%

---

# We.Gov和We.Finance引用站点演练{#we-gov-reference-site-walkthrough}

## 先决条件{#pre-requisites}

按照[设置和配置We.Gov和We.Finance引用站点](../../forms/using/forms-install-configure-gov-reference-site.md)中所述设置引用站点。

## 用户文章{#user-story}

* AEM Forms

   * 自动化表单转换
   * 创作
   * 表单数据模型/数据源

* AEM Forms

   * 数据捕获
   * （可选）数据集成(MS Dynamics)
   * （可选）Adobe Sign

* 工作流
* 电子邮件通知
* （可选）客户通信

   * 打印渠道
   * Web 渠道

* Adobe Analytics
* 数据源集成

### 虚构的用户和组{#fictitious-users-and-groups}

We.Gov演示包附带以下内置虚构用户：

* **阿雅·谭**:有资格从政府机构获得服务的公民

![虚构用户](/help/forms/using/assets/aya_tan_new.png)

* **乔治·朗**:We.Gov代理业务分析师

![虚构用户](/help/forms/using/assets/george_lang.png)

* **卡米拉·桑托斯**:We.Gov代理CX领导

![虚构用户](/help/forms/using/assets/camila_santos.png)

还包括以下组：

* **We.Gov Forms用户**

   * George Lang（成员）
   * 卡米拉·桑托斯（成员）

* **We.Gov用户**

   * George Lang（成员）
   * 卡米拉·桑托斯（成员）
   * 谭雅（成员）

### 演示概述术语图例{#demo-overview-terms-legend}

1. **模拟**:AEM演示中的已定义用户和群组。
1. **按钮**:彩色矩形或带圆圈的箭头用于导航。
1. **单击**:执行用户文章中的操作。
1. **链接**:位于We.Gov网站主菜单顶部。
1. **用户说明**:浏览用户文章时要遵循的一组数字步骤。
1. **Forms门户**: *https://&lt;aemserver>:&lt;port>/content/we-gov/formsportal.html*
1. **移动设备视图**:We.Gov用户通过重新调整浏览器大小来复制移动设备视图。
1. **桌面视图**:We.gov用户可在笔记本电脑或台式机上观看演示。
1. **预屏幕表单**:We.Gov网站主页上的表单。
1. **自适应表单**:We.gov演示的注册申请表。

   *https://&lt;aemserver>:&lt;port>/content/forms/af/adobe-gov-forms/enrollment-application-for-health-benefits.html*

1. **AdobeWe.Gov网站**: *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. **Adobe收件箱**:位于AEM后端上 [的](assets/bell.svg) 顶部菜单栏。

   *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. **电子邮件客户端**:查看电子邮件的首选方式(Gmail、Outlook)
1. **CTA**:行动动员
1. **导航**:在浏览器页面上查找特定引用点。
1. **AFC**:automated forms conversion

## automated forms conversion（卡米拉）{#automated-forms-conversion}

**此部分**:Camila “CX Lead”现有的基于PDF的表单，该表单用作基于纸面的流程的一部分。作为现代化工作的一部分，她希望使用此PDF表单自动创建新的现代自适应Forms。

### automated forms conversion- We.Gov(Camila){#automated-forms-conversion-wegov}

1. 导航到&#x200B;*https://&lt;aemserver>:&lt;port>/aem/start.html*

1. 登录方式：
   * **用户**:卡米拉·桑托斯
   * **密码**:密码
1. 从主页选择Forms > Forms与文档> AEM Forms We.gov Forms > AFC。
1. 卡米拉将PDF上传到AEM Forms。

   ![上传表单](assets/aftia-upload-form.jpg)

1. 然后，Camilla选择PDF表单并单击&#x200B;**启动自动转换**&#x200B;以开始转换过程。 如果已转换表单，则可能需要单击&#x200B;**覆盖转化**。

   >[!NOTE]
   >
   >请注意，AFC中的设置已为最终用户预配置，这意味着不应更改这些设置。

   * **可选**:如果您希望使用无障碍超海洋主题，只需单击指定自适应表单主题并选择选项列表中显示的无障碍超海洋主题。

   ![开始转化](assets/aftia-start-conversion.jpg)

   ![超海洋主题](assets/aftia-upload-conversion-settings.jpg)

   完成百分比状态会在转化期间显示。 显示&#x200B;**Converted**&#x200B;状态后，单击&#x200B;**output**&#x200B;文件夹，选择自适应表单，然后单击&#x200B;**Edit**&#x200B;打开转换后的表单。

1. 然后，卡米拉审阅表单，并确保所有字段都存在

   ![查看转化](assets/aftia-review-conversion.jpg)

1. 然后，卡米拉开始编辑表单。 她选择“根面板”>“编辑”（扳手）>从“面板布局”下拉菜单中选择“顶部的制表符”>选中“复选框”。

   ![查看属性](assets/aftia-review-properties.jpg)

1. 然后，Camilla添加所有必需的CSS和字段修改以生产最终产品。

   ![添加CSS](assets/aftia-add-css.jpg)

### 表单数据模型和数据源(Camila){#data-sources}

**此部分**:转换文档并生成自适应表单后，Camila需要将自适应表单连接到数据源。

1. Camila会打开在[Automated forms conversion- We.Gov](#automated-forms-conversion-wegov)中转换的表单上的属性。

1. 然后，Camila从选项列表中选择“表单模型”>“从选择中选择表单数据模型”>“从选项列表中选择We.gov注册FDM”。

1. 单击保存并关闭按钮。

   ![FDM选择](assets/aftia-select-fdm.jpg)

1. Camila单击&#x200B;**output**&#x200B;文件夹，选择自适应表单，然后单击&#x200B;**编辑**&#x200B;以打开已完成的We.Gov表单。
1. Camila选择自适应表单字段并单击![配置图标](assets/configure-icon.svg)。 她使用&#x200B;**Bind Reference**&#x200B;字段创建与表单数据模型实体的绑定。 她对自适应表单中的所有字段重复此步骤。

### 表单无障碍测试(Camila){#form-accessibility-testing}

Camila还将验证创建的内容是否按照公司标准正确构建且完全可访问。

1. Camila单击&#x200B;**output**&#x200B;文件夹，选择自适应表单，然后单击&#x200B;**预览**&#x200B;以打开已完成的We.Gov表单。

1. 在Chrome开发人员工具中打开审核选项卡。

1. 执行辅助功能检查以验证自适应表单。

   ![辅助功能检查](assets/aftia-accessibility.jpg)

## 自适应表单移动设备视图演示(Aya){#mobile-view-demo}

**此部分必须在演示之前执行。**

**用户说明：**

1. 导航到：*https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. 登录方式：

   1. **用户**:aya.tan
   1. **密码**:密码

1. 重新调整浏览器窗口的大小或使用浏览器的模拟器来复制移动设备大小。

### We.Gov网站(Aya){#aya-user-story-we-gov-website}

![虚构用户](/help/forms/using/assets/aya_tan_new-1.png)

**此部分**:阿亚是公民。她从一位朋友那里得知她可能有资格从政府机构获得服务。 Aya从手机导航到We.Gov网站，了解有关她有资格享受的服务的更多信息。

### We.Gov Pre-Screener(Aya){#aya-user-story-we-gov-pre-screener}

Aya回答了几个问题，通过在手机上填写一份简短的自适应表格来确认她是否符合条件。

**用户说明：**

1. 在每个下拉字段中进行选择。

   >[!NOTE]
   >
   >如果用户每年的收入超过20万美元，则他们将不符合条件。

1. 单击“**我是否符合条件？**” 按钮.
1. 单击“**Apply Now**”按钮以继续。

   ![立即应用链接](/help/forms/using/assets/apply_now_link.png)

### We.Gov自适应表单(Aya){#aya-user-story-we-gov-adaptive-form}

Aya发现她符合条件，开始填写她的申请，以在其移动设备上请求服务。

Aya需要先在家中查看一些文档，然后才能完成服务请求申请。 她从移动设备保存并退出应用程序。

**用户说明：**

1. 填写“基本信息”字段，以下是必填字段和下拉列表：

   1. 基本信息

      1. 名字
      1. 姓氏
      1. 出生日期
      1. 电子邮件

1. 使用以下&#x200B;**动态逻辑**&#x200B;使用&#x200B;**系列状态**&#x200B;下拉列表演示动态功能：

   1. **单个**:显示“亲属”面板的下一个
   1. **已婚**:显示婚内抚养人面板
   1. **离婚**:显示“亲属”面板的下一个
   1. **丧偶**:显示“亲属”面板的下一个
   1. **你有孩子吗？**:（是/否）用于显示子从属面板的单选按钮。

      1. （添加/删除）按钮，可添加/删除多个子从属面板。

1. 单击灰色菜单栏中的向右箭头。
1. 单击底部的“保存”按钮。

   ![自适应表单详细信息](/help/forms/using/assets/adaptive_form.png)

## 桌面演示{#desktop-demo}

**本节：** 回到家中，Aya找到了她需要的信息，并从她的桌面恢复应用程序。Aya导航到在线表单门户以恢复其应用程序。 借助一些简单的自定义功能，代理机构还可以自动生成链接并通过电子邮件发送以恢复应用程序。

### 连续自适应表单(Aya){#aya-user-story-continued-adaptive-form}

**用户说明：**

1. 导航到&#x200B;*https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. 在导航栏中，选择单击“**Online Services**”。
1. 从“Forms草案”面板中，选择现有的“健康福利登记申请”。

   ![健康福利的注册申请](/help/forms/using/assets/enrollment_application.png)

   外观和感觉是相同的，她无需重新输入任何数据。

   **用户说明：**

1. 单击右侧的Circle CTA以移到下一部分。

   ![右圆CTA](/help/forms/using/assets/right_circle_cta_new.png)

   表格填充到Aya最后一个入口的点。 Aya已输入了她的所有信息并准备提交。

   ![提交自适应表单](/help/forms/using/assets/submit_adaptive_form.png)

   >[!NOTE]
   >
   >当Aya填写电话号码字段时，她必须将其作为连续的11位数字进行填充，不带短划线、空格或连字符。

   提交Aya后，会收到感谢页面。 或者，她还会收到一封电子邮件，可以打开该电子邮件，以电子方式与Adobe Sign签署记录文档。

### 可选：Adobe Sign(Aya){#adobe-sign}

**用户说明：**

1. 导航到您的电子邮件客户端，然后找到Adobe Sign电子邮件。
1. 单击指向Adobe Sign的链接。

   ![Adobe链接](/help/forms/using/assets/adobe_sign_link.png)

**用户说明：**

1. 选中“**I agree**”框。
1. 单击“**Accept**”。
1. 滚动到审阅文档的底部。
1. 单击高亮显示的黄色选项卡以对文档进行签名。

   ![签署文](/help/forms/using/assets/sign_document_new.png) ![档签署测试文档](/help/forms/using/assets/sign_test_document.png)

## 政府代理人（乔治）{#government-agent-george}

![乔治](/help/forms/using/assets/george_lang-1.png)

**本节：** George是政府机构Aya的业务分析师，正在向Aya请求服务。George有一个仪表板，他可以在仪表板中看到分配给他审阅的所有服务请求应用程序。

### AEM收件箱(George){#george-user-story-aem-inbox}

**用户说明：**

1. 导航到&#x200B;*https://&lt;aemserver>:&lt;port>/aem/start.html*
1. 单击用户图标（右上角），并使用“**注销**”或“**模拟为**”菜单选项（如果您当前已与管理用户登录）。

   1. 登录方式：

      1. **用户：** george.lang
      1. **密码：** 密码
   1. 或模拟：

      1. 在“**模拟为**”字段中键入“**George**”。

      1. 单击确定以模拟。


1. 单击右上角的通知（铃）图标。
1. 单击“**查看全部**”以导航到收件箱。
1. 从收件箱中，打开最新的“**Health Benefits Application Review**”任务。

   ![健康优势应用程序审查](/help/forms/using/assets/health_benefits.png)

### 可选：AEM Inbox &amp; MS Dynamics(George){#george-user-story-aem-inbox-and-ms-dynamics}

借助数据集成和自动化工作流，Aya的应用程序以及在提交数据时自动生成的CRM记录会一起显示。

**用户说明：**

1. 打开并检查只读自适应表单。
1. 单击“**打开MS Dynamics**”按钮，以在新窗口中打开MS Dynamics记录。
1. 在CRM中，您可以看到所有信息都可以更新

   1. （可选）在Dynamics中直接添加一些审阅注释。

1. 关闭并返回AEM收件箱。

   ![MS Dynamics记录](/help/forms/using/assets/ms_dynamics.png)

### 返回AEM收件箱(George){#george-user-story-back-to-aem-inbox}

George批准了Aya的应用程序，并且由于现有的自动工作流，确认电子邮件也会发送给Aya。

**用户说明：**

1. 导航到左上角，然后单击“**Approve**”以批准应用程序。
1. 在该模式窗口中，您可以为CX潜在客户留言。
1. 单击完成。
1. （公民角色）打开电子邮件客户端以查看发送到Aya的电子邮件。

   ![查看发送到Aya的电子邮件](/help/forms/using/assets/email_client.png)

## CX潜在客户(Camila){#cx-lead-camila}

![Camila（CX潜在客户）](/help/forms/using/assets/camila_santos-1.png)

**本节：** Camila the CX Lead与Aya建立欢迎电话联系，以说明如何利用她获得批准的政府服务。

### （可选）AEM Inbox &amp; MS Dynamics {#camila-user-story-aem-inbox-ms-dynamics}

**用户说明：**

1. 导航到&#x200B;*https://&lt;aemserver>:&lt;port>/aem/start.html*
1. 单击用户图标（右上角），并使用“**注销**”或“**模拟为**”菜单选项（如果您当前已与管理用户登录）。

   1. 登录方式：

      1. **用户**:卡米拉·桑托斯
      1. **密码**:密码
   1. 或模拟：

      1. 在“**模拟为**”字段中键入“**Camila**”。

      1. 单击确定以模拟。


1. 单击右上角的通知（铃铛）图标。
1. 单击“**查看全部**”以导航到收件箱。
1. 从收件箱中，打开最新的“**New Contact Approval**”任务。

![新联系人批准](/help/forms/using/assets/new_contact_approval.png)

**（可选）用户说明：**

1. 打开并检查只读自适应表单。
1. 单击“**打开MS Dynamics**”按钮，以在新窗口中打开MS Dynamics记录。
1. 在CRM中，您可以看到所有信息都可以更新

   1. （可选）直接在Dynamics中添加新的调用活动。
   1. 打开“**Activities**”部分。
   1. 单击“**新建电话呼叫**”选项。
   1. 添加电话呼叫详细信息。
   1. 保存并关闭窗口。

1. 返回AEM，导航到左上角并单击“**Submit**”以提交应用程序。
1. 在该模式窗口中，您可以留言。
1. 单击完成。

   ![“活动”](/help/forms/using/assets/activities_tab.png) ![选项卡确认新联系人](/help/forms/using/assets/confirm_new_contact.png)

## （可选）欢迎Kit公民(Aya){#welcome-kit-citizen-aya}

**此部分：** Aya收到一封电子邮件，其中包含指向交互式通信的链接，该链接概述了Aya的优势，并且还包含要填写的表单字段。附加了PDF优势声明并链接到邮件中的交互式通信信件（与交互式通信具有相同的主题/品牌）。

### 电子邮件客户端通知(Aya){#aya-user-story-email-client}

**用户说明：**

1. 找到并打开欢迎工具包电子邮件。
1. 滚动到页面底部的PDF附件。
1. 单击以打开PDF附件。
1. 在电子邮件客户端中向上滚动，然后单击“**View welcome kit online**”。

   1. 这将打开同一文档的Web渠道版本。

1. 要直接快速参考PDF，请执行以下操作：

   *https://&lt;aemserver>:&lt;port>/aem/formdetails.html/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook*

1. 要直接快速引用IC，请执行以下操作：

   *https://&lt;aemserver>:&lt;port>/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook/jcr:content?channel=web&amp;mode=preview&amp;wcmmode=disabled*

   ![欢迎福利手](/help/forms/using/assets/welcome_benefits_handbook.png) ![册交互式通信链接](/help/forms/using/assets/interactive_communication.png)

## 续约提醒公民(Aya){#renewal-reminder-citizen-aya}

**此部分：** Camila还会安排一年后的通信提醒。（可自动执行和电子邮件的工作流步骤）。

### 电子邮件客户端通知(Aya){#aya-user-story-email-client-updated}

**用户说明：**

1. 导航到您的电子邮件客户端。
1. 找到并打开续订提醒电子邮件。
1. 单击“**提交新应用程序**”按钮以打开自适应表单。

   1. 此部分有意留空，以支持阶段2中的数据预填充。

   ![续订提醒电子邮件](/help/forms/using/assets/renewal_reminder_email.png)

## （可选）表单数据模型(Camila){#form-data-model}

**此部分**:Camila导航到AEM Forms数据集成，在该集成中，她可以运行快速测试，以查看通过表单数据模型集成发送到外部数据源的信息是否确实存在。

### 表单数据模型(Camila){#form-data-model-camila}

**此部分**:Camila导航到“数据源”页以验证服务器已在Derby数据库中复制的数据。

1. 用户体验完成并完成用户提交后，Camila将导航到AEM Forms中的“数据源”选项卡(**Forms** > **数据集成**)

1. 然后，Camila选择AEM Forms **We.gov FDM**，然后编辑&#x200B;**We.gov注册FDM**。

1. 然后，Camila选择&#x200B;**Contact** > **Read Service**&#x200B;要测试。

   ![联系读取服务](assets/aftia-contact-read-service.jpg)

1. 然后，Camila为测试服务提供联系人ID，然后单击“测试”按钮。 例如，如果您提交了表单，则为1或2。 如果您尚未提交表单，则不会返回任何数据。

   ![联系读取服务](assets/aftia-test-service.jpg)

1. 然后，Camila可以验证数据是否已成功插入数据源。

   * Derby DS中的数据类似于以下格式：

   ```xml
      [
         {
         "ADDRESS_COUNTRY": "USA",
         "LAST_NAME": "Tan",
         "ADDRESS_CITY": "New York",
         "FIRST_NAME": "Aya",
         "ADDRESS_STATE": "AL",
         "ADDRESS_LINE1": "123 Street crescent",
         "GENDER_CODE": "2",
         "ADDRESS_LINE2": "123 Street crescent",
         "ADDRESS_POSTAL_CODE": "90210",
         "BIRTH_DATE": "1991-12-12",
         "CONTACT_ID": 1,
         "MIDDLE_NAME": "M",
         "HAS_CHILDREN_CODE": "0"
         }
   ]
   ```

## （可选）Analytics(Camila){#analytics-cx-lead-camila}

**此部分：** Camila导航到功能板，在功能板中，她可以看到整个机构KPI，例如，开始填写并放弃服务请求表的公民百分比、从请求提交到批准/拒绝响应的平均时间，以及她发送给公民的福利手册的参与统计。

### Adobe Analytics Sites报表(Camila){#camila-reviews-sites-reporting-we-gov-adobe-analytics}

1. 导航到&#x200B;*https://&lt;aemserver>:&lt;port>/sites.html/content*
1. 选择“**AEM Forms We.Gov Site**”以查看网站页面。
1. 选择一个网站页面（例如主页），然后选择“**Analytics &amp; Recommendations**”。

   ![Analytics和推荐](/help/forms/using/assets/analytics_recommendation.jpg)

1. 在此页面上，您将看到从Adobe Analytics获取的与AEM Sites页面相关的信息(注意：通过设计，此信息会从Adobe Analytics定期刷新，且不会实时显示)。

   ![Adobe Analytics关键量度](/help/forms/using/assets/analytics_key_metrics.jpg)

1. 返回页面查看页面（在步骤3中访问）后，您还可以通过更改显示设置来查看“**列表视图**”中的项目来查看页面查看信息。
1. 找到“**View**”下拉菜单，然后选择“**列表视图**”。

   ![“视图”下拉菜单中的列表视图](/help/forms/using/assets/list_view_view_dropdown.jpg)

1. 从同一菜单中，选择“**查看设置**”，然后从“**Analytics**”部分选择要显示的列。

   ![配置列的显示](/help/forms/using/assets/view_setting_analytics.jpg)

1. 单击“**Update**”以使新列可用。

   ![使新列可用](/help/forms/using/assets/new_columns_available.jpg)

### Adobe Analytics Forms报道（卡米拉）{#camila-reviews-forms-reporting-we-gov-adobe-analytics}

1. 导航至

   *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. 选择“**Enrollment Application For Health Benefits**”自适应表单，然后选择“**Analytics报表**”选项。

   ![健康福利的注册申请](/help/forms/using/assets/analytics_report_benefits.jpg)

1. 等待页面加载，并查看Analytics报表数据。

   ![Analytics报表数据](/help/forms/using/assets/analytics_report_data_updated.jpg)
