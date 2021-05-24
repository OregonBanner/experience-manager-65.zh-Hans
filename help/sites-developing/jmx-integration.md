---
title: 将服务与JMX控制台集成
seo-title: 将服务与JMX控制台集成
description: 通过创建和部署MBean以使用JMX控制台管理服务，公开服务属性和操作以启用要执行的管理任务
seo-description: 通过创建和部署MBean以使用JMX控制台管理服务，公开服务属性和操作以启用要执行的管理任务
uuid: 4a489a24-af10-4505-8333-aafc0c81dd3e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 83c590e0-2e6c-4499-a6ea-216e4c7bc43c
docset: aem65
exl-id: fe727406-09cb-4516-8278-806fd78cfc12
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1689'
ht-degree: 0%

---

# 将服务与JMX控制台集成{#integrating-services-with-the-jmx-console}

创建和部署MBean以使用JMX控制台管理服务。 显示服务属性和操作以启用要执行的管理任务。

有关使用JMX控制台的信息，请参阅[使用JMX控制台监视服务器资源](/help/sites-administering/jmx-console.md)。

## Felix和CQ5中的JMX框架{#the-jmx-framework-in-felix-and-cq}

在Apache Felix平台上，您将MBean部署为OSGi服务。 在OSGi服务注册表中注册MBean服务后，Aries JMX白板模块会自动向MBean服务器注册MBean。 然后，JMX控制台将可以使用MBean，该控制台会公开公共属性和操作。

![jmx白板](assets/jmxwhiteboard.png)

## 为CQ5和CRX {#creating-mbeans-for-cq-and-crx}创建MBean

您为管理CQ5或CRX资源而创建的MBean基于javax.management.DynamicMBean接口。 要创建它们，请遵循JMX规范中规定的常规设计模式：

* 创建管理界面（包括get、set和）是定义属性的方法，以及定义操作的其他方法。
* 创建实现类。 类必须实现DynamicMBean，或扩展DynamicMBean的实现类。
* 遵循标准命名约定，以便实现类的名称为带MBean后缀的接口名称。

除了定义管理界面外，该界面还定义OSGi服务界面。 实现类实现OSGi服务。

### 使用注释提供MBean信息{#using-annotations-to-provide-mbean-information}

[com.adobe.granite.jmx.annotation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/jmx/annotation/package-summary.html)包提供了多个注释和类，以便轻松地将MBean元数据提供到JMX控制台。 使用这些注释和类，而不是直接向MBean的MBeanInfo对象添加信息。

**注释**

向管理界面添加注释以指定MBean元数据。 JMX控制台中将显示所部署的每个实现类的信息。 以下注释可供使用（有关完整信息，请参阅[com.adobe.granite.jmx.annotation JavaDocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/jmx/annotation/package-summary.html)）：

* **描述：** 提供MBean类或方法的描述。当在类声明中使用时，描述会显示在MBean的JMX控制台页面上。 在方法上使用时，描述将显示为相应属性或操作的悬停文本。
* **影响：** 方法的影响。有效参数值是[javax.management.MBeanOperationInfo](https://docs.oracle.com/javase/1.5.0/docs/api/javax/management/MBeanOperationInfo.html)定义的字段。

* **名称：** 指定要为操作参数显示的名称。使用此注释可覆盖界面中使用的方法参数的实际名称。
* **OpenTypeInfo:** 指定在JMX控制台中用于表示复合数据或表格数据的类。与Open MBean一起使用
* **TabularTypeInfo:** 用于对用于表示表格数据的类添加注释。

**类**

提供了类，用于创建使用您添加到界面中的注释的动态MBean:

* **AnnotatedStandardMBean:** javax.management.StandardMBean类的子类，可自动为JMX控制台提供注释元数据。
* **OpenAnnotatedStandardMBean:** AnnotatedStandardMBean类的子类，用于创建使用OpenTypeInfo批注的Open Mbean。

### 开发MBean {#developing-mbeans}

通常， MBean是对要管理的OSGi服务的反映。 在Felix平台上，您会像在其他Java服务器平台上部署时一样创建MBean。 主要区别在于，您可以使用注释来指定MBean信息：

* 管理界面：使用getter、setter和is方法定义属性。 使用任何其他公共方法定义操作。 使用注释为BeanInfo对象提供元数据。
* MBean类：实施管理接口。 扩展AnnotatedStandardMBean类，以便在界面上处理注释。

以下示例MBean提供了有关CRX存储库的信息。 界面使用“描述”注释向JMX控制台提供信息。

#### 管理接口{#management-interface}

```java
package com.adobe.example.myapp;

import com.adobe.granite.jmx.annotation.Description;

@Description("Example MBean that exposes repository properties.")
public interface ExampleMBean {

    @Description("The name of the repository.")
    String getRepositoryName();

    @Description("The vendor of the repository.")
    String   getRepositoryVendor();

    @Description("The URL of repository vendor.")
    String getVendorUrl();
}
```

实施类使用SlingRepository服务检索有关CRX存储库的信息。

#### MBean实现类{#mbean-implementation-class}

```java
package com.adobe.example.myapp;

import org.apache.felix.scr.annotations.*;
import org.apache.sling.jcr.api.SlingRepository;

import com.adobe.granite.jmx.annotation.AnnotatedStandardMBean;

import javax.management.*;

public class ExampleMBeanImpl extends AnnotatedStandardMBean implements ExampleMBean {

    @Reference(cardinality = ReferenceCardinality.OPTIONAL_UNARY)
    private SlingRepository repository;

    public ExampleMBeanImpl() throws NotCompliantMBeanException {
        super(ExampleMBean.class);
    }

    public String getRepositoryName() {
        return repository.getDescriptor("jcr.repository.name");
    }

    public String getRepositoryVendor() {
        return repository.getDescriptor("jcr.repository.vendor");
    }

    public String getVendorUrl() {
        return repository.getDescriptor("jcr.repository.vendor.url");
    }
}
```

下图显示了JMX控制台中此MBean的页面。

![jmxdescription](assets/jmxdescription.png)

### 正在注册MBeans {#registering-mbeans}

将MBean注册为OSGi服务时，它们会自动注册到MBean服务器。 要在CQ5上安装MBean，请将其包含在包中，并像导出任何其他OSGi服务一样导出MBean服务。

除了与OSGi相关的元数据之外，您还必须提供Aries JMX白板模块在MBean服务器中注册MBean所需的元数据：

* **DynamicMBean接口的名称：** 声明MBean服务实现 `javax.management.DynamicMBea`n接口。此声明会通知Aries JMX白板模块该服务是MBean服务。

* **MBean域和键属性：** 在Felix上，您将此信息作为MBean的OSGi服务的属性提供。这与您通常在`javax.management.ObjectName`对象中向MBean服务器提供的信息相同。

当MBean是单个服务的反映时，只需要MBean服务的单个实例。 在本例中，如果您使用Felix SCR Maven插件，则可以在MBean实现类中使用Apache Felix服务组件运行时(SCR)注释来指定与JMX相关的元数据。 要实例化多个MBean实例，可以创建另一个类来执行MBean的OSGi服务的注册。 在这种情况下，与JMX相关的元数据在运行时生成。

**单个MBean**

可在设计时为其定义所有属性和操作的MBean可使用MBean实现类中的SCR注释进行部署。 在以下示例中，`Service`注释的`value`属性声明服务实现`DynamicMBean`接口。 `Property`注释的`name`属性指定JMX域和键属性。

#### SCR注释{#mbean-implementation-class-with-scr-annotations}的MBean实现类

```java
package com.adobe.example.myapp;

import org.apache.felix.scr.annotations.*;
import org.apache.sling.jcr.api.SlingRepository;

import com.adobe.granite.jmx.annotation.AnnotatedStandardMBean;

import javax.management.*;

@Component(immediate = true)
@Property(name = "jmx.objectname", value="com.adobe.example:type=CRX")
@Service(value = DynamicMBean.class)
public class ExampleMBeanImpl extends AnnotatedStandardMBean implements ExampleMBean {

    @Reference(cardinality = ReferenceCardinality.OPTIONAL_UNARY)
    private SlingRepository repository;

    public ExampleMBeanImpl() throws NotCompliantMBeanException {
        super(ExampleMBean.class);
    }

    public String getRepositoryName() {
        return repository.getDescriptor("jcr.repository.name");
    }

    public String getRepositoryVendor() {
        return repository.getDescriptor("jcr.repository.vendor");
    }

    public String getVendorUrl() {
        return repository.getDescriptor("jcr.repository.vendor.url");
    }
}
```

**多个MBean服务实例**

要管理托管服务的多个实例，请创建相应MBean服务的多个实例。 此外，在启动或停止受管实例时，应创建或删除MBean服务实例。 您可以创建一个MBean管理器类以在运行时实例化MBean服务，并管理服务生命周期。

使用BundleContext将MBean注册为OSGi服务。 在Dictionary对象中包含与JMX相关的信息，该对象用作BundleContext.registerService方法的参数。

在以下代码示例中，ExampleMBean服务以编程方式注册。 componentContext对象是ComponentContext，它提供对BundleContext的访问。

#### 代码片段：程序化MBean服务注册{#code-snippet-programmatic-mbean-service-registration}

```java
Dictionary mbeanProps = new Hashtable();
mbeanProps.put("jmx.objectname", "com.adobe.example:type=CRX");
ExampleMBeanImpl mbean = new ExampleMBeanImpl();
ServiceRegistration serviceregistration =
            componentContext.getBundleContext().registerService(DynamicMBean.class.getName(), mbean, mbeanProps);
```

下一节中的示例MBean提供了更多详细信息。

当服务配置存储在存储库中时， MBean服务管理器非常有用。 管理器可以检索服务信息，并使用它来配置和创建相应的MBean。 管理器类还可以监听存储库更改事件并相应地更新MBean服务。

## 示例：使用JMX {#example-monitoring-workflow-models-using-jmx}监控工作流模型

此示例中的MBean提供了有关存储在存储库中的CQ5工作流模型的信息。 MBean管理器类基于存储在存储库中的工作流模型创建MBean，并在运行时注册其OSGi服务。 此示例由包含以下成员的单个包组成：

* 工作流MBean:管理界面。
* WorkflowMBeanImpl:MBean实现类。
* WorkflowMBeanManager:MBean管理器类的接口。
* WorkflowMBeanManagerImpl:MBean管理器的实现类。

**注意：** 为简便起见，此示例中的代码不执行日志记录或对引发的异常做出反应。

WorkflowMBeanManagerImpl包括组件激活方法。 激活组件后，方法将执行以下任务：

* 获取包的包上下文。
* 查询存储库以获取现有工作流模型的路径。
* 为每个工作流模型创建MBean。
* 在OSGi服务注册表中注册MBean。

MBean元数据以com.adobe.example域显示在JMX控制台中，workflow_model类型，“属性”是工作流模型配置节点的路径。

![jmxworkflowbean](assets/jmxworkflowmbean.png)

### 示例MBean {#the-example-mbean}

此示例需要一个MBean接口和实现，该接口和实现在`com.day.cq.workflow.model.WorkflowModel`接口上进行反映。 MBean非常简单，因此示例可以专注于设计的配置和部署方面。 MBean会公开单个属性（模型名称）。

#### WorkflowMBean接口{#workflowmbean-interface}

```java
package com.adobe.example.myapp.api;

import com.adobe.granite.jmx.annotation.Description;

@Description("Example MBean that exposes Workflow model properties.")
public interface WorkflowMBean {

 @Description("The name of the Workflow model.")
 String getModelName();
}
```

#### WorkflowMBeanImpl {#workflowmbeanimpl}

```java
package com.adobe.example.myapp.impl;

import javax.management.NotCompliantMBeanException;

import com.day.cq.workflow.model.WorkflowModel;
import com.adobe.example.myapp.api.WorkflowMBean;
import com.adobe.granite.jmx.annotation.AnnotatedStandardMBean;

public class WorkflowMBeanImpl extends AnnotatedStandardMBean implements WorkflowMBean {

 WorkflowModel model;

 protected WorkflowMBeanImpl(WorkflowModel inmodel)
   throws NotCompliantMBeanException {
  super(WorkflowMBean.class);
  model=inmodel;
 }

 public String getModelName() {
  return model.getTitle();
 }
}
```

### 示例MBean管理器{#the-example-mbean-manager}

WorkflowMBeanManager服务包括用于创建WorkflowMBean服务的组件激活方法。 服务实施包括以下方法：

* 激活：组分激活器。 创建用于读取WorkflowModel配置节点的JCR会话。 存储模型配置的根节点在静态字段中定义。 配置节点的名称也会在静态字段中定义。 此方法将调用其他方法来获取节点模型路径并创建模型WorkflowMBeans。
* getModelIds:遍历根节点下的存储库并检索每个模型节点的路径。
* makeMBean:使用模型路径创建WorkflowModel对象，为其创建WorkflowMBean，并注册其OSGi服务。

>[!NOTE]
>
>WorkflowMBeanManager实施仅为激活组件时存在的模型配置创建MBean服务。 更可靠的实施监听与新模型配置有关的存储库事件以及现有模型配置的更改或删除。 当发生更改时，管理器可以创建、修改或删除相应的WorkflowMBean服务。


#### WorkflowMBeanManager接口{#workflowmbeanmanager-interface}

```java
package com.adobe.example.myapp.api;

public interface WorkflowMBeanManager {

}
```

#### WorkflowMBeanManagerImpl {#workflowmbeanmanagerimpl}

```java
package com.adobe.example.myapp.impl;

import java.util.*;

import org.apache.felix.scr.annotations.*;

import javax.jcr.Session;
import javax.jcr.Node;
import javax.jcr.NodeIterator;
import javax.jcr.RepositoryException;
import javax.management.ObjectName;

import org.apache.sling.jcr.api.SlingRepository;
import org.osgi.framework.ServiceRegistration;
import org.osgi.service.component.ComponentContext;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.workflow.WorkflowService;
import com.day.cq.workflow.WorkflowSession;
import com.adobe.example.myapp.api.WorkflowMBean;
import com.adobe.example.myapp.api.WorkflowMBeanManager;

/**Instantiates and registers WorkflowMBean services */
@Component(immediate=true)
@Service(value=WorkflowMBeanManager.class)
public class WorkflowMBeanManagerImpl implements WorkflowMBeanManager {
 //The ComponentContext provides access to the BundleContext
 private ComponentContext componentContext;

 //Use the SlingRepository service to read model nodes
 @Reference
        private SlingRepository repository = null;

 //Use the WorkflowService service to create WorkflowModel objects
 @Reference
 private WorkflowService workflowservice = null;

  private Session session;

         //Details about model nodes
  private static final String MODEL_ROOT ="/etc/workflow/models";
  private static final String MODEL_NODE = "model";

  private Set<String> modelIds = new HashSet<String>();

        //Storage for ServiceRegistrations for MBean services
  private Collection<ServiceRegistration> mbeanRegistrations= new Vector<ServiceRegistration>(0,1);

 @Activate
        protected void activate(ComponentContext ctx) {
             //Traverse the repository and load the model nodes
             try {
                   session = repository.loginAdministrative(null);
                   // load and store model node paths
                   if (session.nodeExists(MODEL_ROOT)) {
                          getModelIds(session.getNode(MODEL_ROOT));
                   }
                   //Create MBeans for each model
                   for(String modid: modelIds){
                    makeMBean(modid);
                    }
             }catch(Exception e){ }
          }

        /**
         * Add JMX domain and key properties to a collection
         * Instantiate a WorkflowModel and its WorkflowMBeanImpl object
         * Register the MBean OSGi service
         */
 private void makeMBean(String modelId) {
             // create MBean for the model
             try {
                 Dictionary<String, String> mbeanProps = new Hashtable<String, String>();
                 //These properties appear on the JMX Console home page
                 mbeanProps.put("jmx.objectname", "com.adobe.example:type=workflow_model,id=" + ObjectName.quote(modelId));
                 WorkflowSession wfsession = workflowservice.getWorkflowSession(session);
                 WorkflowMBeanImpl mbean = new WorkflowMBeanImpl(wfsession.getModel(modelId));

                ServiceRegistration serviceregistration = componentContext.getBundleContext().registerService(WorkflowMBean.class.getName(), mbean, mbeanProps);
                //Store the ServiceRegistration objects for deactivation
                mbeanRegistrations.add(serviceregistration);
             } catch (Throwable t) {}
         }

        /**
         * Traverses the repository branch below a given Node. Stores the path of each model node.
         */
 private void getModelIds(Node node) throws RepositoryException {
  try{
                     NodeIterator iter = node.getNodes();
                     while (iter.hasNext()) {
                           Node n = iter.nextNode();
                           //Look for "jcr:content" nodes
                           if (n.getName().equals("jcr:content")) {
                                //get the path of the model node and save it
                                if(n.hasNode(MODEL_NODE)){
                                      modelIds.add(n.getNode(MODEL_NODE).getPath());
                                 }
                           } else{
                                   //Scan child nodes
                                   getModelIds(n);
                           }
                       }
  }catch(Exception e){ }
       }

        /**
         * Log out of the JCR session and unregister WorkflowMBean services
         */
        @Deactivate
        protected void deactivate() {
          session.logout();
          session=null;
          for(ServiceRegistration sr:mbeanRegistrations){
         sr.unregister();
          }
        }
}
```

### 示例MBean {#the-pom-file-for-the-example-mbean}的POM文件

为方便起见，您可以将以下XML代码复制并粘贴到项目pom.xml文件中，以构建组件包。 POM会引用多个必需的插件和依赖项。

**插件:**

* Apache Maven Compiler Plugin:从源代码编译Java类。
* Apache Felix Maven捆绑包插件：创建包和清单
* Apache Felix Maven SCR插件：创建组件描述符文件并配置服务组件清单标头。

**注意：** 在编写时，maven scr插件与用于Eclipse的m2e插件不兼容。（请参阅[Felix bug 3170](https://issues.apache.org/jira/browse/FELIX-3170)。） 要使用Eclipse IDE，请安装Maven并使用命令行界面执行生成。

#### 示例POM文件{#example-pom-file}

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.2-SNAPSHOT</version>
  <name>mbean-simple</name>
  <url>www.adobe.com</url>
  <description>A simple MBean</description>
  <packaging>bundle</packaging>
    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
    <build>
        <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <configuration>
                <source>1.5</source>
                <target>1.5</target>
            </configuration>
        </plugin>
            <plugin>
                <groupId>org.apache.felix</groupId>
                <artifactId>maven-scr-plugin</artifactId>
                <version>1.7.2</version>
                <executions>
                    <execution>
                        <id>generate-scr-scrdescriptor</id>
              <goals>
                 <goal>scr</goal>
              </goals>
            </execution>
         </executions>
            </plugin>
             <plugin>
            <groupId>org.apache.felix</groupId>
            <artifactId>maven-bundle-plugin</artifactId>
            <version>1.4.3</version>
            <extensions>true</extensions>
            <configuration>
                <instructions>
                    <Export-Package>com.adobe.example.myapp.*;version=${project.version}</Export-Package>
                </instructions>
            </configuration>
        </plugin>
        </plugins>
    </build>
    <dependencies>
        <dependency>
            <groupId>org.apache.felix</groupId>
            <artifactId>org.apache.felix.scr.annotations</artifactId>
            <version>1.6.0</version>
            <scope>provided</scope>
        </dependency>
         <dependency>
            <groupId>org.apache.sling</groupId>
            <artifactId>org.apache.sling.api</artifactId>
            <version>2.0.8</version>
            <scope>provided</scope>
        </dependency>
         <dependency>
            <groupId>org.apache.felix</groupId>
            <artifactId>org.apache.felix.scr</artifactId>
            <version>1.6.1-R1236132</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.apache.sling</groupId>
            <artifactId>org.apache.sling.jcr.api</artifactId>
            <version>2.0.4</version>
        </dependency>
        <dependency>
            <groupId>com.adobe.granite</groupId>
            <artifactId>com.adobe.granite.jmx</artifactId>
            <version>0.1.6</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
       <groupId>com.day.cq.wcm</groupId>
       <artifactId>cq-wcm-mobile-api</artifactId>
       <version>5.5.2</version>
       <scope>provided</scope>
      </dependency>
      <dependency>
       <groupId>com.day.cq.workflow</groupId>
       <artifactId>cq-workflow-api</artifactId>
       <version>5.5.0</version>
       <scope>provided</scope>
      </dependency>
      <dependency>
       <groupId>javax.jcr</groupId>
       <artifactId>jcr</artifactId>
       <version>2.0</version>
       <scope>provided</scope>
      </dependency>
      <dependency>
                <groupId>org.slf4j</groupId>
  <artifactId>slf4j-api</artifactId>
  <version>1.6.4</version>
  <scope>provided</scope>
 </dependency>
    </dependencies>
</project>
```

将以下配置文件添加到Maven设置文件中，以使用公共Adobe存储库。

#### Maven配置文件{#maven-profile}

```xml
<profile>
    <id>adobe-public</id>
    <activation>
         <activeByDefault>false</activeByDefault>
    </activation>
    <properties>
         <releaseRepository-Id>adobe-public-releases</releaseRepository-Id>
         <releaseRepository-Name>Adobe Public Releases</releaseRepository-Name>
         <releaseRepository-URL>https://repo.adobe.com/nexus/content/groups/public</releaseRepository-URL>
    </properties>
    <repositories>
         <repository>
             <id>adobe-public-releases</id>
             <name>Adobe Basel Public Repository</name>
             <url>https://repo.adobe.com/nexus/content/groups/public</url>
             <releases>
                 <enabled>true</enabled>
                 <updatePolicy>never</updatePolicy>
             </releases>
             <snapshots>
                 <enabled>false</enabled>
             </snapshots>
         </repository>
     </repositories>
     <pluginRepositories>
         <pluginRepository>
             <id>adobe-public-releases</id>
             <name>Adobe Basel Public Repository</name>
             <url>https://repo.adobe.com/nexus/content/groups/public</url>
             <releases>
                 <enabled>true</enabled>
                 <updatePolicy>never</updatePolicy>
             </releases>
             <snapshots>
                 <enabled>false</enabled>
             </snapshots>
         </pluginRepository>
     </pluginRepositories>
</profile>
```
