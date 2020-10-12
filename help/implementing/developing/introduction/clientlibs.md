---
title: 将AEM上的客户端库用作Cloud Service
description: AEM提供客户端库文件夹，允许您在存储库中存储客户端代码(clientlibs)，将其组织到类别中，并定义何时以及如何向客户端提供每个类别
translation-type: tm+mt
source-git-commit: d4c031e17c0c83e44b687474502252c89ed37922
workflow-type: tm+mt
source-wordcount: '2571'
ht-degree: 1%

---


# 将AEM上的客户端库用作Cloud Service {#using-client-side-libraries}

数字体验严重依赖由复杂的JavaScript和CSS代码驱动的客户端处理。 AEM客户端库(clientlibs)允许您在存储库中组织和集中存储这些客户端库。 再加上AEM [Project原型中的前端构建流程](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype/uifrontend.html) ，为AEM项目管理前端代码变得简单。

在AEM中使用clientlibs的优势包括：

* 客户端代码与所有其他应用程序代码和内容一样存储在存储库中
* AEM中的Clientlibs可以将所有CSS和JS聚合到一个文件中
* 通过调度程序可访问的路径公开客户端 [库](/help/implementing/dispatcher/disp-overview.md)
* 允许重写引用文件或图像的路径

Clientlibs是用于从AEM交付CSS和Javascript的内置解决方案。

>[!TIP]
>
>为AEM项目创建CSS和Javascript的前端开发人员还应熟悉 [AEM Project Archetype及其自动化前端构建流程。](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype/uifrontend.html)

## 什么是客户端库 {#what-are-clientlibs}

站点需要JavaScript和CSS以及静态资源（如要在客户端处理的图标和Web字体）。 clientlib是AEM机制，可引用(根据需要按类别)并提供此类资源。

AEM将站点的CSS和Javascript收集到一个中央位置的单个文件中，以确保HTML输出中只包含任何资源的一个副本。 这最大限度地提高了投放效率，并允许通过代理在存储库中集中维护这些资源，从而保持访问安全。

## 作为Cloud Service的AEM前端开发 {#fed-for-aemaacs}

所有JavaScript、CSS和其他前端资源都应在AEM Project Archetype [的ui.frontend模块中进行维护。](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype/uifrontend.html) 原型的灵活性允许您使用您选择的现代Web工具创建和管理这些资源。

原型随后可以将资源编译为单个CSS和JS文件，并自动将其嵌入到 `cq:clientLibraryFolder` 存储库中。

## 客户端库文件夹结构 {#clientlib-folders}

客户端库文件夹是类型的存储库节点 `cq:ClientLibraryFolder`。 它在CND记 [号中的定义](https://jackrabbit.apache.org/node-type-notation.html)

```text
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

* `cq:ClientLibraryFolder` 节点可以放置在存储库子 `/apps` 树中的任意位置。
* 使用节 `categories` 点的属性来标识它所属的库类别。

每个 `cq:ClientLibraryFolder` 文件都会填入一组JS和／或CSS文件，以及一些支持文件（请参阅下文）。 重要属性 `cq:ClientLibraryFolder` 的配置如下：

* `allowProxy`:由于所有clientlibs都必须存储在下 `apps`面，因此此属性允许通过代理servlet访问clientlibraries。 请参 [阅查找客户端库文件夹和使用下面的代理客户端库](#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) Servlet。
* `categories`:标识今秋内JS和／或CSS文件集所属的类别 `cq:ClientLibraryFolder` 符。 该 `categories` 属性具有多值，允许库文件夹成为多个类别的一部分（请参见下面，了解这可能有何用）。

如果客户端库文件夹包含一个或多个在运行时合并为单个JS和／或CSS文件的源文件。 生成的文件的名称是扩展名为或文件 `.js` 名的 `.css` 节点名称。 例如，名为的库节点 `cq.jquery` 将生成名为或的 `cq.jquery.js` 文件 `cq.jquery.css`。

客户端库文件夹包含以下项目：

* JS和／或CSS源文件
* 支持CSS样式的静态资源，如图标、Web字体等。
* 一个 `js.txt` 文件和／或一 `css.txt` 个文件，用于标识要合并到生成的JS和／或CSS文件中的源文件

![Clientlib体系结构](assets/clientlib-architecture.drawio.png)

## 创建客户端库文件夹 {#creating-clientlib-folders}

客户端库必须位于下 `/apps`面。 这是为了更好地将代码与内容和配置隔离开来。

为了能够访问下的客 `/apps` 户端库，使用代理服务器。 ACL仍然强制在客户端库文件夹上，但如果属性设置为，则Servlet允许 `/etc.clientlibs/` 通过 `allowProxy` 读取内容 `true`。

1. Open CRXDE Lite in a web browser (`https://<host>:<port>/crx/de`).
1. 选择文件夹 `/apps` ，然后单击“ **创建”>“创建节点**”。
1. 输入库文件夹的名称，并在“类型” **列表** 中选择 `cq:ClientLibraryFolder`。 单击 **确定** ，然后单击 **全部保存**。
1. 要指定库所属的类别或类别，请选 `cq:ClientLibraryFolder` 择节点，添加以下属性，然后单击“全 **部保存**:
   * 名称: `categories`
   * 类型：字符串
   * 值：类别名称
   * 多：已选择
1. 要通过代理访问客户端库，请选 `/etc.clientlibs`择节 `cq:ClientLibraryFolder` 点，添加以下属性，然后单击 **全部保存**:
   * 名称: `allowProxy`
   * 类型：布尔型
   * 值: `true`
1. 如果需要管理静态资源，请在客户端库文件夹下 `resources` 创建一个名为子文件夹。
   * 如果将静态资源存储在该文 `resources`件夹下，则无法在发布实例上引用这些资源。
1. 将源文件添加到库文件夹。
   * 这通常由AEM Project Archetype的前端构建 [过程完成。](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype/uifrontend.html)
   * 如果需要，可以在子文件夹中组织源文件。
1. 选择客户端库文件夹，然后单击“ **创建”>“创建文件**”。
1. 在“文件名”框中，键入以下文件名之一，然后单击“确定”:
   * **`js.txt`:** 使用此文件名生成JavaScript文件。
   * **`css.txt`:** 使用此文件名生成层叠样式表。
1. 打开文件并键入以下文本以标识源文件路径的根：
   * `#base=*[root]*`
   * 替换 `[root]` 为包含源文件的文件夹（相对于TXT文件）的路径。 例如，当源文件与TXT文件位于同一文件夹中时，请使用以下文本：
      * `#base=.`
   * 以下代码将根设置为节点下名为mobile的文 `cq:ClientLibraryFolder` 件夹：
      * `#base=mobile`
1. 在下面的行 `#base=[root]`中，键入源文件相对于根的路径。 将每个文件名放在单独的行上。
1. 单击“ **全部保存**”。

## 提供客户端库 {#serving-clientlibs}

根据需要配置客户端 [库文件夹后](#creating-clientlib-folders) ，可以通过代理请求客户端库。 例如：

* 您有一个clientlib `/apps/myproject/clientlibs/foo`
* 您的静态图像 `/apps/myprojects/clientlibs/foo/resources/icon.png`

该 `allowProxy` 属性允许您请求：

* 通过j的clientlib`/etc.clientlibs/myprojects/clientlibs/foo.js`
* 静态图像 `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

### 通过HTL加载客户端库 {#loading-via-htl}

在客户端库文件夹中成功存储和管理客户端库后，即可通过HTL访问它们。

客户端库通过AEM提供的辅助模板加载，可通过该模板进行访问 `data-sly-use`。 帮助程序模板在此文件中可用，可通过调用该模板 `data-sly-call`。

每个帮助程序模板都 `categories` 需要一个用于引用所需客户端库的选项。 该选项可以是字符串值的数组，也可以是包含逗号分隔值列表的字符串。

[有关通过HTL加载客户端](https://docs.adobe.com/content/help/en/experience-manager-htl/using/getting-started/getting-started.html#loading-client-libraries) (ClientLibs)的更多详细信息，请参阅HTL文档。

<!--
### Setting Cache Timestamps {#setting-cache-timestamps}

This is possible. Still need detail.
-->

## 创作与发布时的客户端库 {#clientlibs-author-publish}

AEM publish实例上需要大多数clientlib。 即，大多数客户端的目的是生成内容的最终用户体验。 对于发布实例上的 [clientlib，前端构建工具](#fed-for-aemaacs) ，可通过客户端库文 [件夹进行使用和部署，如上所述。](#creating-clientlib-folders)

但有时可能需要客户端库来自定义创作体验。 例如，自定义对话框可能需要将少量CSS或JS部署到AEM创作实例。

### 在创作时管理客户端库 {#clientlibs-on-author}

如果您需要在创作时使用客户端库，则可以使用与发布相 `/apps` 同的方法创建客户端库，但直接将其编写在 `/apps/.../clientlibs/foo` 下，而不是创建整个项目来管理它。

然后，您可以将客户端库添加到现成的客户端库类别，从而“挂接”到创作JS中。

## 调试工具 {#debugging-tools}

AEM提供了多种工具用于调试和测试客户端库文件夹。

### 发现客户端库 {#discover-client-libraries}

组 `/libs/cq/granite/components/dumplibs/dumplibs` 件会生成有关系统上所有客户端库文件夹的信息页面。 节 `/libs/granite/ui/content/dumplibs` 点将组件作为资源类型。 要打开页面，请使用以下URL（根据需要更改主机和端口）:

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

信息包括库路径和类型（CSS或JS）以及库属性的值，如类别和依赖关系。 页面上的后续表显示了每个类别和渠道中的库。

### 请参阅生成的输出 {#see-generated-output}

该 `dumplibs` 组件包含一个测试选择器，它显示为标记生成的源 `ui:includeClientLib` 代码。 该页面包含js、css和主题属性的不同组合的代码。

1. 使用以下方法之一打开“测试输出”页：
   * 在该页 `dumplibs.html` 面中，单击“单击此处 **以输出测试”文本中的链接** 。
   * 在Web浏览器中打开以下URL（根据需要使用不同的主机和端口）:
      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`
   * 默认页显示没有类别属性值的标记的输出。
1. 要查看类别的输出，请键入客户端库属性的值，然 `categories` 后单击“提 **交查询”**。

## 其他客户端库文件夹功能 {#additional-features}

AEM中的客户端库文件夹还支持许多其他功能。 但是，AEM作为Cloud Service不要求使用这些资源，因此不鼓励使用它们。 这里列出它们是为了完整。

>[!WARNING]
>
>AEM作为Cloud Service不需要客户端库文件夹的这些附加功能，因此不建议使用这些功能。 这里列出它们是为了完整。

### AdobeGranite HTML Li库管理器 {#html-library-manager}

其他客户端库设置可通过系统控 **制台的AdobeGranite** HTML库管理器面板( `https://<host>:<port>/system/console/configMgr`位于)。

### 其他文件夹属性 {#additional-folder-properties}

其他文件夹属性包括允许控制依赖项和嵌入，但通常不再需要，也不建议使用：

* `dependencies`:这是此库文件夹所依赖的其他客户端库类别的列表。 例如，给定两个 `cq:ClientLibraryFolder` 节点 `F` ，如果某个文件需要另一个文件才能正常工作，则至少其中一个节点 `G`应该 `F``G``categories``G``dependencies``F`位于中。
* `embed`:用于嵌入来自其他库的代码。 如果节 `F` 点嵌 `G` 入节点， `H`则生成的HTML将由节点和的内容组 `G` 成 `H`。

### 链接到依赖项 {#linking-to-dependencies}

当客户端库文件夹中的代码引用其他库时，将其他库标识为依赖关系。 引 `ui:includeClientLib` 用客户端库文件夹的标记会导致HTML代码包含指向生成的库文件以及依赖项的链接。

依赖关系必须是另一个 `cq:ClientLibraryFolder`。 要标识依赖关系，请向节点添 `cq:ClientLibraryFolder` 加具有以下属性的属性：

* **名称：** 依赖
* **类型：** 字符串[]
* **值：** 当前库文件夹所依赖的cq:ClientLibraryFolder节点的类别属性值。

例如，该 `/etc/clientlibs/myclientlibs/publicmain` 库具有依赖 `cq.jquery` 关系。 引用主客户端库的页面生成包含以下代码的HTML:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### 从其他库嵌入代码 {#embedding-code-from-other-libraries}

可以将客户端库中的代码嵌入到另一个客户端库中。 在运行时，嵌入库生成的JS和CSS文件包括嵌入库的代码。

嵌入代码对于提供对存储在存储库的安全区域中的库的访问非常有用。

#### 特定于应用程序的客户端库文件夹 {#app-specific-client-library-folders}

最好将所有与应用程序相关的文件保留在下面的应用程序文件夹中 `/app`。 拒绝网站访客访问该文件夹也是最佳做 `/app` 法。 为了同时满足这两种最佳实践，请在嵌入以下客户端库 `/etc` 的文件夹下创建一个客户端库文件夹 `/app`。

使用类别属性标识要嵌入的客户端库文件夹。 要嵌入库，请使用以下属性属 `cq:ClientLibraryFolder` 性向嵌入节点添加属性：

* **名称：** 嵌入
* **类型：** 字符串[]
* **值：** 要嵌入的节点的类别 `cq:ClientLibraryFolder` 属性值。

#### 使用嵌入最小化请求 {#using-embedding-to-minimize-requests}

在某些情况下，您可能会发现，发布实例为典型页面生成的最终HTML包含相对大量的 `<script>` 元素。

在这种情况下，将所有所需的客户端库代码合并到单个文件中，以减少页面加载时来回请求的数量，这是非常有用的。 为此，您可以使用 `embed` 节点的embed属性将所需的库添加到特定于应用程序的客户端 `cq:ClientLibraryFolder` 库中。

#### CSS文件中的路径 {#paths-in-css-files}

嵌入CSS文件时，生成的CSS代码使用相对于嵌入库的资源的路径。 例如，可公开访问的库嵌 `/etc/client/libraries/myclientlibs/publicmain` 入客户端 `/apps/myapp/clientlib` 库：

文 `main.css` 件包含以下样式：

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

节点生成的CSS `publicmain` 文件包含以下样式（使用原始图像的URL）:

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

#### 请参阅HTML输出中的嵌入文件 {#see-embedded-files}

要跟踪嵌入代码的来源，或确保嵌入的客户端库生成预期结果，您可以在运行时查看嵌入的文件名称。 要查看文件名，请将参 `debugClientLibs=true` 数追加到网页的URL。 生成的库包含语 `@import` 句而不是嵌入代码。

在上一个“从其他库 [嵌入代码”部分的示例中](#embedding-code-from-other-libraries) ，客户端库 `/etc/client/libraries/myclientlibs/publicmain` 文件夹会嵌入客户端 `/apps/myapp/clientlib` 库文件夹。 将参数追加到网页后，将在网页的源代码中生成以下链接：

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

打开文 `publicmain.css` 件会显示以下代码：

```javascript
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. 在Web浏览器的地址框中，将以下文本追加到HTML的URL:
   * `?debugClientLibs=true`
1. 载入页面时，视图页面源。
1. 单击作为链接元素的href提供的链接以打开文件并视图源代码。

### 使用预处理器 {#using-preprocessors}

AEM支持可插拔的预处理器，并随附 [对JUI Compressor](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) for CSS和JavaScript以及Google Closure Compiler(GCC) [for JavaScript(GCC)的支持](https://developers.google.com/closure/compiler/) ,YU设置为AEM默认预处理器。

可插拔预处理器允许灵活使用，包括：

* 定义可处理脚本源的脚本处理器
* 处理器可配置选项
* 处理器可用于微型化，也可用于非微型化情况
* clientlib可以定义要使用哪个处理器

>[!NOTE]
>
>默认情况下，AEM使用YUI压缩程序。 有关一 [列表已知问题](https://github.com/yui/yuicompressor/issues) ，请参阅YUI Compressor GitHub文档。 对于特定客户端，切换到GCC压缩程序可解决使用YUI时观察到的一些问题。

>[!CAUTION]
>
>不要将精简库放在客户端库中。 而是提供原始库，如果需要进行微型化，请使用预处理器的选项。

#### 使用 {#usage}

您可以选择根据客户端库或系统范围配置预处理器配置。

* 添加多值属性 `cssProcessor` 并 `jsProcessor` 在clientlibrary节点上添加
* 或通过HTML库管理器OSGi配置 **定义系统默认** 配置。

clientlib节点上的预处理器配置优先于OSGI配置。

#### 格式和示例 {#format-and-examples}

##### 格式 {#format}

```javascript
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

##### YUI压缩程序，用于CSS微型化和GCC，用于JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```javascript
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

##### Typescript to Preprocess, and GCC to Minify and Obfuscate {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

```javascript
jsProcessor: [
   "default:typescript",
   "min:typescript",
   "min:gcc;obfuscate=true"
]
```

##### 其他GCC选项 {#additional-gcc-options}

```javascript
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT5")
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

有关GCC选项的更多详细信息，请参 [阅GCC文档](https://developers.google.com/closure/compiler/docs/compilation_levels)。

#### 设置系统默认迷你符 {#set-system-default-minifier}

在AEM中，YUI设置为默认的minifier。 要将此更改为GCC，请执行以下步骤。

1. 转到Apache Felix Config Manager（位于）(`http://<host>:<portY/system/console/configMgr`)
1. 查找并编辑 **AdobeGranite HTML库管理器**。
1. 启用 **Minify** 选项（如果尚未启用）。
1. 将“JS处理 **器默认配置”值设** 置 `min:gcc`为。
   * 如果以分号分隔，则可以传递选项，例如 `min:gcc;obfuscate=true`.
1. Click **Save** to save the changes.
