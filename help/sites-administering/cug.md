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
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 3%

---

# 创建封闭用户组{#creating-a-closed-user-group}

已关闭的用户组(CUG)用于限制对已发布互联网站点内特定页面的访问。 此类页面需要分配的成员登录并提供安全凭据。

要在您的网站中配置此类区域，请执行以下操作：

* [创建实际的已关闭用户组并分配成员](#creating-the-user-group-to-be-used).

* [将此群组应用到所需页面](#applying-your-closed-user-group-to-content-pages) 并选择（或创建）供CUG成员使用的登录页面；在将CUG应用到内容页面时也指定。

* [以某种形式创建一个链接，指向受保护区域内至少一个页面](#linking-to-the-realm)，否则将不可见。
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

要将CUG应用到页面，请执行以下操作：

1. 导航到要分配给CUG的受限部分的根页面。
1. 单击页面的缩略图，然后单击 **属性** 中。

   ![screenshot_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. 在以下窗口中，转到 **高级** 选项卡。
1. 向下滚动并在 **身份验证要求** 中。

1. 在下面添加配置路径，然后按保存。
1. 接下来，转到 **权限** 按 **编辑已关闭的用户组** 按钮。

   ![screenshot_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[!NOTE]
   >
   >请注意，“权限”选项卡中的 CUG 无法从 Blueprint 转出到 Live Copy。请在配置 Live Copy 时对此进行规划。
   >
   >有关更多信息，请参阅 [本页](closed-user-groups.md#aem-livecopy).

1. 在以下窗口中查找并添加您的CUG — 在本例中，添加名为 **cug_access**. 最后，按 **保存**.
1. 单击 **已启用** 以定义此页面（和任何子页面）属于CUG。
1. 指定 **登录页面** 会使用的；例如：

   `/content/geometrixx/en/toolbar/login.html`

   如果留空，则可选使用标准登录页面。

1. 添加 **允许的组**. 使用+添加组，或使用 — 删除。 只允许这些组的成员登录并访问页面。
1. 分配 **领域** （页面组的名称）。 留空将使用页面标题。
1. 单击 **确定** 以保存规范。

请参阅 [Identity Management](/help/sites-administering/identity-management.md) 有关发布环境中的用户档案以及提供用于登录和退出的表单的信息。

## 链接到领域 {#linking-to-the-realm}

由于指向CUG领域的任何链接的目标对匿名用户不可见，因此链接检查器将删除此类链接。

要避免这种情况，建议创建指向CUG领域内页面的未受保护的重定向页面。 然后，将呈现导航条目，而不会导致链接检查器出现任何问题。 仅当实际访问重定向页面时，用户才会在CUG领域内被重定向 — 成功提供其登录凭据后。

## 为CUG配置Dispatcher {#configure-dispatcher-for-cugs}

如果您使用的是Dispatcher，则需要定义具有以下属性的Dispatcher场：

* [virtualhosts](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#identifying-virtual-hosts-virtualhosts):匹配CUG所应用的页面路径。
* \sessionmanagement:请参阅下文。
* [缓存](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache):专用于CUG所应用文件的缓存目录。

### 为CUG配置Dispatcher会话管理 {#configuring-dispatcher-session-management-for-cugs}

配置 [dispatcher.any文件中的会话管理](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement) CUG的。 请求CUG页面访问时使用的身份验证处理程序决定了如何配置会话管理。

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

1. 配置 [/sessionmanagement](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement) 通过定义 `/directory`;例如：

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. 已设置 [/allowAuthorized](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#caching-when-authentication-is-used) to `0`.
