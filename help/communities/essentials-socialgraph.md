---
title: 社交图基础
seo-title: 社交图基础
description: 后续组件和后续组件概述
seo-description: 后续组件和后续组件概述
uuid: 8ea33760-62b1-4de2-b07f-bc2417ade156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f8d85d72-0215-4680-a334-e37a530fba58
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 3%

---


# 社交图基本信息{#social-graph-essentials}

社区成员遵循[活动](essentials-activities.md)并遵循的能力通过两个组件建立：

`following`组件必须与其他资源关联，并且已经为[社区站点](overview.md#communitiessites)中的现有社区成员和功能建立了此关联。

`following`组件列表当前成员之后或当前成员后面的成员。 在为社区站点建立的用户用户档案中，包含成员之间关系的社交图。

## 客户端{#essentials-for-client-side}的必备工具

### 关注 {#following}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>社交／社交图／组件/hbs/关系</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>可包含</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.socialgraph</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/relationships.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/clientlibs/relationships.css</td>
  </tr>
  <tr>
   <td><strong> 属性</strong></td>
   <td>请参阅<a href="socialgraph.md">使用社交图</a></td>
  </tr>
  <tr>
   <td><strong> 可选<br />属性</strong></td>
   <td>
    <ul>
     <li>名称: <strong><code>outgoing</code></strong></li>
     <li>类型：布尔型</li>
     <li>值:<br />
      <ul>
       <li><i>True - </i>组件 <code>following</code> 将列表当前登录成员的成员 <code>follows</code></li>
       <li><i>False  </i>-组 <code>following</code> 件将列表当前 <code>follow </code>登录成员的成员</li>
      </ul> </li>
    </ul> <p>如果属性缺失，则默认为<i>true</i>。 当前，无法在创作模式下使用编辑对话框设置此属性。 必须使用<a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>将属性添加到<code>following </code>节点的实例中。</p> </td>
  </tr>
 </tbody>
</table>

### 关注 {#follow}

| **resourceType** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**可包含**](scf.md#add-or-include-a-communities-component) | 否 |
| **模板** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **css** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [客户端自定义](client-customize.md)

## 服务器端{#essentials-for-server-side}的必备工具

* [社交图API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [社交图端点](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [服务器端自定义](server-customize.md)

