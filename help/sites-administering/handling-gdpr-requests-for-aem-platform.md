---
title: 处理AEM Foundation的GDPR请求
seo-title: 处理AEM Foundation的GDPR请求
description: 'null'
seo-description: 'null'
uuid: d470061c-bbcf-4d86-9ce3-6f24a764ca39
contentOwner: sarchiz
discoiquuid: 8ee843b6-8cea-45fc-be6c-99c043f075d4
translation-type: tm+mt
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780

---


# 处理AEM Foundation的GDPR请求{#handling-gdpr-requests-for-the-aem-foundation}

>[!IMPORTANT]
>
>GDPR在以下各节中用作示例，但涵盖的详细信息适用于所有数据保护和隐私法规；如GDPR、CCPA等。

## AEM Foundation GDPR支持 {#aem-foundation-gdpr-support}

在AEM Foundation级别，存储的个人数据是用户配置文件。 因此，本文中的信息主要介绍如何访问和删除用户配置文件，以分别解决GDPR访问和删除请求。

## 访问用户配置文件 {#accessing-a-user-profile}

### 手动步骤 {#manual-steps}

1. 通过浏览至“设置”-“安全”-“用户” **[!UICONTROL 或直接浏览至]** “ `https://<serveraddress>:<serverport>/libs/granite/security/content/useradmin.html`

   ![useradmin2](assets/useradmin2.png)

1. 然后，通过在页面顶部的搜索栏中键入名称来搜索相关用户：

   ![用户搜索](assets/usersearch.png)

1. 最后，通过单击打开用户配置文件，然后查看“详细信息”选 **[!UICONTROL 项卡]** 。

   ![userprofile_small](assets/userprofile_small.png)

### HTTP API {#http-api}

如前所述，Adobe为访问用户数据提供API，以便于自动化。 您可以使用几种类型的API:

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

*检索用户数据*

使用从上述命令返回的JSON有效负荷的主属性中的节点路径：

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile.-1.json'
```

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profiles.-1.json'
```

## 禁用用户并删除关联的配置文件 {#disabling-a-user-and-deleting-the-associated-profiles}

### 禁用用户 {#disable-user}

1. 打开“用户管理”控制台，并搜索相关用户，如上所述。
1. 将鼠标悬停在用户上并单击选择图标。 配置文件将变为灰色，表示已选择配置文件。

1. 按上方菜单中的“禁用”按钮以禁用用户：

   ![用户禁用](assets/userdisable.png)

1. 最后，确认操作：

   ![image2018-2-6_1-40-58](assets/image2018-2-6_1-40-58.png)

   然后，用户界面将指示用户已通过灰显并向配置文件卡添加锁定来取消激活：

   ![禁用用户](assets/disableduser.png)

### 删除用户配置文件信息 {#delete-user-profile-information}

1. 登录到CRXDE Lite，然后搜索 `[!UICONTROL userId]`:

   ![image2018-2-6_1-57-11](assets/image2018-2-6_1-57-11.png)

1. 打开默认位于以下位置的用 `[!UICONTROL /home/users]` 户节点：

   ![image2018-2-6_1-58-25](assets/image2018-2-6_1-58-25.png)

1. 删除配置文件节点及其所有子节点。 配置文件节点有两种格式，具体取决于AEM版本：

   1. 默认专用配置文件位于 `[!UICONTROL /profile]`
   1. `[!UICONTROL /profiles]`, for new profiles created using AEM 6.5.
   ![image2018-2-6_2-0-4](assets/image2018-2-6_2-0-4.png)

### HTTP API {#http-api-1}

以下过程使用命 `curl` 令行工具说明如何使用调用禁用用户， ****`userId` 并删除默认位置提供的配置文件。

* *发现用户主页*

```shell
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

* *禁用用户*

使用从上述命令返回的JSON有效负荷的主属性中的节点路径：

```shell
curl -X POST -u user:password -FdisableUser="describe the reasons for disabling this user (GDPR in this case)" 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN.rw.userprops.html'
```

* *删除用户配置文件*

使用从帐户发现命令返回的JSON有效负荷的主属性中的节点路径和现成的已知配置文件节点位置：

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```

