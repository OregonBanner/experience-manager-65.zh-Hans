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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---


# 软件架构{#software-architecture}

## 升级设计{#design-for-upgrades}

在扩展OOTB行为时，请务必牢记升级。 始终在/apps目录中应用自定义，或者在/libs目录中相应节点的顶部进行叠加，或者使用sling:resourceSuperType扩展开箱即用行为。 虽然可能需要进行一些修改以支持新的AEM版本，但如果遵循此惯例，则新版本不应覆盖您的自定义设置。

### 尽可能{#reuse-template-and-components-when-possible}重用模板和组件

这将使站点保持更一致的外观并简化代码维护。 当需要新模板时，请确保从共享的基本模板进行扩展，以便能够在一个位置编码全局要求，如clientlib inclusion。 当需要新组件时，请寻找从现有组件扩展的机会。

### 设计模板设计{#design-template-designs}

通过定义哪些组件可以包括在页面上的每个parsys中，可以控制站点的外观的一致性。 通过限制对页面上设计的访问，“超级作者”可以允许在无需开发人员干预的情况下修改每页允许的组件，同时确保其他作者遵循公司标准。

### 开发SOLID体系结构{#develop-a-solid-architecture}

SOLID是一个缩略语，描述了应当遵循的五项建筑原则：

* **单**&#x200B;责任原则——每个模块、类、方法等只应做一件事。
* **开**&#x200B;放／关闭原则——模块应打开以进行扩展，关闭以进行修改。
* **利**&#x200B;斯科夫替换原则——类型应由其子类型替换。
* **接**&#x200B;口隔离原则——不应强制任何客户端依赖于它不使用的方法。
* **依**&#x200B;赖性反演原则——高级模块不应依赖低级模块。二者都应取决于抽象。 摘要不应取决于详细信息。 详细信息应取决于抽象。

努力遵循这五项原则，应当形成一种严格分开的制度。

### 遵循稳健性原理{#follow-the-robustness-principle}

健壮性原则指出，我们所发送的内容应该保守，但接受的内容应该保持自由。 换句话说，在向第三方发送消息时，我们应该完全符合规范，但在从第三方接收消息时，只要消息的含义明确，就应该接受不一致的消息。

### 在其自己的模块{#implement-spikes-in-their-own-modules}中实现尖峰

尖峰和测试代码是任何Agile软件实施的一个组成部分，但我们希望确保它们在没有适当监督级别的情况下无法进入我们的生产代码库。 因此，建议在自己的模块中创建尖峰。

### 在自己的模块{#implement-data-migration-scripts-in-their-own-module}中实现数据迁移脚本

虽然生产代码，但数据迁移脚本通常在站点初始启动时只运行一次。 因此，一旦站点生效，它就变成无效代码。 为了确保我们不构建依赖迁移脚本的实施代码，应在自己的模块中实现这些代码。 这还允许我们在启动后立即删除并停用此代码，从系统中消除死代码。

### 在POM文件{#follow-published-maven-conventions-in-pom-files}中遵循已发布的Maven约定

Apache已在[https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html)发布了样式约定。 最好遵循这些惯例，因为这样可以更轻松地使新资源快速上手。
