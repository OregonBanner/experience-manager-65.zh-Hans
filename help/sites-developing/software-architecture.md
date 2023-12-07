---
title: 软件体系结构
description: 了解为Adobe Experience Manager构建软件的一些最佳实践。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: cd4f3b4c-5488-4ca7-9c1e-b4c819fda8e8
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---

# 软件体系结构{#software-architecture}

## 针对升级进行设计 {#design-for-upgrades}

扩展OOTB行为时，请务必牢记升级。 始终应用/apps目录中的自定义项，并叠加到/libs目录中的相应节点顶部，或使用sling：resourceSuperType扩展开箱即用的行为。 虽然可能需要进行一些修改才能支持新的AEM版本，但如果遵循此实践，则新版本不应覆盖您的自定义设置。

### 尽可能重用模板和组件 {#reuse-template-and-components-when-possible}

这样做可以使站点保持更加一致的外观，并简化代码维护。 当需要新模板时，请确保从共享的基本模板扩展，以便可以在一个位置对clientlib包含等全局要求进行编码。 当需要新组件时，寻找从现有组件扩展的机会。

### 设计模板设计 {#design-template-designs}

通过定义页面上每个parsys中可包含的组件，可以控制站点外观/感觉的一致性。 通过在页面上限制对设计的访问，可以允许“超级作者”修改每页允许的组件，而无需开发人员干预，同时确保其他作者遵循企业标准。

### 开发SOLID体系结构 {#develop-a-solid-architecture}

SOLID是描述应遵循的五个体系结构原则的缩写：

* **S**&#x200B;单一责任原则 — 每个模块、类、方法等只能有一个责任。
* **O**&#x200B;钢笔/闭合原理 — 模块应该打开进行扩展，并且关闭进行修改。
* **L** iskov替换原则 — 类型应该由其子类型替换。
* **I**&#x200B;接口隔离原则 — 不应强制任何客户依赖其不使用的方法。
* **D**&#x200B;依赖性反转原理 — 高层模块不应依赖低层模块。 两者都应该依靠抽象。 抽象不应依赖于细节。 细节应取决于抽象。

努力遵守这五项原则应导致一种严格区分关切的制度。

>[!TIP]
>
>SOLID是面向对象编程中常用的概念，在工业文献中广泛讨论了它的各个元素。
>
>此信息只是为了便于了解而提供的简短摘要，建议您更深入地了解这些概念。

### 遵循鲁棒性原则 {#follow-the-robustness-principle}

“稳健性原则”规定，对于发送的内容，您应保持保守，但在接受的内容上应保持自由。 换言之，在将消息发送给第三方时，您应完全符合规范。 但是，当您收到来自第三方的消息时，只要该消息的含义明确，您就应该接受不符合规则的消息。

### 在其自己的模块中实施峰值 {#implement-spikes-in-their-own-modules}

尖峰和测试代码是任何Agile软件实施的一部分。 但是，您需要确保在没有适当级别的监督的情况下，他们不会进入生产代码库。 因此，建议在其自身的模块中创建峰值。

### 在其自己的模块中实施数据迁移脚本 {#implement-data-migration-scripts-in-their-own-module}

数据迁移脚本虽然是生产代码，但在首次启动站点时只运行一次。 因此，当站点处于实时状态时，脚本将变为无效代码。 要确保您不会生成依赖于迁移脚本的实施代码，应在其自己的模块中进行实施。 这样，我们可以在启动后立即删除并停用此代码，从而消除系统中的死代码。

### 遵循POM文件中发布的Maven惯例 {#follow-published-maven-conventions-in-pom-files}

Apache已在以下位置发布样式约定： [https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html). 最好遵循这些惯例，因为这样可以更轻松地使新资源快速上线。
