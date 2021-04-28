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
translation-type: tm+mt
source-git-commit: 423e17dadf2e506eb68b37851dde5e68ed950866
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---

# 软件架构{#software-architecture}

## 为{#design-for-upgrades}升级而设计

扩展OOTB行为时，务必牢记升级。 始终在/apps目录中应用自定义，或者在/libs目录中相应节点的顶部应用叠加，或者使用sling:resourceSuperType扩展开箱即用行为。 虽然可能需要进行一些修改以支持新的AEM版本，但如果遵循此做法，则新版本不应覆盖您的自定义。

### 尽可能{#reuse-template-and-components-when-possible}重用模板和组件

这样，站点就能保持更一致的外观，并简化代码维护。 当需要新模板时，请确保从共享基模板扩展，以便全局要求（如clientlib inclusion）可以在一个位置进行编码。 当需要新组件时，寻找从现有组件扩展的机会。

### 设计模板设计{#design-template-designs}

通过定义可包括在页面上每个parsys中的组件，可以控制站点外观的一致性。 通过限制对页面上设计的访问，可允许“超级作者”在确保其他作者遵守公司标准的同时，在不进行开发人员干预的情况下修改每页允许的组件。

### 开发SOLID体系结构{#develop-a-solid-architecture}

SOLID是一个缩略词，描述了应该遵循的五个架构原则：

* **单**&#x200B;责任原则 — 每个模块、类、方法等应仅承担一项责任。
* **开**&#x200B;放/关闭原则 — 模块应打开以扩展，关闭以修改。
* **利**&#x200B;斯科夫替代原则 — 类型应由其子类型可替换。
* **接**&#x200B;口隔离原则 — 不应强制任何客户端依赖其不使用的方法。
* **依**&#x200B;赖性反演原则 — 高级模块不应依赖低级模块。两者都应取决于抽象。 抽象不应取决于细节。 细节应取决于抽象。

努力遵守这五项原则，应导致一个严格分离关切的制度。

>[!TIP]
>
>SOLID是面向对象编程中常用的概念，各个元素在工业文献中都得到了广泛的讨论。
>
>这只是一个简短的摘要，旨在提高认识，我们鼓励您更深入地熟悉这些概念。

### 遵循稳健性原理{#follow-the-robustness-principle}

健壮性原则规定，我们应该在所发送的内容上保持保守，但在我们接受的内容上保持自由。 换句话说，在向第三方发送消息时，我们应完全符合规范，但是当从第三方接收消息时，只要消息的含义明确，我们就应该接受不符的消息。

### 在自己的模块{#implement-spikes-in-their-own-modules}中实现尖峰

尖峰和测试代码是任何Agile软件实施的一个组成部分，但我们希望确保它们在没有适当监督级别的情况下无法进入我们的生产代码库。 因此，建议在自己的模块中创建尖峰。

### 在自己的模块{#implement-data-migration-scripts-in-their-own-module}中实现数据迁移脚本

虽然生产代码，但数据迁移脚本通常在站点初始启动时只运行一次。 因此，一旦站点生效，它就变成死代码。 为了确保我们不构建依赖于迁移脚本的实施代码，应在其自己的模块中实现这些代码。 这还允许我们在启动后立即删除并停用此代码，从系统中消除死代码。

### 在POM文件{#follow-published-maven-conventions-in-pom-files}中遵循已发布的Maven约定

Apache已在[https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html)发布了样式约定。 最好遵循这些惯例，因为这样可以更轻松地使新资源快速上手。
