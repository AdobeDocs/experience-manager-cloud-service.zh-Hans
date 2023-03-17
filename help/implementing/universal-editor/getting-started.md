---
title: AEM中通用编辑器快速入门
description: 了解如何访问通用编辑器，以及如何开始检测您的第一个AEM应用程序以使用它。
source-git-commit: acafa752c354781e41b11e46ac31a59feb8d94e7
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 0%

---


# AEM中通用编辑器快速入门 {#getting-started}

了解如何访问通用编辑器，以及如何开始检测您的第一个AEM应用程序以使用它。

>[!TIP]
>
>如果您希望直接参考一个示例，可以查看 [GitHub上的通用编辑器示例应用程序。](https://github.com/adobe/universal-editor-sample-editable-app)

## 入门步骤 {#onboarding}

尽管通用编辑器可以编辑来自任何源的内容，但本文档将以AEM应用程序为例。

要载入AEM应用程序并检测其以使用通用编辑器，请执行多个步骤。

1. [请求对通用编辑器的访问权限。](#request-access)
1. [包含通用编辑器核心库。](#core-library)
1. [添加必要的OSGi配置。](#osgi-configurations)
1. [设置页面。](#instrument-page)

本文档将指导您完成这些步骤。

## 请求对通用编辑器的访问权限 {#request-access}

您首先需要请求对通用编辑器的访问权限。 请转到 [https://experience.adobe.com/#/aem/editor](https://experience.adobe.com/#/aem/editor) 并验证您是否有权访问通用编辑器。

如果您没有访问权限，则可以通过链接到同一页面上的表单来请求获取该访问权限。

## 包含通用编辑器核心库 {#core-library}

在对应用程序进行分析以便与通用编辑器一起使用之前，它需要包含以下依赖项。

```javascript
@adobe/universal-editor-cors
```

要激活检测，需要将以下导入添加到 `index.js`.

```javascript
import "@adobe/universal-editor-cors";
```

### 非React应用程序的替代方法 {#alternative}

如果您没有实施React应用程序，并且/或需要服务器端渲染，则替代方法是将以下内容包含到文档正文中。

```html
<script src="https://cdn.jsdelivr.net/gh/adobe/universal-editor-cors/dist/universal-editor-embedded.js" async></script>
```

## 添加必要的OSGi配置 {#osgi-configurations}

要使用通用编辑器在您的应用程序中编辑AEM内容，必须在AEM中完成CORS和Cookie设置。

以下 [必须在AEM创作实例中设置OSGi配置。](/help/implementing/deploying/configuring-osgi.md)

* `SameSite Cookies = None`-`com.day.crx.security.token.impl.impl.TokenAuthenticationHandler`
* 删除X-FRAME-OPTIONS:中的SAMEORIGIN标头 `org.apache.sling.engine.impl.SlingMainServlet`

### com.day.crx.security.token.impl.impl.TokenAuthenticationHandler {#samesite-cookies}

登录令牌Cookie必须作为第三方域发送到AEM。 因此，必须将同一站点Cookie明确设置为 `None`.

此属性必须在 `com.day.crx.security.token.impl.impl.TokenAuthenticationHandler` OSGi配置。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
          xmlns:jcr="http://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig"
          token.samesite.cookie.attr="None" />
```

### org.apache.sling.engine.impl.SlingMainServlet {#sameorigin}

X-Frame-Options:SAMEORIGIN阻止在iFrame中渲染AEM页面。 删除标头后，将会加载页面。

此属性必须在 `org.apache.sling.engine.impl.SlingMainServlet` OSGi配置。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
          xmlns:jcr="http://www.jcp.org/jcr/1.0"
          jcr:primaryType="sling:OsgiConfig"
          sling.additional.response.headers="[X-Content-Type-Options=nosniff]"/>
```

## 设置页面 {#instrument-page}

通用编辑器服务需要 [统一资源名称(URN)](https://en.wikipedia.org/wiki/Uniform_Resource_Name) 识别和利用正在编辑的应用程序中的内容的正确后端系统。 因此，需要使用URN模式将内容映射回内容资源。

添加到页面的工具属性主要由 [HTML微数据，](https://developer.mozilla.org/en-US/docs/Web/HTML/Microdata) 一种行业标准，也可用于使HTML更加语义化、使HTML文档可索引等。

### 创建连接 {#connections}

应用程序中使用的连接将存储为 `<meta>` 页面的标记 `<head>`.

```html
<meta name="urn:auecon:<referenceName>" content="<protocol>:<url>">
```

* `<referenceName>`  — 这是一个在文档中重复使用的短名称，用于标识连接。 例如 `aemconnection`
* `<protocol>`  — 这表示要使用通用编辑器持久性服务的哪个持久性插件。 例如 `aem`
* `<url>`  — 这是应保留更改的系统的URL。 例如 `http://localhost:4502`

短标识符 `auecon` 表示Adobe通用编辑器连接。

`itemid`s将使用 `urn` 用于缩短标识符的前缀。

```html
itemid="urn:<referenceName>:<resource>"
```

* `<referenceName>`  — 这是 `<meta>` 标记。 例如 `aemconnection`
* `<resource>`  — 这是指向目标系统中资源的指针。 例如AEM内容路径，如 `/content/page/jcr:content`

>[!TIP]
>
>查看文档 [属性和类型](attributes-types.md) 有关通用编辑器所需的数据属性和类型的更多详细信息。

### 示例连接 {#example}

```html
<html>
<head>
    <meta name="urn:auecon:aemconnection" content="aem:https://localhost:4502">
    <meta name="urn:auecon:fcsconnection" content="fcs:https://example.franklin.adobe.com/345fcdd">
</head>
<body>
        <aside>
          <ul itemscope itemid="urn:aemconnection:/content/example/list" itemtype="container">
            <li itemscope itemid="urn:aemconnection/content/example/listitem" itemtype="component">
              <p itemprop="name" itemtype="text">Jane Doe</p>
              <p itemprop="title" itemtype="text">Journalist</p>
              <img itemprop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" itemtype="image" alt="avatar"/>
            </li>
 
...
 
            <li itemscope itemid="urn:fcsconnection:/documents/mytext" itemtype="component">
              <p itemprop="name" itemtype="text">John Smith</p>
              <p itemid="urn:aemconnection/content/example/another-source" itemprop="title" itemtype="text">Photographer</p>
              <img itemprop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" itemtype="image" alt="avatar"/>
            </li>
          </ul>
        </aside>
</body>
</html>
```

### 通用编辑器翻译服务 {#translation}

通用编辑器根据工具元数据执行翻译。

#### 翻译的基本原则 {#principle}

请考虑上一个示例中的以下选择。

```html
<meta name="urn:auecon:aemconnection" content="aem:https://localhost:4502">
<ul itemscope itemid="urn:aemconnection:/content/example/list" itemtype="urn:fcs:type/list">
```

编辑器将执行替换，并在内部执行 `itemid` 将被重写到以下内容。

```html
itemid="urn:aem:https://localhost:4502/content/example/list"
```

这会导致该术语 `aemconnection` 替换为 `<meta>` 标记。

#### 查询选择器 {#query-selector}

此替换将导致John Smith的查询字符串如下。

```html
<ul itemscope itemid="urn:aemconnection:/content/example/list" itemtype="urn:fcs:type/list">
  <li itemscope itemid="urn:fcsconnection:/documents/mytext" itemtype="urn:fcs:type/fragment">.  
    <p itemprop="name" itemtype="text">John Smith</p>
    <p itemid="urn:aemconnection/content/example/another-source" itemprop="title" itemtype="text">Photographer</p>
    <img itemprop="avatar" src="urn:fcs:missing" itemtype="image" alt="avatar"/>
  </li>
```

`[itemid="urn:fcs:https://example.franklin.adobe.com/345fcdd/content/example/list][itemprop="name"]`

如果要更改John Smith的图块，选择器将如下所示。

`[itemid="urn:aem:https://localhost:4502/content/example/another-source"][itemprop="title"]`

而不是继承 `itemid`和资源，通用编辑器可与范围配合使用。 范围可以在节点级别上定义，并由整个子结构继承。

如果结构内的子结构或定义的休假需要不同的范围，则另一个 `itemid` 可定义。

## 您已准备好使用通用编辑器 {#youre-ready}

您的应用程序现在已被设计为使用通用编辑器！

请参阅该文档 [使用通用编辑器创作内容](authoring.md) 了解内容作者使用通用编辑器创建内容是多么简单、直观。

## 其他资源 {#additional-resources}

要了解有关通用编辑器的更多信息，请参阅这些文档。

* [通用编辑器简介](introduction.md)  — 了解通用编辑器如何允许编辑任何实施中任何内容的任何方面，以便提供卓越的体验、提高内容速度，并提供一流的开发人员体验。
* [使用通用编辑器创作内容](authoring.md)  — 了解内容作者使用通用编辑器创建内容是多么简单、直观。
* [通用编辑器架构](architecture.md)  — 了解通用编辑器的架构以及数据如何在其服务和层之间流动。
* [属性和类型](attributes-types.md)  — 了解通用编辑器所需的数据属性和类型。
* [通用编辑器身份验证](authentication.md)  — 了解通用编辑器如何进行身份验证。
