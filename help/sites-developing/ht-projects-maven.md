---
title: 如何使用Apache Maven构建AEM项目
seo-title: 如何使用Apache Maven构建AEM项目
description: 本文档介绍如何设置基于Apache Maven的AEM项目
seo-description: 本文档介绍如何设置基于Apache Maven的AEM项目
uuid: 5db68639-7393-48b7-9d81-5b19b596ff21
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 3ebc1d22-a7a2-4375-9aa5-a18a7ceb446a
docset: aem65
translation-type: tm+mt
source-git-commit: 90d69ef0ed0fb38bec75a3d36982f80b85dd43af

---


# 如何使用Apache Maven构建AEM项目{#how-to-build-aem-projects-using-apache-maven}

## 概述 {#overview}

本文档介绍如何设置基于 [Apache Maven的AEM项目](https://maven.apache.org/)。

Apache Maven是一个开放源代码工具，用于通过自动化构建和提供高质量的项目信息来管理软件项目。 它是AEM项目的推荐构建管理工具。

基于Maven构建AEM项目为您提供了多项优势：

* 不受IDE限制的开发环境
* Adobe提供的Maven原型和人工物品的使用
* 将Apache Sling和Apache Felix工具集用于基于Maven的开发设置
* 轻松导入IDE;例如，Eclipse和／或IntelliJ
* 与连续集成系统轻松集成

### Maven Project Archetypes {#maven-project-archetypes}

Adobe提供两种Maven原型，可用作AEM项目的基线。 请参阅以下链接的更多详细信息：

* [AEM项目原型](https://github.com/adobe/aem-project-archetype)
* [Maven archetype for Single Page Applications Starter Kit](https://github.com/adobe/aem-spa-project-archetype)

## Experience Manager API依赖关系 {#experience-manager-api-dependencies}

### 什么是UberJar? {#what-is-the-uberjar}

“UberJar”是Adobe提供的特殊Java存档(JAR)文件的非正式名称。 这些JAR文件包含Adobe Experience manager公开的所有公共Java API。 它们还包括有限的外部库，特别是AEM中可用的所有公共API，这些API来自Apache Sling、Apache Jackrabbit、Apache Lucene、Google Guava以及两个用于图像处理的库（Werner Randelshofer的CYMK JPEG imageIO库和TwelveMexe图像库）。 UberJar仅包含API接口和类，这意味着它们只包含由AEM中的OSGi捆绑导出的接口和类。 它们还包含 *MANIFEST.MF* 文件，其中包含所有这些导出包的正确包导出版本，从而确保基于UberJar构建的项目具有正确的包导入范围。

### 为什么Adobe会创建UberJar? {#why-did-adobe-create-the-uberjars}

过去，开发人员必须管理与不同AEM库相对较多的单个依赖关系，并且当使用每个新API时，必须向项目添加一个或多个单个依赖关系。 在一个项目中，UberJar的推出导致从项目中删除了30个单独的依赖项。

从AEM 6.5开始，Adobe提供两个UberJar:一个包含已弃用的接口，另一个用于删除那些已弃用的接口。 通过在构建时显式引用一个代码，客户一定要了解他们是否对已弃用的代码具有依赖关系。

第二个Uber Jar删除了任何已弃用的类、方法和属性，这样客户就可以针对这些类、方法和属性进行编译，并了解自定义代码是否是将来的证明。

### 哪个UberJar可用？ {#which-uberjar-to-use}

AEM 6.5有两种Uber Jar:

1. Uber Jar —— 仅包括未标记为弃用的公共接口。 这是建议 **的** UberJar，因为它可帮助防将来使用的代码库不再依赖已弃用的API。
1. 包含已弃用API的Uber Jar —— 包括所有公共接口，包括在AEM的将来版本中标记为弃用的接口。

### 我如何使用UberJar? {#how-to-i-use-the-uberjars}

如果您将Apache Maven用作构建系统（大多数AEM java项目都是这样），您将需要向 *pom.xml文件添加一两个元素* 。 第一个是将实际 *依赖关系添加* 到项目的依赖关系元素：

**Uber Jar依赖关系(*不包含已弃用的API)***

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

**已弃用API的Uber Jar依赖性**

>[!CAUTION]
>
>Adobe建议针对**不&#x200B;*包含已弃用* **的Uber Jar进行部署，以确保您的应用程序在未来版本的AEM上正常运行。
>
>仅当无法修改依赖已弃用API的代码以适应更改时，才使用包含已弃用API支持的Uber Jar。

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis-with-deprecations</classifier>
    <scope>provided</scope>
</dependency>
```

如果您的公司已在使用Maven Repository Manager（如Sonatype Nexus、Apache Archiva或JFrog Artifactory），请向您的项目添加相应的配置以引用此存储库管理器，并将Adobe的Maven存储库([https://repo.adobe.com/nexus/content/groups/public/](https://repo.adobe.com/nexus/content/groups/public/))添加到您的存储库管理器。

如果您没有使用存储库管理器，则需要将存储库元 *素添加* 到 *pom.xml文件中* :

```xml
<repositories>
    <repository>
        <id>adobe-public-releases</id>
        <name>Adobe Public Repository</name>
        <url>https://repo.adobe.com/nexus/content/groups/public/</url>
        <layout>default</layout>
    </repository>
</repositories>
<pluginRepositories>
    <pluginRepository>
        <id>adobe-public-releases</id>
        <name>Adobe Public Repository</name>
        <url>https://repo.adobe.com/nexus/content/groups/public/</url>
        <layout>default</layout>
    </pluginRepository>
</pluginRepositories>
```

### UberJar有什么用？ {#what-can-i-do-with-the-uberjar}

使用UberJar，您可以编译依赖于AEM API（和上述项目使用的API）的项目代码。 您还可以生成OSGi服务组件运行时(SCR)和OSGi元类型信息。 有了一些限制，您还可以编写和执行单元测试。

### UberJar怎么办？ {#what-can-t-i-do-with-the-uberjar}

由于UberJar仅包 **含** API，因此它不可执行，并且不能用于 **运行** Adobe Experience Manager。 要运行AEM，您需要AEM快速入门(单机或Web应用程序存档(WAR)表单)。

### 您提到了对单元测试的限制。 请进一步说明。 {#you-mentioned-limitations-on-unit-tests-please-explain-further}

单元测试通常以三种不同的方式与产品API交互，每种方式受UberJar的影响略有不同。

#### 用例#1 —— 调用API界面的自定义代码 {#use-case-custom-code-which-calls-a-api-interface}

这种情况最常见，它涉及一些自定义代码，这些代码在AEM API定义的Java界面上执行方法。 该接口的实现可以直接提供或使用依赖注入模式注入。 **此使用案例可通过UberJar处理。**

前者的一个例子是：

```java
public class ClassWhichHasAEMInterfacePassedIn {
    /**
     * Get the first length characters of the page title.
     */
    public String getTrimmedTitle(Page page, int length) {
         String title = page.getTitle();
         return StringUtils.left(title, length);
    }
}
```

后者的一个例子是：

```java
@Component
@Service
public class ComponentWhichHasAEMInterfaceInjected implements TitleTrimmer {
    @Reference
    private PageManagerFactory pageManagerFactory;

    /**
     * Get the first length characters of the title of the page containing the provided Resource.
     */
    public String getTrimmedTitle(Resource resource, int length) {
        PageManager pageManager = pageManagerFactory.getPageManager(resource.getResourceResolver());
        Page page = pageManager.getContainingPage(resource);
        if (page == null) {
           return null;
        }
        String title = page.getTitle();
        return StringUtils.left(title, length);
    }
}
```

要单元测试其中任一方法，开发人员应使用模仿框架(如 [JMockit](http://jmockit.github.io)、 [Mockito](https://mockito.org/)、 [JMock](https://www.jmock.org/)[](https://easymock.org/) 或Easymock)为引用的AEM API创建模拟对象。 这些范例使用JMockit，但对于这个特殊用例，这些框架之间的差异基本上是同义的。

```java
@RunWith(JMockit.class)
public class ClassWhichHasAEMInterfacePassedInTest {

    @Tested
    private ClassWhichHasAEMInterfacePassedIn instance;

    @Mocked
    private Page page;

    @Test
    public void test_that_long_string_is_trimmed() {
        new Expectations() {{
            page.getTitle();
            result = "a really really really really really long string";
        }};
        assertEquals("a really", instance.getTrimmedTitle(page, 8));
    }
}
```

```java
@RunWith(JMockit.class)
public class ComponentWhichHasAEMInterfaceInjectedTest {

    @Tested
    private ComponentWhichHasAEMInterfaceInjected instance;

    @Mocked
    private Page page;

    @Mocked
    private PageManager pageManager;

    @Injectable
    private PageManagerFactory pageManagerFactory;

    @Mocked
    private Resource resource;

    @Mocked
    private ResourceResolver resourceResolver;

    @Test
    public void test_that_long_string_is_trimmed() {
        new Expectations() {{
            resource.getResourceResolver();
            result = resourceResolver;
            pageManagerFactory.getPageManager(resourceResolver);
            result = pageManager;
            pageManager.getContainingPage(resource);
            result = page;
            page.getTitle();
            result = "a really really really really really long string";
        }};
        assertEquals("a really", instance.getTrimmedTitle(resource, 8));
    }
}
```

#### 用例#2 —— 调用API实现类的自定义代码 {#use-case-custom-code-which-calls-an-api-implementation-class}

此用例涉及调用AEM API中某个类的静态或实例方法，在该方法中您引用的是具体类，而与用例#1中的接口相反。

```java
public class ClassWhichUsesAStaticMethodFromAPI {

    /**
     * Get a map of asset titles to asset objects.
     *
     * @param resource either an asset resource or a folder containing assets.
     * @return an map of titles to assets. if an asset doesn't have a title, the name is used instead.
     */
    public Map<String, Asset> getAssetTitles(Resource resource) {
        Iterator<Asset> assets = DamUtil.getAssets(resource);
        Map<String, Asset> result = new HashMap<String, Asset>();
        while (assets.hasNext()) {
            Asset asset = assets.next();
            String title = asset.getMetadataValue(DamConstants.DC_TITLE);
            if (title == null) {
                title = asset.getName();
            }
            result.put(title, asset);
        }
        return result;
    }
}
```

```java
public class ClassWhichUsesAnInstanceMethodFromAPI {

    /**
     * Count the number of paragraphs in a parsys.
     *
     * @param resource the parsys resource
     * @return the count
     */
    public int countParagraphs(Resource resource) {
        return new ParagraphSystem(resource).paragraphs().size();
    }
}
```

**此使用案例可通过UberJar处理**。 但是，仍建议在性能测试中尽可能模仿API。

```java
@RunWith(JMockit.class)
public class ClassWhichUsesAStaticMethodFromAPITest {

    @Tested
    private ClassWhichUsesAStaticMethodFromAPI instance;

    @Mocked(stubOutClassInitialization = true)
    private DamUtil unusedDamUtil = null;

    @Mocked
    private Resource resource;

    @Test
    public void test_that_empty_iterator_produces_empty_map() {
        new Expectations() {
            {
                DamUtil.getAssets(resource);
                result = Collections.<Asset> emptySet().iterator();
            }
        };
        Map<String, Asset> result = new ClassWhichUsesAStaticMethodFromAPI().getAssetTitles(resource);
        assertNotNull(result);
        assertEquals(0, result.size());
    }
    @Test
    public void test_with_reference_search() {
        assertTrue(true);
    }
}
```

```java
@RunWith(JMockit.class)
public class ClassWhichUsesAnInstanceMethodFromAPITest {

    @Tested
    private ClassWhichUsesAnInstanceMethodFromAPI instance;

    @Mocked
    private Resource parsys;

    @Mocked
    private Paragraph firstPar;

    @Mocked
    private Paragraph secondPar;

    @Test
    public void test_empty_parsys_returns_zero() {
        new MockUp<ParagraphSystem>() {
            @Mock
            public void $init(Resource resource) {
                assertEquals(parsys, resource);
            }
            @Mock
            public List<Paragraph> paragraphs() {
                return Collections.<Paragraph> emptyList();
            }
        };
        assertEquals(0, instance.countParagraphs(parsys));
    }
}
```

#### 用例#3 —— 从API扩展基类的自定义代码 {#use-case-custom-code-which-extends-a-base-class-from-the-api}

与SCR生成一样，如果代码从AEM API扩展基类（抽象或具体），则必须 **使** 用UberJar才能对其进行测试。

## 使用Maven的常见开发任务 {#common-development-tasks-with-maven}

### 如何向内容模块添加路径 {#how-to-add-paths-to-the-content-module}

内容模块包含一个文件src/main/content/META-INF/vault/filter.xml，该文件为Maven构建的AEM包定义过滤器。 由Maven原型创建的文件如下所示：

#### src/main/content/META-INF/vault/filter.xml {#src-main-content-meta-inf-vault-filter-xml}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

此文件的使用方式有许多不同：

* 确定 `content-package-maven-plugin` 要包含在包中的内容
* 由VLT工具确定要考虑的路径
* 如果在AEM包管理器中重新构建包，则还定义要包括的路径

根据应用程序的要求，您可能希望向这些路径添加更多内容，例如：

* 转出配置
* Blueprint
* 工作流模型
* 设计页面
* 示例内容

要添加到路径，请添加更多元 `<filter>` 素：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
    <filter root="/etc/msm/rolloutconfigs/myrolloutconfig"/>
    <filter root="/etc/blueprints/mysite/globalsite"/>
    <filter root="/etc/workflow/models/myproject"/>
    <filter root="/etc/designs/myproject"/>
    <filter root="/content/myproject/sample-content"/>
</workspaceFilter>
```

#### 在不同步的情况下添加包路径 {#adding-paths-to-the-package-without-syncing-them}

如果应将文件添加到由content-package-maven-plugin构建的包中，但不应在文件系统和存储库之间同步，则可以使用文 `.vltignore` 件。 这些文件的语法与。gitignore [文件相同](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html) 。

例如，原型使用文 `.vltignore` 件来防止作为包的一部分安装的JAR文件同步回文件系统：

#### src/main/content/jcr_root/apps/myproject/install/.vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore}

```xml
*.jar
```

#### 在不将路径添加到包的情况下同步路径 {#syncing-paths-without-adding-them-to-the-package}

在某些情况下，您可能希望在文件系统和存储库之间保持特定路径的同步，但不要将这些路径包含在要安装到AEM中的包中。

典型情况是路径 `/libs/foundation` 问题。 出于开发目的，您可能希望在文件系统中提供此路径的内容，以便IDE能够解析包含JSP的JSP包含 `/libs`。 但是，您不希望将该部件包含在您构建的包中，因为该部件包 `/libs` 含产品代码，而自定义实施不得修改该产品代码。

为此，您可以提供一个文件 `src/main/content/META-INF/vault/filter-vlt.xml`。 如果此文件存在，则它将由VLT工具使用，例如，执行和时 `vlt up` 间 `vlt ci`，或设置时 `vlt sync` 间。 content-package-maven-plugin在创建包时将继续 `src/main/content/META-INF/vault/filter.xml` 使用文件。

例如，要使本地 `/libs/foundation` 可用于开发，但仅包含在包中， `/apps/myproject` 请使用以下两个文件。

#### src/main/content/META-INF/vault/filter.xml {#src-main-content-meta-inf-vault-filter-xml-1}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

#### src/main/content/META-INF/vault/filter-vlt.xml {#src-main-content-meta-inf-vault-filter-vlt-xml}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/libs/foundation"/>
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

您还需要重新配置maven-resources-plugin，以便不在包中包含这些文件：filter.xml文件在安装包时不会应用，但仅在使用包管理器重新构建包时才会应用。

相应地 `<resources>` 更改内容中的章节：

#### src/main/content/pom.xml {#src-main-content-pom-xml}

```xml
<!-- ... -->
<resources>
 <resource>
  <directory>src/main/content/jcr_root</directory>
  <filtering>false</filtering>
  <excludes>
   <exclude>**/.vlt</exclude>
   <exclude>**/.vltignore</exclude>
   <exclude>libs/</exclude>
  </excludes>
 </resource>
</resources>
<!-- ... -->
```

### How to Work with JSPs {#how-to-work-with-jsps}

到目前为止所述的Maven设置创建了一个内容包，该内容包还可以包括组件及其相应的JSP。 但是，Maven将它们视为属于内容包的任何其他文件，甚至不将它们识别为JSP。

生成的组件在AEM中工作一样，但使Maven了解JSP有两个主要优点

* 如果JSP包含错误，它允许Maven失败，这样，这些错误在构建时出现，而不是在AEM中首次编译时出现
* 对于可以导入Maven项目的IDE，这还支持JSP中的代码完成和标记库支持

启用此设置需要两件事：

1. 添加标签库依赖关系
1. 将JSP作为Maven编译过程的一部分进行编译

#### 添加标记库依赖关系 {#adding-tag-library-dependencies}

需要将以下依赖关系添加 `content` 到模块的POM中。

>[!NOTE]
>
>除非您按照上述导入 [AEM产品依赖关系中所述导入产品依赖关系](#importingaemproductdependencies) ，否则还需要将它们与与AEM设置相匹配的版本一起添加到父POM，如上面添加依赖关系中所 [述](#addingdependencies) 。 下面每个条目中的注释显示要在依赖关系查找器中搜索的包。

>[!NOTE]
>
>该 `com.adobe.granite.xssprotection` 伪像不包括在cq-quickstart-product-dependencies POM中，并且需要从依赖关系查找器获取的完全Maven坐标。

#### 将JSP编译为Maven编译阶段的一部分 {#compiling-jsps-as-part-of-the-maven-compile-phase}

要在Maven的阶段编译JSP, `compile` 我们使用Apache Sling的 [Maven JspC插件](https://sling.apache.org/documentation/development/jspc.html) ，如下所示：

* 我们为目标设置了一个执 `jspc` 行(默认情况下，该执行绑定到 `compile` 阶段，因此我们无需显式指定阶段)

* 我们告诉它编译 `${project.build.directory}/jsps-to-compile`
* 并将结果输 `${project.build.directory}/ignoredjspc` 出到(即 `myproject/content/target/ignoredjspc`)

* 我们设置maven-resources-plugin以将JSP复制到生成源阶段，并将其配置为不复制文件夹(因为这是AEM产品代码，我们既不希望产生用于我们项目编译的依赖关系，也不需要验证它是否进行了编译。 `${project.build.directory}/jsps-to-compile``libs/`

如上所述，我们的主要目标是验证JSP，并确保在构建过程包含错误时失败。 因此，我们将它们编译为一个被忽略的单独目录（事实上，稍后会立即删除，如您稍后所见）。

Maven JspC插件的结果也可以作为OSGi Bundle的一部分进行捆绑和部署，但这有其他含义和副作用，超出了验证JSP的目标。

为了实现从JSP编译的类的删除，我们设置了Maven Clean插件，如下所示。 如果要检查Maven jspC插件的结果，请在中运 `mvn compile` 行 `myproject/content` —之后，您将在中找到结果 `myproject/content/target/ignoredjspc`)。

#### myproject/content/pom.xml {#myproject-content-pom-xml}

```xml
<build>
  <!-- ... -->
  <plugins>
    <!-- ... -->
    <plugin>
      <artifactId>maven-resources-plugin</artifactId>
      <executions>
        <execution>
          <id>copy-resources</id>
          <phase>generate-sources</phase>
          <goals>
            <goal>copy-resources</goal>
          </goals>
          <configuration>
            <outputDirectory>${project.build.directory}/jsps-to-compile</outputDirectory>
            <resources>
              <resource>
                <directory>src/main/content/jcr_root</directory>
                <excludes>
                  <exclude>libs/**</exclude>
                </excludes>
              </resource>
            </resources>
          </configuration>
        </execution>
      </executions>
    </plugin>
    <plugin>
      <groupId>org.apache.sling</groupId>
      <artifactId>maven-jspc-plugin</artifactId>
      <version>2.0.6</version>
      <executions>
        <execution>
          <id>compile-jsp</id>
          <goals>
            <goal>jspc</goal>
          </goals>
          <configuration>
            <jasperClassDebugInfo>false</jasperClassDebugInfo>
            <sourceDirectory>${project.build.directory}/jsps-to-compile</sourceDirectory>
            <outputDirectory>${project.build.directory}/ignoredjspc</outputDirectory>
          </configuration>
        </execution>
      </executions>
    </plugin>
    <plugin>
      <artifactId>maven-clean-plugin</artifactId>
      <executions>
        <execution>
          <id>remove-compiled-jsps</id>
          <goals>
            <goal>clean</goal>
          </goals>
          <phase>process-classes</phase>
          <configuration>
            <excludeDefaultDirectories>true</excludeDefaultDirectories>
            <filesets>
              <fileset>
                <directory>${project.build.directory}/jsps-to-compile</directory>
                <directory>${project.build.directory}/ignoredjspc</directory>
              </fileset>
            </filesets>
          </configuration>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>
```

>[!NOTE]
>
>根据您是否实际在中使用JSP代码 `/libs` （即从中包括JSP），您需要优化要复制哪些JSP以进行编译。
>
>例如，如果您包括 `/libs/foundation/global.jsp`，则可以对以下配置而不是上面完全跳过 `maven-resources-plugin` 的配置进行使用 `/libs`。
>```
> <resource>  
>           <directory>src/main/content/jcr_root</directory>  
>           <includes>  
>                   <include>apps/**</include>  
>                   <include>libs/foundation/global.jsp</include>
>       </includes>  
>   </resource>  
>  ```

### 如何与SCM系统一起使用 {#how-to-work-with-scm-systems}

使用源配置管理(SCM)时，您需要确保

* VCS忽略文件系统中的非源对象
* VLT会忽略VCS的对象，但不会将其签入存储库

>[!NOTE]
>
>本说明不涵盖如何将Maven配置为与您的SCM一起使用， [Maven POM参考和](https://maven.apache.org/pom.html#SCM) Maven SCM插件文档中对此进行了详细说明 [](https://maven.apache.org/scm/)。

#### 从SCM中排除的模式 {#patterns-to-exclude-from-scm}

以下是SCM中要包含的典型模式列表。 例如，如果您使用git，则可以将这些内容添加到项目文 `.gitignore` 件。

#### 示例。gitignore {#sample-gitignore}

```shell
# Ignore VLT files
.vlt
.vlt-sync.log
.vlt-sync-config.properties

# Ignore Quickstart launches in the source tree
license.properties
crx-quickstart

# Ignore compilation results
target

# Ignore IDE and Operating System artifacts
.idea
.classpath
.metadata
.project
.settings
maven-eclipse.xml
*.iml
*.ipr
*.iws
.DS_Store
```

#### 忽略VLT中的单片机控制文件 {#ignoring-scm-control-files-in-vlt}

在某些情况下，内容源树中可能包含SCM控制文件，您不希望将其签入存储库。

请考虑以下情况：

原型已创建。vltignore文件，以防止已安装的bundle jar文件同步回文件系统：

#### src/main/content/jcr_root/apps/myproject/install/.vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore-1}

```shell
*.jar
```

显然，您也不希望在SCM中包含此文件，因此，如果您使用git，您将添加相应的文件。 `gitignore` 文件：

#### src/main/content/jcr_root/apps/myproject/install/.gitignore {#src-main-content-jcr-root-apps-myproject-install-gitignore}

```shell
*.jar
```

作为。 `gitignore` 文件也不应进入存储库， `vltignore` 需要扩展文件以包含。 `gitignore` 文件：

#### src/main/content/jcr_root/apps/myproject/install/.vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore-2}

```shell
*.jar
.gitignore
```

### 使用部署配置文件的方法 {#how-to-work-with-deployment-profiles}

如果您的构建过程是更大的开发生命周期管理设置（如连续集成过程）的一部分，则您通常需要部署到其他计算机，而不仅仅是开发人员的本地实例。

对于此类情况，您可以轻松地将新 [的Maven Build Profiles](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) 添加到项目的POM中。

以下示例添加了一个配置 `integrationServer`文件，该配置文件重新定义了作者实例和发布实例的主机名和端口。 您可以从项目根目录中运行maven来部署到这些服务器，如下所示。

```shell
# install on integration test author
$ mvn -PautoInstallPackage -PintegrationServer install

# install on integration test publisher
$ mvn -PautoInstallPackagePublish -PintegrationServer install
```

#### myproject/pom.xml {#myproject-pom-xml}

```xml
<profiles>

    <!-- ... -->

    <profile>
        <id>integrationServer</id>
        <properties>
            <crx.host>dev-author.intranet</crx.host>
            <crx.port>5502</crx.port>
            <publish.crx.host>dev-publish.intranet</publish.crx.host>
            <publish.crx.port>5503</publish.crx.port>
        </properties>
    </profile>
</profiles>
```

### 如何与AEM Communities一起使用 {#how-to-work-with-aem-communities}

获得AEM Communities功能的许可后，还需要额外的APIjar。

有关详细信息，请参 [阅使用Maven for Communities](/help/communities/maven.md)
