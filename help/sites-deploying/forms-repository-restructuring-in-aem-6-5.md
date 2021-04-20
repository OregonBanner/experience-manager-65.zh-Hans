---
title: Forms 6.5中的存储库重组
seo-title: Forms 6.5中的存储库重组
description: 了解如何进行必要的更改以迁移到适用于Forms的AEM 6.5中的新存储库结构。
seo-description: 了解如何进行必要的更改以迁移到适用于Forms的AEM 6.5中的新存储库结构。
uuid: e60830d4-23ca-4be9-941a-ee4abe4786a6
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 1ce9a622-5968-407f-a74b-d325a2bff669
feature: Upgrading
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Forms 6.5{#forms-repository-restructuring-in-aem}中的存储库重构

如AEM 6.5](/help/sites-deploying/repository-restructuring.md)中的父级[存储库重组页所述，升级到AEM 6.5的客户应使用此页评估与影响AEM Forms解决方案的存储库更改相关的工作。 某些更改需要在AEM 6.5升级过程中进行工作，而其他更改可能会延迟到将来的升级。

**通过6.5升级**

* [Misc](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

**在将来升级之前**

* [EchosignCloud Service配置](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#echosign-cloud-service-configuration)
* [RecaptchaCloud Service配置](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#recaptcha-cloud-service-configurations)
* [TypekitCloud Service配置](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#typekit-cloud-service-configurations)
* [Misc](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

## 使用6.5升级{#with-upgrade}

### Misc {#misc}

| **上一个位置** | `/etc/clientlibs/fd/fp` |
|---|---|
| **新位置** | `/libs/fd/fp/components` |
| **重组指导** | 自定义代码中对旧位置的任何显式引用都必须更新到新位置。 |
| **注释** | 不应修改或扩展这些客户端库。 |

| **上一个位置** | `/etc/clientlibs/fd/rte` |
|---|---|
| **新位置** | `/libs/fd/rte` |
| **重组指导** | 对于客户端库中可通过绝对路径引用的资源，您需要在新资源中使用较新的路径。 |
| **注释** | 不适用 |

| **上一个位置** | `/etc/clientlibs/fd/af` |
|---|---|
| **新位置** | `/libs/fd/af/authoring/clientlibs` |
| **重组指导** | 对于客户端库中可通过绝对路径引用的资源，您需要在新资源中使用较新的路径。 |
| **注释** | 不适用 |

| **上一个位置** | `/etc/clientlibs/fd/xfaforms` |
|---|---|
| **新位置** | `/libs/fd/xfaforms/clientlibs/` |
| **重组指导** | 对于客户端库中可通过绝对路径引用的资源，您需要在新资源中使用较新的路径。 |
| **注释** | 不适用 |

| **上一个位置** | `/etc/clientlibs/fd/af` |
|---|---|
| **新位置** | `/libs/fd/af/runtime/clientlibs` |
| **重组指导** | 对于客户端库中可通过绝对路径引用的资源，您需要在新资源中使用较新的路径。 |
| **注释** | 不适用 |

| **上一个位置** | `/etc/clientlibs/fd/af` |
|---|---|
| **新位置** | `/libs/fd/af/runtime/clientlibs` |
| **重组指导** | 对于客户端库中可通过绝对路径引用的资源，您需要在新资源中使用较新的路径。 |
| **注释** | 不适用 |

| **上一个位置** | `/etc/clientlibs/fd/expeditor` |
|---|---|
| **新位置** | `/libs/fd/expeditor/clientlibs` |
| **重组指导** | 对于客户端库中可通过绝对路径引用的资源，您需要在新资源中使用较新的路径。 |
| **注释** | 不适用 |

| **上一个位置** | `/etc/clientlibs/fd/fmaddon` |
|---|---|
| **新位置** | `/libs/fd/fmaddon` |
| **重组指导** | 从不建议或支持更改这些clientlib。 如果对这些clientlibs进行了修改，则应回滚以使用AEM提供的代码。 |
| **注释** | 不适用 |

| **上一个位置** | `/etc/aep` |
|---|---|
| **新位置** | `/var/fd/content/annotations` |
| **重组指导** | 从不建议或支持更改这些clientlib。 如果对这些clientlibs进行了修改，则应回滚以使用AEM提供的代码。 |
| **注释** | 不适用 |

## 未来升级前{#prior-to-upgrade}

### EchosignCloud Service配置{#echosign-cloud-service-configuration}

| **上一个位置** | `/etc/cloudservices/echosign` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/echosign` |
| **重组指导** | 要从Forms迁移UI触发的[延迟内容迁移](/help/sites-deploying/lazy-content-migration.md)实用程序。 |
| **注释** | 不适用 |

### RecaptchaCloud Service配置{#recaptcha-cloud-service-configurations}

| **上一个位置** | `/etc/cloudservices/recaptcha` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/recaptcha` |
| **重组指导** | 要从Forms迁移UI触发的[延迟内容迁移](/help/sites-deploying/lazy-content-migration.md)实用程序。 |
| **注释** | 不适用 |

### TypekitCloud Service配置{#typekit-cloud-service-configurations}

| **上一个位置** | `/etc/cloudservices/typekit` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/typekit` |
| **重组指导** | 要从Forms迁移UI触发的[延迟内容迁移](/help/sites-deploying/lazy-content-migration.md)实用程序。 |
| **注释** | 不适用 |

### Misc {#misc-1}

| **上一个位置** | `/etc/cloudservices/fdm` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/fdm` |
| **重组指导** | 要从Forms迁移UI触发的[延迟内容迁移](/help/sites-deploying/lazy-content-migration.md)实用程序。 |
| **注释** | 不适用 |

| **上一个位置** | `/etc/designs/fd/fp` |
|---|---|
| **新位置** | `/libs/fd/fp` |
| **重组指导** | 对/etc模板的任何引用最终应更新为指向其`/libs`对应项。 |
| **注释** | 不适用 |

