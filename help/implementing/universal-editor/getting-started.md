---
title: AEM Universal Editor 快速入门
description: 了解如何获取 Universal Editor 访问权限以及如何对第一个 AEM 应用程序插桩以使用 Universal Editor。
exl-id: 9091a29e-2deb-4de7-97ea-53ad29c7c44d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 395cb7b2e37c7358baa7ae07329f42bd5a560cb1
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 71%

---


# AEM Universal Editor 快速入门 {#getting-started}

了解如何获取 Universal Editor 访问权限以及如何对第一个 AEM 应用程序插桩以使用 Universal Editor。

>[!TIP]
>
>如果您想深入研究示例，可以查看 [GitHub 上的 Universal Editor 示例应用程序](https://github.com/adobe/universal-editor-sample-editable-app)。

## 载入步骤 {#onboarding}

虽然 Universal Editor 可以编辑来自任何来源的内容，但本文档将以 AEM 应用程序为例。

载入您的AEM应用程序并检测它是否使用通用编辑器需要多个步骤。

1. [包括 Universal Editor 核心库。](#core-library)
1. [添加必要的 OSGi 配置。](#osgi-configurations)
1. [在页面上插桩。](#instrument-page)

本文档将引导您完成这些步骤。

## 包括 Universal Editor 核心库 {#core-library}

在将您的应用程序检测为可与通用编辑器一起使用之前，它必须包括以下依赖项。

```javascript
@adobe/universal-editor-cors
```

要激活检测，必须将以下导入添加到您的`index.js`。

```javascript
import "@adobe/universal-editor-cors";
```

### 非 React 应用程序的替代项 {#alternative}

如果您未实施React应用程序和/或需要服务器端渲染，另一种方法是在文档正文中包含以下内容。

```html
<script src="https://universal-editor-service.experiencecloud.live/corslib/LATEST" async></script>
```

始终建议使用最新版本，但在发生重大更改时，可以引用服务的先前版本。

* `https://universal-editor-service.experiencecloud.live/corslib/LATEST` — 最新的UE CORS库
* `https://universal-editor-service.experiencecloud.live/corslib/2/LATEST` — 版本2.x下最新的UE CORS库
* `https://universal-editor-service.experiencecloud.live/corslib/2.1/LATEST` - 2.1.x版下最新的UE CORS库
* `https://universal-editor-service.experiencecloud.live/corslib/2.1.1` — 精确的UE CORS库版本2.1.1

## 添加必要的 OSGi 配置 {#osgi-configurations}

要能够使用 Universal Editor 通过应用程序编辑 AEM 内容，必须在 AEM 中完成 CORS 和 Cookie 设置。

[必须在 AEM 创作实例上设置以下 OSGi 配置。](/help/implementing/deploying/configuring-osgi.md)

* `com.day.crx.security.token.impl.impl.TokenAuthenticationHandler` 中的 `SameSite Cookies = None`
* 移除 X-FRAME-OPTIONS：`org.apache.sling.engine.impl.SlingMainServlet` 中的 SAMEORIGIN 标头

### com.day.crx.security.token.impl.impl.TokenAuthenticationHandler {#samesite-cookies}

登录令牌 Cookie 必须作为第三方域发送到 AEM。因此，必须将相同站点 Cookie 明确设置为 `None`。

必须在 `com.day.crx.security.token.impl.impl.TokenAuthenticationHandler` OSGi 配置中设置此属性。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
          xmlns:jcr="http://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig"
          token.samesite.cookie.attr="None" />
```

### org.apache.sling.engine.impl.SlingMainServlet {#sameorigin}

X-Frame-Options：SAMEORIGIN 阻止在 iframe 中呈现 AEM 页面。移除标头将允许加载页面。

必须在 `org.apache.sling.engine.impl.SlingMainServlet` OSGi 配置中设置此属性。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
          xmlns:jcr="http://www.jcp.org/jcr/1.0"
          jcr:primaryType="sling:OsgiConfig"
          sling.additional.response.headers="[X-Content-Type-Options=nosniff]"/>
```

## 在页面上插桩 {#instrument-page}

Universal Editor 服务需要一个[统一资源名称 (URN)](https://en.wikipedia.org/wiki/Uniform_Resource_Name) 来为正在编辑的应用程序内容识别和使用正确的后端系统。因此，需要 URN 模式将内容映射回内容资源。

### 创建连接 {#connections}

应用程序中使用的连接将作为 `<meta>` 标记存储在页面的 `<head>` 中。

```html
<meta name="urn:adobe:aue:<category>:<referenceName>" content="<protocol>:<url>">
```

* `<category>` — 这是连接的分类，带有两个选项。
   * `system` — 用于连接端点
   * `config` — 对于[定义可选配置设置](#configuration-settings)
* `<referenceName>` – 这是一个短名称，可在文档中重复使用以标识连接。例如 `aemconnection`
* `<protocol>` – 这表明要使用的 Universal Editor 持久性服务的持久性插件。例如 `aem`
* `<url>` – 这是保存更改的系统的 URL。例如 `http://localhost:4502`

标识符 `urn:adobe:aue:system` 表示与 Adobe Universal Editor 相连。

`data-aue-resource` 将使用 `urn` 前缀来缩短标识符。

```html
data-aue-resource="urn:<referenceName>:<resource>"
```

* `<referenceName>` – 这是 `<meta>` 标记中提到的命名引用。例如 `aemconnection`
* `<resource>` – 这是指向目标系统中资源的指针。例如 AEM 内容路径（如 `/content/page/jcr:content`）

>[!TIP]
>
>有关 Universal Editor 所需的数据属性和类型的更多详细信息，请参阅文档[属性和类型](attributes-types.md)。

### 示例连接 {#example}

```html
<meta name="urn:adobe:aue:system:<referenceName>" content="<protocol>:<url>">

<html>
<head>
    <meta name="urn:adobe:aue:system:aemconnection" content="aem:https://localhost:4502">
    <meta name="urn:adobe:aue:system:fcsconnection" content="fcs:https://example.franklin.adobe.com/345fcdd">
</head>
<body>
        <aside>
          <ul data-aue-resource="urn:aemconnection:/content/example/list" data-aue-type="container">
            <li data-aue-resource="urn:aemconnection:/content/example/listitem" data-aue-type="component">
              <p data-aue-prop="name" data-aue-type="text">Jane Doe</p>
              <p data-aue-prop="title" data-aue-type="text">Journalist</p>
              <img data-aue-prop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" data-aue-type="image" alt="avatar"/>
            </li>

...

            <li data-aue-resource="urn:fcsconnection:/documents/mytext" data-aue-type="component">
              <p data-aue-prop="name" data-aue-type="text">John Smith</p>
              <p data-aue-resource="urn:aemconnection:/content/example/another-source" data-aue-prop="title" data-aue-type="text">Photographer</p>
              <img data-aue-prop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" data-aue-type="image" alt="avatar"/>
            </li>
          </ul>
        </aside>
</body>
</html>
```

### 配置设置 {#configuration-settings}

如有必要，您可以在连接URN中使用`config`前缀来设置服务和扩展端点。

如果您不希望使用由Adobe托管、但却是您自己的托管版本的通用编辑器服务，则可以在Meta标记中设置此项。 要覆盖通用编辑器提供的默认服务端点，请设置您自己的服务端点：

* 元名称 — `urn:adobe:aue:config:service`
* 元内容 — `content="https://adobe.com"`（示例）

```html
<meta name="urn:adobe:aue:config:service" content="<url>">
```

如果只想为页面启用某些扩展，则可以在Meta标记中设置此项。 要获取扩展，请设置扩展端点：

* 元名称： `urn:adobe:aue:config:extensions`
* 元内容： `content="https://adobe.com,https://anotherone.com,https://onemore.com"`（示例）

```html
<meta name="urn:adobe:aue:config:extensions" content="<url>,<url>,<url>">
```

## 您已准备好使用 Universal Editor {#youre-ready}

您的应用程序现已插桩，可以使用 Universal Editor 了！

请参阅[使用 Universal Editor 创作内容](/help/sites-cloud/authoring/universal-editor/authoring.md)，了解内容作者使用 Universal Editor 创建内容是多么轻松和直观。

## 其他资源 {#additional-resources}

要了解有关 Universal Editor 的更多信息，请参阅这些文档。

* [Universal Editor 简介](introduction.md) – 了解 Universal Editor 如何支持在任意实施中编辑任何内容的任何方面，以提供卓越的体验，提升内容速度并提供最先进的开发人员体验。
* [使用 Universal Editor 创作内容](/help/sites-cloud/authoring/universal-editor/authoring.md) – 了解内容作者使用 Universal Editor 创建内容是多么轻松和直观。
* [使用 Universal Editor 发布内容](/help/sites-cloud/authoring/universal-editor/publishing.md) – 了解 Universal Editor 如何发布内容以及您的应用程序如何处理发布的内容。
* [Universal Editor 架构](architecture.md) – 了解 Universal Editor 的架构以及数据如何在其服务和层之间流动。
* [属性和类型](attributes-types.md) – 了解 Universal Editor 所需的数据属性和类型。
* [Universal Editor 身份验证](authentication.md) – 了解 Universal Editor 如何进行身份验证。

