---
title: 更新版本车辆定义
seo-title: 更新版本车辆定义
description: 本文详细介绍了各种类型的AEM版本，包括完整版本、功能包和服务包。
seo-description: 本文详细介绍了各种类型的AEM版本，包括完整版本、功能包和服务包。
uuid: 388fb6f5-0249-41e2-a460-1bb4cd0f8494
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 32695db5-d62d-4959-8a24-3d56b4a19904
translation-type: tm+mt
source-git-commit: b827c8acb1db158060d209c819fc72ffbfeca65f

---


# AEM Update发布版本车辆定义{#update-release-vehicle-definitions}

本文档包含有关各种Adobe Experience Manager(AEM)版本的详细信息，包括Adobe向客户交付的完整版本、功能包和服务包。

>[!Note]
>
>有关AEM更新版本的发布计划，请参阅 [AEM更新版本路线图](https://helpx.adobe.com/experience-manager/update-releases-roadmap.html)

## 完整版本 {#full-release}

<table>
 <tbody>
  <tr>
   <td><strong>定义</strong></td>
   <td>
    <ul>
     <li>计划发布</li>
     <li>支持特定版本的升级路径（发行说明中定义）</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>命名</strong></td>
   <td>
    <ul>
     <li>主要版本的版本号根据公式X+1.Y.Z增加。 </li>
     <li>次要版本的版本号根据公式X.Y+1.Z增加</li>
    </ul> <p>其中，X是主版本号，Y是次版本号，Z是修补程序号。</p> </td>
  </tr>
  <tr>
   <td><strong>Inclusion</strong></td>
   <td>
    <ul>
     <li>新增功能</li>
     <li>改进</li>
     <li>错误修复</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>文档</strong></td>
   <td>
    <ul>
     <li>发行说明可在文档门户上找到</li>
     <li>有关功能、改进和错误修复的文档可在文档门户上找到</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td>每年</td>
  </tr>
  <tr>
   <td><strong>可用性和安装</strong></td>
   <td>
    <ul>
     <li>以独立产品安装程序形式提供</li>
     <li>可从授权许可网站和托管服务授权许可网站获得</li>
     <li>可能需要迁移内容存储库</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>测试级别</strong></td>
   <td>由QA完全验证</td>
  </tr>
 </tbody>
</table>

## Service Pack {#service-pack}

<table>
 <tbody>
  <tr>
   <td><strong>定义</strong></td>
   <td>
    <ul>
     <li>计划发布</li>
     <li>当前，无法回滚</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>命名</strong></td>
   <td>
    <ul>
     <li>修补程序发行号是一个单位数字</li>
     <li>安装后，将根据公式X.Y.Z.SPx增加已安装的发行版号修补程序数</li>
     <li>其中，X是主版本号，Y是次版本号，Z是修补程序号。 x是服务包编号。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Inclusion</strong></td>
   <td>
    <ul>
     <li>新增功能</li>
     <li>改进</li>
     <li>错误修复</li>
     <li>Common Interest功能包（如果有）</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>文档</strong></td>
   <td>
    <ul>
     <li>文档门户上提供的发行说明</li>
     <li>文档门户上关于功能、改进和错误修复的文档</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td>季度</td>
  </tr>
  <tr>
   <td><strong>可用性和安装</strong></td>
   <td>
    <ul>
     <li>以包的形式交付</li>
     <li>在包共享中可用</li>
     <li>需要现有功能安装</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>测试级别</strong></td>
   <td>
    <ul>
     <li>已验证所有修复</li>
     <li>自动运行时的总体包完整性</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 累积修复程序包  {#cumulative-fix-pack-aem}

<table>
 <tbody>
  <tr>
   <td><strong>定义</strong></td>
   <td>
    <ul>
     <li>释放修复的单一交付模型</li>
     <li>包含各个组件的内容包的聚合器内容包</li>
     <li>CFP是热修复程序的翻转版本，但其中没有任何改进。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>命名</strong></td>
   <td><p>X.Y.Z.CFPx</p> <p>其中，X是主版本号，Y是次版本号，Z是修补程序号。 x是累积服务包编号。</p> </td>
  </tr>
  <tr>
   <td><strong>Inclusion</strong></td>
   <td><p>CFP是包含所有组件在指定日期的修复的累积修复包。 例如，如果客户应用CFP3，则CFP3 = CFP1 + CFP2。</p> </td>
  </tr>
  <tr>
   <td><strong>文档</strong></td>
   <td>文档门户上提供的发行说明</td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td>季风</td>
  </tr>
  <tr>
   <td><strong>可用性和安装</strong></td>
   <td>
    <ul>
     <li>以包的形式交付</li>
     <li>在包共享中可用</li>
     <li>取决于发布的最新服务包</li>
     <li>CFP是自相关的。 客户无需担心查找／解决依赖关系。 CFP应安装在最新发布的Service pack上。</li>
     <li>CFP可以作为单个包安装，从而改善客户体验。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>测试级别</strong></td>
   <td>在集成级别和回归测试中验证的QA</td>
  </tr>
 </tbody>
</table>

## Oak累积修复包 {#oak-cumulative-fix-pack}

<table>
 <tbody>
  <tr>
   <td><strong>定义</strong></td>
   <td>
    <ul>
     <li>与标准CFP类似，但仅包含与Oak相关的修复</li>
     <li>COFP是自依赖的（无依赖关系）。 客户无需担心查找／解决依赖关系。 [1]</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>命名</strong></td>
   <td>oak &lt;版本&gt;</td>
  </tr>
  <tr>
   <td><strong>Inclusion</strong></td>
   <td>COFP是包含针对特定1.x版本的所有Oak组件的修复的累积修复包。 例如，如果客户应用COHF 1.x.3，则应用COHF 1.x.3。 = COHF 1.x.1 + COHF 1.x.2。</td>
  </tr>
  <tr>
   <td><strong>文档</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td><p>根据需要</p> </td>
  </tr>
  <tr>
   <td><strong>可用性和安装</strong></td>
   <td>
    <ul>
     <li>COFP安装过程已经简化，可改善客户体验。 （客户只需为所有组件安装一个包即可）。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>测试级别</strong></td>
   <td><p>QA已验证</p> </td>
  </tr>
 </tbody>
</table>

## 热修复 {#hot-fix}

<table>
 <tbody>
  <tr>
   <td><strong>定义</strong></td>
   <td><p>包含为解决严重降低基本服务或显着影响业务运营的产品缺陷而创建的一个或多个文件。 </p> </td>
  </tr>
  <tr>
   <td><strong>命名</strong></td>
   <td>cq-&lt;发行版&gt;-修补程序-&lt;修补程序ID&gt;-&lt;修补程序版本&gt;</td>
  </tr>
  <tr>
   <td><strong>Inclusion</strong></td>
   <td>包括针对特定问题的修复</td>
  </tr>
  <tr>
   <td><strong>文档</strong></td>
   <td>仅根据客户通过AEM支持门户提出的请求，才提供公共修补程序的发行说明。</td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td>根据需要</td>
  </tr>
  <tr>
   <td><strong>可用性和安装</strong></td>
   <td>
    <ul>
     <li>以包的形式交付</li>
     <li>在包共享中可用</li>
     <li>取决于发布的最新服务包</li>
     <li>除非另有规定，否则大多数热修复都是独立的。 可以按任意顺序安装。 可以通过“依赖关系”元素的“包共享详细信息”选项卡进行验证。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>测试级别</strong></td>
   <td>
    <ul>
     <li>由客户关怀部门验证</li>
     <li>AEM热修复与Service Pack或产品发行版的质量保证级别相同，因此不会从中受益。 因此，作为质量部署流程的一部分，应首先在分阶段环境中验证它们。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 叠加 {#overlay}

<table>
 <tbody>
  <tr>
   <td><strong>定义</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>命名</strong></td>
   <td>overlay-&lt;ticket ID&gt;</td>
  </tr>
  <tr>
   <td><strong>Inclusion</strong></td>
   <td>JS或JSP文件的错误修复</td>
  </tr>
  <tr>
   <td><strong>文档</strong></td>
   <td>无</td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td>根据需要</td>
  </tr>
  <tr>
   <td><strong>可用性和安装</strong></td>
   <td>
    <ul>
     <li>由AEM客户关怀团队以包形式提供</li>
     <li>不一定包含在Service pack或完整版本中</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>测试级别</strong></td>
   <td>由客户关怀部门验证</td>
  </tr>
 </tbody>
</table>

## 功能包 {#feature-pack}

<table>
 <tbody>
  <tr>
   <td><strong>定义</strong></td>
   <td>
    <ul>
     <li>功能包是附加功能，通过Service pack提供。 如果AEM版本发布了最后一个服务包，Adobe将来不会为其提供任何功能包。</li>
     <li>FP包含产品增强功能，计划在随后的产品发布中发布，但根据Adobe产品管理的决定提前发布。</li>
     <li>功能始终与下一个主要版本合并，然后备份到客户所需的AEM版本</li>
     <li>Common Interest和GA功能包合并到下一个服务包中</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>命名</strong></td>
   <td>cq-&lt;发行版&gt;-featurepack-&lt;featurepack ID&gt;-&lt;featurepack version&gt;</td>
  </tr>
  <tr>
   <td><strong>Inclusion</strong></td>
   <td>
    <ul>
     <li>新增功能</li>
     <li>改进</li>
     <li>错误修复（增量产品更新）</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>文档</strong></td>
   <td>帮助x.adobe.com上提供相关文档。</td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td>因产品区域而异</td>
  </tr>
  <tr>
   <td><strong>可用性和安装</strong></td>
   <td>
    <ul>
     <li>通过Service pack交付</li>
     <li>可用于包共享。 客户通过包共享接受Adobe的条款和条件。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>测试级别</strong></td>
   <td>“常规可用性”功能包已通过QA验证</td>
  </tr>
 </tbody>
</table>

* [1]:OAK修复不作为单独的热修复提供。 但是，它们会包含在后续的Cumulative Oak热修复中。 如有必要，可在最新COFP上构建诊断版本。 前提是客户拥有最新的COFP运行。 诊断构建只提供与热修复相同的级别质量保证。 因此，他们提供的质量保证级别与累积修复包、服务包或产品版本不同。 最终的修复随下一个CFP一起提供。

