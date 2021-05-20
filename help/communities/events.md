---
title: 社区组件的OSGi事件
seo-title: 社区组件的OSGi事件
description: 发送可触发异步侦听器的OSGi事件
seo-description: 发送可触发异步侦听器的OSGi事件
uuid: 317e2add-689d-4c99-ae38-0703b6649cb7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 25b7ac08-6cdc-4dd5-a756-d6169b86f9ab
exl-id: 8049d797-e758-44c2-a89b-51d2b2fca8dc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 4%

---

# 社区组件的OSGi事件{#osgi-events-for-communities-components}

## 概述 {#overview}

当成员与社区功能交互时，会发送可触发异步侦听器的OSGi事件，如通知或游戏化（评分和徽章）。

组件的[SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html)实例将`topic`发生的事件记录为`actions`。 SocialEvent包括一种方法，用于返回与操作关联的`verb`。 `actions`和`verbs`之间存在&#x200B;*n-1*&#x200B;关系。

对于版本中提供的社区组件，下表描述了为每个`topic`可用组件定义的`verbs`。

## 主题和动词{#topics-and-verbs}

[日](calendar-basics-for-developers.md)
历组 `topic`件SocialEvent = com/adobe/cq/social/calendar

| **动词** | **描述** |
|---|---|
| POST | 成员创建日历事件 |
| 添加 | 日历事件中的成员评论 |
| 更新 | 编辑会员的日历事件或评论 |
| 删除 | 会删除成员的日历事件或评论 |

[评](essentials-comments.md)
论组 `topic`件SocialEvent = com/adobe/cq/social/comment

| **动词** | **描述** |
|---|---|
| POST | 成员创建评论 |
| 添加 | 成员对评论的答复 |
| 更新 | 编辑会员的评论 |
| 删除 | 会员评论已删除 |

[文件](essentials-file-library.md)
库 `topic`ComponentSocialEvent = com/adobe/cq/social/fileLibrary

| **动词** | **描述** |
|---|---|
| POST | 成员创建文件夹 |
| 附加 | 成员上传文件 |
| 更新 | 成员更新文件夹或文件 |
| 删除 | 成员删除文件夹或文件 |

[论](essentials-forum.md)
坛组 `topic`件SocialEvent = com/adobe/cq/social/forum

| **动词** | **描述** |
|---|---|
| POST | 成员创建论坛主题 |
| 添加 | 成员对论坛主题的答复 |
| 更新 | 编辑会员的论坛主题或回复 |
| 删除 | 会员的论坛主题或回复将被删除 |

[日](blog-developer-basics.md)
记帐组 `topic`件SocialEvent = com/adobe/cq/social/journal

| **动词** | **描述** |
|---|---|
| POST | 会员创建博客文章 |
| 添加 | 会员对博客文章的评论 |
| 更新 | 编辑会员的博客文章或评论 |
| 删除 | 会员的博客文章或评论会被删除 |

[QnA ](qna-essentials.md)
ComponentSocialEvent  `topic` = com/adobe/cq/social/qna

| **动词** | **描述** |
|---|---|
| POST | 成员创建QnA问题 |
| 添加 | 成员创建QnA答案 |
| 更新 | 编辑会员的问题解答问题或答案 |
| 选择 | 已选择会员的答案 |
| 取消选择 | 已取消选择会员的答案 |
| 删除 | 成员的问题解答问题或答案将被删除 |

[查](reviews-basics.md)
看ComponentSocialEvent  `topic`= com/adobe/cq/social/review

| **动词** | **描述** |
|---|---|
| POST | 成员创建审阅 |
| 更新 | 编辑会员的审阅 |
| 删除 | 会员的审阅已删除 |

[评](rating-basics.md)
分组 `topic`件SocialEvent = com/adobe/cq/social/tally

| **动词** | **描述** |
|---|---|
| 添加评级 | 会员的内容已被评级 |
| 删除评级 | 会员的内容已被降级 |

[投票](essentials-voting.md)
组件 `topic`SocialEvent = com/adobe/cq/social/tally

| **动词** | **描述** |
|---|---|
| 添加投票 | 会员的内容已投票通过 |
| 删除投票 | 会员的内容已被否决 |

**启用审核**
的组 `topic`件SocialEvent = com/adobe/cq/social/moderation

| **动词** | **描述** |
|---|---|
| 拒绝 | 会员的内容被拒绝 |
| 不当标志 | 会员的内容已标记 |
| 不标记为不适当 | 会员的内容未标记 |
| 接受 | 会员的内容由审核者批准 |
| 关闭 | 成员关闭对编辑和回复的评论 |
| 打开 | 会员重新打开评论 |

## 自定义组件{#events-for-custom-components}事件

对于自定义组件，必须扩展[SocialEvent抽象类](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) ，以将组件的事件记录为`topic`发生的`actions`事件。

自定义事件将覆盖方法`getVerb()`，以便为每个`action`返回适当的`verb`。 为操作返回的`verb`可以是一个常用的（如`POST`），也可以是一个专门用于组件的（如`ADD RATING`）。 `actions`和`verbs`之间存在&#x200B;*n-1*&#x200B;关系。

>[!NOTE]
>
>确保使用低于产品中任何现有实施的排名来注册自定义扩展。

### 自定义组件事件{#pseudo-code-for-custom-component-event}的伪代码

[org.osgi.service.event.Event](https://osgi.org/javadoc/r4v41/org/osgi/service/event/Event.html);
[com.adobe.cq.social.scf.core.SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html);
[com.adobe.granite.activitystreams.ObjectTypes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ObjectTypes.html);
[com.adobe.granite.activitystreams.Verbts](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/Verbs.html);

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

## 过滤活动流数据{#sample-eventlistener-to-filter-activity-stream-data}的EventListener示例

可以侦听事件，以修改活动流中显示的内容。

以下伪代码示例将从活动流中删除“注释”组件的DELETE事件。

### EventListener {#pseudo-code-for-eventlistener}的伪代码

需要[最新功能包](deploy-communities.md#latestfeaturepack)。

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
