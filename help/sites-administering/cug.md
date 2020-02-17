---
title: 创建已关闭的用户组
seo-title: 创建已关闭的用户组
description: 了解如何创建已关闭的用户组。
seo-description: 了解如何创建已关闭的用户组。
uuid: dc3c7dbd-2e86-43f9-9377-3b75053203b3
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ae57874-a9a1-4208-9001-7f44a1f57cbe
docset: aem65
translation-type: tm+mt
source-git-commit: 29328ff7fde4ed0e7f9728af1be911133259dc6c

---


# 创建已关闭的用户组{#creating-a-closed-user-group}

已关闭的用户组(CUG)用于限制对已发布Internet站点内特定页面的访问。 此类页面需要分配的成员登录并提供安全凭据。

要在网站中配置此类区域，请执行以下操作：

* [创建实际已关闭的用户组并分配成员](#creating-the-user-group-to-be-used)。

* [将此组应用到所需页面](#applying-your-closed-user-group-to-content-pages) ，并选择（或创建）供CUG成员使用的登录页面；在将CUG应用到内容页面时也指定。

* [为某些表单创建指向保护区域内至少一个页面的链接](#linking-to-the-realm)，否则，该链接将不可见。
* [配置Dispatcher](#configure-dispatcher-for-cugs) （如果正在使用）。

>[!CAUTION]
>
>应始终在创建封闭用户组(CUG)时考虑性能。
>
>尽管CUG中的用户和用户组数量不限，但页面上的大量CUG可能会降低渲染性能。
>
>执行性能测试时，应始终考虑CUG的影响。

## 创建要使用的用户组 {#creating-the-user-group-to-be-used}

要创建已关闭的用户组，请执行以下操作：

1. 从AEM主 **屏幕转到工具** -安全性。

   >[!NOTE]
   >
   >有关创 [建和配置用户和用户组的完整信息](/help/sites-administering/security.md#managing-users-and-groups) ，请参阅管理用户和用户组。

1. 从下一 **屏幕** ，选择“组”卡。

   ![screanth_2018-10-30at145502](assets/screenshot_2018-10-30at145502.png)

1. 按右 **上角的** “创建”按钮可创建新组。
1. 命名新组；例如， `cug_access`。

   ![screanth_2018-10-30at151459](assets/screenshot_2018-10-30at151459.png)

1. 转到“成 **员** ”选项卡，将所需的用户分配到此组。

   ![screanth_2018-10-30at151808](assets/screenshot_2018-10-30at151808.png)

1. 激活您分配给您的CUG的任何用户；在本例中，所有成员都是 `cug_access`。
1. 激活已关闭的用户组，以便在发布环境中可用；在本例中， `cug_access`。

## 将已关闭的用户组应用到内容页面 {#applying-your-closed-user-group-to-content-pages}

要将CUG应用到页面，请执行以下操作：

1. 导览至要分配给CUG的受限部分的根页面。
1. 单击页面的缩略图，然后单击顶部面 **板中的** “属性”。

   ![screanth_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. 在下面的窗口中，转到高级 **选项卡** 。
1. 向下滚动并启用“身份验证要求”部 **分中的复选框** 。

1. 在下面添加配置路径，然后按保存。
1. 接下来，转到“权限 **”选项卡** ，然后按“编 **辑已关闭的用户组** ”按钮。

   ![screanth_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[注意!]
   >
   > 请注意，“权限”选项卡中的CUG无法从Blueprint回滚到Live Copy。 请在配置Live copy时针对此进行规划。
   >
   > 有关详细信息，请参 [阅此页](closed-user-groups.md#aem-livecopy)。

1. 在以下窗口中查找并添加您的CUG —— 在此示例中，添加名为 **cug_access的组**。 最后，按“ **保存**”。
1. 单击 **启用** ，以定义此页面（和任何子页面）属于CUG。
1. 指定 **** 用户组成员将使用的登录页面；例如：

   `/content/geometrixx/en/toolbar/login.html`

   这是可选的，如果留空，则将使用标准登录页面。

1. 添加“已允 **许的组**”。 使用+可添加用户组，使用——可删除。 只允许这些组的成员登录并访问页面。
1. 根据需要 **分配领域** （页面组的名称）。 留空将使用页面标题。
1. Click **OK** to save the specification.

有关发 [布环境中的配置文件](/help/sites-administering/identity-management.md) ，以及提供登录和注销表单的信息，请参阅标识管理。

## 链接到领域 {#linking-to-the-realm}

由于匿名用户看不到指向CUG领域的任何链接的目标，因此链接检查器将删除此类链接。

要避免这种情况，建议创建指向CUG领域内页面的未受保护的重定向页面。 然后渲染导航条目，而不会导致链接检查器出现任何问题。 仅当实际访问重定向页面时，用户才会在CUG领域内重定向——成功提供其登录凭据后。

## 为CUG配置Dispatcher {#configure-dispatcher-for-cugs}

如果您使用的是Dispatcher，则需要定义具有以下属性的Dispatcher群：

* [virtualhosts](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#identifying-virtual-hosts-virtualhosts):匹配CUG所应用的页面的路径。
* \会话管理：请参见下文。
* [缓存](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache):专用于CUG所应用的文件的缓存目录。

### 为CUG配置Dispatcher Session Management {#configuring-dispatcher-session-management-for-cugs}

在 [CUG的dispatcher.any文件中配置会话管理](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement) 。 请求对CUG页面的访问时使用的身份验证处理函数决定了如何配置会话管理。

```xml
/sessionmanagement
    ...
    /header "Cookie:login-token"
    ...
```

>[!NOTE]
>
>当调度程序群启用会话管理时，不会缓存该群处理的所有页面。 要缓存CUG之外的页面，请在dispatcher.any中创建另一个农场
>处理非CUG页面。

1. 通过 [定义](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement) /会话管理 `/directory`;例如：

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. 将 [/allowAuthorized设置为](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#caching-when-authentication-is-used)`0`。

