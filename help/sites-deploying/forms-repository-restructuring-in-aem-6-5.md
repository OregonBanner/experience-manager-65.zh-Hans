---
title: AEM 6.5中的Forms存储库重组
description: 了解如何进行必要的更改，以迁移到AEM 6.5 for Forms中的新存储库结构。
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: d555422e-dc97-4d45-9525-4299d22315e2
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 7%

---

# AEM 6.5中的Forms存储库重组{#forms-repository-restructuring-in-aem}

如父项中所述 [AEM 6.5中的存储库重组](/help/sites-deploying/repository-restructuring.md) 页面，升级到AEM 6.5的客户应使用此页面评估与影响AEM Forms解决方案的存储库更改相关的工作量。 在AEM 6.5升级过程中，有些更改需要您投入精力，而有些则可能会推迟到将来升级。

**6.5版升级**

* [杂项](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

**在将来升级之前**

* [EchosignCloud Service配置](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#echosign-cloud-service-configuration)
* [RecaptchaCloud Service配置](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#recaptcha-cloud-service-configurations)
* [TypekitCloud Service配置](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#typekit-cloud-service-configurations)
* [杂项](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

## 6.5版升级 {#with-upgrade}

### 杂项 {#misc}

| **上一个位置** | `/etc/clientlibs/fd/fp` |
|---|---|
| **新位置** | `/libs/fd/fp/components` |
| **重构指南** | 自定义代码中对旧版位置的任何显式引用都必须更新到新位置。 |
| **注释** | 不应编辑或扩展这些客户端库。 |

| **上一个位置** | `/etc/clientlibs/fd/rte` |
|---|---|
| **新位置** | `/libs/fd/rte` |
| **重构指南** | 对于可由绝对路径引用的客户端库中的资源，您必须在新资源中使用较新的路径。 |
| **注释** | 不适用 |

| **上一个位置** | `/etc/clientlibs/fd/af` |
|---|---|
| **新位置** | `/libs/fd/af/authoring/clientlibs` |
| **重构指南** | 对于可由绝对路径引用的客户端库中的资源，您必须在新资源中使用较新的路径。 |
| **注释** | 不适用 |

| **上一个位置** | `/etc/clientlibs/fd/xfaforms` |
|---|---|
| **新位置** | `/libs/fd/xfaforms/clientlibs/` |
| **重构指南** | 对于可由绝对路径引用的客户端库中的资源，您必须在新资源中使用较新的路径。 |
| **注释** | 不适用 |

| **上一个位置** | `/etc/clientlibs/fd/af` |
|---|---|
| **新位置** | `/libs/fd/af/runtime/clientlibs` |
| **重构指南** | 对于可由绝对路径引用的客户端库中的资源，您必须在新资源中使用较新的路径。 |
| **注释** | 不适用 |

| **上一个位置** | `/etc/clientlibs/fd/af` |
|---|---|
| **新位置** | `/libs/fd/af/runtime/clientlibs` |
| **重构指南** | 对于可由绝对路径引用的客户端库中的资源，您必须在新资源中使用较新的路径。 |
| **注释** | 不适用 |

| **上一个位置** | `/etc/clientlibs/fd/expeditor` |
|---|---|
| **新位置** | `/libs/fd/expeditor/clientlibs` |
| **重构指南** | 对于可由绝对路径引用的客户端库中的资源，您必须在新资源中使用较新的路径。 |
| **注释** | 不适用 |

| **上一个位置** | `/etc/clientlibs/fd/fmaddon` |
|---|---|
| **新位置** | `/libs/fd/fmaddon` |
| **重构指南** | 从不建议或支持更改这些clientlibs。 如果对这些clientlib进行了修改，则应回退以使用AEM提供的代码。 |
| **注释** | 不适用 |

| **上一个位置** | `/etc/aep` |
|---|---|
| **新位置** | `/var/fd/content/annotations` |
| **重构指南** | 从不建议或支持更改这些clientlibs。 如果对这些clientlib进行了修改，则应回退以使用AEM提供的代码。 |
| **注释** | 不适用 |

## 在将来升级之前 {#prior-to-upgrade}

### EchosignCloud Service配置 {#echosign-cloud-service-configuration}

| **上一个位置** | `/etc/cloudservices/echosign` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/echosign` |
| **重构指南** | 此 [延迟内容迁移](/help/sites-deploying/lazy-content-migration.md) 要从Forms迁移UI触发的实用程序。 |
| **注释** | 不适用 |

### RecaptchaCloud Service配置 {#recaptcha-cloud-service-configurations}

| **上一个位置** | `/etc/cloudservices/recaptcha` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/recaptcha` |
| **重构指南** | 此 [延迟内容迁移](/help/sites-deploying/lazy-content-migration.md) 要从Forms迁移UI触发的实用程序。 |
| **注释** | 不适用 |

### TypekitCloud Service配置 {#typekit-cloud-service-configurations}

| **上一个位置** | `/etc/cloudservices/typekit` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/typekit` |
| **重构指南** | 此 [延迟内容迁移](/help/sites-deploying/lazy-content-migration.md) 要从Forms迁移UI触发的实用程序。 |
| **注释** | 不适用 |

### 杂项 {#misc-1}

| **上一个位置** | `/etc/cloudservices/fdm` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/fdm` |
| **重构指南** | 此 [延迟内容迁移](/help/sites-deploying/lazy-content-migration.md) 要从Forms迁移UI触发的实用程序。 |
| **注释** | 不适用 |

| **上一个位置** | `/etc/designs/fd/fp` |
|---|---|
| **新位置** | `/libs/fd/fp` |
| **重构指南** | 更新对/etc模板的任何引用以指向其 `/libs` 对方。 |
| **注释** | 不适用 |
