---
title: 扩展Adobe Experience Manager资产中的搜索选项和功能
description: 扩展资产的搜索功能。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# 扩展资产搜索 {#extend-assets-search}

您可以扩展Adobe Experience Manager(AEM)资产搜索功能。 开箱即用，AEM资产会按字符串搜索资产。

搜索通过QueryBuilder界面完成，因此可以使用多个谓词自定义搜索。 您可以在以下目录中叠加默认的谓词集： `/apps/dam/content/search/searchpanel/facets`.

您还可以向AEM资产管理面板添加其他选项卡。

## 叠加 {#overlay}

要叠加预配置的谓词，请将节 `facets` 点从复制到 `/libs/dam/content/search/searchpanel` , `/apps/dam/content/search/searchpanel/` 或在搜索面板配置 `facetURL` 中指定其他属性(默认为 `/libs/dam/content/search/searchpanel/facets.overlay.infinity.json`to)。

>[!NOTE]
>
>默认情况下，下面的目 `/apps` 录结构不存在，需要创建。 确保节点类型与下的节点类型匹配 `/libs`。

### 添加选项卡 {#add-tabs}

您可以通过在AEM资产管理员中配置其他搜索选项卡来添加这些选项卡。 要创建其他选项卡，请执行以下操作：

1. 如果文件夹结 `/apps/wcm/core/content/damadmin/tabs,`构尚不存在，请创建该结构，然后从中复 `tabs` 制并粘 `/libs/wcm/core/content/damadmin` 贴该结构。
1. 根据需要创建和配置第二个选项卡。

   >[!NOTE]
   >
   >创建第二个表 `siteadminsearchpanel`单时，请务必设置一 `id` 个属性以防止表单冲突。

### 创建自定义谓词 {#create-custom-predicates}

AEM资产附带一组预定义谓词，可用于自定义资产共享页面。
<!-- In addition to using pre-existing predicates, AEM developers can also create their own predicates using the [Query Builder API](/help/sites-developing/querybuilder-api.md). -->

创建自定义谓词需要有关构件框架的 [基本知识](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)。

最佳实践是复制现有谓词并对其进行调整。 示例谓词位于 **/libs/cq/search/components/谓词中**。

#### 示例：构建简单属性谓词 {#example-build-a-simple-property-predicate}

要构建属性谓词，请执行以下操作：

1. 在项目目录中创建组件文件夹，例如 **/apps/geometrixx/components/titlepredicate**。
1. 添 **加content.xml**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Title Predicate"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. 将 `titlepredicate.jsp`.

   ```xml
   <%--
   
     Sample title predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Title</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:title";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // createId adds a counter to the predicate name - useful in case this predicate
           // is inserted multiple times on the same page.
           var id = qb.createId(predicateName);
   
           // Hidden field that defines the property to search for; in our case this
           // is the "dc:title" metadata. The name "property" (or "1_property", "2_property" etc.)
           // indicates the server to use the property predicate
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id,
               "value": propertyName
           });
   
           // The visible text field. The name has to be like the one of the hidden field above
           // plus the ".value" suffix.
           qb.addField({
               "xtype": "textfield",
               "renderTo": elemId,
               "name": id + ".value"
           });
   
           // Depending on the predicate additional parameters allow to configure the
           // predicate. Here we add an operation parameter to create a "like" query.
           // Again note the name set to the id and a suffix.
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id + ".operation",
               "value": "like"
           });
       });
   </script>
   ```

1. 要使组件可用，您需要能够编辑它。 要使组件可编辑，请在CRXDE中添加主类型 **cq:editConfig** 的节点 **cq:EditConfig**。 为了删除段落，请添加一个单值 **DELETE的多值属性cq:actions******。
1. 导航到浏览器，在示例页面(例如， **press.html**)上切换到设计模式，为谓词段落系统启用新组件(例如， **left**)。

1. 在“ **编辑** ”模式中 **，新组件现在可在Sidekick中使用(在“搜索”组中** 找到)。 将组件插入谓 **词列** ，然后键入搜索词(例如， **Diamond** )，然后单击放大镜开始搜索。

   >[!NOTE]
   >
   >搜索时，请务必准确键入术语，包括正确的大小写。

#### 示例：构建简单的用户组谓词 {#example-build-a-simple-group-predicate}

要构建用户组谓词，请执行以下操作：

1. 在项目目录中创建组件文件夹，例如 **/apps/geometrixx/components/picspredicate。**
1. 添 **加content.xml**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Formats"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. 添 **加titlepredicate.jsp**:

   ```xml
   <%--
   
     Sample group predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page.
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Image Formats</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:format";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // Create a unique group ID; will return e.g. "1_group".
           var groupId = qb.createGroupId();
   
           // Hidden field that defines the property to search for  - in our case "dc:format" -
           // and declares the group of predicates. "property" in the name ("1_group.property")
           // indicates to the server to use the "property predicate"
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": "<%= elemId %>",
               "name": groupId + "." + predicateName, // 1_group.property
               "value": propertyName
           });
   
           // Declare to combine the multiple values using OR.
           qb.add(new CQ.Ext.form.Hidden({
               "name": groupId + ".p.or",  // 1_group.p.or
               "value": "true"
           }));
   
           // The options
           var options = [
               { "label":"JPEG", "value":"image/jpeg"},
               { "label":"PNG",  "value":"image/png" },
               { "label":"GIF",  "value":"image/gif" }
           ];
   
           // Build a checkbox for each option.
           for (var i = 0; i < options.length; i++) {
               qb.addField({
                   "xtype": "checkbox",
                   "renderTo": "<%= elemId %>",
                   // 1_group.property.0_value, 1_group.property.1_value etc.
                   "name": groupId + "." +  predicateName + "." + i + "_value",
                   "inputValue": options[i].value,
                   "boxLabel": options[i].label,
                   "listeners": {
                       "check": function() {
                           // Submit the search form when checking/unchecking a checkbox.
                           qb.submit();
                       }
                   }
               });
           }
       });
   ```

1. 要使组件可用，您需要能够编辑它。 要使组件可编辑，请在CRXDE中添加主类型 **cq:editConfig** 的节点 **cq:EditConfig**。 为了删除段落，请添加一个单值 **DELETE的多值属性cq:actions******。
1. 导航到浏览器，在示例页面(例如， **press.html**)上切换到设计模式，为谓词段落系统启用新组件(例如， **left**)。
1. 在“ **编辑** ”模式中 **，新组件现在可在Sidekick中使用(在“搜索”组中** 找到)。 将组件插入谓 **词列** 。

### 已安装的谓词构件 {#installed-predicate-widgets}

以下谓词可作为预配置的ExtJS构件使用。

#### 全文谓词 {#fulltextpredicate}

<table>
 <tbody>
  <tr>
   <td><strong>属性<br /> </strong></td>
   <td><strong>类型</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>predicateName</td>
   <td>字符串</td>
   <td>谓词的名称。 默认为“全文”</td>
  </tr>
  <tr>
   <td>searchCallback</td>
   <td>函数</td>
   <td>回调以在事件“keyup”上触发搜索。 默认为“CQ.wcm.SiteAdmin.doSearch”</td>
  </tr>
 </tbody>
</table>

#### 属性谓词 {#propertypredicate}

<table>
 <tbody>
  <tr>
   <td><strong>属性<br /> </strong></td>
   <td><strong>类型</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>predicateName</td>
   <td>字符串</td>
   <td>谓词的名称。 默认为“property”</td>
  </tr>
  <tr>
   <td>propertyName</td>
   <td>字符串 </td>
   <td>JCR属性的名称。 默认为“jcr:title”</td>
  </tr>
  <tr>
   <td>defaultValue<br /> </td>
   <td>String<br /> </td>
   <td>预填充的默认值。<br /> </td>
  </tr>
 </tbody>
</table>

#### 路径谓词 {#pathpredicate}

<table>
 <tbody>
  <tr>
   <td><strong>属性<br /> </strong></td>
   <td><strong>类型</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>predicateName</td>
   <td>字符串</td>
   <td>谓词的名称。 默认为“路径”</td>
  </tr>
  <tr>
   <td>rootPath</td>
   <td>字符串 </td>
   <td>谓词的根路径。 默认为“/content/dam”</td>
  </tr>
  <tr>
   <td>pathFieldPredicateName</td>
   <td>字符串</td>
   <td>默认为“folder”</td>
  </tr>
  <tr>
   <td>showFlatOption</td>
   <td>布尔型</td>
   <td>显示复选框“在子文件夹中搜索”的标记。 默认设置为 true。</td>
  </tr>
 </tbody>
</table>

#### 日期谓词 {#datepredicate}

<table>
 <tbody>
  <tr>
   <td><strong>属性<br /> </strong></td>
   <td><strong>类型</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>predicateName</td>
   <td>字符串</td>
   <td>谓词的名称。 默认为“更改”</td>
  </tr>
  <tr>
   <td>propertyname</td>
   <td>字符串</td>
   <td>JCR属性的名称。 默认为“jcr:content/jcr:lastModified”</td>
  </tr>
  <tr>
   <td>defaultValue </td>
   <td>字符串 </td>
   <td>预填充的默认值 </td>
  </tr>
 </tbody>
</table>

#### 选项谓词 {#optionspredicate}

<table>
 <tbody>
  <tr>
   <td><strong>属性<br /> </strong></td>
   <td><strong>类型</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>职位 </td>
   <td>字符串 </td>
   <td>添加其他顶部标题 </td>
  </tr>
  <tr>
   <td>predicateName</td>
   <td>字符串</td>
   <td>谓词的名称。 默认为“更改”</td>
  </tr>
  <tr>
   <td>propertyname</td>
   <td>字符串</td>
   <td>JCR属性的名称。 默认为“jcr:content/metadata/cq:tags”</td>
  </tr>
  <tr>
   <td>折叠</td>
   <td>字符串</td>
   <td>折叠级别。 默认为“level1”</td>
  </tr>
  <tr>
   <td>triggerSearch</td>
   <td>布尔型 </td>
   <td>用于在选中时触发搜索的标记。 默认为false</td>
  </tr>
  <tr>
   <td>searchCallback</td>
   <td>函数</td>
   <td>回调以触发搜索。 默认为“CQ.wcm.SiteAdmin.doSearch”</td>
  </tr>
  <tr>
   <td>searchTimeoutTime</td>
   <td>数字</td>
   <td>触发searchCallback之前的超时。 默认为800毫秒</td>
  </tr>
 </tbody>
</table>
