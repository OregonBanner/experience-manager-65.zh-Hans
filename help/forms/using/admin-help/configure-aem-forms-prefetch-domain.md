---
title: 配置AEM表单以预取域信息
description: 如果由于深度嵌套群组而导致响应时间变慢或者您是多个群组的成员，请配置AEM表单以预取域信息。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: cf5283a5-dbfb-460d-a8bd-11cd15ab8640
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# 配置AEM表单以预取域信息 {#configure-aem-forms-to-prefetchdomain-information}

如果用户属于多个组（例如，500个或更多）或这些组嵌套得很深（例如，30个级别），则用户响应速度可能会较慢。 如果遇到此问题，可以将AEM表单配置为从特定域预取信息。

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

   在此示例中，为预取配置了多个域。 域名用“/”分隔。 以上示例显示了使用 *域名1*， *域名2*、和 *域名3*.

1. 要导入更新的文件，请在“用户管理”中单击 **[!UICONTROL 配置>导入和导出配置文件]**.
1. 单击 **[!UICONTROL 浏览]** 要查找文件，请单击“导入”，然后单击 **[!UICONTROL 确定]**.
