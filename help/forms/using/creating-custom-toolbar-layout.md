---
title: 创建自定义工具栏布局
seo-title: Creating custom toolbar layout
description: 您可以为表单指定工具栏布局。 工具栏布局定义命令和表单上工具栏的布局。
seo-description: You can specify a toolbar layout for the form. The toolbar layout defines the commands and the layout of the toolbar on the form.
uuid: 389a715a-4c91-4a63-895d-bb2d0f1054eb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 0d817a7e-2758-4308-abda-6194716c2d97
docset: aem65
exl-id: 44516956-00aa-41d5-a7e9-746c7618e5db
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

# 创建自定义工具栏布局{#creating-custom-toolbar-layout}

## 工具栏布局 {#layout}

创建自适应表单时，可以指定表单的工具栏布局。 工具栏布局定义命令和表单上工具栏的布局。

工具栏布局使用在很大程度上依赖于由复杂的JavaScript和CSS代码驱动的客户端处理。 组织和优化此代码的服务可能是一个复杂的问题。 为帮助解决此问题，AEM提供了客户端库文件夹，您可以使用这些文件夹将客户端代码存储在存储库中，将其划分为不同类别，并定义每个类别的代码何时以及如何提供给客户端。 然后，客户端库系统负责在最终网页中产生正确的链接，以加载正确的代码。 有关详细信息，请参阅 [客户端库在AEM中的工作方式。](/help/sites-developing/clientlibs.md)

![工具栏的示例布局](assets/default_toolbar_layout.png)

工具栏的示例布局

自适应表单提供一组现成的布局：

![现成可用的工具栏布局 ](assets/toolbar1.png)

现成可用的工具栏布局

此外，您还可以创建自定义工具栏布局。

以下过程详细介绍了创建自定义工具栏的步骤，该工具栏在工具栏中显示三个操作，并在工具栏的下拉列表中显示其他操作。

附加的内容包包含下面描述的整个代码。 安装内容包后，打开 `/content/forms/af/CustomLayoutDemo.html` 查看自定义工具栏布局演示。

CustomToolbarLayoutDemo.zip

[获取文件](assets/customtoolbarlayoutdemo.zip)
演示自定义工具栏布局

## 创建自定义工具栏布局 {#layout-1}

1. 创建一个文件夹以维护自定义工具栏布局。 例如：

   `/apps/customlayout/toolbar`。

   要创建自定义布局，您可以使用（和自定义）以下文件夹中提供的现成的工具栏布局之一：

   `/libs/fd/af/layouts/toolbar`

   例如，复制 `mobileFixedToolbarLayout` 节点来自 `/libs/fd/af/layouts/toolbar` 文件夹到 `/apps/customlayout/toolbar` 文件夹。

   此外，将toolbarCommon.jsp复制到 `/apps/customlayout/toolbar` 文件夹。

   >[!NOTE]
   >
   >您创建的用于维护自定义版面的文件夹大部分是使用 `apps` 文件夹。

1. 重命名复制的节点， `mobileFixedToolbarLayout`，至 `customToolbarLayout.`

   此外，为节点提供相关描述。 例如，将节点的jcr：description更改为 **自定义工具栏布局**.

   此 `guideComponentType` 节点的属性确定布局类型。 在这种情况下，布局类型为工具栏，因此显示在工具栏布局选择下拉列表中。

   ![具有相关说明的节点](assets/toolbar3.png)

   具有相关说明的节点

   您的新自定义工具栏布局显示在 **自适应表单工具栏** 对话框配置。

   ![可用工具栏布局列表](assets/toolbar4.png)

   可用工具栏布局列表

   >[!NOTE]
   >
   >上一步中更新的描述将显示在布局下拉列表中。

1. 选择此自定义工具栏布局，然后单击“确定”。

   在中添加clientlib （javascript和css） `/etc/customlayout` 节点并将clientlib的引用包含在 `customToolbarLayout.jsp`.

   ![customToolbarLayout.css文件的路径](assets/toolbar_3.png)

   customToolbarLayout.css文件的路径

   样本 `customToolbarLayout.jsp`:

   ```jsp
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <cq:includeClientLib categories="customtoolbarlayout" />
   <c:if test="${isEditMode}">
           <cq:includeClientLib categories="customtoolbarlayoutauthor" />
   </c:if>
   <div class="guidetoolbar mobileToolbar mobilecustomToolbar" data-guide-position-class="guide-element-hide">
       <div data-guide-scroll-indicator="true"></div>
       <%@include file="../toolbarCommon.jsp" %>
   </div>
   ```

   >[!NOTE]
   >
   >为布局添加guidetoolbar类。 工具栏的现成样式是根据guidetoolbar类定义的。

   样本 `toolBarCommon.jsp`:

   ```jsp
   <%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions"%>
   <%--------------------
   This code iterates over all the tool bar items using the guideToolbar bean.
   If the number of toolbar items are more than 3, then we create a dropdown menu using bootstrap for other actions present in the toolbar.
   In both desktop and mobile devices, the layout is different.
   ---------------------------------%>
   
   <c:forEach items="${guideToolbar.items}" var="toolbarItem" varStatus="loop">
       <c:choose>
         <c:when test="${loop.index gt 2}">
      <c:choose>
       <c:when test="${loop.index eq 3}">
                     <div class="btn-group dropdown">
                       <button type="button" class="btn btn-primary dropdown-toggle label" data-toggle="dropdown">Actions <span class="caret"></code></button>
                       <button type="button" class="btn btn-primary dropdown-toggle icon" data-toggle="dropdown"><span class="glyphicon glyphicon-th-list"></code></button>
             <ul class="dropdown-menu" role="menu">
                           <li>
                               <div id="${toolbarItem.id}_guide-item">
                                 <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
                              </div>
                           </li>
                           <c:if test="${loop.index eq (fn:length(guideToolbar.items)-1)}">
                                </ul>
                                </div>
                           </c:if>
       </c:when>
       <c:when test="${loop.index eq (fn:length(guideToolbar.items)-1)}">
                          <li>
                                     <div id="${toolbarItem.id}_guide-item">
                                         <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
                                     </div>
                           </li>
                       </ul>
                     </div>
   
       </c:when>
       <c:otherwise>
         <li>
          <div id="${toolbarItem.id}_guide-item">
           <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
          </div>
         </li>
       </c:otherwise>
      </c:choose>
         </c:when>
         <c:otherwise>
     <div id="${toolbarItem.id}_guide-item">
           <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
        </div>
         </c:otherwise>
    </c:choose>
   </c:forEach>
   ```

   clientlib节点中存在的CSS：

   ```css
   .mobilecustomToolbar .dropdown {
       display: inline-block;
   }
   
   .mobilecustomToolbar .dropdown {
       float: right;
   }
   
   .mobilecustomToolbar .dropdown > button {
      padding: 6px 12px;
   }
   
   .mobilecustomToolbar .dropdown .guideFieldWidget, .mobilecustomToolbar .dropdown .guideFieldWidget button {
       width: 100%;
   }
   
   .mobilecustomToolbar .dropdown .caret{
       border-bottom: 6px solid;
       border-right: 6px solid transparent;
       border-left: 6px solid transparent;
    border-top: transparent;
   }
   
   .mobilecustomToolbar .dropdown-menu{
    top: auto;
    bottom: 100%;
   }
   
   .mobilecustomToolbar .btn-group {
    vertical-align: super;
   }
   
   .mobilecustomToolbar .glyphicon {
    font-size: 24px;
   }
   
   @media (max-width: 767px){
   
    .mobilecustomToolbar .dropdown .guideButton .iconButton-icon {
      display: none;
       }
   
       .mobilecustomToolbar .dropdown .guideButton .iconButton-label {
      display: inline-block;
       }
   
       .mobilecustomToolbar .dropdown .guideButton button {
      background-color: #013853;
       }
   
    .mobilecustomToolbar .btn-group {
     vertical-align: top;
    }
   
   }
   ```

>[!NOTE]
>
>上一步中更新的描述将显示在布局下拉列表中。

![自定义布局工具栏的桌面视图](assets/toolbar_1.png)

自定义布局工具栏的桌面视图
