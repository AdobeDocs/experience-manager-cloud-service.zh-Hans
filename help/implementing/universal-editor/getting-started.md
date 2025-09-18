---
title: AEM Universal Editor 快速入门
description: 了解如何获取 Universal Editor 访问权限以及如何对第一个 AEM 应用程序插桩以使用 Universal Editor。
exl-id: 9091a29e-2deb-4de7-97ea-53ad29c7c44d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 8e1610e2835a9e85de2d2bffa6a883777c92fe96
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 100%

---


# AEM Universal Editor 快速入门 {#getting-started}

了解如何获取 Universal Editor 访问权限以及如何对第一个 AEM 应用程序插桩以使用 Universal Editor。

>[!TIP]
>
>如果您想深入研究一个示例，可以查看 [GitHub 上的通用编辑器应用程序示例](https://github.com/adobe/universal-editor-sample-editable-app)。

通用编辑器可以编辑来自任何来源的内容，本文档将以一个 AEM 应用程序为例。本文档将引导您完成这些步骤。

## 适配页面 {#instrument-page}

通用编辑器需要一个 JavaScript 库才能在编辑器中渲染和编辑页面。

此外，通用编辑器服务需要一个[统一资源名称 (URN)](https://en.wikipedia.org/wiki/Uniform_Resource_Name) 来为要编辑的应用程序中的内容识别和使用正确的后端系统。因此，需要 URN 架构将内容映射回内容资源。

### 包含通用编辑器 CORS 库 {#cors-library}

要让通用编辑器与您的应用程序连接，您的应用程序必须包含通用编辑器 CORS 库。将以下脚本添加到您的应用程序中。

```html
 <script src="https://universal-editor-service.adobe.io/cors.js" async></script>
```

### 创建连接 {#connections}

应用程序中使用的连接将作为 `<meta>` 标记存储在页面的 `<head>` 中。

```html
<meta name="urn:adobe:aue:<category>:<referenceName>" content="<protocol>:<url>">
```

* `<category>` - 这个连接分类有两个选项。
   * `system` - 用于连接端点
   * `config` - 用于[定义可选配置设置](#configuration-settings)
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

需要时，您可以使用连接 URN 中的 `config` 前缀来设置服务和扩展端点。

如果您不想使用 Adobe 托管的通用编辑器服务，而是使用您自己的托管版本，您可以在元标记中设置这一点。要覆盖通用编辑器提供的默认服务端点，请设置您自己的服务端点：

* 元名称 - `urn:adobe:aue:config:service`
* 元内容 - `content="https://adobe.com"`（示例）

```html
<meta name="urn:adobe:aue:config:service" content="<url>">
```

如果您只想为页面启用特定的扩展，您可以在元标记中设置这一点。要获取扩展，请设置扩展端点：

* 元名称：`urn:adobe:aue:config:extensions`
* 元内容：`content="https://adobe.com,https://anotherone.com,https://onemore.com"`（示例）

```html
<meta name="urn:adobe:aue:config:extensions" content="<url>,<url>,<url>">
```

## 定义应为哪些内容路径或 `sling:resourceType` 打开通用编辑器。（可选） {#content-paths}

如果您现有的 AEM 项目使用[页面编辑器](/help/sites-cloud/authoring/page-editor/introduction.md)，当内容作者编辑页面时，页面会自动在页面编辑器中打开。您可以根据内容路径或 `sling:resourceType` 定义 AEM 应打开哪个编辑器，这样无论所选内容需要使用哪个编辑器，都能为作者带来无缝体验。

1. 打开配置管理器。

   `http://<host>:<port>/system/console/configMgr`

1. 在列表中找到&#x200B;**通用编辑器 URL 服务**，然后点击&#x200B;**编辑配置值**。

1. 定义应为哪些内容路径或 `sling:resourceType` 打开通用编辑器。

   * 在&#x200B;**通用编辑器打开映射**&#x200B;字段中，提供通用编辑器为其打开的路径。
   * 在 Universal Editor 打开的 **Sling:resourceTypes**&#x200B;字段中，提供 Universal Editor 直接打开的一个资源列表。

1. 单击&#x200B;**保存**。

1. 检查您的[外部化器配置](/help/implementing/developing/tools/externalizer.md)，确保至少已设置了本地、作者和发布三个环境，如下例所示。

   ```text
   "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
   "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
   "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]"
   ```

完成这些配置步骤后，AEM 将按以下顺序为页面打开 Universal Editor。

1. AEM 会检查 `Universal Editor Opening Mapping` 中的映射，如果内容位于那里定义的任何路径下，就会为其打开 Universal Editor。
1. 如果内容不位于 `Universal Editor Opening Mapping` 中定义的路径下，AEM 会检查此内容的 `resourceType` 是否与 Universal Editor 打开的 **Sling:resourceTypes 中定义的类型匹配**，如果内容与其中一个类型匹配，就会在 `${author}${path}.html` 上为其打开 Universal Editor。
1. 否则，AEM 就打开页面编辑器。

以下变量可用于在&#x200B;**通用编辑器打开映射**&#x200B;字段中定义您的映射。

* `path`：要打开的资源的内容路径
* `localhost`：没有架构的用于 `localhost` 的外部化器条目，例如 `localhost:4502`
* `author`：没有架构的用于作者的外部化器条目，例如 `localhost:4502`
* `publish`：没有架构的用于发布的外部化器条目，例如 `localhost:4503`
* `preview`：没有架构的用于预览的外部化器条目，例如 `localhost:4504`
* `env`：`prod`、`stage`、`dev` 基于已定义的 Sling 运行模式
* `token`：`QueryTokenAuthenticationHandler` 需要查询令牌

### 映射示例 {#example-mappings}

* 打开 AEM 作者上 `/content/foo` 下的所有页面：

   * `/content/foo:${author}${path}.html?login-token=${token}`
   * 这会打开 `https://localhost:4502/content/foo/x.html?login-token=<token>`

* 打开远程 NextJS 服务器上 `/content/bar` 下的所有页面，提供所有变量的信息：

   * `/content/bar:nextjs.server${path}?env=${env}&author=https://${author}&publish=https://${publish}&login-token=${token}`
   * 这会打开 `https://nextjs.server/content/bar/x?env=prod&author=https://localhost:4502&publish=https://localhost:4503&login-token=<token>`

## 您已准备好使用 Universal Editor {#youre-ready}

您的应用程序现已插桩，可以使用 Universal Editor 了！

请参阅[使用 Universal Editor 创作内容](/help/sites-cloud/authoring/universal-editor/authoring.md)，了解内容作者使用 Universal Editor 创建内容是多么轻松和直观。

{{ue-headless-auth}}

## 其他资源 {#additional-resources}

要了解有关 Universal Editor 的更多信息，请参阅这些文档。

* [Universal Editor 简介](introduction.md) – 了解 Universal Editor 如何支持在任意实施中编辑任何内容的任何方面，以提供卓越的体验，提升内容速度并提供最先进的开发人员体验。
* [使用 Universal Editor 创作内容](/help/sites-cloud/authoring/universal-editor/authoring.md) – 了解内容作者使用 Universal Editor 创建内容是多么轻松和直观。
* [使用 Universal Editor 发布内容](/help/implementing/universal-editor/publishing.md) – 了解 Universal Editor 如何发布内容以及您的应用程序如何处理发布的内容。
* [Universal Editor 架构](architecture.md) – 了解 Universal Editor 的架构以及数据如何在其服务和层之间流动。
* [属性和类型](attributes-types.md) – 了解 Universal Editor 所需的数据属性和类型。
* [Universal Editor 身份验证](authentication.md) – 了解 Universal Editor 如何进行身份验证。

