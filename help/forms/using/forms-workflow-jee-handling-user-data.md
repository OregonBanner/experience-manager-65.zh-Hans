---
title: Forms JEE工作流程 |處理使用者資料
seo-title: Forms JEE workflows | Handling user data
description: Forms JEE工作流程 |處理使用者資料
uuid: 3b06ef19-d3c4-411e-9530-2c5d2159b559
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5632a8df-a827-4e38-beaa-18b61c2208a3
role: Admin
exl-id: 847fa303-8d1e-4a17-b90d-5f9da5ca2d77
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 0%

---

# Forms JEE工作流程 |處理使用者資料 {#forms-jee-workflows-handling-user-data}

AEM Forms JEE工作流程提供設計、建立和管理業務流程的工具。 工作流程處理包含一系列以指定順序執行的步驟。 每個步驟都會執行特定動作，例如將任務指派給使用者或傳送電子郵件訊息。 程式可以與資產、使用者帳戶和服務互動，並且可以使用以下任何方法觸發：

* 從AEM Forms工作區啟動程式
* 使用SOAP或RESTful服務
* 提交最適化表單
* 使用watched資料夾
* 使用電子郵件

如需建立AEM Forms JEE工作流程程式的詳細資訊，請參閱 [Workbench說明](https://www.adobe.com/go/learn_aemforms_workbench_65).

## 使用者資料和資料存放區 {#user-data-and-data-stores}

當流程被觸發並且進行時，它會擷取流程參與者的相關資料、參與者在與流程相關的表單中輸入的資料，以及新增至表單的附件。 資料會儲存在AEM Forms JEE伺服器資料庫中，而如已設定，部分資料（如附件）會儲存在全域檔案儲存(GDS)目錄中。 GDS目錄可以在共用檔案系統或資料庫上設定。

## 存取和刪除使用者資料 {#access-and-delete-user-data}

觸發程式時，系統會產生唯一的程式執行個體ID和長效的叫用ID，並與程式執行個體建立關聯。 您可以根據長效的叫用ID來存取和刪除程式執行個體的資料。 您可以使用已提交其任務的程式發起人或程式參與者的使用者名稱，來推斷程式執行個體的長期叫用ID。

不過，在下列情況下，您無法識別初始器的處理序執行個體ID：

* **透過watched資料夾觸發的程式**：如果程式是由watched資料夾觸發，則無法使用程式執行個體的啟動器來識別該程式執行個體。 在此情況下，使用者資訊會編碼在儲存的資料中。
* **從發佈AEM執行個體開始的流程**：所有從AEM發佈執行個體觸發的流程執行個體都不會擷取關於初始器的資訊。 不過，使用者資料可能會以與程式相關聯的表單擷取，並儲存在工作流程變數中。
* **透過電子郵件起始的程式**：寄件者的電子郵件ID會擷取為的不透明blob欄中的屬性， `tb_job_instance` 無法直接查詢的資料庫表格。

### 在已知工作流程發起人或參與者時識別流程執行個體ID {#initiator-participant}

執行以下步驟來識別工作流程發起人或參與者的程式執行處理ID：

1. 在AEM Forms伺服器資料庫中執行以下命令，以從擷取工作流程發起人或參與者的主體ID `edcprincipalentity` 資料庫表格。

   ```sql
   select id from edcprincipalentity where canonicalname='user_ID'
   ```

   查詢會傳回指定之主體ID `user_ID`.

1. (**對於工作流程發起人**)執行以下命令，從擷取與初始器的主體ID相關聯的所有任務 `tb_task` 資料庫表格。

   ```sql
   select * from tb_task where start_task = 1 and create_user_id= 'initiator_principal_id'
   ```

   查詢會傳回由指定的所起始的任務 `initiator`_ `principal_id`. 任務分為兩種型別：

   * **已完成任務**：這些工作已提交，並在下列位置顯示英數字元： `process_instance_id` 欄位。 記下已提交任務的所有程式執行個體ID，並繼續這些步驟。
   * **已起始但未完成的工作**：這些任務已開始，但尚未提交。 中的值 `process_instance_id` 這些任務的欄位是 **0** （零）。 在此情況下，請記下對應的任務ID並參閱 [處理孤立任務](#orphan).

1. (**對於工作流程參與者**)執行以下命令，從擷取與啟動器之程式參與者的主體識別碼相關聯的程式執行個體ID `tb_assignment` 資料庫表格。

   ```sql
   select distinct a.process_instance_id from tb_assignment a join tb_queue q on a.queue_id = q.id where q.workflow_user_id='participant_principal_id'
   ```

   查詢會傳回與參與者相關聯的所有處理序的執行個體ID，包括參與者尚未提交任何任務的那些處理序。

   記下已提交任務的所有程式執行個體ID，並繼續這些步驟。

   對於孤立任務或任務，如果 `process_instance_id` 為0 （零），記下對應的任務ID並檢視 [處理孤立任務](#orphan).

1. 請依照下列說明操作： [根據流程執行個體ID從工作流程執行個體中清除使用者資料](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) 區段來刪除已識別程式執行個體ID的使用者資料。

### 當使用者資料儲存在基本變數中時，識別程式執行個體ID {#primitive}

可將工作流程設計為擷取使用者資料於變數中，並將該變數儲存為資料庫中的blob。 在這種情況下，只有當使用者資料儲存在下列其中一個基本型別變數中時，才能查詢使用者資料：

* **字串**：直接包含使用者ID或作為子字串包含，且可使用SQL查詢。
* **數值**：直接包含使用者ID。
* **XML**：包含使用者ID，作為儲存為資料庫中文字欄的文字中的子字串，並可像字串一樣進行查詢。

執行以下步驟，判斷以基本型別變數儲存資料的工作流程是否包含使用者的資料：

1. 執行以下資料庫命令：

   ```sql
   select database_table from omd_object_type where name='pt_<app_name>/<workflow_name>'
   ```

   查詢會傳回表格名稱，位於 `tb_<number>` 指定應用程式的格式( `app_name`)和工作流程( `workflow_name`)。

   >[!NOTE]
   >
   >的值 `name` 如果工作流程巢狀內嵌於應用程式內的子資料夾中，屬性可能會很複雜。 請務必指定工作流程的完整路徑，此路徑可從 `omd_object_type` 資料庫表格。

1. 檢閱 `tb_<number>` 資料表結構描述。 此表格包含儲存指定工作流程之使用者資料的變數。 表格中的變數會與工作流程中的變數相對應。

   識別並記下與包含使用者ID的工作流程變數相對應的變數。 如果識別的變數屬於基本型別，您可以執行查詢來判斷與使用者ID相關聯的工作流程例項。

1. 執行以下資料庫命令。 在此命令中， `user_var` 是包含使用者ID的基本型別變數。

   ```sql
   select process_instance_id from <tb_name> where <user_var>=<user_ID>
   ```

   查詢會傳回與指定的關聯的所有處理序執行個體ID `user_ID`.

1. 請依照下列說明操作： [根據流程執行個體ID從工作流程執行個體中清除使用者資料](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) 區段來刪除已識別程式執行個體ID的使用者資料。

### 根據流程執行個體ID從工作流程執行個體中清除使用者資料 {#purge}

現在您已識別與使用者相關聯的程式執行個體ID，請執行以下動作以從個別程式執行個體中刪除使用者資料。

1. 執行以下命令，從擷取處理序執行個體的長效啟動ID和狀態 `tb_process_instance` 表格。

   ```sql
   select long_lived_invocation_id, status from tb_process_instance where id='process_instance_id'
   ```

   查詢會傳回指定之長期引動識別碼和狀態 `process_instance_id`.

1. 建立公開的執行個體 `ProcessManager` 使用者端( `com.adobe.idp.workflow.client.ProcessManager`)使用 `ServiceClientFactory` 具有正確連線設定的執行個體。

   如需詳細資訊，請參閱Java API參考資料，以瞭解 [類別程式管理員](https://helpx.adobe.com/experience-manager/6-3/forms/ProgramLC/javadoc/com/adobe/idp/workflow/client/ProcessManager.html).

1. 檢查工作流程例項的狀態。 如果狀態不是2 (COMPLETE)或4 (TERMINATED)，請先呼叫下列方法來終止執行處理：

   `ProcessManager.terminateProcess(<long_lived_invocation_id>)`。

1. 呼叫下列方法以清除工作流程執行個體：

   `ProcessManager.purgeProcessInstance(<long_lived_invocation_id>)`

   此 `purgeProcessInstance` 方法會從AEM Forms伺服器資料庫和GDS （若已設定）中完全刪除指定叫用ID的所有資料。

### 處理孤立任務 {#orphan}

孤立任務是指其容納流程已啟動但尚未提交的任務。 在此案例中， `process_instance_id` 是 **0** （零）。 因此，您無法使用程式執行個體ID來追蹤為孤立任務儲存的使用者資料。 不過，您可以使用孤立任務的工作ID來追蹤它。 您可以透過以下連結識別任務ID： `tb_task` 使用者的表格（如所述） [在已知工作流程發起人或參與者時識別流程執行個體ID](/help/forms/using/forms-workflow-jee-handling-user-data.md#initiator-participant).

取得工作ID後，請執行以下動作，從GDS和資料庫中清除具有孤立工作的相關檔案和資料。

1. 在AEM Forms伺服器資料庫上執行以下命令，以擷取已識別工作ID的ID。

   ```sql
   select id from tb_form_data where task_id=<task_id>
   ```

   查詢會傳回ID清單。 對於每個ID ( `fd_id`)，建立工作階段ID字串的清單，如下所示：

   * _ `wfattach<task_id>`
   * `_wftask<fd_id>`
   * `_wftaskformid<fd_id>`

1. 根據您的GDS指向檔案系統或資料庫，請執行下列步驟之一：

   1. **檔案系統中的GDS**

      在GDS檔案系統中：

      1. 搜尋副檔名為下列工作階段ID字串的檔案：
      * `_wfattach<task_id>`
      * `_wftask<fd_id>`
      * `_wftaskformid<fd_id>`

      具有這些副檔名的檔案是標籤檔案。 檔案名稱會以下列格式儲存：

      `<file_name_guid>.session<session_id_string>`

      1. 刪除所有標籤檔案和其他檔案，檔案名稱完全符合 `<file_name_guid>` 從檔案系統。
   1. **資料庫中的GDS**

      針對每個工作階段ID執行以下命令：

      ```sql
      delete from tb_dm_chunk where documentid in (select documentid from tb_dm_session_reference where sessionid=<session_id>)
      delete from tb_dm_session_reference where sessionid=<session_id>
      delete from tb_dm_deletion where sessionid=<session_id>
      ```




1. 執行以下命令，從AEM Forms伺服器資料庫刪除工作ID的資料：

   ```sql
   delete from tb_task_acl where task_id=<task_id>
   delete from tb_task_attachment where task_id=<task_id>
   delete from tb_form_data where task_id=<task_id>
   delete from tb_assignment where task_id=<task_id>
   delete from tb_task where id=<task_id>
   ```
