---
title: 创建已关闭的用户组
seo-title: Creating a Closed User Group
description: 了解如何创建已关闭的用户组。
seo-description: Learn how to work with Closed User Groups in Adobe Experience Manager.
uuid: dc3c7dbd-2e86-43f9-9377-3b75053203b3
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ae57874-a9a1-4208-9001-7f44a1f57cbe
docset: aem65
exl-id: 9efba91d-45e8-42e1-9db6-490d21bf7412
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 2%

---

# 创建已关闭的用户组{#creating-a-closed-user-group}

封闭用户组(CUG)用于限制对已发布Internet站点内特定页面的访问。 此类页面要求分配的成员登录并提供安全凭据。

要在网站中配置此类区域，您可以：

* [创建实际的已关闭用户组并分配成员](#creating-the-user-group-to-be-used).

* [将此组应用到所需的页面](#applying-your-closed-user-group-to-content-pages) 并选择（或创建）CUG成员使用的登录页面；将CUG应用于内容页面时也会指定登录页面。

* [创建某种形式的链接，至少指向保护区内的一个页面](#linking-to-the-cug-pages)，否则它将不可见。

* [配置调度程序](#configure-dispatcher-for-cugs) 如果正在使用中。

>[!CAUTION]
>
>创建封闭用户组(CUG)时应当始终考虑性能。
>
>尽管CUG中的用户和组数量不受限制，但页面上的CUG数量过高可能会降低渲染性能。
>
>在进行性能测试时，应始终考虑CUG的影响。

## 创建要使用的用户组 {#creating-the-user-group-to-be-used}

要创建已关闭的用户组，请执行以下操作：

1. 转到 **工具 — 安全性** 从AEM主屏幕上。

   >[!NOTE]
   >
   >请参阅 [管理用户和组](/help/sites-administering/security.md#managing-users-and-groups) 有关创建和配置用户和组的完整信息。

1. 选择 **组** 下一屏幕中的信息卡。

   ![screenshot_2018-10-30at145502](assets/screenshot_2018-10-30at145502.png)

1. 按 **创建** 按钮，以创建新组。
1. 命名您的新组；例如， `cug_access`.

   ![screenshot_2018-10-30at151459](assets/screenshot_2018-10-30at151459.png)

1. 转到 **成员** 选项卡，并将所需的用户分配给此组。

   ![screenshot_2018-10-30at151808](assets/screenshot_2018-10-30at151808.png)

1. 激活您分配给CUG的任何用户；在本例中，是所有 `cug_access`.
1. 激活已关闭的用户组，使其在发布环境中可用；在本例中， `cug_access`.

## 将已关闭的用户组应用于内容页面 {#applying-your-closed-user-group-to-content-pages}

要将CUG应用到一个或多个页面，请执行以下操作：

1. 导航到要分配给CUG的受限制部分的根页面。
1. 单击页面的缩略图，然后选择 **属性** 工具栏中。

   ![screenshot_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. 在以下窗口中，打开 **高级** 选项卡。

1. 向下滚动到 **身份验证要求** 部分。

   1. 激活 **启用** 勾选框。

   1. 将路径添加到 **登录页面**.
这是可选的，如果留空，将使用标准登录页面。

   ![已添加CUG](assets/cug-authentication-requirement.png)

1. 接下来，转到 **权限** 选项卡并选择 **编辑已关闭的用户组**.

   ![screenshot_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[!NOTE]
   >
   >“权限”选项卡中的 CUG 无法从 Blueprint 转出到 Live Copy。请在配置 Live Copy 时对此进行规划。
   >
   >有关更多信息，请参阅 [此页面](closed-user-groups.md#aem-livecopy).

1. 此 **编辑已关闭的用户组** 此时将打开对话框。 在此处，您可以搜索并选择您的CUG，然后使用确认组选择 **保存**.

   该组将被添加到列表中；例如，组 **cug_access**.

   ![已添加CUG](assets/cug-added.png)

1. 使用确认更改 **保存并关闭**.

>[!NOTE]
>
>请参阅 [Identity Management](/help/sites-administering/identity-management.md) 有关发布环境中的用户档案以及提供用于登录和退出的表单的信息。

## 链接到CUG页面 {#linking-to-the-cug-pages}

由于指向CUG页面的任何链接的目标对匿名用户不可见，因此linkchecker将删除此类链接。

要避免出现这种情况，建议您创建指向CUG区域内的页面的无保护重定向页面。 然后呈现导航条目，而不会导致linkchecker出现任何问题。 仅当实际访问重定向页面时，用户才会在CUG区域中被重定向 — 在成功提供其登录凭据之后。

## 为CUG配置Dispatcher {#configure-dispatcher-for-cugs}

如果您使用的是Dispatcher，则需要使用以下属性定义Dispatcher场：

* [虚拟主机](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#identifying-virtual-hosts-virtualhosts)：匹配CUG应用于的页面的路径。
* \sessionmanagement：请参见下文。
* [缓存](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-the-dispatcher-cache-cache)：专用于CUG应用于的文件的缓存目录。

### 为CUG配置Dispatcher会话管理 {#configuring-dispatcher-session-management-for-cugs}

配置 [dispatcher.any文件中的会话管理](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#enabling-secure-sessions-sessionmanagement) CUG的。 在请求访问CUG页面时使用的身份验证处理程序决定了如何配置会话管理。

```xml
/sessionmanagement
    ...
    /header "Cookie:login-token"
    ...
```

>[!NOTE]
>
>当Dispatcher场启用了会话管理时，不会缓存场处理的所有页面。 要缓存超出CUG的页面，请在dispatcher.any中创建第二个场
>处理非CUG页面。

1. 配置 [/sessionmanagement](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#enabling-secure-sessions-sessionmanagement) 通过定义 `/directory`；例如：

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. 设置 [/allowAuthorized](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#caching-when-authentication-is-used) 到 `0`.
