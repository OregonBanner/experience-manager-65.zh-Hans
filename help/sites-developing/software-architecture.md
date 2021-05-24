---
title: 软件架构
seo-title: 软件架构
description: 构建软件的最佳实践
seo-description: 构建软件的最佳实践
uuid: a557f6ca-c3f1-486e-a45e-6e1f986fab41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 92971747-1c74-4917-b5a0-7b79b3ae1e68
exl-id: cd4f3b4c-5488-4ca7-9c1e-b4c819fda8e8
source-git-commit: 423e17dadf2e506eb68b37851dde5e68ed950866
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---

# 软件架构{#software-architecture}

## 升级设计{#design-for-upgrades}

在扩展OOTB行为时，务必牢记升级。 始终在/apps目录中应用自定义设置，并在/libs目录中相应节点的顶部进行叠加，或使用sling:resourceSuperType扩展开箱即用的行为。 虽然可能需要进行一些修改才能支持新的AEM版本，但如果遵循此做法，新版本不应覆盖您的自定义设置。

### 尽可能重复使用模板和组件{#reuse-template-and-components-when-possible}

这样，站点就可以保持更一致的外观，并简化代码维护。 当需要新模板时，请确保从共享的基本模板进行扩展，以便能够在一个位置对全局要求（如clientlib包含）进行编码。 当需要新组件时，请寻找从现有组件扩展的机会。

### 设计模板设计{#design-template-designs}

通过定义页面上每个Parsys中可包含的组件，可以控制网站外观的一致性。 通过限制对页面上设计的访问，允许“超级作者”在确保其他作者遵守公司标准的同时，在无需开发人员干预的情况下修改每页允许的组件。

### 开发SOLID体系结构{#develop-a-solid-architecture}

SOLID是一个缩略词，用于描述应当遵循的五个架构原则：

* ****&#x200B;单一责任原则 — 每个模块、类、方法等应仅负一个责任。
* **** Open/Closed Price — 模块应打开以进行扩展，并关闭以进行修改。
* **** Liskov替换原则 — 类型应由其子类型替换。
* ****&#x200B;接口隔离原则 — 不应强制任何客户端依赖其不使用的方法。
* ****&#x200B;依赖关系反演原则 — 高级模块不应依赖于低级模块。两者都应该取决于抽象概念。 抽象不应取决于细节。 细节应该取决于抽象概念。

努力遵守这五项原则应导致一种严格区分关切的制度。

>[!TIP]
>
>SOLID是面向对象编程中常用的概念，在工业文献中对每个元素都进行了广泛的讨论。
>
>这只是为了提高认识而提供的简短摘要，我们鼓励您更深入地了解这些概念。

### 遵循稳健性原则{#follow-the-robustness-principle}

健壮性原则指出，我们应该在所发送的内容上保持保守，但在我们接受的内容上保持自由。 换句话说，在向第三方发送消息时，我们应该完全符合规范，但是在从第三方接收消息时，只要消息的含义明确，就应该接受不符的消息。

### 在其自己的模块中实施尖峰{#implement-spikes-in-their-own-modules}

尖峰和测试代码是任何灵活软件实施的一个组成部分，但我们希望确保它们在没有适当监督级别的情况下无法进入我们的生产代码库。 因此，建议在其自己的模块中创建峰值。

### 在其自己的模块{#implement-data-migration-scripts-in-their-own-module}中实施数据迁移脚本

虽然生产代码为数据迁移脚本，但通常只在网站首次启动时运行一次。 因此，一旦站点启动，就会变为无效代码。 为确保我们不会构建依赖于迁移脚本的实施代码，应在其自己的模块中实施这些代码。 这还允许我们在启动后立即删除并停用此代码，从而消除系统中的死代码。

### 在POM文件{#follow-published-maven-conventions-in-pom-files}中遵循已发布的Maven约定

Apache已在[https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html)发布了样式约定。 最好遵循这些惯例，因为这样可以更轻松地使新资源快速上线。
