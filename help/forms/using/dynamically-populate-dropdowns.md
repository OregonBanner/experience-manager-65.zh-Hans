---
title: 動態填入下拉式清單
seo-title: Dynamically populating drop-down lists
description: 根據某些邏輯動態填入下拉式清單的程式
seo-description: Procedure to dynamically populate drop-down lists based on some logic
uuid: b3408aee-ac24-43af-a380-a5892abf0248
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: ad6db3fd-0d26-4241-bf73-be74b7f6e509
docset: aem65
exl-id: 64b88423-aaae-4258-bf48-73df5c9353ea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# 動態填入下拉式清單 {#dynamically-populating-drop-down-lists}

## 前提条件 {#prerequisites}

* [建立OSGI套件組合](https://helpx.adobe.com/experience-manager/using/creating-osgi-bundles-digital-marketing.html)
* [開發AEM元件](/help/sites-developing/components.md)
* [建立最適化表單](../../forms/using/creating-adaptive-form.md)
* [製作最適化表單](../../forms/using/introduction-forms-authoring.md)

## 動態填入下拉式清單的程式 {#procedure-to-dynamically-populate-drop-down-lists}

請考量您希望填入 **州** 下拉式清單的下拉式清單中，您所選取的 **國家** 下拉式清單。 如果您在「 」中選取「澳洲」 **國家** 下拉式清單、 **州** 下拉式清單會顯示澳洲境內的州。 下列程式說明如何完成此工作。

1. 建立專案並搭配下列模組：

   * 包含用來填入下拉式清單之邏輯的套件組合，在此例中為servlet。
   * 內嵌.jar檔案且具有下拉式資源的內容。 此servlet指向此資源。

1. 根據請求引數Country編寫servlet，這會傳回包含國家/地區內州名的陣列。

   ```java
   @Component(metatype = false)
   @Service(value = Servlet.class)
   @Properties({
           @Property(name = "sling.servlet.resourceTypes", value = "/apps/populatedropdown"),
           @Property(name = "sling.servlet.methods", value = {"GET", "POST"}),
           @Property(name = "service.description", value = "Populate states dropdown based on country value")
   })
   public class DropDownPopulator extends SlingAllMethodsServlet {
       private Logger logger = LoggerFactory.getLogger(DropDownPopulator.class);
   
       protected void doPost(SlingHttpServletRequest request,
                             final SlingHttpServletResponse response)
               throws ServletException, IOException {
           response.setHeader("Access-Control-Allow-Origin", "*");
           response.setContentType("application/json");
           response.setCharacterEncoding("UTF-8");
           try {
               String US_STATES[] = {"0=Alabama",
                       "1=Alaska",
                       "2=Arizona",
                       "3=Arkansas",
                       "4=California",
                       "5=Colorado",
                       "6=Connecticut",
                       "7=Delaware",
                       "8=Florida",
                       "9=Georgia",
                       "10=Hawaii",
                       "11=Idaho",
                       "12=Illinois",
                       "13=Indiana",
                       "14=Iowa",
                       "15=Kansas",
                       "16=Kentucky",
                       "17=Louisiana",
                       "18=Maine",
                       "19=Maryland",
                       "20=Massachusetts",
                       "21=Michigan",
                       "22=Minnesota",
                       "23=Mississippi",
                       "24=Missouri",
                       "25=Montana",
                       "26=Nebraska",
                       "27=Nevada",
                       "28=New Hampshire",
                       "29=New Jersey",
                       "30=New Mexico",
                       "31=New York",
                       "32=North Carolina",
                       "33=North Dakota",
                       "34=Ohio",
                       "35=Oklahoma",
                       "36=Oregon",
                       "37=Pennsylvania",
                       "38=Rhode Island",
                       "39=South Carolina",
                       "40=South Dakota",
                       "41=Tennessee",
                       "42=Texas",
                       "43=Utah",
                       "44=Vermont",
                       "45=Virginia",
                       "46=Washington",
                       "47=West Virginia",
                       "48=Wisconsin",
                       "49=Wyoming"};
               String AUSTRALIAN_STATES[] = {"0=Ashmore and Cartier Islands",
                       "1=Australian Antarctic Territory",
                       "2=Australian Capital Territory",
                       "3=Christmas Island",
                       "4=Cocos (Keeling) Islands",
                       "5=Coral Sea Islands",
                       "6=Heard Island and McDonald Islands",
                       "7=Jervis Bay Territory",
                       "8=New South Wales",
                       "9=Norfolk Island",
                       "10=Northern Territory",
                       "11=Queensland",
                       "12=South Australia",
                       "13=Tasmania",
                       "14=Victoria",
                       "15=Western Australia"};
               String country = request.getParameter("country");
               JSONArray stateJsonArray = new JSONArray();
               if (country.length() > 0) {
                   if ("australia".equalsIgnoreCase(country)) {
                       stateJsonArray = new JSONArray();
                       for (String state : AUSTRALIAN_STATES) {
                           stateJsonArray.put(state);
                       }
                   } else if ("unitedstates".equalsIgnoreCase(country)) {
                       stateJsonArray = new JSONArray();
                       for (String state : US_STATES) {
                           stateJsonArray.put(state);
                       }
                   }
                   response.setContentType("application/json");
                   response.getWriter().write(stateJsonArray.toString());
               }
   
           } catch ( Exception e) {
               logger.error(e.getMessage(), e);
           }
       }
   }
   ```

1. 在應用程式中的特定資料夾階層下建立下拉式節點（例如，在/apps/myfolder/demo下建立節點）。 確保 `sling:resourceType` 節點的引數與servlet所指向的引數相同(/apps/populatedropdown)。

   ![建立下拉式節點](assets/dropdown-node.png)

1. 封裝內容節點並將.jar檔案內嵌於特定位置（例如/apps/myfolder/demo/install/）。 在伺服器上部署相同的檔案。
1. 建立最適化表單，並在其中新增兩個下拉式清單：國家/地區和州。 國家/地區清單可包含國家/地區的名稱。 「州」清單可動態填入您在第一個清單中所選國家/地區的州名。

   新增要在「國家/地區」清單中顯示的國家/地區名稱。 在「州」清單中，新增指令碼，以根據「國家/地區」清單中的國家/地區名稱填入。

   ![新增國家/地區名稱](assets/country-dropdown.png) ![新增指令碼以填入狀態名稱](assets/state-dropdown.png) ![收集國家/地區和州別下拉式清單](assets/2dropdowns.png)

   ```javascript
   JSON.parse(
       $.ajax({
           url: "/apps/myfolder/demo/dropdown",
           type: "POST",
           async: false,
           data: {"country": country.value},
            success: function(res){},
            error : function (message) {
                 guideBridge._guide.logger().log(message);
                 successFlag = false;
                 }
              })
   .responseText);
   ```

內容套件，其中包含已實作上述程式碼的範例最適化表單（示範/AFdemo）。

[获取文件](assets/dropdown-demo-content-1.0.1-snapshot.zip)
