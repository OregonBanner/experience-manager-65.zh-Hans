---
title: 创建封闭用户组
seo-title: 创建封闭用户组
description: 了解如何创建封闭用户组。
seo-description: 了解如何创建封闭用户组。
uuid: dc3c7dbd-2e86-43f9-9377-3b75053203b3
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ae57874-a9a1-4208-9001-7f44a1f57cbe
docset: aem65
exl-id: 9efba91d-45e8-42e1-9db6-490d21bf7412
source-git-commit: cb4b0cb60b8709beea3da70495a15edc8c4831b8
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 0%

---

# 创建封闭用户组{#creating-a-closed-user-group}

已关闭的用户组(CUG)用于限制对已发布互联网站点内特定页面的访问。 此类页面需要分配的成员登录并提供安全凭据。

要在您的网站中配置此类区域，请执行以下操作：

* [创建实际的已关闭用户组并分配成员](#creating-the-user-group-to-be-used)。

* [将此群组应用到所](#applying-your-closed-user-group-to-content-pages) 需页面，然后选择（或创建）供CUG成员使用的登录页面；在将CUG应用到内容页面时也指定。

* [创建一个链接（某种形式），指向保护区域内的至少一个页面](#linking-to-the-realm)，否则将不显示该链接。
* [配置](#configure-dispatcher-for-cugs) Dispatcher（如果正在使用）。

>[!CAUTION]
>
>应始终在创建封闭用户组(CUG)时考虑性能。
>
>尽管CUG中的用户和组数量不受限制，但页面上的大量CUG可能会降低渲染性能。
>
>在进行性能测试时，应始终考虑CUG的影响。

## 创建要使用的用户组{#creating-the-user-group-to-be-used}

要创建已关闭的用户组，请执行以下操作：

1. 从AEM主屏幕中转到&#x200B;**工具 — Security**。

   >[!NOTE]
   >
   >有关创建和配置用户和组的完整信息，请参阅[管理用户和组](/help/sites-administering/security.md#managing-users-and-groups)。

1. 从下一个屏幕中选择&#x200B;**Groups**&#x200B;卡。

   ![screenshot_2018-10-30at145502](assets/screenshot_2018-10-30at145502.png)

1. 按右上角的&#x200B;**创建**&#x200B;按钮以创建新组。
1. 命名新群组；例如，`cug_access`。

   ![screenshot_2018-10-30at151459](assets/screenshot_2018-10-30at151459.png)

1. 转到&#x200B;**Members**&#x200B;选项卡，并将所需用户分配给此组。

   ![screenshot_2018-10-30at151808](assets/screenshot_2018-10-30at151808.png)

1. 激活您分配给CUG的任何用户；在这种情况下，`cug_access`的所有成员。
1. 激活已关闭的用户组，以便该组在发布环境中可用；在本例中， `cug_access`。

## 将已关闭的用户组应用到内容页面{#applying-your-closed-user-group-to-content-pages}

要将CUG应用到页面，请执行以下操作：

1. 导航到要分配给CUG的受限部分的根页面。
1. 单击页面的缩略图，然后单击顶部面板中的&#x200B;**属性**&#x200B;以选择页面。

   ![screenshot_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. 在以下窗口中，转到&#x200B;**Advanced**&#x200B;选项卡。
1. 向下滚动，并启用&#x200B;**Authentication Requirement**&#x200B;部分中的Tickbox。

1. 在下面添加配置路径，然后按保存。
1. 接下来，转到&#x200B;**权限**&#x200B;选项卡，然后按&#x200B;**编辑已关闭的用户组**&#x200B;按钮。

   ![screenshot_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[注意!]
   >
   > 请注意，“权限”选项卡中的CUG无法从Blueprint中转出到Live Copy。 请在配置Live Copy时针对此进行规划。
   >
   > 有关更多信息，请参阅[此页面](closed-user-groups.md#aem-livecopy)。

1. 在以下窗口中查找并添加您的CUG — 在本例中，添加名为&#x200B;**cug_access**&#x200B;的组。 最后，按&#x200B;**Save**。
1. 单击&#x200B;**启用**&#x200B;以定义此页面（和任何子页面）属于CUG。
1. 指定组成员将使用的&#x200B;**登录页面**;例如：

   `/content/geometrixx/en/toolbar/login.html`

   如果留空，则可选使用标准登录页面。

1. 添加&#x200B;**Acceaded Groups**。 使用+添加组，或使用 — 删除。 只允许这些组的成员登录并访问页面。
1. 根据需要，指定&#x200B;**领域**（页面组的名称）。 留空将使用页面标题。
1. 单击&#x200B;**确定**&#x200B;以保存规范。

请参阅[Identity Management](/help/sites-administering/identity-management.md) ，以了解有关发布环境中的配置文件以及提供登录和退出表单的信息。

## 链接到领域{#linking-to-the-realm}

由于指向CUG领域的任何链接的目标对匿名用户不可见，因此链接检查器将删除此类链接。

要避免这种情况，建议创建指向CUG领域内页面的未受保护的重定向页面。 然后，将呈现导航条目，而不会导致链接检查器出现任何问题。 仅当实际访问重定向页面时，用户才会在CUG领域内被重定向 — 成功提供其登录凭据后。

## 为CUG配置Dispatcher {#configure-dispatcher-for-cugs}

如果您使用的是Dispatcher，则需要定义具有以下属性的Dispatcher场：

* [virtualhosts](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#identifying-virtual-hosts-virtualhosts):匹配CUG所应用的页面路径。
* \sessionmanagement:请参阅下文。
* [缓存](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache):专用于CUG所应用文件的缓存目录。

### 为CUG配置Dispatcher会话管理{#configuring-dispatcher-session-management-for-cugs}

在CUG的dispatcher.any文件](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement)中配置[会话管理。 请求CUG页面访问时使用的身份验证处理程序决定了如何配置会话管理。

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

1. 通过定义`/directory`配置[/sessionmanagement](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement);例如：

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. 将[/allowAuthorized](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#caching-when-authentication-is-used)设置为`0`。
