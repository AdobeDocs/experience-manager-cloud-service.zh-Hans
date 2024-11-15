---
title: AEM Universal Editor 快速入门
description: 了解如何获取 Universal Editor 访问权限以及如何对第一个 AEM 应用程序插桩以使用 Universal Editor。
exl-id: 9091a29e-2deb-4de7-97ea-53ad29c7c44d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: edef86c67becf3b8094196d39baa9e69d6c81777
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 76%

---


# AEM Universal Editor 快速入门 {#getting-started}

了解如何获取 Universal Editor 访问权限以及如何对第一个 AEM 应用程序插桩以使用 Universal Editor。

>[!TIP]
>
>如果您想深入研究示例，可以查看 [GitHub 上的 Universal Editor 示例应用程序](https://github.com/adobe/universal-editor-sample-editable-app)。

尽管通用编辑器可以编辑来自任何源的内容，但本文档将以AEM应用程序为例。 本文档将引导您完成这些步骤。

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

