---
title: 工作流步骤参考
seo-title: 工作流步骤参考
description: 'null'
seo-description: 'null'
uuid: 88bf6997-73a1-4639-82aa-5dff08d3ef86
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e3afffd0-d90c-4bd0-b814-f7aeac6ceb6d
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# 工作流步骤参考 {#workflow-step-reference}

工作流模型由一系列不同类型的步骤组成。 根据类型，可以使用参数和脚本配置和扩展这些步骤，以提供所需的功能和控制。

>[!NOTE]
>
>此部分涵盖标准工作流步骤。
>
>有关模块的特定步骤，另请参阅：
>
>* [AEM Forms Workflow步骤参考](/help/forms/using/aem-forms-workflow-step-reference.md)
>* [使用媒体处理程序和工作流处理资产](/help/assets/media-handlers.md)
>



## 步骤属性 {#step-properties}

每个步骤组件都有一个“ **步骤属性** ”对话框，通过该对话框可以定义和编辑所需的属性。

### 步骤属性——常用选项卡 {#step-properties-common-tab}

大多数工作流步骤组件都可使用以下属性组合，它位于属性对话框的“公 **用** ”选项卡上：

* **标题**&#x200B;步骤的标题。

* **说明**&#x200B;步骤的说明。

* **工作流暂存**

   一个下拉选择器，用于对 [步骤](/help/sites-developing/workflows.md#workflow-stages) 应用舞台。

* **超时**

   步骤将在其后“超时”的时间段。
您可以在以下两种方式中进行选择：关 **闭**，即时 **1h,** 16h, **** 12h, **24h**********,PhistimePh。

* **超时处理程序**

   在步骤超时时控制工作流的处理函数；例如：
   `Auto Advancer`

* **处理程序前进**

   选择此选项可将工作流自动推进到执行后的下一步。 如果未选择，则实施脚本必须处理工作流的进度。

### 步骤属性-“用户／用户组”选项卡 {#step-properties-user-group-tab}

属性对话框的“用户／组”选项卡上的许多工作流 **步骤组件都有以下属性** :

* **通过电子邮件通知用户**

   * 您可以在工作流到达步骤时向参加者发送电子邮件，以通知他们。
   * 如果启用，则将向属性“用户／用户组”定义的用户发送电子邮件，或向用户组的每个成员发送电子邮件(如果已定义用户组 **** )。

* **用户/组**

   * 下拉选择框将允许您导航和选择用户或用户组。
   * 如果您将步骤分配给特定用户，则只有此用户才能对该步骤执行操作。
   * 如果您将该步骤分配给整个组，则当工作流到达此步骤时，该组中的所有用户都将在其工作流收件箱中执行 **相应操作**。
   * 有关更 [多信息，请参阅](/help/sites-authoring/workflows-participating.md) “参与工作流”。

## AND 拆分 {#and-split}

“ **AND拆分** ”(AND Split)在工作流中创建一个拆分，之后两个分支都将处于活动状态。 您可以根据需要向每个分支添加工作流步骤。 通过此步骤，您可以在工作流中引入多个处理路径。 例如，您可以允许并行执行某些审阅步骤，从而节省时间。

![wf-26](assets/wf-26.png)

### 和拆分——配置 {#and-split-configuration}

配置拆分：

* 编辑 **AND拆分属性**:

   * **拆分名称**:为说明性目的指定名称
   * 选择所需的分支数量；2、3、4或5。

* 根据需要向分支添加工作流步骤。

   ![wf-27](assets/wf-27.png)

## 容器步骤 {#container-step}

容器步骤启动另一个作为子工作流执行的工作流模型。

此容器允许您重复使用工作流模型以实现常见的步骤序列。 例如，翻译工作流模型可用于多个编辑工作流。

![wf-28](assets/wf-28.png)

### 容器步骤——配置 {#container-step-configuration}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](#step-properties-common-tab)
* **容器**

   * **子工作流**:选择要启动的工作流。

## 跳转步骤 {#goto-step}

“转 **到步骤** ”(Goto Step)允许您指定要在工作流模型中执行的下一步。 可以指定规则定义、外部脚本或ECMA脚本作为路由表达式，以评估工作流模型的下一步。

* 如果您指定的条件保持为true，则跳转 **步骤将完成** ，工作流引擎将执行指定的步骤。
* 如果您指定的条件不保持为true，则跳转步骤将完成，而 **** 常规路由逻辑将确定要执行的下一步。

使用 **跳转步骤** ，您可以在工作流模型中实现高级路由结构。 例如，要实现循环，可以定义 **Goto步骤** ，以在工作流中执行前一步骤，路由表达式评估循环条件。

### 跳转步骤——配置 {#goto-step-configuration}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](#step-properties-common-tab)
* **进程**

   * **目标步骤**:在评估路由表达式的条件后选择要执行的步骤。
   * **路由表达式**:选择“规则定义”、“外部脚本”或确定是否执行目标步骤的ECMA **脚本**。

      * **** 规则定义：使用表达 [式编辑器](/help/forms/using/variable-in-aem-workflows.md#use-expression-editor) ，定义规则。
      * **** 外部脚本：外部脚本的路径。
      * **ECMA脚本**:确定是否执行跳转步骤 **的脚本**。

#### 模拟for循环 {#simulating-a-for-loop}

模拟for循环需要保持已发生循环迭代次数的计数：

* 计数通常表示工作流中执行操作的项目的索引。
* 该计数将作为循环的退出标准进行计算。

例如，要实现对多个JCR节点执行操作的工作流，可以使用循环计数器作为节点的索引。 要保留计数，请在工 `integer` 作流实例的数据映射中存储一个值。 使用跳转步 **骤的脚本** ，可增加计数并将计数与退出条件进行比较。

```
function check(){
   var count=0;
   var keyname="loopcount"
   try{
      if (workflowData.getMetaDataMap().containsKey(keyname)){
        log.info("goto script: found loopcount key");
        count= parseInt(workflowData.getMetaDataMap().get(keyname))+1;
      }

     workflowData.getMetaDataMap().put(keyname,count);

     }catch(err) {
         log.info(err.message);
         return false;
    }
   if (parseInt(count) <7){
       return true;
   } else {
      return false;
   }
}
```

### 使用规则定义模拟for循环 {#simulateforloop}

您还可以使用规则定义作为路由表达式模拟for循环。 [创建长 **数据类型**](/help/forms/using/variable-in-aem-workflows.md#create-a-variable) 的count变量。 在“ **设置变量****[”步骤中，将“计数变量”的值设置为“计数+1”，以](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable)**执行“设置变量步骤集”的每&#x200B;************个步骤时，“计数+1”的值。

![模拟for循环](assets/variable_use_case_count_new.png)

在跳转步 **骤中**，使用设 **置变量作为目标步** 骤计数 **，使****** 用计数&lt; 5的路由表达式。

![模拟for循环的条件](assets/variable_use_case_count1_new.png)

“设 **置变量** ”(Set Variable **** )步骤在每次执行时将count变量的值重复增加1，直到值达到5。

## OR 拆分 {#or-split}

“ **OR拆分** ”(OR Split)在工作流中创建拆分，之后只有一个分支处于活动状态。 通过此步骤，您可以将条件处理路径引入工作流中。 您可以根据需要向每个分支添加工作流步骤。

>[!NOTE]
>
>有关创建OR拆分的其他信息，请参阅： [https://helpx.adobe.com/experience-manager/using/aem64_workflow_servlet.html](https://helpx.adobe.com/experience-manager/using/aem64_workflow_servlet.html)

![使用OR拆分进行分支](assets/variables_orsplit_new.png)

### OR拆分——配置 {#or-split-configuration}

配置拆分：

* 编辑或 **拆分属性**:

   * **通用**

      * 指定拆分名称。
   * **分支(*x)***

      * **** 添加分支：为步骤添加更多分支。
      * **选择路由表达式**:选择路由表达式以计算活动分支。 可能的值包括：规则定义、外部脚本和ECMA脚本。
      * **单击以添加表达式**:如果选择规则定义作为路由表达式，则添加表达式 **以计算活动分支** 。
      * **脚本路径**:如果选择“外部脚本”作为路由表达式，则包含用于计算活动分支的脚本的 **文件的路径** 。
      * **脚本**:如果选择 **ECMA Script作为路由表达式，请在框中添加脚本以评估活动分支** 。
      * **默认路由**:如果有多个分支，则默认分支后面会跟随。 默认情况下只能指定一个分支。
   >[!NOTE]
   >
   >    * 根据路由表达式一次计算一个分支。
   >    * 将从上到下评估分支。
   >    * 执行计算结果为true的第一个脚本。
   >    * 如果没有分支的计算结果为true，则工作流不会前进。


   >[!NOTE]
   >
   >请参 [阅为OR拆分定义规则](/help/sites-developing/workflows-models.md#defineruleecmascript)。

* 根据需要向分支添加工作流步骤。

## 参加者步骤和选择器 {#participant-steps-and-choosers}

### 参与者步骤 {#participant-step}

“参 **加者步骤** ”允许您为特定操作分配所有权。 只有在用户手动确认该步骤后，该工作流才会继续。 当您希望某人对工作流执行操作时，会使用此功能；例如，审阅步骤。

虽然与用户不直接相关，但在分配操作时必须考虑用户授权；用户必须有权访问工作流有效负荷的页面。

#### 参加者步骤——配置 {#participant-step-configuration}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](#step-properties-common-tab)
* [用户/组](#step-properties-user-group-tab)

>[!NOTE]
>
>在以下情况下，始终会通知工作流发起者：
>
>* 工作流已完成（已完成）。
>* 工作流已中止（终止）。
>



>[!NOTE]
>
>需要配置某些属性才能启用电子邮件通知。 您还可以自定义电子邮件模板或为新语言添加电子邮件模板。 See [Configuring Email Notification](/help/sites-administering/notification.md#configuringemailnotification) to configure email notifications in AEM.

### 对话框参与者步骤 {#dialog-participant-step}

使用对 **话框参加者步骤** ，从分配了工作项的用户处收集信息。 此步骤对于收集稍后在工作流中使用的少量数据很有用。

完成该步骤后，“完 **成工作项** ”对话框将包含您在对话框中定义的字段。 在字段中收集的数据存储在工作流有效负荷的节点中。 随后的工作流步骤随后可以从存储库中读取值。

要配置该步骤，请指定要将工作项分配给的组或用户，以及对话框的路径。

#### 对话框参加者步骤——配置 {#dialog-participant-step-configuration}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](#step-properties-common-tab)
* [用户/组](#step-properties-user-group-tab)
* **对话框**

   * **对话框路径**:您创建的对话框的对话框节 [点的路径](#dialog-participant-step-creating-a-dialog)。

#### 对话框参加者步骤——创建对话框 {#dialog-participant-step-creating-a-dialog}

要创建对话框，您需要创建对话框：

* 确定结果数据将存储在有 [效负荷中的位置](#dialog-participant-step-storing-data-in-the-payload)。
* [定义对话框；这包括定义用于收集（和保存）数据的字段](#dialog-participant-step-dialog-definition)。

#### 对话框参加者步骤——在有效负荷中存储数据 {#dialog-participant-step-storing-data-in-the-payload}

您可以将构件数据存储在工作流有效负荷或工作项元数据中。 构件节点的 `name` 属性格式决定数据存储的位置。

* **使用有效负荷存储数据**

   * 要将构件数据存储为工作流有效负荷的属性，请对构件节点的name属性值使用以下格式：
      `./jcr:content/nodename`

   * 数据存储在有效负荷节 `nodename` 点的属性中。 如果节点不包含该属性，则创建该属性。
   * 当与有效负荷一起存储时，后续使用具有相同有效负荷的对话框会覆盖属性的值。

* **将数据与工作项一起存储**

   * 要将构件数据存储为工作项元数据的属性，请对name属性的值使用以下格式：
      `nodename`

   * 数据存储在工 `nodename` 作项的属性中 `metadata`。 如果随后与相同有效负荷一起使用的对话框，则保留数据。

#### 对话框参加者步骤——对话框定义 {#dialog-participant-step-dialog-definition}

1. **对话框结构**

   对话框参与者步骤的对话框与您为创作组件创建的对话框类似。 它们存储在：

   `/apps/myapp/workflow/dialogs`

   触屏优化UI的对话框具有以下节点结构：

   ```xml
   newComponent (cq:Component)
     |- cq:dialog (nt:unstructured)
       |- content
         |- layout
           |- items
             |- column
               |- items
                 |- component0
                 |- component1
                 |- ...
   ```

   >[!NOTE]
   >
   >有关详细信息，请 [参阅创建和配置对话框](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog)。

1. **对话框路径属性**

   对话 **框参加者步骤** ，具有“对 **话框路径** ”属性(以及参加者步骤 [的属性](#participant-step))。 “对话框路 **径** ”属性的值是对话框 `dialog` 节点的路径。

   例如，该对话框包含在存储在节点中名为 `EmailWatch` 的组件中：

   `/apps/myapp/workflows/dialogs`

   对于触屏优化UI,“对话框路径”属性使用 **以下值** :

   `/apps/myapp/workflow/dialogs/EmailWatch/cq:dialog`

   ![wf-30](assets/wf-30.png)

1. **示例对话框定义**

   以下XML代码片断表示一个对话框，该对话框将 `String` 值存储在有 `watchEmail` 效负荷内容的节点中。 标题节点表示 [TextField组件](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/textfield/index.html) :

   ```xml
   jcr:primaryType="nt:unstructured"
       jcr:title="Watcher Email Address Dialog"
       sling:resourceType="cq/gui/components/authoring/dialog">
       <content jcr:primaryType="nt:unstructured"
           sling:resourceType="granite/ui/components/foundation/container">
           <layout jcr:primaryType="nt:unstructured"
               margin="false"
               sling:resourceType="granite/ui/components/foundation/layouts/fixedcolumns"
           />
           <items jcr:primaryType="nt:unstructured">
               <column jcr:primaryType="nt:unstructured"
                   sling:resourceType="granite/ui/components/foundation/container">
                   <items jcr:primaryType="nt:unstructured">
                       <title jcr:primaryType="nt:unstructured"
                           fieldLabel="Notification Email Address"
                           name="./jcr:content/watchEmails"
                           sling:resourceType="granite/ui/components/foundation/form/textfield"
                       />
                   </items>
               </column>
           </items>
       </content>
   </cq:dialog>
   ```

   对于触屏优化UI，此示例将生成如下对话框：

   ![chlimage_1-70](assets/chlimage_1-70.png)

### 动态参与者步骤 {#dynamic-participant-step}

“动 **态参加者步骤** ”组件与“参 **[加者步骤](#participant-step)**”类似，其差异是参加者在运行时自动选择。

要配置该步骤，请选择一个参 **加者选择器** ，该选择器标识要将工作项分配给的参加者，以及一个对话框。

#### 动态参与者步骤——配置 {#dynamic-participant-step-configuration}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](#step-properties-common-tab)
* **参与者选择器**

   * **参加者选择器**:您创建的参 [加者选择器的名称](#developingtheparticipantchooser)。
   * **参数**:任何必需参数。
   * **电子邮件**:是否应向用户发送电子邮件通知。

* **对话框**

   * **对话框路径**:您创建的对话框的对话框节 [点的路径(与对话框参 **加者步骤一样**)](#dialog-participant-step-creating-a-dialog)。

#### 动态参与者步骤——开发参与者选择器 {#dynamic-participant-step-developing-the-participant-chooser}

您可以创建参加者选择器。 因此，您可以使用任何选择逻辑或条件。 例如，参加者选择器可以选择工作项最少的用户（在组内）。 您可以创建任意数量的参加者选择器以与工作流模型中“动态参 **加者步骤** ”组件的不同实例一起使用。

创建一个OSGi服务或选择用户将工作项分配到的ECMAScript。

* **ECMAscript**

   脚本必须包含一个名为getParticipant的函数，该函数将用户ID返回为 `String` 值。 将自定义脚本存储在文件夹或 `/apps/myapp/workflow/scripts` 子文件夹中。

   标准AEM实例中包含示例脚本：

   `/libs/workflow/scripts/initiator-participant-chooser.ecma`

   >[!CAUTION]
   >
   >您 ***不得*** 更改路径中的任 `/libs` 何内容。
   >
   >
   >这是因为下次升级实 `/libs` 例时，将覆盖其内容（应用修补程序或功能包时，可能会覆盖该内容）。

   此脚本选择工作流启动器作为参加者：

   ```
   function getParticipant() {
       return workItem.getWorkflow().getInitiator();
   }
   ```

   >[!NOTE]
   >
   >工作 **流发起者参与者选择器** ，组件扩展 **了动态参与者步骤** ，并使用此脚本作为步骤实现。

* **OSGi服务**

   服务必须实 [现com.day.cq.workflow.exec.ParticipantStepChooser](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/ParticipantStepChooser.html) 接口。 接口定义以下成员：

   * `SERVICE_PROPERTY_LABEL` 字段：使用此字段可指定参加者选择器的名称。 该名称显示在“动态参加者步骤”属性中的可用参 **加者选择器列表** 。

   * `getParticipant` 方法：将动态解析的主体id返回为 `String` 值。
   >[!CAUTION]
   >
   >该方 `getParticipant` 法返回动态解析的Principal id。 这可以是组ID或用户ID。
   >
   >
   >但是，组ID只能用于返回参加者列 **表时的参加者步骤**。 对于动 **态参加者步骤** ，将返回空列表，且此列表不能用于委派。

   要使您的实施对 **Dynamic Participant Step组件可用** ，请将您的Java类添加到导出服务的OSGi捆绑包，然后将捆绑包部署到AEM服务器。

   >[!NOTE]
   >
   >**“随机参加者选择器** ”是选择随机用户()的示例服 `com.day.cq.workflow.impl.process.RandomParticipantChooser`务。 随机 **参与者**&#x200B;选择器步骤组件范例扩展了动态参 **与者步骤** ，并使用此服务作为步骤实现。

#### 动态参与者步骤——参加者选择器服务示例 {#dynamic-participant-step-example-participant-chooser-service}

以下Java类实现该接 `ParticipantStepChooser` 口。 该类返回启动工作流的参加者的姓名。 代码使用的逻辑与示例脚本(`initiator-participant-chooser.ecma`)使用的逻辑相同。

注 `@Property` 释将字段的值设 `SERVICE_PROPERTY_LABEL` 置为 `Workflow Initiator Participant Chooser`。

```java
package com.adobe.example;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.osgi.framework.Constants;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.ParticipantStepChooser;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.metadata.MetaDataMap;

@Component
@Service
@Properties({
        @Property(name = Constants.SERVICE_DESCRIPTION, value = "An example implementation of a dynamic participant chooser."),
        @Property(name = ParticipantStepChooser.SERVICE_PROPERTY_LABEL, value = "Workflow Initiator Participant Chooser (service)") })
public class InitiatorParticipantChooser implements ParticipantStepChooser {

 private Logger logger = LoggerFactory.getLogger(this.getClass());

 public String getParticipant(WorkItem arg0, WorkflowSession arg1,
   MetaDataMap arg2) throws WorkflowException {

  String initiator = arg0.getWorkflow().getInitiator();
  logger.info("Assigning Dynamic Participant Step work item to {}",initiator);

  return initiator;
 }
}
```

在“动 **态参加者步骤** ”属性对话框中，“参 **加者选择器** ”列表包含 `Workflow Initiator Participant Chooser (script)`表示此服务的项。

启动工作流模型时，日志会指示启动工作流的用户的ID以及工作项的分配者。 在此示例中，用 `admin` 户启动了工作流。

`13.09.2015 15:48:53.037 *INFO* [10.176.129.223 [1347565733037] POST /etc/workflow/instances HTTP/1.1] com.adobe.example.InitiatorParticipantChooser Assigning Dynamic Participant Step work item to admin`

### 表单参与者步骤 {#form-participant-step}

在打 **开工作项时** ，表单参与者步骤会显示一个表单。 当用户填写并提交表单时，字段数据存储在工作流有效负荷的节点中。

要配置该步骤，请指定要将工作项分配到的组或用户以及表单的路径。

>[!CAUTION]
>
>此部分介绍用于页面 [创作的基础组件的“表单”部分](/help/sites-authoring/default-components-foundation.md#form)。

#### 表单参加者步骤——配置 {#form-participant-step-configuration}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](#step-properties-common-tab)
* [用户/组](#step-properties-user-group-tab)
* **表单**

   * **表单路径**:您创建的表 [单的路径](#form-participant-step-creating-the-form)。

#### 表单参加者步骤——创建表单 {#form-participant-step-creating-the-form}

创建表单以正常方式与表 **单参加者步骤一起** 。 但是，“表单参加者步骤”的表单必须具有以下配置：

* 表 **单的开头组件必须将“** 操作类型 **”属性设置为**`Edit Workflow Controlled Resource(s)`。
* 表 **单的开始** ，组件必须具有该属性的 `Form Identifier` 值。
* 表单组件必须将“元 **素名称** ”属性设置为存储字段数据的节点的路径。 路径必须在工作流有效负荷内容中找到一个节点。 该值使用以下格式：

   `./jcr:content/path_to_node`

* 表单必须包含 **工作流提交按钮组件** 。 不配置组件的任何属性。

工作流程的要求决定了您应将字段数据存储到何处。 例如，字段数据可用于配置页面内容的属性。 元素名称属性的 **以下值将字段数据存储为节** 点属性的 `redirectTarget``jcr:content` 值：

`./jcr:content/redirectTarget`

在以下示例中，字段数据用作有效负荷页面上的 **Text** 组件的内容：

`./jcr:content/par/text_3/text`

第一个示例可用于组件呈现的任何 `cq:Page` 页面。 第二个示例仅在有效负荷页面包含ID为的 **Text** 组件时才可用 `text_3`。

表单可以位于存储库中的任意位置，但必须授权工作流用户读取表单。

### 随机参与者选择器 {#random-participant-chooser}

“随 **机参加者选择器** ”步骤是将生成的工作项分配给从列表中随机选择的用户的参加者选择器。

![wf-31](assets/wf-31.png)

#### 随机参加者选择器——配置 {#random-participant-chooser-configuration}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](#step-properties-common-tab)
* **参数**

   * **参加者**:指定可供选择的用户列表。 要将用户添加到列表，请单 **击“添加项目** ”，然后键入用户节点的主路径或用户ID。 用户的顺序不会影响被分配工作项的可能性。

### 工作流发起者参与人选择器 {#workflow-initiator-participant-chooser}

“工 **作流发起者参与者选择器** ”步骤是一个参与者选择器，用于将生成的工作项分配给启动工作流的用户。 除了“常用”属性之外，没有其他 **属性** 。

#### Workflow Initiator Participant Chooser - Configuration {#workflow-initiator-participant-chooser-configuration}

要配置该步骤，请使用以下选项卡进行编辑：

* [通用](#step-properties-common-tab)

## 进程步骤 {#process-step}

处 **理步骤** (Process Step)执行ECMAScript或调用OSGi服务以执行自动处理。

![wf-32](assets/wf-32.png)

### 流程步骤——配置 {#process-step-configuration}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](#step-properties-common-tab)
* **进程**

   * **流程**:要执行的进程实现。 使用下拉菜单选择ECMAScript或OSGi服务。 有关以下信息：

      * 标准ECMAScript和OSGi服务，请参阅 [处理步骤的内置流程](/help/sites-developing/workflows-process-ref.md)。
      * 为进程步骤创建ECMAScript，请参 [阅使用ECMAScript实现进程步骤](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript)。
      * 为进程步骤创建OSGi服务，请参 [阅使用Java类实现进程步骤](/help/sites-developing/workflows-customizing-extending.md#implementing-a-process-step-with-a-java-class)。
   * **处理程序高级**:选择此选项可将工作流自动推进到执行后的下一步。 如果未选择，则实施脚本必须处理工作流的进度。
   * **参数**:要传递到进程的参数。


## 设置变量 {#set-variable}

“设置变量”(Set Variable)步骤允许您设置变量的值并定义值的设置顺序。 变量按变量映射在设置变量步骤中的列出顺序设置。

![添加映射以设置变量](assets/set_variable_addmappingnew.png)

### 设置变量——配置 {#setvariable}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](/help/sites-developing/workflows-step-ref.md#step-properties-common-tab)
* **映射**

   * **** 选择变量：使用此选项可选择变量以设置其值。
   * **** 选择映射模式：选择映射模式以设置变量的值。 根据变量的数据类型，您可以使用以下选项设置变量的值：

      * **** 文本：当您知道要指定的确切值时，请使用此选项。
      * **** 表达式：根据表达式计算要使用的值时，请使用此选项。 表达式是在提供的表达式编辑器中创建的。
      * **** JSON点表示法：使用此选项从JSON或FDM类型变量检索值。
      * **** XPATH:使用此选项从XML类型变量检索值。
      * **** 相对于有效负荷：当要保存到变量的值在相对于有效负荷的路径上可用时，请使用此选项。
      * **** 绝对路径：当要保存到变量的值在绝对路径上可用时，请使用此选项。
   * **** 指定值：指定要映射到变量的值。 在此字段中指定的值取决于映射模式。
   * **** 添加映射：使用此选项可添加更多映射以设置变量的值。
