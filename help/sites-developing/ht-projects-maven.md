---
title: 如何使用Apache Maven构建AEM项目
seo-title: 如何使用Apache Maven构建AEM项目
description: 本文档介绍如何基于Apache Maven设置AEM项目
seo-description: 本文档介绍如何基于Apache Maven设置AEM项目
uuid: 5db68639-7393-48b7-9d81-5b19b596ff21
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 3ebc1d22-a7a2-4375-9aa5-a18a7ceb446a
docset: aem65
translation-type: tm+mt
source-git-commit: add17f46dfb292aeaf8425e5f75cfe955ed93cbc
workflow-type: tm+mt
source-wordcount: '2468'
ht-degree: 0%

---


# 如何使用Apache Maven构建AEM项目{#how-to-build-aem-projects-using-apache-maven}

## 概述 {#overview}

本文档介绍如何基于Apache Maven设置AEM [项目](https://maven.apache.org/)。

Apache Maven是一个开放源码工具，用于通过自动化构建和提供高质量项目信息来管理软件项目。 它是AEM项目的推荐构建管理工具。

基于Maven优惠构建AEM项目可为您带来以下几大好处：

* 与IDE无关的开发环境
* Maven原型和由Adobe提供的文物的使用
* 将Apache Sling和Apache Felix工具集用于基于Maven的开发设置
* 轻松导入IDE;例如，Eclipse和／或IntelliJ
* 与连续集成系统轻松集成

### Maven Project Archetypes {#maven-project-archetypes}

Adobe提供两种Maven原型，可用作AEM项目的基线。 请参阅以下链接，了解更多详细信息：

* [AEM项目原型](https://github.com/adobe/aem-project-archetype)
* [Maven原型，用于单页应用程序Starter Kit](https://github.com/adobe/aem-spa-project-archetype)

## Experience ManagerAPI依赖关系 {#experience-manager-api-dependencies}

### 什么是UberJar? {#what-is-the-uberjar}

“UberJar”是Adobe提供的特殊Java归档文件(JAR)文件的非正式名称。 这些JAR文件包含Adobe Experience Manager公开的所有公共Java API。 它们还包括有限的外部库，特别是AEM中提供的所有公共API，这些API来自Apache Sling、Apache Jackrabbit、Apache Lucene、Google Guava以及两个用于图像处理的库（Werner Randelshofer的CYMK JPEG ImageIO库和Twelkes图像库）。 UberJar只包含API接口和类，这意味着它们只包含由AEM中的OSGi捆绑导出的接口和类。 它们还包含一 *个MANIFEST.MF文件* ，其中包含所有这些导出包的正确包导出版本，从而确保基于UberJar构建的项目具有正确的包导入范围。

### Adobe为何创建UberJar? {#why-did-adobe-create-the-uberjars}

过去，开发人员必须管理到不同AEM库的相对大量的单个依赖关系，当使用每个新API时，必须向项目添加一个或多个单个依赖关系。 在一个项目中，引入UberJar导致从项目中删除30个单独的依赖项。

从AEM 6.5开始，Adobe提供了两个UberJar:一个包含已弃用的接口，另一个用于删除那些已弃用的接口。 通过在构建时显式引用一个代码，客户一定要了解他们是否对已弃用的代码具有依赖关系。

第二个Uber Jar删除了任何已弃用的类、方法和属性，使客户能够根据它们进行编译并了解自定义代码是否为将来的验证。

### 哪个UberJar可用？ {#which-uberjar-to-use}

AEM 6.5有两种Uber Jar:

1. Uber Jar —— 仅包括未标记为弃用的公共接口。 这是推荐 **的** UberJar，因为它可帮助将来验证代码库，避免依赖已弃用的API。
1. 包含已弃用API的Uber Jar —— 包括所有公共接口，包括在AEM的未来版本中标记为弃用的接口。

>[!NOTE]
>
>从AEM 6.5.6开始，UberJar和其他相关对象可在Maven Central存储库 [中使用](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/) ，而不是Adobe公共Maven存储库(repo.adobe.com)。 主UberJar文件已重命名为 `uber-jar-<version>.jar`。 因此，标签没 `classifier`有 `apis` 任何值（作为值） `dependency` 。

### 我如何使用UberJar? {#how-do-i-use-the-uberjars}

如果您将Apache Maven用作构建系统(大多数AEM Java项目都是如此)，您需要向pom.xml文件添加一 *两个元素* 。 第一个是将实际 *依赖关系* 添加到您的项目的依赖关系元素：

**Uber Jar依赖&#x200B;*关系（没有弃用的API）***

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
>Adobe建议针对**不包&#x200B;*含已弃* 用的API的Uber Jar进行部署，以确保您的应用程序在AEM的将来版本上正常运行。
>
>仅当无法修改依赖已弃用API的代码以适应更改时，才使用支持已弃用API的Uber Jar。

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis-with-deprecations</classifier>
    <scope>provided</scope>
</dependency>
```

如果公司已使用Maven Repository Manager（如Sonatype Nexus、Apache Archiva或JFrog Artifactory），请向项目添加适当的配置以引用此存储库管理器，并将Adobe的Maven Repository([https://repo.maven.apache.org/maven2/](https://repo.maven.apache.org/maven2/))添加到存储库管理器。

如果您没有使用存储库管理器，则需要向pom.xml文 *件中* 添加一 *个存储库元素* :

```xml
<repositories>
    <repository>
        <id>adobe-public-releases</id>
        <name>Adobe Public Repository</name>
        <url>https://repo.maven.apache.org/maven2/</url>
        <layout>default</layout>
    </repository>
</repositories>
<pluginRepositories>
    <pluginRepository>
        <id>adobe-public-releases</id>
        <name>Adobe Public Repository</name>
        <url>https://repo.maven.apache.org/maven2/</url>
        <layout>default</layout>
    </pluginRepository>
</pluginRepositories>
```

### UberJar有什么用？ {#what-can-i-do-with-the-uberjar}

借助UberJar，您可以编译依赖AEM API（以及上述项目使用的API）的项目代码。 您还可以生成OSGi服务组件运行时(SCR)和OSGi元类型信息。 有一些限制，您还可以编写和执行单元测试。

### UberJar怎么办？ {#what-can-t-i-do-with-the-uberjar}

由于UberJar仅 **包含** API，因此它不可执行，不能用于运 **行Adobe Experience Manager** 。 要运行AEM，您需要AEM快速入门(独立或Web 应用程序存档(WAR)表单)。

### 您提到了设备测试的限制。 请进一步说明。 {#you-mentioned-limitations-on-unit-tests-please-explain-further}

单元测试通常以三种不同的方式与产品API交互，每种方式受UberJar的影响都略有不同。

#### 用例#1 —— 调用API接口的自定义代码 {#use-case-custom-code-which-calls-a-api-interface}

这种情况下最常见的是一些自定义代码，它们在AEM API定义的Java界面上执行方法。 该接口的实现可以直接提供或使用依赖注入模式注入。 **此用例可通过UberJar处理。**

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

要单元测试其中任一方法，开发者应使用模 [拟框架](http://jmockit.github.io)(如 [JMockit](https://mockito.org/)、Mockito [、](https://www.jmock.org/)JMock [或Easymock)为引](https://easymock.org/) 用的AEM API创建模拟对象。 这些示例使用JMockit，但对于此特定用例，这些框架之间的差异在很大程度上是同步的。

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

此用例涉及调用AEM API中某个类的静态或实例方法，在该类中您引用的是具体类，而与用例#1中的接口相对。

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

**此用例可通过UberJar处理**。 但是，仍建议在可能的情况下模仿API进行性能测试。

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

#### 用例#3 —— 自定义代码，它从API扩展基类 {#use-case-custom-code-which-extends-a-base-class-from-the-api}

与SCR生成一样，如果代码从AEM API扩展基类（抽象或具体），则 **必须** 使用UberJar来测试它。

## 与Maven的常见开发任务 {#common-development-tasks-with-maven}

### 如何向内容模块添加路径 {#how-to-add-paths-to-the-content-module}

内容模块包含一个文件src/main/content/META-INF/vault/filter.xml，它定义由Maven构建的AEM包的过滤器。 由Maven原型创建的文件如下所示：

#### src/main/content/META-INF/vault/filter.xml {#src-main-content-meta-inf-vault-filter-xml}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

此文件有多种不同的使用方式：

* 确 `content-package-maven-plugin` 定要包含在包中的内容
* 由VLT工具确定要考虑的路径
* 如果在AEM Package Manager中重新构建包，则还定义要包括的路径

根据应用程序的要求，您可能希望添加到这些路径中以包含更多内容，如：

* 转出配置
* Blueprint
* 工作流模型
* 设计页面
* 示例内容

要添加到路径中，请添加更多 `<filter>` 元素：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
    <filter root="/content/myproject/sample-content"/>
</workspaceFilter>
```

#### 在未同步的情况下添加包的路径 {#adding-paths-to-the-package-without-syncing-them}

如果您的文件应该添加到由content-package-maven-plugin构建的包中，但不应在文件系统和存储库之间同步，则可以使用文 `.vltignore` 件。 这些文件的语法与。gitignore [文件的语](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html) 法相同。

例如，原型使用文 `.vltignore` 件来防止作为捆绑包的一部分安装的JAR文件同步回文件系统：

#### src/main/content/jcr_root/apps/myproject/install/.vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore}

```xml
*.jar
```

#### 在不将路径添加到包的情况下同步路径 {#syncing-paths-without-adding-them-to-the-package}

在某些情况下，您可能希望在文件系统和存储库之间保持特定路径的同步，但是不要将它们包含在构建为安装到AEM的包中。

典型情况是路 `/libs/foundation` 径。 出于开发目的，您可能希望在文件系统中提供此路径的内容，例如，您的IDE可以解析包含JSP的JSP包含 `/libs`。 但是，您不希望将该部件包含在您构建的包中，因为该部 `/libs` 件包含产品代码，而自定义实施不能修改该产品代码。

要实现此目的，您可以提供一个文件 `src/main/content/META-INF/vault/filter-vlt.xml`。 如果此文件存在，则它将由VLT工具使用，例如，执行和 `vlt up` 时 `vlt ci`或设置时 `vlt sync` 使用。 content-package-maven-plugin在创建包时将继续 `src/main/content/META-INF/vault/filter.xml` 使用文件。

例如，要使本地 `/libs/foundation` 可用进行开发，但只包含 `/apps/myproject` 在包中，请使用以下两个文件。

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

您还需要重新配置maven-resources-plugin，以不在包中包含这些文件：在安装包时不应用filter.xml文件，但仅当使用包管理器重新构建包时才应用filter.xml文件。

相应 `<resources>` 地更改内容中的部分：

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

到目前为止所描述的Maven设置创建了一个内容包，该内容包还可以包含组件及其相应的JSP。 但是，Maven将它们视为属于内容包的任何其他文件，甚至不将它们识别为JSP。

生成的组件在AEM中工作一样，但使Maven了解JSP有两个主要优点

* 如果JSP包含错误，它允许Maven失败，因此这些错误在构建时出现，而不是在AEM中首次编译时出现
* 对于可以导入Maven项目的IDE，这还支持JSP中的代码完成和标记库支持

启用此设置需要两件事：

1. 添加标记库依赖项
1. 将JSP作为Maven编译过程的一部分进行编译

#### 添加标记库依赖项 {#adding-tag-library-dependencies}

需要将以下依赖项添加 `content` 到模块的POM。

>[!NOTE]
>
>除非如上面的“导入AEM产品依赖关系 [”中所述导入产品依赖关系](#importingaemproductdependencies) ，否则还需要将它们与与AEM设置匹配的版本一起添加到父POM，如上面的添加依赖 [关系中所述](#addingdependencies) 。 以下每个条目中的注释显示要在依赖关系查找器中搜索的包。

>[!NOTE]
>
>该 `com.adobe.granite.xssprotection` 伪像不包括在cq-quickstart-product-dependencies POM中，并且需要从依赖关系查找器获取的完整Maven坐标。

#### 将JSP编译为Maven编译阶段的一部分 {#compiling-jsps-as-part-of-the-maven-compile-phase}

要在Maven阶段编译JSP, `compile` 我们使用Apache Sling的Maven [JspC插件](https://sling.apache.org/documentation/development/jspc.html) ，如下所示：

* 我们为目标设置 `jspc` 了执行(默认情况下，该 `compile` 执行绑定到阶段，因此我们无需显式指定阶段)

* 我们告诉它编译 `${project.build.directory}/jsps-to-compile`
* 并将结果输 `${project.build.directory}/ignoredjspc` 出到(即 `myproject/content/target/ignoredjspc`)

* 我们设置maven-resources-plugin以在“生成源” `${project.build.directory}/jsps-to-compile``libs/` 阶段将JSP复制到文件夹，并将其配置为不复制该文件夹(因为这是AEM产品代码，我们不想为我们的项目生成依赖项，也不需要验证它是否进行编译。

如上所述，我们的主要目标是验证JSP，并确保在生成过程包含错误时失败。 因此，我们将它们编译为一个被忽略的单独目录（事实上，稍后会立即删除，您将看到）。

Maven JspC插件的结果也可以作为OSGi Bundle的一部分进行捆绑和部署，但这有其他影响和副作用，超出了验证JSP的目标。

为了删除从JSP编译的类，我们设置了Maven Clean插件，如下所示。 如果要检查Maven JspC插件的结果，请在中 `mvn compile` 运 `myproject/content` 行——之后，您将在中找到结果 `myproject/content/target/ignoredjspc`)。

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
>根据您是否确实在中使 `/libs` 用JSP代码（即从中包括JSP），您需要优化要复制哪些JSP进行编译。
>
>例如，如果您包括 `/libs/foundation/global.jsp`，则可以对以下配置而 `maven-resources-plugin` 不是完全跳过上面的配置进行配置 `/libs`。
>
>
```
> <resource>  
>           <directory>src/main/content/jcr_root</directory>  
>           <includes>  
>                   <include>apps/**</include>  
>                   <include>libs/foundation/global.jsp</include>
>       </includes>  
>   </resource>  
>```

### 如何与SCM系统配合使用 {#how-to-work-with-scm-systems}

使用源配置管理(SCM)时，您需要确保

* VCS忽略文件系统中的非源对象
* VLT忽略VCS的工件，不将其签入存储库

>[!NOTE]
>
>本说明不涵盖如何配置Maven以与您的SCM配合使用，Maven POM参考和Maven SCM插 [件的文档对](https://maven.apache.org/pom.html#SCM)[此进行了详尽的说明](https://maven.apache.org/scm/)。

#### 从SCM排除的模式 {#patterns-to-exclude-from-scm}

以下是SCM中包含的典型模式列表。 例如，如果您使用git，则可以将这些内容添加到项目文 `.gitignore` 件。

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

在某些情况下，您可能在内容源树中有SCM控制文件，您不希望将其签入到存储库。

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

作为。 `gitignore` 文件也不应进入存储库。 `vltignore` 文件需要扩展以包含。 `gitignore` 文件：

#### src/main/content/jcr_root/apps/myproject/install/.vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore-2}

```shell
*.jar
.gitignore
```

### 如何与部署用户档案配合使用 {#how-to-work-with-deployment-profiles}

如果您的构建过程是较大的开发生命周期管理设置的一部分，例如连续集成过程，您通常需要部署到其他计算机，而不仅仅是开发人员的本地实例。

对于此类情况，您可以轻松地 [将新的Maven Build](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) 用户档案添加到项目的POM。

以下示例添加了一个用户档案 `integrationServer`，它重新定义了作者实例和发布实例的主机名和端口。 您可以通过从项目根目录运行maven来部署到这些服务器，如下所示。

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

### 如何与AEM Communities {#how-to-work-with-aem-communities}

获得AEM Communities功能许可后，需要额外的APIjar。

有关详细信息，请参 [阅将Maven用于社区](/help/communities/maven.md)
