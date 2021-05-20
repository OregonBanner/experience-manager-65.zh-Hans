---
title: 更改身份验证的评估顺序
seo-title: 更改身份验证的评估顺序
description: 您可以更改AEM表单评估多个身份验证提供程序的顺序。
seo-description: 您可以更改AEM表单评估多个身份验证提供程序的顺序。
uuid: c2693e5b-cf09-4bb8-815a-2b20ebf6eea0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5434df9c-ecf6-450a-aa7e-d9ab69b66fe6
exl-id: 7e29c9d4-fb82-4308-aac7-0f5cb1f4aef2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# 更改验证评估的顺序{#change-the-order-of-evaluation-for-authentication}

如果您配置了多个身份验证提供程序，则可以更改AEM表单对其进行身份验证评估的顺序。 config.xml文件中列出的身份验证提供程序的顺序决定了身份验证评估的顺序。

1. 在管理控制台中，单击设置>用户管理>配置>导入和导出配置文件。
1. 要将当前配置设置导出到文件，请单击“导出”，然后将配置文件保存到其他位置。
1. 在文件中找到以下节点：

   ```xml
    <node name="AuthSchemes">
        <map />
            <node name="CertificateAuth">
                <map>
                    <entry key="order" value="3" />
                    <entry key="name" value="edc.server.auth.scheme.certificate" />
                </map>
        </node>
        <node name="Kerberos">
            <map>
                <entry key="kerberosSPN" value="defaultSPN" />
                <entry key="order" value="1" />
                <entry key="name" value="edc.server.auth.scheme.kerberos" />
            </map>
    </node>
   ```

   在`<entry key="order" value="3" />`中，编辑每个节点的值以设置身份验证评估的顺序。

1. 要导入更新的文件，请在“用户管理”中，单击配置>导入和导出配置文件。
1. 单击“浏览”(Browse)查找文件，单击“导入”(Import)，然后单击“确定”(OK)。
