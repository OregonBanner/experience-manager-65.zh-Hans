---
title: OSGi事件社区组件
seo-title: OSGi事件社区组件
description: OSGi事件被发送，可触发异步监听器
seo-description: OSGi事件被发送，可触发异步监听器
uuid: 317e2add-689d-4c99-ae38-0703b6649cb7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 25b7ac08-6cdc-4dd5-a756-d6169b86f9ab
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 4%

---


# OSGi事件社区组件  {#osgi-events-for-communities-components}

## 概述 {#overview}

当成员与社区功能交互时，会发送可触发异步监听器的OSGi事件，如通知或游戏化（评分和徽章）。

组件的SocialEvent [实例](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) 将事件记录 `actions` 为发生的 `topic`。 SocialEvent包括返回与操作关 `verb` 联的方法。 和之 *间存在* n- `actions` 1关系 `verbs`。

对于版本中提供的社区组件，下表描述了为每个可 `verbs` 用组件定 `topic` 义的内容。

## 主题与动词 {#topics-and-verbs}

[日历组](calendar-basics-for-developers.md)件 `topic`社交活动= com/adobe/cq/social/calendar

| **动词** | **描述** |
|---|---|
| POST | 成员创建日历事件 |
| 添加 | 日历事件上的成员注释 |
| 更新 | 会员的日历事件或评论已编辑 |
| 删除 | 会员的日历事件或评论已被删除 |

[评论组](essentials-comments.md)件 `topic`SocialEvent= com/adobe/cq/social/comment

| **动词** | **描述** |
|---|---|
| POST | 成员创建注释 |
| 添加 | 会员对评论的答复 |
| 更新 | 已编辑会员的注释 |
| 删除 | 会员的注释已删除 |

[文件库组](essentials-file-library.md)件 `topic`SocialEvent= com/adobe/cq/social/fileLibrary

| **动词** | **描述** |
|---|---|
| POST | 成员创建文件夹 |
| 附加 | 成员上传文件 |
| 更新 | 成员更新文件夹或文件 |
| 删除 | 成员删除文件夹或文件 |

[论坛组](essentials-forum.md)件社 `topic`交活动= com/adobe/cq/social/forum

| **动词** | **描述** |
|---|---|
| POST | 会员创建论坛主题 |
| 添加 | 会员对论坛主题的回复 |
| 更新 | 会员的论坛主题或回复已编辑 |
| 删除 | 会员的论坛主题或回复已被删除 |

[日志组](blog-developer-basics.md)件社 `topic`交活动= com/adobe/cq/social/日志

| **动词** | **描述** |
|---|---|
| POST | 成员创建博客文章 |
| 添加 | 成员对博客文章的评论 |
| 更新 | 编辑会员的博客文章或评论 |
| 删除 | 已删除会员的博客文章或评论 |

[问题与](qna-essentials.md)组 `topic` 件社交事件= com/adobe/cq/social/qna

| **动词** | **描述** |
|---|---|
| POST | 成员创建问题与答案问题 |
| 添加 | 成员创建问题与答案 |
| 更新 | 会员的问题与答案已编辑 |
| 选择 | 已选择会员的答案 |
| 取消选择 | 会员的答案已取消选择 |
| 删除 | 会员的问题与答案已删除 |

[审阅组](reviews-basics.md)件 `topic`SocialEvent= com/adobe/cq/social/review

| **动词** | **描述** |
|---|---|
| POST | 成员创建审阅 |
| 更新 | 已编辑会员的审阅 |
| 删除 | 会员的审阅已删除 |

[评级组](rating-basics.md)件SocialEvent `topic`= com/adobe/cq/social/tally

| **动词** | **描述** |
|---|---|
| 添加等级 | 会员的内容已评级 |
| 删除等级 | 会员的内容已降级 |

[投票组](essentials-voting.md)件 `topic`社交活动= com/adobe/cq/social/tally

| **动词** | **描述** |
|---|---|
| 添加投票 | 会员的内容已投票 |
| 删除投票 | 会员的内容已被否决 |

**支持协调的**&#x200B;组 `topic`件SocialEvent= com/adobe/cq/social/仲裁

| **动词** | **描述** |
|---|---|
| 拒绝 | 会员的内容被拒绝 |
| 不当标志 | 会员的内容已标记 |
| 取消标记为不适当 | 会员的内容未标记 |
| 接受 | 会员的内容由审查方批准 |
| 关闭 | 会员关闭对编辑和回复的注释 |
| 打开 | 会员重新打开注释 |

## 自定义组件事件 {#events-for-custom-components}

对于自定义组件， [必须扩展](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) d个SocialEvent抽象类，以记录组件 `actions`的事件与发生的 `topic`。

自定义事件将覆盖该方 `getVerb()` 法，以便为每 `verb`个返回相应的 `action`。 为 `verb` 操作返回的内容可以是常用的(如 `POST`)或专用于组件的(如 `ADD RATING`)。 和之 *间存在* n- `actions`1关系 `verbs`。

>[!NOTE]
>
>确保自定义扩展的注册级别低于产品中任何现有实施的级别。

### 自定义组件事件的伪代码 {#pseudo-code-for-custom-component-event}

[org.osgi.service.事件.事件](https://osgi.org/javadoc/r4v41/org/osgi/service/event/Event.html);[com.adobe.cq.social.scf.core.SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html);[com.adobe.granite.activitystreams.ObjectTypes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ObjectTypes.html);[com.adobe.granite.activitystreams.Vervipts](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/Verbs.html);

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

## 过滤活动流数据的示例EventListener {#sample-eventlistener-to-filter-activity-stream-data}

可以侦听事件以修改活动流中显示的内容。

以下伪代码示例将从DELETE流中删除“注释”组件的事件。

### EventListener的伪代码 {#pseudo-code-for-eventlistener}

需要 [最新的功能包](deploy-communities.md#latestfeaturepack)。

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

