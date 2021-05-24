---
title: 为AEM Foundation处理GDPR请求
seo-title: 为AEM Foundation处理GDPR请求
description: 为AEM Foundation处理GDPR请求
seo-description: 'null'
uuid: d470061c-bbcf-4d86-9ce3-6f24a764ca39
contentOwner: sarchiz
discoiquuid: 8ee843b6-8cea-45fc-be6c-99c043f075d4
exl-id: 411d40ab-6be8-4658-87f6-74d2ac1a4913
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 6%

---

# 处理AEM Foundation的GDPR请求{#handling-gdpr-requests-for-the-aem-foundation}

>[!IMPORTANT]
>
>GDPR用作以下部分的示例，但相关详细信息适用于所有数据保护和隐私法规；例如GDPR、CCPA等

## AEM Foundation GDPR支持{#aem-foundation-gdpr-support}

在AEM Foundation级别，存储的个人数据是用户配置文件。 因此，本文中的信息主要介绍如何访问和删除用户配置文件，以及如何分别处理GDPR访问和删除请求。

## 访问用户配置文件{#accessing-a-user-profile}

### 手动步骤{#manual-steps}

1. 通过浏览到&#x200B;**[!UICONTROL Settings - Security - Users]**&#x200B;或直接浏览到`https://<serveraddress>:<serverport>/libs/granite/security/content/useradmin.html`打开用户管理控制台

   ![useradmin2](assets/useradmin2.png)

1. 然后，通过在页面顶部的搜索栏中键入名称来搜索相关用户：

   ![用户搜索](assets/usersearch.png)

1. 最后，单击以打开用户配置文件，然后查看&#x200B;**[!UICONTROL Details]**&#x200B;选项卡下的。

   ![userprofile_small](assets/userprofile_small.png)

### HTTP API {#http-api}

如前所述，Adobe为访问用户数据提供了API，以便于自动化。 您可以使用以下几种类型的API:

**用户属性API**

```shell
curl -u user:password http://localhost:4502/libs/granite/security/search/profile.userproperties.json\?authId\=cavery
```

**Sling API**

*了解用户主页：*

```xml
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

*检索用户数据*

使用从上述命令返回的JSON有效负载的home属性中的节点路径：

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile.-1.json'
```

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profiles.-1.json'
```

## 禁用用户并删除关联的配置文件{#disabling-a-user-and-deleting-the-associated-profiles}

### 禁用用户{#disable-user}

1. 如上所述，打开用户管理控制台并搜索相关用户。
1. 将鼠标悬停在用户上，然后单击选择图标。 用户档案将变为灰色，表示已选择该用户档案。

1. 按上方菜单中的禁用按钮以禁用用户：

   ![userdisable](assets/userdisable.png)

1. 最后，确认操作：

   ![image2018-2-6_1-40-58](assets/image2018-2-6_1-40-58.png)

   随后，用户界面将通过注销并向用户档案卡添加锁来指示用户已被停用：

   ![禁用用户](assets/disableduser.png)

### 删除用户配置文件信息{#delete-user-profile-information}

1. 登录CRXDE Lite，然后搜索`[!UICONTROL userId]`:

   ![image2018-2-6_1-57-11](assets/image2018-2-6_1-57-11.png)

1. 默认情况下，打开位于`[!UICONTROL /home/users]`下的用户节点：

   ![image2018-2-6_1-58-25](assets/image2018-2-6_1-58-25.png)

1. 删除配置文件节点及其所有子节点。 配置文件节点有两种格式，具体取决于AEM版本：

   1. `[!UICONTROL /profile]`下的默认专用配置文件
   1. `[!UICONTROL /profiles]`，用于使用AEM 6.5创建的新用户档案。

   ![image2018-2-6_2-0-4](assets/image2018-2-6_2-0-4.png)

### HTTP API {#http-api-1}

以下过程使用 `curl` 命令行工具说明如何使用 **[!UICONTROL cavery]** `userId` 禁用用户，并删除默认位置提供的配置文件。

* *了解用户主页*

```shell
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

* *禁用用户*

使用从上述命令返回的JSON有效负载的home属性中的节点路径：

```shell
curl -X POST -u user:password -FdisableUser="describe the reasons for disabling this user (GDPR in this case)" 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN.rw.userprops.html'
```

* *删除用户配置文件*

使用从帐户发现命令返回的JSON有效负载的home属性中的节点路径和已知的现成配置文件节点位置：

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```
