---
title: 组织您的数字资产
description: 使用Experience Manager整理您的数字资产、图像、文件、文件夹等。
contentOwner: AG
translation-type: tm+mt
source-git-commit: abc4821ec3720969bf1c2fb068744c07477aca46

---


# 组织您的数字资产 {#organize-digital-assets}

Microsoft Office和PDF文档的所有数字资产、元数据和内容都会被提取并变得可搜索。 搜索功能允许对资产进行复杂的筛选，并完全尊重正确的权限。 数字资产管理中的元数据中详细介绍了元数据。

AEM资产支持多种组织内容的方式。 您可以使用文件夹以分层方式组织它们，或者使用示例标记以无序的临时方式组织它们。 用户可以在显示子资产、演绎版和元数据的DAM资产编辑器中编辑标记。

## 在文件夹中组织资产 {#organize-using-folders}

组织资产的最基本方法是将这些资产保存到文件夹中。 它类似于组织本地文件系统中文件夹中的文件。 有关如何创建和管理文件夹的详细信息，请参阅管 [理资产](managing-assets-touch-ui.md)。 对文件和文件夹的命名方式、对子文件夹的排列方式以及处理这些文件夹中的文件的方式可能会对这些资产的处理方式产生重大影响。 通过使用一致、适当的文件和文件夹命名策略以及良好的元数据实践，您可以充分利用数字资产存储库。

* 在大多数情况下，您的数字资产存储库始终在增长。 因此，在内容创建周期的早期，务必将元数据的使用、文件夹结构和文件命名规范化。
* 仅使用文件夹为数字资产强制实施一致的存储结构。 这种一致性有助于您更好地处理和管理资产。 例如，放置在以下类型文件夹中的资产可以帮助您使用相 [应的用户档案处理资产](processing-profiles.md):

   * **开发文件夹**:包含您当前正在处理的数字资产。
   * **客户端文件夹**:包含基于客户或项目名称的数字资产。
   * **主文件夹**:包含原始的源数字资源。
   * **再现文件夹**:包含原始源数字资产的演绎版和副本。
   * **文件大小文件夹**:包含基于小、中或大文件大小的数字资产。
   * **暂存文件夹**:包含已准备好在您的网站上实时发布的数字资产。
   * **MIME类型文件夹**:包含特定于图像、文档和多媒体等MIME类型的数字资产。
   * **存档文件夹**:包含已弃用的数字资产。
   * **基于日期的文件夹**:包含基于创建日期或上次修改日期的数字资产。

* 创建不可能更改的文件夹目录，以便继续进行任何自定义或自动化操作。 例如，分配的处理用户档案将继续工作。
* If an asset is already published, then you use AEM to move the asset to another folder, and re-publish from its new location, the original published asset location is still available, along with the newly re-published asset. The original published asset, however, is *lost* to AEM and cannot be unpublished. 因此，作为最佳实践，首先取消发布资产，然后将其移至其他文件夹。

## 使用标记组织资产 {#use-tags-to-organize-assets}

使用标记作为元数据，您可以轻松搜索资产、使用搜索结果创建集合、提升某些资产的搜索排名并利用Adobe Sensei的AI算法进行资产发现。

Adobe Experience Manager Assets使用自学算法创建高度描述性的标记，只需单击几下即可找到正确的资产。 智能标记使用Adobe Sensei（我们的人工智能和机器学习框架），该框架经过培训，可识别标准标记和业务特定标记并将其应用于图像。 智能标记还可以识别内容、单个单词或短语，并自动将描述性标记应用于资产

有关详细信息，请参阅以下文章：

* [关于AEM中的标记](/help/sites-authoring/tags.md)
* [编辑资产元数据](meta-edit.md)
* [资产中增强的智能标记](enhanced-smart-tags.md)

## 组织为集合 {#organize-as-collections}

借助Experience Manager资产中的资产收藏集，您可以简化在用户之间创建、编辑和共享资产的功能。 根据您使用收藏集的方式创建多种类型的收藏集，包括包含资产、文件夹和收藏集的静态引用列表的收藏集，以及根据搜索条件拉入资产的收藏集。  您还可以使用不同位置的资产创建收藏集，并与具有不同访问、查看和编辑权限级别的多个用户共享这些收藏集。

有关详细信息，请参阅管 [理集合](managing-collections-touch-ui.md)

<!-- TBD items: add screenshots where applicable
Any hints/recommendations of when to use what method of organizing? Some examples of how organizing helps towards a better taxonomy and improved content velocity.
Add back links to blog posts by marketing?
-->

## 组织资源以使用用户档案 {#organize-to-use-profiles}

处理用户档案包含资产处理命令，这些命令适用于上传到预定义文件夹的资产。 用户档案用于自动处理文件夹或新上传的资产的内容。 您可以利用用户档案更好地组织资产。

实现元数据使用、文件命名和文件夹结构标准化可确保随着数字资产池的增长，您可以更精确地将处理用户档案应用于文件夹并保持一致性。

有关可创建和管理以处理资产的各种用户档案的详细信息，请参阅

* [用户档案处理元数据、图像和视频](processing-profiles.md)
* [元数据配置文件](metadata-profiles.md)
* [视频配置文件](video-profiles.md)
* [Dynamic Media图像用户档案](image-profiles.md)
