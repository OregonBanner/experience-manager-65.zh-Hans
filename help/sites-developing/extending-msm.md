---
title: 扩展多站点管理器
seo-title: 扩展多站点管理器
description: 本页帮助您扩展多站点管理器的功能
seo-description: 本页帮助您扩展多站点管理器的功能
uuid: dfa7d050-29fc-4401-8d4d-d6ace6b49bea
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6128c91a-4173-42b4-926f-bbbb2b54ba5b
docset: aem65
translation-type: tm+mt
source-git-commit: fa99c3bc2110aadb403920aa3e0fcf0919f26735
workflow-type: tm+mt
source-wordcount: '2611'
ht-degree: 2%

---


# 扩展多站点管理器{#extending-the-multi-site-manager}

本页帮助您扩展多站点管理器的功能：

* 了解MSM Java API的主要成员。
* 创建可在转出配置中使用的新同步操作。
* 删除“创建站点”向导中的“章节”步骤。
* 修改默认语言和国家代码。

>[!NOTE]
>
>本页应结合重用内容 [进行阅读： 多站点管理器](/help/sites-administering/msm.md)。
>
>AEM 6.4中的站点存储库重构的以下部分可能也值得关注：
>* [多站点管理器Blueprint配置](https://docs.adobe.com/content/help/en/experience-manager-64/deploying/restructuring/sites-repository-restructuring-in-aem-6-4.html#multi-site-manager-blueprint-configurations)
>* [多站点管理器转出配置](https://docs.adobe.com/content/help/en/experience-manager-64/deploying/restructuring/sites-repository-restructuring-in-aem-6-4.html#multi-site-manager-rollout-configurations)


>[!CAUTION]
>
>创作网站时使用多站点管理器及其API，因此仅用于创作环境。

## Java API概述 {#overview-of-the-java-api}

多站点管理包括以下包：

* [com.day.cq.wcm.msm.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/package-frame.html)
* [com.day.cq.wcm.msm.commons](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/commons/package-frame.html)

主MSM API对象交互如下(另请参阅 [使用的术语](/help/sites-administering/msm.md#terms-used)):

![chlimage_1-73](assets/chlimage_1-73.png)

* **`Blueprint`**

   A( `Blueprint` 如在 [Blueprint配置中](/help/sites-administering/msm.md#source-blueprints-and-blueprint-configurations))指定Live Copy可从中继承内容的页面。

   ![chlimage_1-74](assets/chlimage_1-74.png)

   * 使用Blueprint配置() `Blueprint`是可选的，但：

      * 允许作者在源上使 **用** “转出”选项(将修改（显式）推送到继承自此源的Live Copy)。
      * 允许作者使用创 **建站点**; 这允许用户轻松选择语言并配置Live Copy的结构。
      * 为任何生成的Live Copy定义默认转出配置。

* **`LiveRelationship`** 指 `LiveRelationship` 定Live Copy分支中的资源与其等效的源／蓝图资源之间的连接（关系）。

   * 在实现继承和转出时使用关系。
   * `LiveRelationship` 对象提供对转出配置()、和与关 `RolloutConfig`系相关 `LiveCopy`的对 `LiveStatus` 象的访问（引用）。

   * 例如，在的source/blueprint中 `/content/copy/us` 创建Live Copy `/content/we-retail/language-masters`。 资源 `/content/we.retail/language-masters/en/jcr:content` 并 `/content/copy/us/en/jcr:content` 形成关系。

* **`LiveCopy`** `LiveCopy` 包含Live Copy资源与其源/ `LiveRelationship`Blueprint资源之间关系()的配置详细信息。

   * 使用 `LiveCopy` 类可访问页面的路径、源／蓝图页面的路径、转出配置以及子页面是否也包含在中 `LiveCopy`。

   * 每次 `LiveCopy` 使用创建站点 **或创建****Live Copy时都会创建节点** 。

* **`LiveStatus`**

   `LiveStatus` 对象提供对的运行时状态的访 `LiveRelationship`问。 用于查询Live Copy的同步状态。

* **`LiveAction`**

   A `LiveAction` 是对转出中涉及的每个资源执行的操作。

   * LiveActions只由RolloutConfigs生成。

* **`LiveActionFactory`**

   创建 `LiveAction` 给定配置的 `LiveAction` 对象。 配置作为资源存储在存储库中。

* **`RolloutConfig`** 保 `RolloutConfig` 存列表, `LiveActions`在触发时使用。 继 `LiveCopy` 承该 `RolloutConfig` 属性，并且结果会出现在中 `LiveRelationship`。

   * 首次设置Live Copy时还会使用RolloutConfig（它触发LiveActions）。

### 创建新同步操作 {#creating-a-new-synchronization-action}

创建要用于转出配置的自定义同步操作。 当安装的操作不满足您的 [特定应用程序要](/help/sites-administering/msm-sync.md#installed-synchronization-actions) 求时，创建同步操作。 为此，请创建两个类：

* 执行操作 [ 的接 `com.day.cq.wcm.msm.api.LiveAction`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveAction.html) 口的实现。
* 一个OSGI组件，用于实 [ 现接 `com.day.cq.wcm.msm.api.LiveActionFactory`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) 口并创建类的 `LiveAction` 实例。

为 `LiveActionFactory` 给定配置 `LiveAction` 创建类的实例：

* `LiveAction` 类包括以下方法：

   * `getName`: 返回操作的名称。名称用于引用操作，例如转出配置中。
   * `execute`: 执行操作的任务。

* `LiveActionFactory` 类包括以下成员：

   * `LIVE_ACTION_NAME`: 包含关联名称的字段 `LiveAction`。 此名称必须与类的方法返回 `getName` 的值重 `LiveAction` 合。

   * `createAction`: 创建实例 `LiveAction`。 可选参 `Resource` 数可用于提供配置信息。

   * `createsAction`: 返回关联的名称 `LiveAction`。

### 访问LiveAction配置节点 {#accessing-the-liveaction-configuration-node}

使用存 `LiveAction` 储库中的配置节点存储影响实例运行时行为的 `LiveAction` 信息。 存储配置的存储库中的节 `LiveAction` 点在运行时可供对 `LiveActionFactory` 象使用。 因此，您可以根据需要向配置节点添加属性并在实施 `LiveActionFactory` 中使用它们。

例如，需 `LiveAction` 要存储blueprint作者的名称。 配置节点的属性包括存储信息的蓝图页的属性名称。 在运行时， `LiveAction` 从配置中检索属性名称，然后获取属性值。

方法的参 ` [LiveActionFactory](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html).createAction` 数是对 `Resource` 象。 此对 `Resource` 象表示转 `cq:LiveSyncAction` 出配置中此实时操作的节点； 请参 [阅创建转出配置](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration)。 与常用配置节点一样，您应将其调整为对 `ValueMap` 象：

```java
public LiveAction createAction(Resource resource) throws WCMException {
        ValueMap config;
        if (resource == null || resource.adaptTo(ValueMap.class) == null) {
            config = new ValueMapDecorator(Collections.<String, Object>emptyMap());
        } else {
            config = resource.adaptTo(ValueMap.class);
        }
        return new MyLiveAction(config, this);
}
```

### 访问目标节点、源节点和LiveRelationship {#accessing-target-nodes-source-nodes-and-the-liverelationship}

以下对象作为对象方法 `execute` 的参数提 `LiveAction` 供：

* 表 [ 示Live `Resource`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) Copy源的对象。
* 一 `Resource` 个对象，它表示Live Copy的目标。
* Live [ Copy `LiveRelationship`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveRelationship.html) 的对象。
* 值 `autoSave` 指示您是否 `LiveAction` 应保存对存储库所做的更改。

* 重置值指示转出重置模式。

从这些对象中，您可以获得有关该对象的所有信息 `LiveCopy`。 您还可以使用 `Resource` 对象获 `ResourceResolver`取、 `Session`和 `Node` 对象。 这些对象可用于处理存储库内容：

在以下代码的第一行中，source是 `Resource` 源页面的对象：

```java
ResourceResolver resolver = source.getResourceResolver();
Session session = resolver.adaptTo(javax.jcr.Session.class);
Node sourcenode = source.adaptTo(javax.jcr.Node.class);
```

>[!NOTE]
>
>参 `Resource` 数可以是 `null` 或不适应 `Resources` 对象的对象，如 `Node` 对 [`NonExistingResource`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/NonExistingResource.html) 象。

### Creating a New Rollout Configuration {#creating-a-new-rollout-configuration}

当安装的转出配置不符合您的应用程序要求时，创建转出配置：

* [创建转出配置](#create-the-rollout-configuration)。
* [向转出配置添加同步操作](#add-synchronization-actions-to-the-rollout-configuration)。

在 Blueprint 或 Live Copy 页面上设置转出配置时，您可以使用该新转出配置。

>[!NOTE]
>
>另请参阅自 [定义转出的最佳实践](/help/sites-administering/msm-best-practices.md#customizing-rollouts)。

#### Create the Rollout Configuration {#create-the-rollout-configuration}

要创建新转出配置，请执行以下操作：

1. 打开CRXDE Lite; 例如：
   [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. 导航至 :
   `/apps/msm/<your-project>/rolloutconfigs`

   >[!NOTE]
   >这是您项目的自定义版本：
   >`/libs/msm/wcm/rolloutconfigs`
   >如果这是您的第一个配置，则必须创建。

   >[!NOTE]
   >
   >您不得更改/libs路径中的任何内容。
   >这是因为下次升级实例时，/libs的内容会被覆盖（当您应用修补程序或功能包时，很可能会被覆盖）。
   >建议的配置和其他更改方法是：
   >* 在/apps下重新创建所需项（即，它存在于/libs中）
   >* 在/apps中进行任何更改


1. 在此 **下** ，创建具有以下属性的节点：

   * **名称**: 转出配置的节点名称。 md#installed-synchronization-actions)，例如 `contentCopy` 或 `workflow`。
   * **类型**: `cq:RolloutConfig`

1. 向此节点添加以下属性：
   * **名称**: `jcr:title`

      **类型**: `String`
      **值**: 将在UI中显示的标识标题。
   * **名称**: `jcr:description`

      **类型**: `String`
      **值**: 可选描述。
   * **名称**: `cq:trigger`

      **类型**: `String`
      **值**: 要 [使用的转](/help/sites-administering/msm-sync.md#rollout-triggers) 出触发器。 选择自：
      * `rollout`
      * `modification`
      * `publish`
      * `deactivate`

1. 单击“ **全部保存**”。

#### Add Synchronization Actions to the Rollout Configuration {#add-synchronization-actions-to-the-rollout-configuration}

转出配置存储在您在 [节点下创建](#create-the-rollout-configuration) 的转出配置节点 `/apps/msm/<your-project>/rolloutconfigs` 下。

添加类型的子节 `cq:LiveSyncAction` 点以向转出配置添加同步操作。 同步操作节点的顺序决定操作的发生顺序。

1. 仍在CRXDE Lite中，选择您的转 [出配置节](#create-the-rollout-configuration) 点。

   例如：
   `/apps/msm/myproject/rolloutconfigs/myrolloutconfig`

1. **创建具** 有以下节点属性的节点：

   * **名称**: 同步操作的节点名称。
该名称必须与“同步操 **作”(Synchronization Actions** )下的表 [中的“操作名称”(Action Name](/help/sites-administering/msm-sync.md#installed-synchronization-actions))相同 `contentCopy` ，例如 `workflow`或。
   * **类型**: `cq:LiveSyncAction`

1. 根据需要添加和配置任意数量的同步操作节点。 重新排列操作节点，使其顺序与您希望它们出现的顺序相匹配。 最先出现的操作节点。

### 创建和使用简单的LiveActionFactory类 {#creating-and-using-a-simple-liveactionfactory-class}

按照本节中的步骤开发并 `LiveActionFactory` 在转出配置中使用它。 这些过程使用Maven和Eclipse开发和部署 `LiveActionFactory`:

1. [创建主项目](#create-the-maven-project) ，并将其导入Eclipse。
1. [向POM文件](#add-dependencies-to-the-pom-file) 添加依赖关系。
1. [实施 `LiveActionFactory` 界面](#implement-liveactionfactory) 并部署OSGi捆绑包。
1. [创建转出配置](#create-the-example-rollout-configuration)。
1. [创建Live Copy](#create-the-live-copy)。

Maven项目和Java类的源代码可在公共Git存储库中使用。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开experiencemanager-java-msmrollout项目](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout)
* 以ZIP文件的 [形式下载项目](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout/archive/master.zip)

#### 创建Maven项目 {#create-the-maven-project}

以下过程要求您已将adobe-public用户档案添加到Maven设置文件。

* 有关adobe-public用户档案的信息，请参 [阅获取内容包Maven插件](/help/sites-developing/vlt-mavenplugin.md#obtaining-the-content-package-maven-plugin)
* 有关Maven设置文件的信息，请参阅Maven设 [置参考](https://maven.apache.org/settings.html)。

1. 打开终端或命令行会话并更改目录以指向创建项目的位置。
1. 输入以下命令：

   ```xml
   mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault -DarchetypeArtifactId=multimodule-content-package-archetype -DarchetypeVersion=1.0.0 -DarchetypeRepository=adobe-public-releases
   ```

1. 在交互式提示符下指定以下值：

   * `groupId`: `com.adobe.example.msm`
   * `artifactId`: `MyLiveActionFactory`
   * `version`: `1.0-SNAPSHOT`
   * `package`: `MyPackage`
   * `appsFolderName`: `myapp`
   * `artifactName`: `MyLiveActionFactory package`
   * `packageGroup`: `myPackages`

1. 开始Eclipse并 [导入Maven项目](/help/sites-developing/howto-projects-eclipse.md#import-the-maven-project-into-eclipse)。

#### 向POM文件添加依赖项 {#add-dependencies-to-the-pom-file}

添加依赖关系，以便Eclipse编译器可以引用代码中使用的 `LiveActionFactory` 类。

1. 从Eclipse项目资源管理器中，打开文件：

   `MyLiveActionFactory/pom.xml`

1. 在编辑器中，单击选 `pom.xml` 项卡并找到该 `project/dependencyManagement/dependencies` 部分。
1. 在元素中添加以 `dependencyManagement` 下XML，然后保存文件。

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
     <version>5.6.2</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
     <version>2.4.3-R1488084</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
     <version>5.6.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
     <version>2.0.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
     <version>2.0.0</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
   ```

1. 从Project Explorer打开捆绑包的POM **文件** , `MyLiveActionFactory-bundle/pom.xml`网址
1. 在编辑器中，单击选 `pom.xml` 项卡并找到项目／依赖关系部分。 在依赖关系元素中添加以下XML，然后保存文件：

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
   ```

#### 实施LiveActionFactory {#implement-liveactionfactory}

以下类 `LiveActionFactory` 实现一个 `LiveAction` 类，它记录有关源和目标页的消息，并将属性 `cq:lastModifiedBy` 从源节点复制到目标节点。 实时操作的名称为 `exampleLiveAction`。

1. 在Eclipse项目资源管理器中，右键单击包 `MyLiveActionFactory-bundle/src/main/java/com.adobe.example.msm` ，然后单 **击** “新 **建”**> 在“名 **称**”中， `ExampleLiveActionFactory` 输入，然后单 **击完成**。
1. 打开文 `ExampleLiveActionFactory.java` 件，用以下代码替换内容并保存文件。

   ```java
   package com.adobe.example.msm;
   
   import java.util.Collections;
   
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   import org.apache.sling.api.resource.Resource;
   import org.apache.sling.api.resource.ResourceResolver;
   import org.apache.sling.api.resource.ValueMap;
   import org.apache.sling.api.wrappers.ValueMapDecorator;
   import org.apache.sling.commons.json.io.JSONWriter;
   import org.apache.sling.commons.json.JSONException;
   
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   
   import com.day.cq.wcm.msm.api.ActionConfig;
   import com.day.cq.wcm.msm.api.LiveAction;
   import com.day.cq.wcm.msm.api.LiveActionFactory;
   import com.day.cq.wcm.msm.api.LiveRelationship;
   import com.day.cq.wcm.api.WCMException;
   
   @Component(metatype = false)
   @Service
   public class ExampleLiveActionFactory implements LiveActionFactory<LiveAction> {
    @Property(value="exampleLiveAction")
    static final String actionname = LiveActionFactory.LIVE_ACTION_NAME;
   
    public LiveAction createAction(Resource config) {
     ValueMap configs;
     /* Adapt the config resource to a ValueMap */
           if (config == null || config.adaptTo(ValueMap.class) == null) {
               configs = new ValueMapDecorator(Collections.<String, Object>emptyMap());
           } else {
               configs = config.adaptTo(ValueMap.class);
           }
   
     return new ExampleLiveAction(actionname, configs);
    }
    public String createsAction() {
     return actionname;
    }
    /************* LiveAction ****************/
    private static class ExampleLiveAction implements LiveAction {
     private String name;
     private ValueMap configs;
     private static final Logger log = LoggerFactory.getLogger(ExampleLiveAction.class);
   
     public ExampleLiveAction(String nm, ValueMap config){
      name = nm;
      configs = config;
     }
   
     public void execute(Resource source, Resource target,
       LiveRelationship liverel, boolean autoSave, boolean isResetRollout)
         throws WCMException {
   
      String lastMod = null;
   
      log.info(" *** Executing ExampleLiveAction *** ");
   
      /* Determine if the LiveAction is configured to copy the cq:lastModifiedBy property */
      if ((Boolean) configs.get("repLastModBy")){
   
       /* get the source's cq:lastModifiedBy property */
       if (source != null && source.adaptTo(Node.class) !=  null){
        ValueMap sourcevm = source.adaptTo(ValueMap.class);
        lastMod = sourcevm.get(com.day.cq.wcm.msm.api.MSMNameConstants.PN_PAGE_LAST_MOD_BY, String.class);
       }
   
       /* set the target node's la-lastModifiedBy property */
       Session session = null;
       if (target != null && target.adaptTo(Node.class) !=  null){
        ResourceResolver resolver = target.getResourceResolver();
        session = resolver.adaptTo(javax.jcr.Session.class);
        Node targetNode;
        try{
         targetNode=target.adaptTo(javax.jcr.Node.class);
         targetNode.setProperty("la-lastModifiedBy", lastMod);
         log.info(" *** Target node lastModifiedBy property updated: {} ***",lastMod);
        }catch(Exception e){
         log.error(e.getMessage());
        }
       }
       if(autoSave){
        try {
         session.save();
        } catch (Exception e) {
         try {
          session.refresh(true);
         } catch (RepositoryException e1) {
          e1.printStackTrace();
         }
         e.printStackTrace();
        }
       }
      }
     }
     public String getName() {
      return name;
     }
   
     /************* Deprecated *************/
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
       ActionConfig arg2, boolean arg3) throws WCMException {
     }
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
       ActionConfig arg2, boolean arg3, boolean arg4)
         throws WCMException {
     }
     @Deprecated
     public String getParameterName() {
      return null;
     }
     @Deprecated
     public String[] getPropertiesNames() {
      return null;
     }
     @Deprecated
     public int getRank() {
      return 0;
     }
     @Deprecated
     public String getTitle() {
      return null;
     }
     @Deprecated
     public void write(JSONWriter arg0) throws JSONException {
     }
    }
   }
   ```

1. 使用终端或命令会话，将目录更改 `MyLiveActionFactory` 为目录（Maven项目目录）。 然后，输入以下命令：

   ```shell
   mvn -PautoInstallPackage clean install
   ```

   AEM文 `error.log` 件应指示捆绑已启动。

   例如， [https://localhost:4502/system/console/status-slinglogs](https://localhost:4502/system/console/status-slinglogs)。

   ```xml
   13.08.2013 14:34:55.450 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent RESOLVED
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTING
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTED
   13.08.2013 14:34:55.453 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle Service [com.adobe.example.msm.ExampleLiveActionFactory,2188] ServiceEvent REGISTERED
   13.08.2013 14:34:55.454 *INFO* [OsgiInstallerImpl] org.apache.sling.audit.osgi.installer Started bundle com.adobe.example.msm.MyLiveActionFactory-bundle [316]
   ```

#### Create the Example Rollout Configuration {#create-the-example-rollout-configuration}

创建使用您创建的MSM转 `LiveActionFactory` 出配置：

1. 使用标准过 [程创建和配置转出配置](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) -并使用属性：

   * **标题**: 示例转出配置
   * **名称**: examplerolloutconfig
   * **cq:trigger**: `publish`

#### 将Live Action添加到示例转出配置 {#add-the-live-action-to-the-example-rollout-configuration}

配置您在上一个过程中创建的转出配置，以便它使用 `ExampleLiveActionFactory` 类。

1. 打开CRXDE Lite; 例如， [https://localhost:4502/crx/de](https://localhost:4502/crx/de)。
1. 在下面创建以下节点 `/apps/msm/rolloutconfigs/examplerolloutconfig/jcr:content`:

   * **名称**: `exampleLiveAction`
   * **类型**: `cq:LiveSyncAction`

1. 单击“ **全部保存**”。
1. 选择节 `exampleLiveAction` 点并添加以下属性：

   * **名称**: `repLastModBy`
   * **类型**: `Boolean`
   * **值**: `true`

   此属性向类指 `ExampleLiveAction` 示应将 `cq:LastModifiedBy` 属性从源复制到目标节点。

1. 单击“ **全部保存**”。

#### 创建Live Copy {#create-the-live-copy}

[使用转出配置](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) ，创建We.Retail Reference Site的English/Products分支的Live Copy:

* **来源**: `/content/we-retail/language-masters/en/products`

* **转出配置**: 示例转出配置

激活 **源分支** 的“产品”（英语）页面，并观察类生成的日志 `LiveAction` 消息：

```xml
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***ExampleLiveAction has been executed.***
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***Target node lastModifiedBy property updated: admin ***
```

<!--
### Removing the Chapters Step in the Create Site Wizard {#removing-the-chapters-step-in-the-create-site-wizard}

In some cases, the **Chapters** selection is not required in the create site wizard (only the **Languages** selection is required). To remove this step in the default We.Retail English blueprint:

1. In CRX Explorer, remove the node:
   `/etc/blueprints/weretail-english/jcr:content/dialog/items/tabs/items/tab_chap`.

1. Navigate to `/libs/wcm/msm/templates/blueprint/defaults/livecopy_tab/items` and create a new node:

    1. **Name** = `chapters`; **Type** = `cq:Widget`.

1. Add following properties to the new node:

    1. **Name** = `name`; **Type** = `String`; **Value** = `msm:chapterPages`

    1. **Name** = `value`; **Type** = `String`; **Value** = `all`

    1. **Name** = `xtype`; **Type** = `String`; **Value** = `hidden`
-->

### 更改语言名称和默认国家／地区 {#changing-language-names-and-default-countries}

AEM使用一组默认的语言和国家／地区代码。

* 默认语言代码是ISO-639-1定义的小写双字母代码。
* 默认国家／地区代码是ISO 3166定义的小写或大写双字母代码。

MSM使用语言和国家代码的存储列表来确定与页面语言版本名称关联的国家／地区名称。 您可以根据需要更改列表的以下方面：

* 语言标题
* 国家／地区名称
* 语言的默认国家／地区(如 `en`、 `de`等代码)

语言列表存储在节点 `/libs/wcm/core/resources/languages` 下。 每个子节点表示语言或语言国家／地区：

* 节点的名称是语言代码( `en` 如 `de`或)或language_country代码(如 `en_us` 或 `de_ch`)。

* 节 `language` 点的属性存储代码语言的全名。
* 节 `country` 点的属性存储代码的国家／地区的全名。
* 当节点名称仅包含语言代码(如 `en`)时，国家／地区属性 `*`为，并且附加属性 `defaultCountry` 存储语言国家／地区的代码以指示要使用的国家／地区。

![chlimage_1-76](assets/chlimage_1-76.png)

要修改语言，请执行以下操作：

1. 在Web浏览器中打开CRXDE Lite; 例如， [https://localhost:4502/crx/de](https://localhost:4502/crx/de)
1. 选择文件 `/apps` 夹，单击 **创建**，然后 **单击创建文件夹。**

   命名新文件夹 `wcm`。

1. 重复上一步，创建文 `/apps/wcm/core` 件夹树。 创建名为的类 `sling:Folder` 型 `core` 的节点 `resources`。

   ![chlimage_1-77](assets/chlimage_1-77.png)

1. 右键单击该节 `/libs/wcm/core/resources/languages` 点，然后单 **击复制**。
1. 右键单击文件夹 `/apps/wcm/core/resources` ，然后单击“ **粘贴”**。 根据需要修改子节点。
1. 单击“ **全部保存**”。
1. 单击 **工具**、 **操作** ，然 **后单击Web控制台**。 从此控制台中， **单击** OSGi, **然后单击Configuration**。
1. 找到并单 **击Day CQ WCM Language Manager**，将“Language Manager”(语言 **列表)的值更改为** , `/apps/wcm/core/resources/languages`然后单击“ **Save**”（保存）。

   ![chlimage_1-78](assets/chlimage_1-78.png)

### 在页面属性上配置MSM锁（触屏优化UI） {#configuring-msm-locks-on-page-properties-touch-enabled-ui}

创建自定义页面属性时，您可能需要考虑新属性是否有资格转出到任何Live Copy。

例如，如果添加了两个新页面属性：

* 联系电子邮件:

   * 此属性不必推出，因为它在每个国家／地区（或品牌等）都会有所不同。

* 关键视觉样式：

   * 项目要求是，此属性将按所有国家（或品牌等）共同的方式（通常）推广。

然后，您需要确保：

* 联系电子邮件:

   * 从转出属性中排除； 请参 [阅从同步中排除属性和节点类型](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization)。

* 关键视觉样式：

   * 确保在触屏优化UI中不允许编辑此属性，除非取消继承，还可以恢复继承； 可通过单击切换以指示连接状态的链／断链链链接来控制此连接。

页面属性是否可以滚出，因此在编辑时可以取消／恢复继承，这由对话框属性控制：

* `cq-msm-lockable`

   * 适用于触屏优化UI对话框中的项
   * 将在对话框中创建链式链接符号
   * 仅允许在继承被取消（链链链断开）时进行编辑
   * 仅适用于资源的第一个子级别
   * **类型**: `String`

   * **值**: 持有所考虑物业之名称(及与物业价值相若 `name`; 例如，请参阅
      `/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title`

定 `cq-msm-lockable` 义后，断开／关闭链将通过以下方式与MSM交互：

* 如果值 `cq-msm-lockable` 为：

   * **相对** (例如 `myProperty` 或 `./myProperty`)

      * 它将添加和删除属性 `cq:propertyInheritanceCancelled`。
   * **绝对** (例如， `/image`)

      * 通过将mixin添加到并将其设置为，中断 `cq:LiveSyncCancelled` 链将取 `./image` 消继 `cq:isCancelledForChildren` 承 `true`。

      * 关闭链将恢复继承。


>[!NOTE]
>
>`cq-msm-lockable` 应用于要编辑的资源的第一个子级，它在任何更深层的祖先上都不起作用，无论该值是定义为绝对值还是相对值。

>[!NOTE]
>
>重新启用继承时，Live Copy页面属性不会自动与源属性同步。 如果需要，可以手动请求同步。
