---
title: 社交图要点
seo-title: Social Graph Essentials
description: 跟随组件和跟随组件概述
seo-description: follow component and following component overview
uuid: 8ea33760-62b1-4de2-b07f-bc2417ade156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f8d85d72-0215-4680-a334-e37a530fba58
exl-id: c037a788-c943-4f95-a028-1fcb0ef48f86
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 3%

---

# 社交图要点  {#social-graph-essentials}

社区成员可以关注的功能 [活动](essentials-activities.md) 以及遵循通过两个组件来建立：

此 `following` 组件必须与其他资源相关联，并且已为中的现有Communities成员和功能建立此关联 [社区站点](overview.md#communitiessites).

此 `following` 组件列出位于当前成员后面或位于当前成员后面的成员。 此成员之间关系的社交图包含在为社区站点建立的用户配置文件中。

## 适用于客户端的Essentials {#essentials-for-client-side}

### 关注 {#following}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/socialgraph/components/hbs/relationships</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>可包含</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
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
   <td>参见 <a href="socialgraph.md">使用社交图</a></td>
  </tr>
  <tr>
   <td><strong> 可选<br /> 属性</strong></td>
   <td>
    <ul>
     <li>名称: <strong><code>outgoing</code></strong></li>
     <li>类型：布尔型</li>
     <li>值:<br />
      <ul>
       <li><i>True </i>- <code>following</code> 组件将列出当前登录的成员 <code>follows</code></li>
       <li><i>False </i>- <code>following</code> 组件将列出满足以下条件的成员 <code>follow </code>当前登录的成员</li>
      </ul> </li>
    </ul> <p>默认为 <i>true</i> 如果属性缺失。 目前，在创作模式下无法使用“编辑”对话框设置此属性。 必须将属性添加到的实例 <code>following </code>节点使用 <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>.</p> </td>
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

## 服务器端Essentials {#essentials-for-server-side}

* [社交图API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [社交图端点](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [服务器端自定义](server-customize.md)
