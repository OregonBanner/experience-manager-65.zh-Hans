---
title: 创建设备组过滤器
seo-title: 创建设备组过滤器
description: 创建设备组过滤器以定义一组设备功能要求
seo-description: 创建设备组过滤器以定义一组设备功能要求
uuid: 30c0699d-2388-41b5-a062-f5ea9d6f08bc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 9fef1f91-a222-424a-8e20-3599bedb8b41
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/groupfilters
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 0%

---


# 创建设备组过滤器{#creating-device-group-filters}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

创建设备组过滤器以定义一组设备功能要求。 创建所需数量的过滤器以目标所需的设备功能组。

设计过滤器，以便使用它们的组合来定义功能组。 通常，不同设备组的功能存在重叠。 因此，您可能对多个设备组定义使用一些过滤器。

创建过滤器后，可以在[组配置中使用它。](/help/sites-developing/mobile.md#creating-a-device-group)

## 过滤器Java类{#the-filter-java-class}

设备组过滤器是实现[com.day.cq.wcm.mobile.api.device.DeviceGroupFilter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html)接口的OSGi组件。 部署后，实现类提供可用于设备组配置的过滤器服务。

本文描述的解决方案使用Apache Felix Maven SCR插件来促进组件和服务的开发。 因此，示例Java类使用`@Component`和`@Service`注释。 该类具有以下结构：

```java
package com.adobe.example.myapp;

import java.util.Map;

import com.day.cq.wcm.mobile.api.device.DeviceGroup;
import com.day.cq.wcm.mobile.api.device.DeviceGroupFilter;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

@Component(metatype = false)
@Service
public class myDeviceGroupFilter implements DeviceGroupFilter {

       public String getDescription() {
  return null;
 }

 public String getTitle() {
  return null;
 }

 public boolean matches(DeviceGroup arg0, String arg1, Map arg2) {
  return false;
 }

}
```

您需要为以下方法提供代码：

* `getDescription`:返回筛选器描述。说明显示在设备组配置对话框中。
* `getTitle`:返回筛选器的名称。为设备组选择过滤器时，将显示该名称。
* `matches`:确定设备是否具备所需的功能。

### 提供过滤器名称和说明{#providing-the-filter-name-and-description}

`getTitle`和`getDescription`方法分别返回筛选器名称和说明。 以下代码说明了最简单的实现：

```java
public String getDescription() {
    return "An example device group filter";
}

public String getTitle() {
 return "myFilter";
}
```

将名称和描述文本硬编码足以用于单语言创作环境。 请考虑将字符串外置以用于多语言使用，或启用字符串更改而不重新编译源代码。

### 根据筛选条件{#evaluating-against-filter-criteria}进行评估

如果设备功能满足所有筛选器条件，则`matches`函数返回`true`。 评估方法参数中提供的信息，以确定设备是否属于组。 以下值作为参数提供：

* DeviceGroup对象
* 用户代理的名称
* 包含设备功能的Map对象。 Map键是WURFL™功能名称，值是WURFL™数据库中的相应值。

[com.day.cq.wcm.mobile.api.deviceceps.DeviceSpecsConstants](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html)接口包含静态字段中WURFL™功能名称的子集。 从设备功能映射检索值时，请将这些字段常量用作键。

例如，以下代码示例确定设备是否支持CSS:

```xml
boolean cssSupport = true;
cssSupport = NumberUtils.toInt(capabilities.get(DeviceSpecsConstants.DSPEC_XHTML_SUPPORT_LEVEL)) > 1;
```

`org.apache.commons.lang.math`包提供`NumberUtils`类。

>[!NOTE]
>
>确保部署到AEM的WURFL™数据库包含用作筛选条件的功能。 （请参阅[设备检测](/help/sites-developing/mobile.md#server-side-device-detection)。）

### 屏幕大小{#example-filter-for-screen-size}的示例过滤器

下面的示例DeviceGroupFilter实现确定设备的物理大小是否满足最低要求。 此过滤器用于向触摸设备组添加粒度。 无论实际屏幕大小如何，应用程序UI中按钮的大小都应相同。 其他项目（如文本）的大小可能不同。 该滤镜允许动态选择控制UI元素大小的特定CSS。

此过滤器将大小条件应用于`physical_screen_height`和`physical_screen_width` WURFL™属性名称。

```java
package com.adobe.example.myapp;

import java.util.Map;

import com.day.cq.wcm.mobile.api.device.DeviceGroup;
import com.day.cq.wcm.mobile.api.device.DeviceGroupFilter;

import org.apache.commons.lang.math.NumberUtils;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

@Component(metatype = false)
@Service
@SuppressWarnings("unused")
public class ScreenSizeLarge implements DeviceGroupFilter {
    private int len=400;
    private int wid=200;
    public String getDescription() {

        return "Requires the physical size of the screen to have minimum dimensions " + len + "x" + wid+".";
    }

    public String getTitle() {
        return "Screen Size Large ("+len + "x" + wid+")";
    }

    public boolean matches(DeviceGroup deviceGroup, String userAgent,
            Map<String, String> deviceCapabilities) {

        boolean longEnough=true;
        boolean wideEnough=false;
        int dimension1=NumberUtils.toInt(deviceCapabilities.get("physical_screen_height"));
        int dimension2=NumberUtils.toInt(deviceCapabilities.get("physical_screen_width"));
        if(dimension1>dimension2){
            longEnough=dimension1>=len;
            wideEnough=dimension2>=wid;
        }else{
            longEnough=dimension2>=len;
            wideEnough=dimension1>=wid;
        }

        return longEnough && wideEnough;
    }
}
```

getTitle方法返回的字符串值显示在设备组属性的下拉列表中。

![filterdtogroup](assets/filteraddtogroup.png)

getTitle和getDescription方法返回的字符串值包含在设备组摘要页的底部。

![过滤器描述](assets/filterdescription.png)

### Maven POM文件{#the-maven-pom-file}

如果您使用Maven构建应用程序，以下POM代码非常有用。 POM引用了多个必需的插件和依赖项。

**插件:**

* Apache Maven Compiler Plugin:从源代码编译Java类。
* Apache Felix Maven Bundle Plugin:创建捆绑和清单
* Apache Felix Maven SCR插件：创建组件描述符文件并配置服务组件清单头。

**依赖关系:**

* `cq-wcm-mobile-api-5.5.2.jar`:提供DeviceGroup和DeviceGroupFilter接口。

* `org.apache.felix.scr.annotations.jar`:提供组件和服务注释。

DeviceGroup和DeviceGroupFilter接口包含在Day Commutle 5 WCM Mobile API包中。 Apache Felix Declationative Services捆绑包中包含Felix批注。 您可以从公共Adobe库获取此JAR文件。

在创作时，5.5.2是AEM最新版本中的WCM Mobile API包版本。 使用AdobeWeb控制台([https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles))确保这是在环境中部署的捆绑版本。

**POM:** （您的POM将使用不同的groupId和版本。）

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
        xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
      <groupId>com.adobe.example.myapp</groupId>
      <artifactId>devicefilter</artifactId>
      <version>0.0.1-SNAPSHOT</version>
      <name>my app device filter</name>
      <url>https://dev.day.com/docs/en/cq/current.html</url>
  <packaging>bundle</packaging>
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
         <groupId>com.day.cq.wcm</groupId>
         <artifactId>cq-wcm-mobile-api</artifactId>
         <version>5.5.2</version>
         <scope>provided</scope>
     </dependency>
     <dependency>
        <groupId>org.apache.felix</groupId>
        <artifactId>org.apache.felix.scr.annotations</artifactId>
        <version>1.6.0</version>
        <scope>compile</scope>
    </dependency>
</dependencies>
</project>
```

将[获取内容包Maven插件](/help/sites-developing/vlt-mavenplugin.md)部分提供的用户档案添加到主设置文件中以使用公共Adobe库。
