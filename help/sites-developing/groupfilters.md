---
title: 建立裝置群組篩選器
seo-title: Creating Device Group Filters
description: 建立裝置群組篩選器，以定義一組裝置功能需求
seo-description: Create a device group filter to define a set of device capability requirements
uuid: 30c0699d-2388-41b5-a062-f5ea9d6f08bc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 9fef1f91-a222-424a-8e20-3599bedb8b41
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/groupfilters
exl-id: 419d2e19-1198-4ab5-9aa0-02ad18fe171d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 0%

---

# 建立裝置群組篩選器{#creating-device-group-filters}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

建立裝置群組篩選器，以定義一組裝置功能需求。 建立您需要的篩選器，以鎖定所需的裝置功能群組。

設計篩選器以便使用它們的組合來定義功能群組。 通常，不同裝置群組的功能會重疊。 因此，您可能會使用具有多個裝置群組定義的篩選器。

建立篩選器後，您可在以下位置使用它： [群組設定。](/help/sites-developing/mobile.md#creating-a-device-group)

## 篩選器Java類別 {#the-filter-java-class}

裝置群組篩選器是實作的OSGi元件 [com.day.cq.wcm.mobile.api.device.DeviceGroupFilter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html) 介面。 部署後，實作類別會提供裝置群組設定可用的篩選服務。

本文所述的解決方案使用Apache Felix Maven SCR外掛程式來促進元件和服務的開發。 因此，範例Java類別會使用 `@Component`和 `@Service` 註解。 類別具有下列結構：

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

您必須提供下列方法的程式碼：

* `getDescription`：傳回篩選器說明。 說明會顯示在「裝置群組設定」對話方塊中。
* `getTitle`：傳回篩選的名稱。 選取裝置群組的篩選器時，名稱就會出現。
* `matches`：判斷裝置是否具備必要的功能。

### 提供篩選器名稱和說明 {#providing-the-filter-name-and-description}

此 `getTitle` 和 `getDescription` 方法會分別傳回篩選器名稱和說明。 下列程式碼說明最簡單的實施：

```java
public String getDescription() {
    return "An example device group filter";
}

public String getTitle() {
 return "myFilter";
}
```

以硬式編碼撰寫名稱和說明文字，已足以用於單一語言的撰寫環境。 請考慮將字串外部化以供多語言使用，或啟用變更字串而不重新編譯原始程式碼。

### 根據篩選條件進行評估 {#evaluating-against-filter-criteria}

此 `matches` 函式傳回 `true` 如果裝置功能滿足所有篩選條件。 評估方法引數中提供的資訊，以判斷裝置是否屬於群組。 下列值會提供為引數：

* devicegroup物件
* 使用者代理程式的名稱
* 包含裝置功能的對映物件。 Map索引鍵是WURFL™功能名稱，值是WURFL™資料庫的對應值。

此 [com.day.cq.wcm.mobile.api.devicespecs.DeviceSpecsConstants](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html) 介麵包含靜態欄位中WURFL™功能名稱的子集。 從裝置功能對應擷取值時，使用這些欄位常數作為索引鍵。

例如，下列程式碼範例會判斷裝置是否支援CSS：

```xml
boolean cssSupport = true;
cssSupport = NumberUtils.toInt(capabilities.get(DeviceSpecsConstants.DSPEC_XHTML_SUPPORT_LEVEL)) > 1;
```

此 `org.apache.commons.lang.math` 套件提供 `NumberUtils` 類別。

>[!NOTE]
>
>確保部署到AEM的WURFL™資料庫包含您用作篩選條件的功能。 (請參閱 [裝置偵測](/help/sites-developing/mobile.md#server-side-device-detection).)

### 熒幕大小篩選範例 {#example-filter-for-screen-size}

後續的範例DeviceGroupFilter實作會決定裝置的實體大小是否符合最低需求。 此篩選器的用途是新增詳細程度至觸控裝置群組。 無論實體熒幕大小為何，應用程式UI中的按鈕大小都應相同。 其他專案（例如文字）的大小會有所不同。 此篩選器可讓您動態選取特定CSS，以控制UI元素的大小。

此篩選器會將大小條件套用至 `physical_screen_height` 和 `physical_screen_width` WURFL™屬性名稱。

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

getTitle方法傳回的字串值會顯示在裝置群組屬性的下拉式清單中。

![filteraddtogroup](assets/filteraddtogroup.png)

getTitle和getDescription方法傳回的String值會包含在裝置群組摘要頁面的底部。

![篩選器說明](assets/filterdescription.png)

### Maven POM檔案 {#the-maven-pom-file}

如果您使用Maven建置應用程式，以下POM程式碼會很實用。 POM會參照數個必要的外掛程式和相依性。

**插件:**

* Apache Maven編譯器外掛程式：從原始程式碼編譯Java類別。
* Apache Felix Maven套件組合外掛程式：建立套件組合和資訊清單
* Apache Felix Maven SCR外掛程式：建立元件描述項檔案並設定服務元件資訊清單標頭。

**依赖项:**

* `cq-wcm-mobile-api-5.5.2.jar`：提供DeviceGroup和DeviceGroupFilter介面。

* `org.apache.felix.scr.annotations.jar`：提供元件和服務註解。

DeviceGroup和DeviceGroupFilter介面包含在Day Communique 5 WCM Mobile API套件組合中。 Felix註解包含在Apache Felix宣告式服務套件組合中。 您可以從公用Adobe存放庫取得此JAR檔案。

編寫時，5.5.2是AEM最新版本中的WCM Mobile API套件組合版本。 使用AdobeWeb主控台([https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles))以確保這是部署在您的環境中的套件組合版本。

**POM：** （您的POM將使用不同的groupId和版本。）

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

新增設定檔， [取得內容套件Maven外掛程式](/help/sites-developing/vlt-mavenplugin.md) 一節會提供您的maven設定檔案來使用公共Adobe存放庫。
