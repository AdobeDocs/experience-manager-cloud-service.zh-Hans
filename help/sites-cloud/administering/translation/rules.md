---
title: 确定要翻译的内容
description: 了解翻译规则如何识别需要翻译的内容。
translation-type: tm+mt
source-git-commit: 4fc4dbe2386d571fa39fd6d10e432bb2fc060da1
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 0%

---


# 确定要翻译的内容{#identifying-content-to-translate}

翻译规则可标识要翻译的内容，这些内容适用于翻译项目中包含或排除的页面、组件和资产。 当页面或资产被翻译时，AEM会提取此内容，以便将其发送到翻译服务。

页面和资产在JCR存储库中表示为节点。 提取的内容是节点的一个或多个属性值。 翻译规则标识包含要提取内容的属性。

翻译规则以XML格式表示，并存储在以下可能位置：

* `/libs/settings/translation/rules/translation_rules.xml`
* `/apps/settings/translation/rules/translation_rules.xml`
* `/conf/global/settings/translation/rules/translation_rules.xml`

该文件适用于所有翻译项目。

规则包括以下信息：

* 应用规则的节点的路径
   * 该规则也适用于节点的后代。
* 包含要翻译的内容的节点属性的名称
   * 该属性可以特定于特定资源类型或所有资源类型。

例如，您可以创建一个规则，用于转换作者添加到页面上所有文本组件的内容。 规则可以标识`/content`节点和`core/wcm/components/text/v2/text`组件的`text`属性。

添加了一个[console](#translation-rules-ui)，用于配置转换规则。 UI中的定义将为您填充文件。

有关AEM中内容翻译功能的概述，请参阅[多语言站点内容翻译](overview.md)。

>[!NOTE]
>
>AEM支持在资源类型和引用属性之间进行一对一映射，以转换页面上的引用内容。

## 页面、组件和资产的规则语法{#rule-syntax-for-pages-components-and-assets}

规则是一个`node`元素，其中包含一个或多个子元素`property`和零个或多个子元素`node`:

```xml
<node path="content path">
          <property name="property name" [translate="false"]/>
          <node resourceType="component path" >
               <property name="property name" [translate="false"]/>
          </node>
</node>
```

每个`node`元素具有以下特征：

* `path`属性包含规则所应用分支的根节点的路径。
* 子`property`元素标识要转换的所有资源类型的节点属性：
   * `name`属性包含属性名称。
   * 如果属性未转换，则可选`translate`属性等于`false`。 默认情况下，值为`true`。 此属性在覆盖以前的规则时很有用。
* 子`node`元素标识要针对特定资源类型进行转换的节点属性：
   * `resourceType`属性包含解析到实现资源类型的组件的路径。
   * 子`property`元素标识要转换的节点属性。 以与节点规则的子`property`元素相同的方式使用此节点。

下面的示例规则导致转换`/content`节点下所有页面的所有`text`属性的内容。 规则对于在`text`属性中存储内容的任何组件（如文本组件）都有效。

```xml
<node path="/content">
          <property name="text"/>
</node>
```

下面的示例转换所有`text`属性的内容，还转换图像组件的其他属性。 如果其他组件具有同名属性，则规则不适用于这些组件。

```xml
<node path="/content">
      <property name="text"/>
      <node resourceType="core/wcm/components/image/v2/image">
         <property name="image/alt"/>
         <property name="image/jcr:description"/>
         <property name="image/jcr:title"/>
      </node>
</node>
```

## 从页面{#rule-syntax-for-extracting-assets-from-pages}提取资产的规则语法

使用以下规则语法来包括嵌入到组件中或从组件中引用的资产：

```xml
<assetNode resourceType="path to component" assetReferenceAttribute="property that stores asset"/>
```

每个`assetNode`元素具有以下特征：

* 一个`resourceType`属性，它等于解析到组件的路径
* 一个`assetReferenceAttribute`属性，它等于存储资产二进制文件（对于嵌入式资产）的属性或引用资产的路径的名称

下面的示例从图像组件中提取图像：

```xml
<assetNode resourceType="core/wcm/components/image/v2/image" assetReferenceAttribute="fileReference"/>
```

## 覆盖规则{#overriding-rules}

`translation_rules.xml`文件由具有多个子`node`元素的`nodelist`元素组成。 AEM从上到下读取节点列表。 当多个规则目标同一节点时，将使用文件中较低的规则。 例如，以下规则导致除页面的`/content/mysite/en`分支外，`text`属性中的所有内容都要进行翻译：

```xml
<nodelist>
     <node path="/content”>
           <property name="text" />
     </node>
     <node path=“/content/mysite/en”>
          <property name=“text” translate=“false" />
     </node>
<nodelist>
```

## 筛选属性{#filtering-properties}

可以使用`filter`元素筛选具有特定属性的节点。

例如，以下规则导致除属性`draft`设置为`true`的节点外，`text`属性中的所有内容都要进行转换。

```xml
<nodelist>
    <node path="/content”>
     <filter>
   <node containsProperty="draft" propertyValue="true" />
     </filter>
        <property name="text" />
    </node>
<nodelist>
```

## 翻译规则UI {#translation-rules-ui}

控制台也可用于配置翻译规则。

要访问它：

1. 导航到&#x200B;**工具**，然后导航到&#x200B;**常规**。

1. 选择&#x200B;**转换配置**。

在翻译规则UI中，您可以：

1. **添加上下文**，它允许您添加路径。

   ![添加翻译上下文](../assets/add-translation-context.png)

1. 使用路径浏览器选择所需的上下文，然后点按或单击要保存的&#x200B;**确认**&#x200B;按钮。

   ![选择上下文](../assets/select-context.png)

1. 然后，您需要选择上下文，然后单击&#x200B;**编辑**。 这将打开翻译规则编辑器。

   ![翻译规则编辑器](../assets/translation-rules-editor.png)

您可以通过UI更改以下四个属性：

* `isDeep`
* `inherit`
* `translate`
* `updateDestinationLanguage`

### isDeep {#isdeep}

**`isDeep`**  适用于节点过滤器，默认情况下为true。它检查节点（或其祖先）是否在筛选器中包含具有指定属性值的属性。 如果为false，则仅检查当前节点。

例如，即使父节点的属性`draftOnly`设置为true以标记草稿内容，子节点也会添加到转换作业。 此处`isDeep`开始运行并检查父节点是否将属性`draftOnly`作为true并排除这些子节点。

在编辑器中，您可以选中/取消选中&#x200B;**过滤器**&#x200B;选项卡中的&#x200B;**深**。

![筛选规则](../assets/translation-rules-editor-filters.png)

以下是在UI中未选中&#x200B;**深**&#x200B;时生成的XML的示例：

```xml
 <filter>
    <node containsProperty="draftOnly" isDeep="false" propertyValue="true"/>
</filter>
```

### 继承 {#inherit}

**`inherit`** 适用于属性。默认情况下，每个属性都是继承的，但如果您希望某些属性不由子项继承，则可以将此属性标记为false，以便仅将其应用于该特定节点。

在UI中，您可以选中/取消选中&#x200B;**属性**&#x200B;选项卡中的&#x200B;**继承**。

### 翻译{#translate}

**`translate`** 仅用于指定是否翻译属性。

在UI中，您可以选中/取消选中&#x200B;**属性**&#x200B;选项卡中的&#x200B;**翻译**。

### updateDestinationLanguage {#updatedestinationlanguage}

**`updateDestinationLanguage`** 用于没有文本但语言代码的属性，例如 `jcr:language`用户不是在翻译文本，而是在从源到目标的语言区域设置中。 此类属性不会发送用于翻译。

在UI中，您可以选中/取消选中&#x200B;**属性**&#x200B;选项卡中的&#x200B;**转换**&#x200B;以修改此值，但是对于具有语言代码作为值的特定属性。

为了帮助阐明`updateDestinationLanguage`和`translate`之间的差异，以下是仅包含两个规则的上下文的一个简单示例：

![updateDestinationLanguage示例](../assets/translation-rules-updatedestinationlanguage.png)

xml中的结果将如下所示：

```xml
<property inherit="true" name="text" translate="true" updateDestinationLanguage="false"/>
<property inherit="true" name="jcr:language" translate="false" updateDestinationLanguage="true"/>
```

## 手动编辑规则文件{#editing-the-rules-file-manually}

随AEM安装的`translation_rules.xml`文件包含一组默认的转换规则。 您可以编辑文件以支持翻译项目的要求。 例如，您可以添加规则，以便对自定义组件的内容进行翻译。

如果编辑`translation_rules.xml`文件，请在内容包中保留备份副本。 重新安装某些AEM包可以将当前`translation_rules.xml`文件替换为原始文件。 要在此情况下恢复规则，可以安装包含备份副本的包。

>[!NOTE]
>
>创建内容包后，每次编辑文件时都重新构建该包。

## 翻译规则文件示例{#example-translation-rules-file}

```xml
<?xml version="1.0" encoding="UTF-8"?><nodelist>
  <node path="/content">
    <property name="addLabel"/>
    <property name="allowedResponses"/>
    <property name="alt"/>
    <property name="attachFileLabel"/>
    <property name="benefits"/>
    <property name="buttonLabel"/>
    <property name="chartAlt"/>
    <property name="confirmationMessageToggle"/>
    <property name="confirmationMessageUntoggle"/>
    <property name="constraintMessage"/>
    <property name="contentLabel"/>
    <property name="denyText"/>
    <property name="detailDescription"/>
    <property name="emptyText"/>
    <property name="helpMessage"/>
    <property name="image/alt"/>
    <property name="image/jcr:description"/>
    <property name="image/jcr:title"/>
    <property name="jcr:description"/>
    <property name="jcr:title"/>
    <property name="heading"/>
    <property name="label"/>
    <property name="main"/>
    <property name="listLabel"/>
    <property name="moreText"/>
    <property name="pageTitle"/>
    <property name="placeholder"/>
    <property name="requiredMessage"/>
    <property name="resetTitle"/>
    <property name="subjectLabel"/>
    <property name="subtitle"/>
    <property name="tableData"/>
    <property name="text"/>
    <property name="title"/>
    <property name="navTitle"/>
    <property name="titleDivContent"/>
    <property name="toggleLabel"/>
    <property name="transitionLabel"/>
    <property name="untoggleLabel"/>
    <property name="name"/>
    <property name="occupations"/>
    <property name="greetingLabel"/>
    <property name="signInLabel"/>
    <property name="signOutLabel"/>
    <property name="pretitle"/>
    <property name="cq:panelTitle"/>
    <property name="actionText"/>
    <property name="cq:language" updateDestinationLanguage="true"/>
    <node pathContains="/cq:annotations">
      <property name="text" translate="false"/>
    </node>
    <node path="/content/wknd"/>
  </node>
  <node path="/content/forms">
    <property name="text" translate="false"/>
  </node>
  <node path="/content/dam">
    <property name="dc:description"/>
    <property name="dc:rights"/>
    <property name="dc:subject"/>
    <property name="dc:title"/>
    <property name="defaultContent"/>
    <property name="jcr:description"/>
    <property name="jcr:title"/>
    <property name="pdf:Title"/>
    <property name="xmpRights:UsageTerms"/>
    <property name="main"/>
    <property name="adventureActivity"/>
    <property name="adventureDescription"/>
    <property name="adventureDifficulty"/>
    <property name="adventureGearList"/>
    <property name="adventureGroupSize"/>
    <property name="adventureItinerary"/>
    <property name="adventurePrice"/>
    <property name="adventureTitle"/>
    <property name="adventureTripLength"/>
    <property name="adventureType"/>
    <node pathContains="/jcr:content/metadata/predictedTags">
      <property name="name"/>
    </node>
  </node>
  <assetNode assetReferenceAttribute="fragmentPath" resourceType="cq/experience-fragments/editor/components/experiencefragment"/>
  <assetNode assetReferenceAttribute="fragmentVariationPath" resourceType="core/wcm/components/experiencefragment/v1/experiencefragment"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="dam/cfm/components/contentfragment"/>
  <assetNode resourceType="docs/components/download"/>
  <assetNode resourceType="docs/components/image"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="foundation/components/image"/>
  <assetNode assetReferenceAttribute="asset" resourceType="foundation/components/video"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="foundation/components/download"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="core/wcm/components/download/v1/download"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="wcm/foundation/components/image"/>
  <assetNode assetReferenceAttribute="fragmentPath" resourceType="core/wcm/components/contentfragment/v1/contentfragment"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="core/wcm/components/image/v2/image"/>
</nodelist>
```
