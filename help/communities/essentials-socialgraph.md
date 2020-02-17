---
title: Social Graph Essentials
seo-title: Social Graph Essentials
description: 后续组件和以下组件概述
seo-description: 后续组件和以下组件概述
uuid: 8ea33760-62b1-4de2-b07f-bc2417ade156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f8d85d72-0215-4680-a334-e37a530fba58
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Social Graph Essentials {#social-graph-essentials}

社区成员可以通过以下两个部 [分](essentials-activities.md) ，来开展和开展活动：

该组 `follow`件必须与其他资源关联，并且该关联已针对社区站点中的现有社区成员和功能 [建立](overview.md#communitiessites)。

组 `following`件列出当前成员之后或当前成员后面的成员。 此社交图形包含在为社区站点建立的用户配置文件中。

## 客户端必备工具 {#essentials-for-client-side}

### 关注 {#following}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>社交／社交图形／组件/hbs/关系</td>
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
   <td>请参阅 <a href="socialgraph.md">使用社交图</a></td>
  </tr>
  <tr>
   <td><strong> 可选属性<br /> (Optional Property)</strong></td>
   <td>
    <ul>
     <li>名称: <strong><code>outgoing</code></strong></li>
     <li>类型：布尔型</li>
     <li>值:<br />
      <ul>
       <li><i>true </i>-组 <code>following</code> 件将列出当前已登录成员的成员 <code>follows</code></li>
       <li><i>false </i>-组 <code>following</code> 件将列出当前登 <code>follow </code>录成员的成员</li>
      </ul> </li>
    </ul> <p>如果属 <i>性缺失</i> ，则默认为true。 当前，无法在创作模式下使用编辑对话框设置此属性。 必须使用CRXDE|Lite将该属性添 <code>following </code>加到节 <a href="../../help/sites-developing/developing-with-crxde-lite.md">点实例中</a>。</p> </td>
  </tr>
 </tbody>
</table>

### 关注 {#follow}

| **resourceType** | social/socialgraph/components/hbs/following |
|---|---|
| [**可包含&#x200B;**](scf.md#add-or-include-a-communities-component) | 否 |
| **模板** | /libs/social/socialgraph/components/hbs/following/following.hbs |
| **css** | /libs/social/socialgraph/components/hbs/following/clientlibs/following.css |

* [客户端自定义](client-customize.md)

## 服务器端必备工具 {#essentials-for-server-side}

* [社交图API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [社交图端点](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [服务器端自定义](server-customize.md)

