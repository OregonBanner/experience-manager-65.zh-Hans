---
title: 適用於Communities元件的OSGi事件
seo-title: OSGi Events for Communities Components
description: 會傳送可觸發非同步接聽程式的OSGi事件
seo-description: OSGi events are sent that can trigger asynchronous listeners
uuid: 317e2add-689d-4c99-ae38-0703b6649cb7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 25b7ac08-6cdc-4dd5-a756-d6169b86f9ab
exl-id: 8049d797-e758-44c2-a89b-51d2b2fca8dc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 4%

---

# 適用於Communities元件的OSGi事件  {#osgi-events-for-communities-components}

## 概述 {#overview}

當成員與Communities功能互動時，會傳送可觸發非同步接聽程式的OSGi事件，例如通知或遊戲化（評分和徽章）。

元件的 [社交事件](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) 執行個體會將事件記錄為 `actions` 發生於 `topic`. SocialEvent包含傳回 `verb` 與動作相關聯。 有一個 *n-1* 關係介於 `actions` 和 `verbs`.

針對發行版本中提供的Communities元件，下表說明 `verbs` 已為每個專案定義 `topic` 可供使用。

## 主題和動詞 {#topics-and-verbs}

[行事曆元件](calendar-basics-for-developers.md)
社交事件 `topic`= com/adobe/cq/social/calendar

| **動詞** | **描述** |
|---|---|
| POST | 成員建立行事曆事件 |
| 添加 | 行事曆事件的成員註解 |
| 更新 | 編輯成員的行事曆事件或註解 |
| 删除 | 已刪除成員的行事曆事件或註解 |

[註解元件](essentials-comments.md)
社交事件 `topic`= com/adobe/cq/social/comment

| **動詞** | **描述** |
|---|---|
| POST | 成員建立註解 |
| 添加 | 成員回複評論 |
| 更新 | 已編輯成員的註解 |
| 删除 | 已刪除成員的註解 |

[檔案庫元件](essentials-file-library.md)
社交事件 `topic`= com/adobe/cq/social/fileLibrary

| **動詞** | **描述** |
|---|---|
| POST | 成員建立資料夾 |
| 附加 | 成員上傳檔案 |
| 更新 | 成員更新資料夾或檔案 |
| 删除 | 成員刪除資料夾或檔案 |

[論壇元件](essentials-forum.md)
社交事件 `topic`= com/adobe/cq/social/forum

| **動詞** | **描述** |
|---|---|
| POST | 成員建立論壇主題 |
| 添加 | 論壇主題的成員回覆 |
| 更新 | 編輯成員的論壇主題或回覆 |
| 删除 | 已刪除成員的論壇主題或回覆 |

[日誌元件](blog-developer-basics.md)
社交事件 `topic`= com/adobe/cq/social/journal

| **動詞** | **描述** |
|---|---|
| POST | 成員建立部落格 |
| 添加 | 成員對部落格的評論 |
| 更新 | 編輯成員的部落格或評論 |
| 删除 | 已刪除成員的部落格或評論 |

[QnA元件](qna-essentials.md)
社交事件 `topic` = com/adobe/cq/social/qna

| **動詞** | **描述** |
|---|---|
| POST | 成員建立QnA問題 |
| 添加 | 成員建立QnA答案 |
| 更新 | 編輯成員的QnA問題或答案 |
| 選取 | 已選取成員的答案 |
| 取消選取 | 已取消選取成員的答案 |
| 删除 | 已刪除成員的QnA問題或答案 |

[檢閱元件](reviews-basics.md)
社交事件 `topic`= com/adobe/cq/social/review

| **動詞** | **描述** |
|---|---|
| POST | 成員建立稽核 |
| 更新 | 已編輯成員的評論 |
| 删除 | 已刪除成員的評論 |

[評等元件](rating-basics.md)
社交事件 `topic`= com/adobe/cq/social/tally

| **動詞** | **描述** |
|---|---|
| 新增評等 | 已對成員內容進行分級 |
| 移除評等 | 成員的內容已降級 |

[投票元件](essentials-voting.md)
社交事件 `topic`= com/adobe/cq/social/tally

| **動詞** | **描述** |
|---|---|
| 新增投票 | 會員內容已投票 |
| 移除投票 | 會員的內容已被投票否決 |

**啟用稽核的元件**
社交事件 `topic`= com/adobe/cq/social/moderation

| **動詞** | **描述** |
|---|---|
| 拒绝 | 成員的內容被拒絕 |
| 標幟為不適當 | 已標幟成員的內容 |
| 不適宜取消標幟 | 成員的內容未標幟 |
| ACCEPT | 仲裁者已核准成員的內容 |
| 關閉 | 成員關閉評論以進行編輯和回覆 |
| OPEN | 成員重新開啟註解 |

## 自訂元件的事件 {#events-for-custom-components}

對於自訂元件， [SocialEvent抽象類別](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) 必須延伸d才能將元件的事件記錄為 `actions`發生於 `topic`.

自訂事件會覆寫方法 `getVerb()` 以便適當的 `verb`會針對每個傳回 `action`. 此 `verb` 針對動作傳回的可能是常用的(例如 `POST`)或專用於元件的元件(例如 `ADD RATING`)。 有一個 *n-1* 關係介於 `actions`和 `verbs`.

>[!NOTE]
>
>確保自訂擴充功能註冊的排名低於產品中任何現有實作。

### 自訂元件事件的虛擬程式碼 {#pseudo-code-for-custom-component-event}

[org.osgi.service.event.Event](https://osgi.org/javadoc/r4v41/org/osgi/service/event/Event.html)；
[com.adobe.cq.social.scf.core.SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html)；
[com.adobe.granite.activitystreams.ObjectTypes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ObjectTypes.html)；
[com.adobe.granite.activitystreams.Verbs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/Verbs.html)；

```java
package com.mycompany.recipe;

import org.osgi.service.event.Event;
import com.adobe.cq.social.scf.core.SocialEvent;
import com.adobe.granite.activitystreams.ObjectTypes;
import com.adobe.granite.activitystreams.Verbs;

/*
 * The Recipe type, passed to RecipeEvent(), would be a custom Recipe class
 * that extends either
 * com.adobe.cq.social.scf.SocialComponent
 * or
 * com.adobe.cq.social.scf.SocialCollectionComponent
 * See https://docs.adobe.com/docs/en/aem/6-2/develop/communities/scf/server-customize.html
 */

/**
 * Defines events that are triggered on a custom component, "Recipe".
 */
public class RecipeEvent extends SocialEvent<RecipeEvent.RecipeActions> {

    private static final long serialVersionUID = 1L;
    protected static final String PARENT_PATH = "PARENT_PATH";

    /**
     * The event topic suffix for Recipe events
     */
    public static final String RECIPE_TOPIC = "recipe";

    /**
     * @param recipe - the recipe resource on which the event was triggered
     * @param userId - the user id of the user who triggered the action
     * @param action - the recipe action that triggered this event
     */
    public RecipeEvent(final Recipe recipe, final String userId, final RecipeEvent.RecipeActions action) {
        String recipePath = recipe.getResource().getPath();
        String parentPath = (recipe.getParentComponent() != null) ?
                             recipe.getParentComponent().getResource().getPath() :
                             recipe.getSourceComponentId();
        this(recipePath, userId, parentPath, action);
    }

    /**
     * @param recipePath - the path to the recipe resource (jcr node) on which the event was triggered
     * @param userId - the user id of the user who triggered the action
     * @param parentPath - the path to the parent node of the recipe resource
     * @param action - the recipe action that triggered this event
     */
    public RecipeEvent(final String recipePath, final String userId, final String parentPath) {
        super(RECIPE_TOPIC, recipePath, userId, action,
              new BaseEventObject(recipePath, ObjectTypes.ARTICLE),
              new BaseEventObject(parentPath, ObjectTypes.COLLECTION),
              new HashMap<String, Object>(1) {
            private static final long serialVersionUID = 1L;
            {
                if (parentPath != null) {
                    this.put(PARENT_PATH, parentPath);
                }

            }
        });
    }

    private RecipeEvent (final Event event) {
      super(event);
    }

    /**
     * List of available recipe actions that can trigger a recipe event.
     */
    public static enum RecipeActions implements SocialEvent.SocialActions {
        RecipeAdded,
        RecipeModified,
        RecipeDeleted;

        @Override
        public String getVerb() {
            switch (this) {
                case RecipeAdded:
                    return Verbs.POST;
                case RecipeModified:
                    return Verbs.UPDATE;
                case RecipeDeleted:
                    return Verbs.DELETE;
                default:
                    throw new IllegalArgumentException("Unsupported action");
            }
        }
    }

}
```

## 用於篩選活動資料流的EventListener範例 {#sample-eventlistener-to-filter-activity-stream-data}

您可以監聽事件，以修改活動資料流中顯示的內容。

下列虛擬程式碼範例將從活動資料流中移除Comments元件的DELETE事件。

### EventListener的虛擬碼 {#pseudo-code-for-eventlistener}

需要 [最新feature pack](deploy-communities.md#latestfeaturepack).

```java
package my.company.comments;

import java.util.Collections;
import java.util.Map;

import org.apache.commons.lang.StringUtils;
import org.apache.felix.scr.annotations.Activate;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Modified;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.commons.osgi.PropertiesUtil;
import org.osgi.service.component.ComponentContext;

import com.adobe.cq.social.activitystreams.listener.api.ActivityStreamProviderExtension;
import com.adobe.cq.social.commons.events.CommentEvent.CommentActions;
import com.adobe.cq.social.scf.core.SocialEvent;

@Service
@Component(metatype = true, label = "My Comment Delete Event Filter",
        description = "Prevents comment DELETE events from showing up in activity streams")
public class CommentDeleteEventActivityFilter implements ActivityStreamProviderExtension {

    @Property(name = "ranking", intValue = 10)
    protected int ranking;

    @Activate
    public void activate(final ComponentContext ctx) {
        ranking = PropertiesUtil.toInteger(ctx.getProperties().get("ranking"), 10);
    }

    @Modified
    public void update(final Map<String, Object> props) {
        ranking = PropertiesUtil.toInteger(props.get("ranking"), 10);
    }

    @Override
    public boolean evaluate(final SocialEvent<?> evt, final Resource resource) {
        if (evt.getAction() != null && evt.getAction() instanceof SocialEvent.SocialActions) {
            final SocialEvent.SocialActions action = evt.getAction();
            if (StringUtils.equals(action.getVerb(), CommentActions.DELETED.getVerb())) {
                return false;
            }
        }
        return true;
    }

    @Override
    public Map<String, ? extends Object> getActivityProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public Map<String, ? extends Object> getActorProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public String getName() {
        return "My Comment Delete Event Filter";
    }

    @Override
    public Map<String, ? extends Object> getObjectProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    /* Ensure a custom extension is registered with a ranking lower than any existing implementation in the product. */
    @Override
    public int getRanking() {
        return this.ranking;
    }

    @Override
    public Map<String, ? extends Object> getTargetProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public String[] getStreamProviderPid() {
        return new String[]{"*"};
    }

}
```
