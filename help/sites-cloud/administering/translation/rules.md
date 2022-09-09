---
title: 标识要翻译的内容
description: 了解翻译规则如何标识需要翻译的内容。
feature: Language Copy
role: Admin
exl-id: 24cc6aa6-5b3c-462b-a10a-8b25277229dc
source-git-commit: 6be7cc7678162c355c39bc3000716fdaf421884d
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 100%

---

# 标识要翻译的内容 {#identifying-content-to-translate}

翻译规则为翻译项目中包含或排除的页面、组件和资产标识要翻译的内容。在翻译页面或资产时，AEM 会提取此内容，以便将其发送到翻译服务。

>[!TIP]
>
>如果不熟悉如何翻译内容，请参阅我们的[站点翻译历程](/help/journey-sites/translation/overview.md)，将指导您使用 AEM 强大的翻译工具翻译您的 AEM Sites 内容，非常适合没有 AEM 或翻译经验的人士。

## 内容片段和翻译规则 {#content-fragments}

仅当未在[翻译集成框架配置级别](integration-framework.md#assets-configuration-properties)激活&#x200B;**为翻译启用内容模型字段**&#x200B;选项时，本文档中描述的翻译规则才应用于内容片段。

如果&#x200B;**为翻译启用内容模型字段**&#x200B;选项已激活，AEM 将使用[内容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#properties)上的&#x200B;**可翻译**&#x200B;字段来确定是否要翻译该字段并相应地自动创建翻译规则。 此选项取代了您可能已创建的任何翻译规则，无需干预或附加步骤。

如果要使用翻译规则来翻译内容片段，必须禁用翻译集成框架配置上的&#x200B;**为翻译启用内容模型字段**&#x200B;选项，并且您需要执行下面列出的步骤来创建规则。

## 概述 {#overview}

页面和资产在 JCR 存储库中表示为节点。提取的内容是节点的一个或多个属性值。翻译规则标识包含要提取的内容的属性。

翻译规则以 XML 格式表示，并且可能存储在以下位置：

* `/libs/settings/translation/rules/translation_rules.xml`
* `/apps/settings/translation/rules/translation_rules.xml`
* `/conf/global/settings/translation/rules/translation_rules.xml`

该文件应用于所有翻译项目。

规则包含以下信息：

* 规则应用于的节点的路径
   * 规则也应用于节点的子级。
* 包含要翻译的内容的节点属性的名称
   * 属性可以特定于某个特定的资源类型或所有资源类型。

例如，您可以创建一个规则来翻译作者添加到您页面上所有文本组件的内容。此规则可以标识 `core/wcm/components/text/v2/text` 组件的 `/content` 节点和 `text` 属性。

已添加一个可用于配置翻译规则的[控制台](#translation-rules-ui)。UI 中的定义将为您填充文件。

有关 AEM 中内容翻译功能的概述，请参阅[翻译多语言站点的内容](overview.md)。

>[!NOTE]
>
>AEM 支持资源类型和引用属性之间的一对一映射，以便翻译页面上的引用内容。

## 页面、组件和资产的规则语法 {#rule-syntax-for-pages-components-and-assets}

规则是一个 `node` 元素，它包含一个或多个子 `property` 元素以及零个或多个子 `node` 元素：

```xml
<node path="content path">
          <property name="property name" [translate="false"]/>
          <node resourceType="component path" >
               <property name="property name" [translate="false"]/>
          </node>
</node>
```

其中每个 `node` 元素均具有以下特性：

* `path` 属性包含应用规则的分支的根节点的路径。
* 子 `property` 元素为所有资源类型标识要翻译的节点属性：
   * `name` 属性包含属性名。
   * 可选 `translate` 属性等于 `false`（如果该属性未翻译）。默认情况下，该值为 `true`。在覆盖以前的规则时，此属性很有用。
* 子 `node` 元素为特定资源类型标识要翻译的节点属性：
   * `resourceType` 属性包含解析为实施资源类型的组件的路径。
   * 子 `property` 元素标识要翻译的节点属性。按照与节点规则的子 `property` 元素相同的方式使用此节点。

以下示例规则导致为 `/content` 节点下的所有页面翻译所有 `text` 属性的内容。该规则适用于任何将内容存储在 `text` 属性中的组件，例如文本组件。

```xml
<node path="/content">
          <property name="text"/>
</node>
```

以下示例翻译了所有 `text` 属性的内容，并翻译了图像组件的其他属性。如果其他组件具有同名属性，则该规则不适用于它们。

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

## 用于从页面提取资产的规则语法  {#rule-syntax-for-extracting-assets-from-pages}

使用以下规则语法可包含嵌入在组件中或从组件中引用的资产：

```xml
<assetNode resourceType="path to component" assetReferenceAttribute="property that stores asset"/>
```

每个 `assetNode` 元素均具有以下特性：

* 一个 `resourceType` 属性，代表解析为组件的路径
* 一个 `assetReferenceAttribute` 属性，代表存储资产二进制文件（用于嵌入资产）的属性的名称或引用资产的路径

以下示例从图像组件中提取图像：

```xml
<assetNode resourceType="core/wcm/components/image/v2/image" assetReferenceAttribute="fileReference"/>
```

## 覆盖规则 {#overriding-rules}

`translation_rules.xml` 文件包含一个 `nodelist` 元素和多个子 `node` 元素。AEM 从上到下读取节点列表。如果有多个规则针对同一节点，则使用文件中较低位置的规则。例如，以下规则导致翻译 `text` 属性中的所有内容，但页面的 `/content/mysite/en` 分支除外：

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

## 筛选属性 {#filtering-properties}

您可以使用 `filter` 元素筛选具有特定属性的节点。

例如，以下规则导致翻译 `text` 属性中的所有内容，但属性 `draft` 设置为 `true` 的节点除外。

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

## 翻译规则 UI {#translation-rules-ui}

控制台也可用于配置翻译规则。

要访问它，请执行以下操作：

1. 依次导航到&#x200B;**工具**&#x200B;和&#x200B;**常规**。

1. 选择&#x200B;**翻译配置**。

在翻译规则 UI 中，您可以：

1. **添加上下文**，可让您添加路径。

   ![添加翻译上下文](../assets/add-translation-context.png)

1. 使用路径浏览器选择所需的上下文，然后点按或单击&#x200B;**确认**&#x200B;按钮进行保存。

   ![选择上下文](../assets/select-context.png)

1. 之后，您需要选择上下文，然后单击&#x200B;**编辑**。该操作将打开翻译规则编辑器。

   ![翻译规则编辑器](../assets/translation-rules-editor.png)

您可以通过 UI 更改四个属性：

* `isDeep`
* `inherit`
* `translate`
* `updateDestinationLanguage`

### isDeep {#isdeep}

**`isDeep`** 适用于节点过滤器且默认情况下为 true。它检查节点（或其祖先）是否在过滤器中包含具有指定属性值的属性。如果为 false，则仅检查当前节点。

例如，即使父节点将属性 `draftOnly` 设置为 true 以标记草稿内容，子节点也会添加到翻译作业中。此时 `isDeep` 将发挥作用，并检查父节点是否已将属性 `draftOnly` 设置为 true 并排除这些子节点。

在编辑器中，您可以在&#x200B;**过滤器**&#x200B;选项卡中选中/取消选中 **Is Deep**。

![过滤器规则](../assets/translation-rules-editor-filters.png)

以下是在 UI 中取消选中 **Is Deep** 时生成的 XML 的示例：

```xml
 <filter>
    <node containsProperty="draftOnly" isDeep="false" propertyValue="true"/>
</filter>
```

### inherit {#inherit}

**`inherit`** 适用于属性。默认情况下，每个属性都会被继承，但如果您希望某个属性不被子级继承，则可以将此属性标记为 false，使其仅应用于该特定节点。

在 UI 中，您可以在&#x200B;**属性**&#x200B;选项卡中选中/取消选中 **Inherit**。

### translate {#translate}

**`translate`** 仅用于指定是否翻译属性。

在 UI 中，您可以在&#x200B;**属性**&#x200B;选项卡中选中/取消选中 **Translate**。

### updateDestinationLanguage {#updatedestinationlanguage}

**`updateDestinationLanguage`** 用于没有文本但有语言代码的属性，例如 `jcr:language`。用户不会翻译文本，而是进行从源到目标的语言区域设置。不会发送此类属性进行翻译。

在 UI 中，您可以在&#x200B;**属性**&#x200B;选项卡中选中/取消选中 **Translate** 来修改此值，但目标对象是将语言代码作为值的特定属性

为了帮助阐明 `updateDestinationLanguage` 和 `translate` 之间的区别，以下提供了仅具有两个规则的上下文的简单示例：

![updateDestinationLanguage 示例](../assets/translation-rules-updatedestinationlanguage.png)

xml 中的结果将如下所示：

```xml
<property inherit="true" name="text" translate="true" updateDestinationLanguage="false"/>
<property inherit="true" name="jcr:language" translate="false" updateDestinationLanguage="true"/>
```

## 手动编辑规则文件 {#editing-the-rules-file-manually}

与 AEM 一起安装的 `translation_rules.xml` 文件包含一组默认的翻译规则。您可以编辑该文件以支持翻译项目的要求。例如，您可以添加规则以翻译自定义组件的内容。

如果您编辑 `translation_rules.xml` 文件，请在内容包中保留备份副本。重新安装某些 AEM 包可将当前 `translation_rules.xml` 文件替换为原始文件。要在此情况下恢复您的规则，您可以安装包含备份副本的包。

>[!NOTE]
>
>创建内容包后，每次编辑文件时都会重新构建包。

## 示例翻译规则文件 {#example-translation-rules-file}

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
