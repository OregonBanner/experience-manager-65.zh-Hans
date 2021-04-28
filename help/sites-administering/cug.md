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
exl-id: 9efba91d-45e8-42e1-9db6-490d21bf7412
translation-type: tm+mt
source-git-commit: cb4b0cb60b8709beea3da70495a15edc8c4831b8
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 0%

---

# 创建已关闭的用户组{#creating-a-closed-user-group}

已关闭的用户组(CUG)用于限制对已发布Internet站点内特定页面的访问。 此类页面需要分配的成员登录并提供安全凭据。

要在您的网站中配置此区域，请执行以下操作：

* [创建实际已关闭的用户组并分配成员](#creating-the-user-group-to-be-used)。

* [将此组应用到所](#applying-your-closed-user-group-to-content-pages) 需页面，并选择（或创建）供CUG成员使用的登录页面；当将CUG应用到内容页面时也指定。

* [创建一个链接（某种形式），指向保护区域内至少一个页面](#linking-to-the-realm)，否则将不可见。
* [配置](#configure-dispatcher-for-cugs) Dispatcherif正在使用。

>[!CAUTION]
>
>应始终在创建封闭用户组(CUG)时注重性能。
>
>尽管CUG中的用户和用户组数量不限，但页面上的大量CUG可能会降低渲染性能。
>
>在进行性能测试时，应始终考虑CUG的影响。

## 创建要使用{#creating-the-user-group-to-be-used}的用户组

要创建已关闭的用户组，请执行以下操作：

1. 从AEM主屏幕转至&#x200B;**工具 — 安全**。

   >[!NOTE]
   >
   >有关创建和配置用户和组的完整信息，请参阅[管理用户和组](/help/sites-administering/security.md#managing-users-and-groups)。

1. 从下一个屏幕中选择&#x200B;**组**&#x200B;卡。

   ![screenth_2018-10-30at145502](assets/screenshot_2018-10-30at145502.png)

1. 按右上角的&#x200B;**创建**&#x200B;按钮以创建新组。
1. 命名新组；例如，`cug_access`。

   ![screenth_2018-10-30at151459](assets/screenshot_2018-10-30at151459.png)

1. 转到&#x200B;**成员**&#x200B;选项卡，将所需的用户分配给此组。

   ![screenth_2018-10-30at151808](assets/screenshot_2018-10-30at151808.png)

1. 激活您分配给您的CUG的所有用户；在这种情况下，`cug_access`的所有成员。
1. 激活已关闭的用户组，以便在发布环境中可用；在本例中，`cug_access`。

## 将已关闭的用户组应用到内容页面{#applying-your-closed-user-group-to-content-pages}

要将CUG应用于页面，请执行以下操作：

1. 导航到要分配给CUG的受限部分的根页面。
1. 单击页面的缩略图，然后单击顶部面板中的&#x200B;**属性**，以选择页面。

   ![screenth_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. 在以下窗口中，转到&#x200B;**高级**&#x200B;选项卡。
1. 向下滚动并启用&#x200B;**身份验证要求**&#x200B;部分中的复选框。

1. 在下面添加配置路径，然后按保存。
1. 接下来，转到&#x200B;**权限**&#x200B;选项卡，然后按&#x200B;**编辑已关闭的用户组**&#x200B;按钮。

   ![screenth_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[注意!]
   >
   > 请注意，“权限”选项卡中的CUG无法从Blueprint中转出到Live Copy。 请在配置Live Copy时针对此进行规划。
   >
   > 有关详细信息，请参阅[此页](closed-user-groups.md#aem-livecopy)。

1. 在以下窗口中查找并添加您的CUG — 在此示例中，添加名为&#x200B;**cug_access**&#x200B;的组。 最后，按&#x200B;**保存**。
1. 单击&#x200B;**已启用**&#x200B;可定义此页面（和任何子页面）属于CUG。
1. 指定组成员将使用的&#x200B;**登录页面**;例如：

   `/content/geometrixx/en/toolbar/login.html`

   如果留空，则使用标准登录页面为可选。

1. 添加&#x200B;**已允许的组**。 使用+可添加用户组，使用 — 可删除。 将仅允许这些用户组的成员登录并访问页面。
1. 根据需要指定&#x200B;**领域**（页面组的名称）。 留空将使用页面标题。
1. 单击&#x200B;**确定**&#x200B;以保存规范。

请参阅[Identity Management](/help/sites-administering/identity-management.md)，了解有关发布环境中的用户档案以及提供登录和注销表单的信息。

## 链接到领域{#linking-to-the-realm}

由于匿名用户看不到任何指向CUG领域的链接的目标，链接检查器将删除此类链接。

要避免这种情况，建议创建指向CUG领域内页面的未受保护的重定向页面。 然后渲染导航条目，而不会导致链接检查器出现任何问题。 仅在实际访问重定向页面时，用户才会在CUG领域内被重定向 — 在成功提供其登录凭据后。

## 为CUG {#configure-dispatcher-for-cugs}配置调度程序

如果您使用的是Dispatcher，则需要定义具有以下属性的Dispatcher群：

* [virtualhosts](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#identifying-virtual-hosts-virtualhosts):匹配CUG所应用的页面的路径。
* \会话管理：请参见下文。
* [缓存](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache):专用于CUG所应用的文件的缓存目录。

### 为CUG {#configuring-dispatcher-session-management-for-cugs}配置调度程序会话管理

在CUG的dispatcher.any文件](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement)中配置[会话管理。 请求CUG页的访问时使用的身份验证处理函数决定如何配置会话管理。

```xml
/sessionmanagement
    ...
    /header "Cookie:login-token"
    ...
```

>[!NOTE]
>
>当调度程序群启用会话管理时，不会缓存群处理的所有页面。 要缓存CUG以外的页面，请在dispatcher.any中创建第二个场
>处理非CUG页面。

1. 通过定义`/directory`配置[/sessionmanagement](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement);例如：

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. 将[/allowAuthorized](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#caching-when-authentication-is-used)设置为`0`。
