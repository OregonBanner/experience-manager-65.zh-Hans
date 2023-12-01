---
title: 处理Adobe Experience Manager Foundation的GDPR请求
description: 处理Adobe Experience Manager Foundation的GDPR请求
contentOwner: sarchiz
exl-id: 411d40ab-6be8-4658-87f6-74d2ac1a4913
source-git-commit: 5e56441d2dc9b280547c91def8d971e7b1dfcfe3
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 45%

---

# 处理Adobe Experience Manager (AEM)基金会的GDPR请求{#handling-gdpr-requests-for-the-aem-foundation}

>[!IMPORTANT]
>
>以下部分使用GDPR作为示例，但包含的详细信息适用于所有数据保护和隐私法规；例如GDPR、CCPA等。

## AEM Foundation GDPR支持 {#aem-foundation-gdpr-support}

在AEM Foundation级别，存储的个人数据是用户配置文件。 因此，本文中的信息主要介绍如何访问和删除用户配置文件，以及分别处理GDPR访问和删除请求。

## 访客用户配置文件 {#accessing-a-user-profile}

### 手动步骤 {#manual-steps}

1. 通过浏览至，打开用户管理控制台 **[!UICONTROL 设置 — 安全 — 用户]** 或直接浏览到 `https://<serveraddress>:<serverport>/libs/granite/security/content/useradmin.html`

   ![useradmin2](assets/useradmin2.png)

1. 然后，通过在页面顶部的搜索栏中键入有问题的用户的名称来搜索该用户：

   ![usersearch](assets/usersearch.png)

1. 最后，单击用户配置文件以将其打开，然后查看&#x200B;**[!UICONTROL 详细信息]**&#x200B;选项卡下的内容。

   ![userprofile_small](assets/userprofile_small.png)

### HTTP API {#http-api}

如前所述，Adobe 提供了用于访问用户数据的 API 来促进自动化。有多种类型的 API 可供您使用：

**UserProperties API**

```shell
curl -u user:password http://localhost:4502/libs/granite/security/search/profile.userproperties.json\?authId\=cavery
```

**Sling API**

*发现用户主页：*

```xml
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

*正在检索用户数据*

使用从上述命令返回的 JSON 负载的 home 属性中的节点路径：

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile.-1.json'
```

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profiles.-1.json'
```

## 禁用用户并删除关联的配置文件 {#disabling-a-user-and-deleting-the-associated-profiles}

### 禁用用户 {#disable-user}

1. 如上所述，打开用户管理控制台并搜索有问题的用户。
1. 将鼠标悬停在用户上方并单击选择图标。配置文件显示为灰色，表明它已被选中。

1. 按上方菜单中的禁用按钮禁用用户：

   ![userdisable](assets/userdisable.png)

1. 最后，确认操作：

   ![image2018-2-6_1-40-58](assets/image2018-2-6_1-40-58.png)

   用户界面指示用户已通过灰显配置文件卡并向其添加锁定而被停用：

   ![disableduser](assets/disableduser.png)

### 删除用户配置文件信息 {#delete-user-profile-information}

1. 登录到CRXDE Lite，然后搜索 `[!UICONTROL userId]`：

   ![image2018-2-6_1-57-11](assets/image2018-2-6_1-57-11.png)

1. 打开位于下的用户节点 `[!UICONTROL /home/users]` 默认情况下：

   ![image2018-2-6_1-58-25](assets/image2018-2-6_1-58-25.png)

1. 删除配置文件节点及其所有子节点。 配置文件节点有两种格式，具体取决于AEM版本：

   1. 下的默认个人资料 `[!UICONTROL /profile]`
   1. `[!UICONTROL /profiles]`，适用于使用AEM 6.5创建的新配置文件。

   ![image2018-2-6_2-0-4](assets/image2018-2-6_2-0-4.png)

### HTTP API {#http-api-1}

以下过程使用 `curl` 命令行工具，说明如何使用 **[!UICONTROL cavery]** `userId` 并删除配置文件 `cavery` 在默认位置可用的文件。

* *发现用户主页*

```shell
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

* *禁用用户*

使用从上述命令返回的 JSON 负载的 home 属性中的节点路径：

```shell
curl -X POST -u user:password -FdisableUser="describe the reasons for disabling this user (GDPR in this case)" 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN.rw.userprops.html'
```

* *删除用户配置文件*

使用从帐户发现命令返回的 JSON 负载的 home 属性中的节点路径和已知的现成配置文件节点位置：

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```
