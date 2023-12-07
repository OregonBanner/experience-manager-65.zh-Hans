---
title: 适用于社区组件的OSGi事件
description: 发送可触发异步侦听器的OSGi事件
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8049d797-e758-44c2-a89b-51d2b2fca8dc
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 5%

---

# 适用于社区组件的OSGi事件  {#osgi-events-for-communities-components}

## 概述 {#overview}

当成员与社区功能交互时，会发送可触发异步侦听器的OSGi事件，例如通知或游戏化（评分和徽章）。

组件的 [社交事件](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) 实例将事件记录为 `actions` 发生于 `topic`. SocialEvent包括用于返回 `verb` 与操作相关联。 有一个 *n-1* 关系介于 `actions` 和 `verbs`.

对于发行版中交付的Communities组件，下表介绍了 `verbs` 为每项定义 `topic` 可供使用。

## 主题和动词 {#topics-and-verbs}

[日历组件](calendar-basics-for-developers.md)
社交事件 `topic`= com/adobe/cq/social/calendar

| **动词** | **描述** |
|---|---|
| POST | 成员创建日历事件 |
| 添加 | 日历事件的成员注释 |
| 更新 | 编辑成员的日历事件或评论 |
| 删除 | 成员的日历事件或评论已删除 |

[注释组件](essentials-comments.md)
社交事件 `topic`= com/adobe/cq/social/comment

| **动词** | **描述** |
|---|---|
| POST | 成员创建注释 |
| 添加 | 成员回复评论 |
| 更新 | 编辑成员的注释 |
| 删除 | 已删除成员的评论 |

[文件库组件](essentials-file-library.md)
社交事件 `topic`= com/adobe/cq/social/fileLibrary

| **动词** | **描述** |
|---|---|
| POST | 成员创建文件夹 |
| 附加 | 成员上传文件 |
| 更新 | 成员更新文件夹或文件 |
| 删除 | 成员删除文件夹或文件 |

[论坛组件](essentials-forum.md)
社交事件 `topic`= com/adobe/cq/social/forum

| **动词** | **描述** |
|---|---|
| POST | 成员创建论坛主题 |
| 添加 | 成员对论坛主题的回复 |
| 更新 | 编辑成员的论坛主题或回复 |
| 删除 | 已删除成员的论坛主题或回复 |

[日志组件](blog-developer-basics.md)
社交事件 `topic`= com/adobe/cq/social/journal

| **动词** | **描述** |
|---|---|
| POST | 成员创建博客文章 |
| 添加 | 成员对博客文章的评论 |
| 更新 | 编辑成员的博客文章或评论 |
| 删除 | 已删除成员的博客文章或评论 |

[问题与解答组件](qna-essentials.md)
社交事件 `topic` = com/adobe/cq/social/qna

| **动词** | **描述** |
|---|---|
| POST | 成员创建问题与解答问题 |
| 添加 | 成员创建问题与解答答案 |
| 更新 | 编辑成员的问题或答案 |
| 选择 | 已选择成员的答案 |
| 取消选择 | 已取消选择成员的答案 |
| 删除 | 已删除成员的问题或答案 |

[审核组件](reviews-basics.md)
社交事件 `topic`= com/adobe/cq/social/review

| **动词** | **描述** |
|---|---|
| POST | 成员创建审核 |
| 更新 | 成员的审核已编辑 |
| 删除 | 已删除成员的审核 |

[评级组件](rating-basics.md)
社交事件 `topic`= com/adobe/cq/social/tally

| **动词** | **描述** |
|---|---|
| 添加评级 | 成员内容已上标 |
| 删除评级 | 成员内容已降级 |

[投票组件](essentials-voting.md)
社交事件 `topic`= com/adobe/cq/social/tally

| **动词** | **描述** |
|---|---|
| 添加投票 | 成员内容已被投票表决 |
| 删除投票 | 成员内容已被否决 |

**启用审核的组件**
社交事件 `topic`= com/adobe/cq/social/moderation

| **动词** | **描述** |
|---|---|
| 拒绝 | 成员内容被拒绝 |
| 标记为不适当 | 成员内容已标记 |
| 取消标记为不适当 | 成员内容未标记 |
| ACCEPT | 审查方已批准成员的内容 |
| 关闭 | 成员关闭评论以进行编辑和回复 |
| 打开 | 成员重新打开注释 |

## 自定义组件的事件 {#events-for-custom-components}

对于自定义组件， [SocialEvent抽象类](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) 必须扩展才能将组件的事件记录为 `actions`发生于 `topic`.

自定义事件将覆盖方法 `getVerb()` 以便适当地 `verb`针对每个维度返回 `action`. 此 `verb` 针对操作返回的可能是常用的(例如 `POST`)或组件专用的(例如 `ADD RATING`)。 有一个 *n-1* 关系介于 `actions`和 `verbs`.

>[!NOTE]
>
>确保自定义扩展注册的排名低于产品中的任何现有实施。

### 自定义组件事件的伪代码 {#pseudo-code-for-custom-component-event}

[org.osgi.service.event.Event](https://osgi.org/javadoc/r4v41/org/osgi/service/event/Event.html)；
[com.adobe.cq.social.scf.core.SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html)；
[com.adobe.granite.activitystreams.ObjectType](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ObjectTypes.html)；
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

## 用于筛选活动流数据的示例EventListener {#sample-eventlistener-to-filter-activity-stream-data}

可以侦听事件，以修改活动流中显示的内容。

以下伪代码示例将从活动流中删除Comments组件的DELETE事件。

### EventListener伪代码 {#pseudo-code-for-eventlistener}

需要 [最新功能包](deploy-communities.md#latestfeaturepack).

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
