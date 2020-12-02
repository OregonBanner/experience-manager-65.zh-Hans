---
title: 配置AEM表单以预取域信息
seo-title: 配置AEM表单以预取域信息
description: 如果由于嵌套较深的组或您是许多组的成员而导致响应时间较慢，请将AEM表单配置为预回迁域信息。
seo-description: 如果由于嵌套较深的组或您是许多组的成员而导致响应时间较慢，请将AEM表单配置为预回迁域信息。
uuid: 53c8995e-3f9d-42e8-9f75-cee7debe6ce1
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f9a3f897-90c6-4942-8a86-aae510298f2a
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# 将AEM表单配置为预取域信息{#configure-aem-forms-to-prefetchdomain-information}

如果用户属于多个组（例如，500或更多），或者这些组深度嵌套（例如，30个级别），则可能会遇到较慢的响应时间。 如果遇到此问题，可将AEM表单配置为从某些域预取信息。

1. 在管理控制台中，单击&#x200B;**[!UICONTROL 设置>用户管理>配置>导入和导出配置文件]**。
1. 要将当前配置设置导出到文件，请单击&#x200B;**[!UICONTROL 导出]**，然后将配置文件保存到另一个位置。
1. 添加以下节点（以粗体标记）:

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

   在此示例中，为预取配置了多个域。 域名以“/”分隔。 以上示例中显示了这一点，其中&#x200B;*Domain_Name1*、*Domain_Name2*&#x200B;和&#x200B;*Domain_Name3*。

1. 要导入更新的文件，请在“用户管理”中，单击&#x200B;**[!UICONTROL “配置”>“导入和导出配置文件”]**。
1. 单击&#x200B;**[!UICONTROL 浏览]**&#x200B;以查找文件，单击“导入”，然后单击&#x200B;**[!UICONTROL 确定]**。

