---
title: 配置AEM表单以预取域信息
seo-title: Configure AEM forms to prefetchdomain information
description: 如果由于深度嵌套群组或您是多个群组的成员，导致响应速度变慢，请将AEM表单配置为预取域信息。
seo-description: Configure AEM forms to prefetch domain information if you experience a slower response time due to deeply nested groups or if you are a member of many groups.
uuid: 53c8995e-3f9d-42e8-9f75-cee7debe6ce1
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f9a3f897-90c6-4942-8a86-aae510298f2a
exl-id: cf5283a5-dbfb-460d-a8bd-11cd15ab8640
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# 配置AEM表单以预取域信息 {#configure-aem-forms-to-prefetchdomain-information}

如果用户属于多个组（例如，500个或更多）或者这些组嵌套得很深（例如，30个级别），则用户响应速度可能会较慢。 如果您遇到此问题，可以将AEM表单配置为从特定域预取信息。

1. 在管理控制台中，单击 **[!UICONTROL 设置>用户管理>配置>导入和导出配置文件]**.
1. 要将当前配置设置导出到文件，请单击 **[!UICONTROL 导出]** 并将配置文件保存到其他位置。
1. 添加以下节点（以粗体标记）：

   ```xml
    <node name="UM">
    <map/>
    <node name="PrincipalCache">
        <map>
            <entry key="principalCacheSize" value="1000"/>
            <entry key="principalCacheBatchFetchSize" value="10"/>
            <entry key="rebuildCacheAfterSync" value="true />
            <entry key="enableFullPrefetch" value="false"/>
            <entry key="principalCacheDomains" value="Domain_Name1/Domain_Name2/Domain_Name3"/>
        <map>
    </node>
    <node name="APSAuditService">
   ```

   在本例中，为预取配置了多个域。 域名以“/”分隔。 上面的示例中显示了使用 *域名1*， *域名2*、和 *域名3*.

1. 要导入更新的文件，请在“用户管理”中单击 **[!UICONTROL 配置>导入和导出配置文件]**.
1. 单击 **[!UICONTROL 浏览]** 要查找文件，请单击“导入”，然后单击 **[!UICONTROL 确定]**.
