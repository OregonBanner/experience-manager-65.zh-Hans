---
title: AEM 6.5中的表单存储库重组
seo-title: AEM 6.5中的表单存储库重组
description: 了解如何进行必要的更改以迁移到AEM 6.5 for Forms中的新存储库结构。
seo-description: 了解如何进行必要的更改以迁移到AEM 6.5 for Forms中的新存储库结构。
uuid: e60830d4-23ca-4be9-941a-ee4abe4786a6
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 1ce9a622-5968-407f-a74b-d325a2bff669
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb

---


# AEM 6.5中的表单存储库重组{#forms-repository-restructuring-in-aem}

如AEM 6.5页面中的父存储库重组中所述 [](/help/sites-deploying/repository-restructuring.md) ，升级到AEM 6.5的客户应使用此页面评估与影响AEM Forms Solution的存储库更改相关的工作成果。 某些更改需要在AEM 6.5升级过程中进行工作，而其他更改可能会延迟到将来升级。

**升级6.5版**

* [Misc](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

**在将来升级之前**

* [Echosign云服务配置](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#echosign-cloud-service-configuration)
* [Recaptcha云服务配置](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#recaptcha-cloud-service-configurations)
* [Typekit云服务配置](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#typekit-cloud-service-configurations)
* [Misc](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

## 升级6.5版 {#with-upgrade}

### Misc {#misc}

| **上一位置** | `/etc/clientlibs/fd/fp` |
|---|---|
| **新位置** | `/libs/fd/fp/components` |
| **重组指导** | 对旧版位置的自定义代码中的任何显式引用都必须更新到新位置。 |
| **注释** | 不应修改或扩展这些客户端库。 |

| **上一位置** | `/etc/clientlibs/fd/rte` |
|---|---|
| **新位置** | `/libs/fd/rte` |
| **重组指导** | 对于客户端库中可通过绝对路径引用的资源，您需要在新资源中使用较新的路径。 |
| **注释** | 不适用 |

| **上一位置** | `/etc/clientlibs/fd/af` |
|---|---|
| **新位置** | `/libs/fd/af/authoring/clientlibs` |
| **重组指导** | 对于客户端库中可通过绝对路径引用的资源，您需要在新资源中使用较新的路径。 |
| **注释** | 不适用 |

| **上一位置** | `/etc/clientlibs/fd/xfaforms` |
|---|---|
| **新位置** | `/libs/fd/xfaforms/clientlibs/` |
| **重组指导** | 对于客户端库中可通过绝对路径引用的资源，您需要在新资源中使用较新的路径。 |
| **注释** | 不适用 |

| **上一位置** | `/etc/clientlibs/fd/af` |
|---|---|
| **新位置** | `/libs/fd/af/runtime/clientlibs` |
| **重组指导** | 对于客户端库中可通过绝对路径引用的资源，您需要在新资源中使用较新的路径。 |
| **注释** | 不适用 |

| **上一位置** | `/etc/clientlibs/fd/af` |
|---|---|
| **新位置** | `/libs/fd/af/runtime/clientlibs` |
| **重组指导** | 对于客户端库中可通过绝对路径引用的资源，您需要在新资源中使用较新的路径。 |
| **注释** | 不适用 |

| **上一位置** | `/etc/clientlibs/fd/expeditor` |
|---|---|
| **新位置** | `/libs/fd/expeditor/clientlibs` |
| **重组指导** | 对于客户端库中可通过绝对路径引用的资源，您需要在新资源中使用较新的路径。 |
| **注释** | 不适用 |

| **上一位置** | `/etc/clientlibs/fd/fmaddon` |
|---|---|
| **新位置** | `/libs/fd/fmaddon` |
| **重组指导** | 从不建议或支持更改这些clientlib。 如果对这些clientlib进行了修改，则应回滚这些修改以使用AEM提供的代码。 |
| **注释** | 不适用 |

| **上一位置** | `/etc/aep` |
|---|---|
| **新位置** | `/var/fd/content/annotations` |
| **重组指导** | 从不建议或支持更改这些clientlib。 如果对这些clientlib进行了修改，则应回滚这些修改以使用AEM提供的代码。 |
| **注释** | 不适用 |

## 在将来升级之前 {#prior-to-upgrade}

### Echosign云服务配置 {#echosign-cloud-service-configuration}

| **上一位置** | `/etc/cloudservices/echosign` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/echosign` |
| **重组指导** | 要从 [表单迁移](/help/sites-deploying/lazy-content-migration.md) UI触发的延迟内容迁移实用程序。 |
| **注释** | 不适用 |

### Recaptcha云服务配置 {#recaptcha-cloud-service-configurations}

| **上一位置** | `/etc/cloudservices/recaptcha` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/recaptcha` |
| **重组指导** | 要从 [表单迁移](/help/sites-deploying/lazy-content-migration.md) UI触发的延迟内容迁移实用程序。 |
| **注释** | 不适用 |

### Typekit云服务配置 {#typekit-cloud-service-configurations}

| **上一位置** | `/etc/cloudservices/typekit` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/typekit` |
| **重组指导** | 要从 [表单迁移](/help/sites-deploying/lazy-content-migration.md) UI触发的延迟内容迁移实用程序。 |
| **注释** | 不适用 |

### Misc {#misc-1}

| **上一位置** | `/etc/cloudservices/fdm` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/fdm` |
| **重组指导** | 要从 [表单迁移](/help/sites-deploying/lazy-content-migration.md) UI触发的延迟内容迁移实用程序。 |
| **注释** | 不适用 |

| **上一位置** | `/etc/designs/fd/fp` |
|---|---|
| **新位置** | `/libs/fd/fp` |
| **重组指导** | 对/etc模板的任何引用最终应更新为指向其对应的 `/libs` 模板。 |
| **注释** | 不适用 |

