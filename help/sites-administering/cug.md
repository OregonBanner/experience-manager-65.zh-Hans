---
title: 创建封闭用户组
seo-title: Creating a Closed User Group
description: 了解如何创建封闭用户组。
seo-description: Learn how to create a Closed User Group.
uuid: dc3c7dbd-2e86-43f9-9377-3b75053203b3
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ae57874-a9a1-4208-9001-7f44a1f57cbe
docset: aem65
exl-id: 9efba91d-45e8-42e1-9db6-490d21bf7412
source-git-commit: 64d174cc824c8bf200cece4e29f60f946ee5560e
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 1%

---

# 创建封闭用户组{#creating-a-closed-user-group}

已关闭的用户组(CUG)用于限制对已发布互联网站点内特定页面的访问。 此类页面需要分配的成员登录并提供安全凭据。

要在您的网站中配置此类区域，请执行以下操作：

* [创建实际的已关闭用户组并分配成员](#creating-the-user-group-to-be-used).

* [将此群组应用到所需页面](#applying-your-closed-user-group-to-content-pages) 并选择（或创建）供CUG成员使用的登录页面；在将CUG应用到内容页面时也指定。

* [以某种形式创建一个链接，指向受保护区域内至少一个页面](#linking-to-the-cug-pages)，否则将不可见。

* [配置Dispatcher](#configure-dispatcher-for-cugs) （如果在使用）。

>[!CAUTION]
>
>应始终在创建封闭用户组(CUG)时考虑性能。
>
>尽管CUG中的用户和组数量不受限制，但页面上的大量CUG可能会降低渲染性能。
>
>在进行性能测试时，应始终考虑CUG的影响。

## 创建要使用的用户组 {#creating-the-user-group-to-be-used}

要创建已关闭的用户组，请执行以下操作：

1. 转到 **工具 — 安全性** 从AEM主屏幕。

   >[!NOTE]
   >
   >请参阅 [管理用户和群组](/help/sites-administering/security.md#managing-users-and-groups) 以了解有关创建和配置用户和组的完整信息。

1. 选择 **群组** 下一个屏幕中的卡片。

   ![screenshot_2018-10-30at145502](assets/screenshot_2018-10-30at145502.png)

1. 按 **创建** 按钮以创建新组。
1. 命名新群组；例如， `cug_access`.

   ![screenshot_2018-10-30at151459](assets/screenshot_2018-10-30at151459.png)

1. 转到 **成员** 选项卡，并将所需的用户分配给此组。

   ![screenshot_2018-10-30at151808](assets/screenshot_2018-10-30at151808.png)

1. 激活您分配给CUG的任何用户；在本例中， `cug_access`.
1. 激活已关闭的用户组，以便该组在发布环境中可用；在本例中， `cug_access`.

## 将已关闭的用户组应用到内容页面 {#applying-your-closed-user-group-to-content-pages}

要将CUG应用到一个或多个页面，请执行以下操作：

1. 导航到要分配给CUG的受限部分的根页面。
1. 单击页面的缩略图并选择 **属性** 中。

   ![screenshot_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. 在以下窗口中，打开 **高级** 选项卡。

1. 向下滚动到 **身份验证要求** 中。

   1. 激活 **启用** 复选框。

   1. 将路径添加到 **登录页面**.
如果留空，则可选使用标准登录页面。

   ![添加了CUG](assets/cug-authentication-requirement.png)

1. 接下来，转到 **权限** 选项卡，选择 **编辑已关闭的用户组**.

   ![screenshot_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[!NOTE]
   >
   >“权限”选项卡中的CUG无法从Blueprint中转出到Live Copy。 请在配置 Live Copy 时对此进行规划。
   >
   >有关更多信息，请参阅 [本页](closed-user-groups.md#aem-livecopy).

1. 的 **编辑已关闭的用户组** 对话框。 在此，您可以搜索并选择您的CUG，然后使用确认群组选择 **保存**.

   该组将被添加到列表中；例如，群组 **cug_access**.

   ![添加了CUG](assets/cug-added.png)

1. 确认更改 **保存并关闭**.

>[!NOTE]
>
>请参阅 [Identity Management](/help/sites-administering/identity-management.md) 有关发布环境中的用户档案以及提供用于登录和退出的表单的信息。

## 链接到CUG页面 {#linking-to-the-cug-pages}

由于匿名用户看不到指向CUG页面的任何链接的目标，链接检查程序将删除此类链接。

要避免这种情况，建议创建指向CUG区域内页面的未受保护的重定向页面。 然后，将呈现导航条目，而不会导致链接检查器出现任何问题。 仅当实际访问重定向页面时，用户才会在CUG区域内被重定向 — 成功提供其登录凭据后。

## 为CUG配置Dispatcher {#configure-dispatcher-for-cugs}

如果您使用的是Dispatcher，则需要定义具有以下属性的Dispatcher场：

* [virtualhosts](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#identifying-virtual-hosts-virtualhosts):匹配CUG所应用的页面路径。
* \sessionmanagement:请参阅下文。
* [缓存](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-the-dispatcher-cache-cache):专用于CUG所应用文件的缓存目录。

### 为CUG配置Dispatcher会话管理 {#configuring-dispatcher-session-management-for-cugs}

配置 [dispatcher.any文件中的会话管理](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#enabling-secure-sessions-sessionmanagement) CUG的。 请求CUG页面访问时使用的身份验证处理程序决定了如何配置会话管理。

```xml
/sessionmanagement
    ...
    /header "Cookie:login-token"
    ...
```

>[!NOTE]
>
>当调度程序场启用了会话管理时，不会缓存场处理的所有页面。 要缓存CUG外的页面，请在dispatcher.any中创建第二个场
>来处理非CUG页面。

1. 配置 [/sessionmanagement](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#enabling-secure-sessions-sessionmanagement) 通过定义 `/directory`;例如：

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. 已设置 [/allowAuthorized](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#caching-when-authentication-is-used) to `0`.
