---
title: 自定义草稿和提交数据服务
seo-title: 自定义草稿和提交数据服务
description: AEM Forms，默认情况下，将草稿和提交的自适应表单存储在Publish实例的默认节点中。 但是，您可以配置AEM Forms的草稿和提交数据服务，以自定义草稿和提交的自适应表单的存储。
seo-description: AEM Forms，默认情况下，将草稿和提交的自适应表单存储在Publish实例的默认节点中。 但是，您可以配置AEM Forms的草稿和提交数据服务，以自定义草稿和提交的自适应表单的存储。
uuid: c3ec1708-3b11-4142-93f0-1cffb6643f34
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 602fd6a9-9a65-411c-8475-a4082a3fdee0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---


# 自定义草稿和提交数据服务{#customizing-draft-and-submission-data-services}

## 概述 {#overview}

AEM Forms允许用户将自适应表单另存为草稿。 草稿功能为用户提供了维护在制品表单的选项。 用户随后可以从任何设备随时填写和提交表单。

默认情况下，AEM Forms将与草稿和提交关联的用户数据存储在`/content/forms/fp`节点的Publish实例中。

但是，AEM Forms门户组件提供数据服务，允许您自定义为草稿和提交内容存储用户数据的实施。 例如，可以将数据存储在组织中当前实施的数据存储中。

要自定义用户数据的存储，您需要实施[Draft Data](/help/forms/using/custom-draft-submission-data-services.md#p-draft-data-service-p)和[ Submission Data](/help/forms/using/custom-draft-submission-data-services.md#p-submission-data-service-p)服务。

## 前提条件 {#prerequisites}

* 启用[Forms门户组件](/help/forms/using/enabling-forms-portal-components.md)
* 创建[表单门户页面](/help/forms/using/creating-form-portal-page.md)
* 为表单门户启用[自适应表单](/help/forms/using/draft-submission-component.md)
* 了解自定义存储的[实现详细信息](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## 草稿数据服务{#draft-data-service}

要自定义用户草拟数据的存储，您需要为`DraftAFDataService`接口的所有方法提供实现。

接口的以下代码示例提供了方法及其参数的说明：

```java
public interface DraftAFDataService {

 /**
  * Deletes the user data stored against the ID passed as the argument
  *
  * @param draftDataID
  * @return status for the just occurred delete draft UserData operation
  * @throws FormsPortalException
  */
 public Boolean deleteAFDraftUserData (String draftDataID) throws FormsPortalException;

 /**
  * Saves user data provided in the argument map
  *
  * @param draftUserDataMap contains Form Data (key - "guideState"), Adaptive Form Name (Key - "guideName"), and Draft DataID (Key - "userDataID") in case of update
  * @return userData ID would be returned which needs to be saved in metadata node
  * @throws FormsPortalException
  */
 public String saveAFUserData (Map<String, Object> draftUserDataMap) throws FormsPortalException;

 /**
  * Gets the user data stored against the ID passed as the argument
  *
  * @param Draft DataID
  * @return guideState (which would then be populated in adaptive form to reload the draft) which is stored against draftDataID
  * @throws FormsPortalException
  */
 public byte[] getAFDraftUserData(String draftDataID) throws FormsPortalException;

 /**
  * Saves the attachments for current adaptive form instance
  *
  * @param attachmentsBytes would expect byte array of the attachment to be saved
  * @return id for the attachment just saved (so that it could be retrieved later)
  * @throws FormsPortalException
  */
 public String saveAttachments(byte[] attachmentBytes) throws FormsPortalException;
}
```

## 提交数据服务{#submission-data-service}

要自定义用户提交数据的存储，您需要为`SubmittedAFDataService`接口的所有方法提供实现。

接口的以下代码示例提供了方法及其参数的说明：

```java
public interface SubmittedAFDataService {

 /**
  * Submits the user data passed in argument map
  *
  * @param submittedAFUserdataMap contains Form Data (key - "guideState"), Adaptive Form Name (Key - "guideName"), and Draft DataID (Key - "userDataID")
  * @return userData ID is returned that needs to be saved in the metadata node
  * @throws FormsPortalException
  */
 public String submitAFUserData (Map<String, Object> submittedAFUserdataMap) throws FormsPortalException;

 /**
  * Gets the user data stored against the ID passed as argument
  *
  * @param submitDataID
  * @return guideState which would be used to open DOR
  * @throws FormsPortalException
  */
 public byte[] getSubmittedAFUSerData(String submitDataID) throws FormsPortalException;

 /**
  * Deletes user data stored against the ID passed as argument
  *
  * @param Submit DataID
  * @return status of the delete operation on Submitted User data
  * @throws FormsPortalException
  */

 public Boolean deleteSubmittedAFUserData(String submitDataID) throws FormsPortalException;

 /**
  * Submits the attachment bytes passed as argument
  *
  * @param attachmentsBytes would expect byte array of the attachment to be saved
  * @return id for the attachment just saved (so that it could be retrieved later)
  * @throws FormsPortalException
  */
 public String submitAttachments(Object attachmentBytes) throws FormsPortalException;

}
```

