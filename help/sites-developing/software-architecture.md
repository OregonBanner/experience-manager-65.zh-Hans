---
title: 软件体系结构
seo-title: Software Architecture
description: 构建软件的最佳实践
seo-description: Best practices for architecting your software
uuid: a557f6ca-c3f1-486e-a45e-6e1f986fab41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 92971747-1c74-4917-b5a0-7b79b3ae1e68
exl-id: cd4f3b4c-5488-4ca7-9c1e-b4c819fda8e8
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# 软件体系结构{#software-architecture}

## 针对升级进行设计 {#design-for-upgrades}

扩展OOTB行为时，请务必牢记升级。 始终应用/apps目录中的自定义项，并叠加到/libs目录中的相应节点顶部，或使用sling：resourceSuperType扩展开箱即用行为。 虽然可能需要进行一些修改才能支持新的AEM版本，但是如果遵循此实践，则新版本不应覆盖您的自定义设置。

### 尽可能重用模板和组件 {#reuse-template-and-components-when-possible}

这将使站点能够保持更一致的外观，并简化代码维护。 当需要新模板时，请确保从共享基础模板扩展，以便可以在一个位置对clientlib包含等全局要求进行编码。 当需要新组件时，寻找从现有组件扩展的机会。

### 设计模板设计 {#design-template-designs}

通过定义页面上每个parsys中可包含的组件，可以控制站点外观/感觉的一致性。 通过在页面上限制对设计的访问，可以允许“超级作者”修改每页允许的组件，而无需开发人员干预，同时确保其他作者遵循企业标准。

### 开发SOLID体系结构 {#develop-a-solid-architecture}

SOLID是描述应遵循的五个体系结构原则的缩写：

* **S**&#x200B;单一责任原则 — 每个模块、类、方法等只能有一个责任。
* **O**&#x200B;钢笔/封闭式原则 — 模块应开放进行扩展，封闭进行修改。
* **L** iskov替换原理 — 类型应该由其子类型替换。
* **I**&#x200B;接口分隔原则 — 不应强制任何客户端依赖它未使用的方法。
* **D**&#x200B;依赖性反转原理 — 高层模块不应依赖低层模块。 两者都应该依靠抽象。 抽象不应依赖于细节。 细节应取决于抽象概念。

努力遵守这五项原则应导致一种严格区分各种关切的制度。

>[!TIP]
>
>SOLID是面向对象编程中常用的概念，在工业文献中广泛讨论了它的各个元素。
>
>这只是为便于了解而提供的简短摘要，鼓励您更深入地了解这些概念。

### 遵循鲁棒性原则 {#follow-the-robustness-principle}

稳健性原则指出我们对于所发送的内容应保持保守，但在所接受的内容上应保持自由。 换句话说，向第三方发送消息时，我们应完全符合规范，但在接收来自第三方的消息时，我们应接受不符合规范的消息，只要该消息的含义是明确的。

### 在自己的模块中实施峰值 {#implement-spikes-in-their-own-modules}

尖峰和测试代码是任何Agile软件实施中不可或缺的一部分，但我们希望确保它们在没有适当监督的情况下不会进入我们的生产代码库。 因此，建议在其自身的模块中创建峰值。

### 在其自己的模块中实施数据迁移脚本 {#implement-data-migration-scripts-in-their-own-module}

数据迁移脚本虽然是生产代码，但通常在网站的初始启动时只运行一次。 因此，只要站点处于活动状态，它就会成为死代码。 为了确保我们不构建依赖于迁移脚本的实施代码，应该在它们自己的模块中实施它们。 这还允许我们在启动后立即删除并停用此代码，从而消除系统中的死代码。

### 遵循POM文件中发布的Maven惯例 {#follow-published-maven-conventions-in-pom-files}

Apache已在以下位置发布样式约定 [https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html). 最好遵循这些惯例，因为这将使新资源更容易快速上手。
