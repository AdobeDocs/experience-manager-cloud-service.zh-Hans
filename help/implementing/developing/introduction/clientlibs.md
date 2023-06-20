---
title: 在AEMas a Cloud Service上使用客户端库
description: AEM提供了客户端库文件夹，通过该文件夹，您可以在存储库中存储客户端代码(clientlibs)，将其组织为不同类别，并定义每个类别的代码何时以及如何提供给客户端
exl-id: 370db625-09bf-43fb-919d-4699edaac7c8
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '2562'
ht-degree: 1%

---


# 在AEMas a Cloud Service上使用客户端库 {#using-client-side-libraries}

数字体验在很大程度上依赖于由复杂的JavaScript和CSS代码驱动的客户端处理。 AEM客户端库(clientlibs)允许您在存储库中组织和集中存储这些客户端库。 与 [AEM项目原型中的前端构建过程，](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) 可以轻松管理AEM项目的前端代码。

在AEM中使用clientlibs的优点包括：

* 客户端代码与所有其他应用程序代码和内容一样，存储在存储库中
* AEM中的Clientlibs可以将所有CSS和JS聚合到一个文件中
* 通过路径公开clientlibs，该路径可通过 [dispatcher](/help/implementing/dispatcher/disp-overview.md)
* 允许重写引用的文件或图像的路径

Clientlibs是用于从AEM提供CSS和Javascript的内置解决方案。

>[!TIP]
>
>为AEM项目创建CSS和Javascript的前端开发人员还应熟悉 [AEM项目原型及其自动前端构建过程。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)

## 什么是客户端库 {#what-are-clientlibs}

站点需要在客户端处理JavaScript和CSS以及静态资源，例如图标和Web字体。 clientlib是一种引用（如果需要，按类别）并为此类资源提供服务的AEM机制。

AEM将站点的CSS和Javascript收集到一个位于中心位置的文件中，以确保HTML输出中只包含任何资源的一个副本。 这样可以最大限度地提高交付效率，并且可以通过代理在存储库中集中维护此类资源，从而确保访问安全。

## AEMas a Cloud Service的前端开发 {#fed-for-aemaacs}

所有JavaScript、CSS和其他前端资产都应在 [AEM项目原型的ui.frontend模块。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) 原型的灵活性允许您使用所选择的现代Web工具来创建和管理这些资源。

然后，原型可以将资源编译为单个CSS和JS文件，并将它们自动嵌入到 `cq:clientLibraryFolder` 在存储库中。

## 客户端库文件夹结构 {#clientlib-folders}

客户端库文件夹是类型的存储库节点 `cq:ClientLibraryFolder`. 其定义位于 [CND表示法](https://jackrabbit.apache.org/node-type-notation.html) 是

```text
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

* `cq:ClientLibraryFolder` 节点可以放置在 `/apps` 存储库的子树。
* 使用 `categories` 节点的属性，用于标识其所属的库类别。

每个 `cq:ClientLibraryFolder` 使用一组JS和/或CSS文件以及几个支持文件（见下文）填充。 的重要属性 `cq:ClientLibraryFolder` 配置如下：

* `allowProxy`：由于所有clientlib都必须存储在 `apps`，此属性允许通过代理servlet访问客户端库。 请参阅部分 [查找客户端库文件夹并使用代理客户端库Servlet](#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) 下面的。
* `categories`：标识此JS和/或CSS文件集所属的类别 `cq:ClientLibraryFolder` 摔倒。 此 `categories` 属性是多值属性，允许库文件夹属于多个类别（请参阅下方了解其用处）。

如果client library文件夹包含一个或多个源文件，则在运行时，这些文件将合并到单个JS和/或CSS文件中。 生成的文件的名称是节点名称，带有 `.js` 或 `.css` 文件扩展名。 例如，库节点命名为 `cq.jquery` 生成的文件中的结果，名为 `cq.jquery.js` 或 `cq.jquery.css`.

客户端库文件夹包含以下项目：

* JS和/或CSS源文件
* 支持CSS样式的静态资源，例如图标、Web字体等。
* 一个 `js.txt` 文件和/或一个 `css.txt` 标识要合并到生成的JS和/或CSS文件中的源文件的文件

![Clientlib架构](assets/clientlib-architecture.drawio.png)

## 创建客户端库文件夹 {#creating-clientlib-folders}

客户端库必须位于 `/apps`. 此规则是更好地将代码与内容和配置隔离所必需的。

对于下的客户端库 `/apps` 要访问，将使用代理servelt。 仍会在客户端库文件夹上强制执行ACL，但servlet允许通过读取内容 `/etc.clientlibs/` 如果 `allowProxy` 属性设置为 `true`.

1. 在Web浏览器中打开CRXDE Lite(`https://<host>:<port>/crx/de`)。
1. 选择 `/apps` 文件夹并单击 **创建>创建节点**.
1. 输入库文件夹的名称，然后在 **类型** 列表选择 `cq:ClientLibraryFolder`. 单击 **确定** 然后单击 **全部保存**.
1. 要指定库所属的类别，请选择 `cq:ClientLibraryFolder` 节点，添加以下属性，然后单击 **全部保存**：
   * 名称: `categories`
   * 类型：字符串
   * 值：类别名称
   * 多个：已选定
1. 为了通过下的代理访问客户端库 `/etc.clientlibs`，选择 `cq:ClientLibraryFolder` 节点，添加以下属性，然后单击 **全部保存**：
   * 名称: `allowProxy`
   * 类型：布尔值
   * 价值: `true`
1. 如果需要管理静态资源，请创建一个名为的子文件夹 `resources` 客户端库文件夹下方。
   * 如果您将静态资源存储在文件夹下以外的任何位置 `resources`，无法在发布实例上引用它们。
1. 将源文件添加到库文件夹。
   * 这通常通过的前端构建过程完成 [AEM项目原型。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)
   * 如果需要，可以在子文件夹中组织源文件。
1. 选择客户端库文件夹并单击 **“创建”>“创建文件”**.
1. 在“文件名”框中，键入以下文件名之一，然后单击“确定”：
   * **`js.txt`：** 使用此文件名可生成JavaScript文件。
   * **`css.txt`：** 使用此文件名可生成层叠样式表。
1. 打开文件并键入以下文本以标识源文件路径的根：
   * `#base=*[root]*`
   * Replace `[root]` 包含源文件的文件夹的路径（相对于TXT文件）。 例如，当源文件与TXT文件位于同一文件夹时，请使用以下文本：
      * `#base=.`
   * 以下代码将根设置为名为mobile的文件夹，该文件夹位于 `cq:ClientLibraryFolder` 节点：
      * `#base=mobile`
1. 在以下行上 `#base=[root]`，键入源文件相对于根的路径。 将每个文件名放在单独的一行上。
1. 单击 **全部保存**.

## 为客户端库提供服务 {#serving-clientlibs}

一旦您的客户端库文件夹 [根据需要进行配置，](#creating-clientlib-folders) 可以通过代理请求您的clientlibs。 例如：

* 您在中有一个clientlib `/apps/myproject/clientlibs/foo`
* 您有一个静态图像 `/apps/myprojects/clientlibs/foo/resources/icon.png`

此 `allowProxy` 属性允许您请求：

* clientlib通过 `/etc.clientlibs/myprojects/clientlibs/foo.js`
* 静态图像，通过 `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

### 通过HTL加载客户端库 {#loading-via-htl}

一旦您的clientlibs成功存储并管理在其客户端库文件夹中，便可以通过HTL访问它们。

客户端库是通过AEM提供的帮助程序模板加载的，该模板可通过访问 `data-sly-use`. 帮助程序模板在此文件中可用，可通过调用 `data-sly-call`.

每个帮助程序模板都需要一个 `categories` 选项来引用所需的客户端库。该选项可以是字符串值的数组，也可以是包含逗号分隔值列表的字符串。

[请参阅HTL文档](https://experienceleague.adobe.com/docs/experience-manager-htl/using/getting-started/getting-started.html#loading-client-libraries) 有关通过HTL加载clientlibs的更多详细信息。

<!--
### Setting Cache Timestamps {#setting-cache-timestamps}

This is possible. Still need detail.
-->

## 有关创作与发布的客户端库 {#clientlibs-author-publish}

AEM发布实例上需要大多数clientlibs。 也就是说，大多数clientlibs的目的是生成内容的最终用户体验。 对于发布实例上的clientlibs， [前端构建工具](#fed-for-aemaacs) 可以通过以下方式使用和部署 [客户端库文件夹（如上所述）。](#creating-clientlib-folders)

但是，有时可能需要客户端库来自定义创作体验。 例如，自定义对话框可能需要将少量CSS或JS部署到AEM创作实例。

### 管理有关作者的客户端库 {#clientlibs-on-author}

如果您需要在作者上使用客户端库，可以在以下位置创建客户端库： `/apps` 使用与publish相同的方法，但将其直接写在 `/apps/.../clientlibs/foo` 而不是创建整个项目来管理它。

然后，您可以通过将客户端库添加到现成的客户端库类别来“挂接”到创作JS中。

## 调试工具 {#debugging-tools}

AEM提供了多种用于调试和测试客户端库文件夹的工具。

### 发现客户端库 {#discover-client-libraries}

此 `/libs/cq/granite/components/dumplibs/dumplibs` 组件生成一个页面，其中包含有关系统上所有客户端库文件夹的信息。 此 `/libs/granite/ui/content/dumplibs` 节点将组件作为资源类型。 要打开该页面，请使用以下URL（根据需要更改主机和端口）：

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

这些信息包括库路径和类型（CSS或JS）以及库属性的值（如类别和依赖项）。 页面上的后续表将显示每个类别和渠道中的库。

### 查看生成的输出 {#see-generated-output}

此 `dumplibs` 组件包括一个测试选择器，该选择器显示为生成的源代码 `ui:includeClientLib` 标记之间。 该页面包含js、css和主题化属性的不同组合的代码。

1. 使用以下方法之一打开“测试输出”页：
   * 从 `dumplibs.html` 页面上，单击以下位置中的链接： **单击此处进行输出测试** 文本。
   * 在Web浏览器中打开以下URL（根据需要使用不同的主机和端口）：
      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`
   * 默认页面显示没有categories属性值的标记的输出。
1. 要查看某个类别的输出，请键入客户端库的 `categories` 属性并单击 **提交查询**.

## 其他客户端库文件夹功能 {#additional-features}

AEM中的客户端库文件夹支持许多其他功能。 但是，在AEMas a Cloud Service上不需要这些参数，因此建议不要使用这些参数。 为了完整起见，此处列出了它们。

>[!WARNING]
>
>在AEMas a Cloud Service上不需要客户端库文件夹的这些附加功能，因此建议不要使用这些功能。 为了完整起见，此处列出了它们。

### AdobeGraniteHTML库管理器 {#html-library-manager}

其他客户端库设置可通过 **AdobeGraniteHTML库管理器** 位于的系统控制台面板 `https://<host>:<port>/system/console/configMgr`)。

### 其他文件夹属性 {#additional-folder-properties}

其他文件夹属性包括允许控制依赖项和嵌入，但通常不再需要这些属性，因此建议不要使用这些属性：

* `dependencies`：这是此库文件夹所依赖的其他客户端库类别的列表。 例如，给定两个 `cq:ClientLibraryFolder` 节点 `F` 和 `G`，如果文件位于 `F` 需要另一个文件 `G` 才能正常运行，则 `categories` 之 `G` 应该属于 `dependencies` 之 `F`.
* `embed`：用于嵌入其他库中的代码。 If节点 `F` 嵌入节点 `G` 和 `H`，则生成的HTML是来自节点的内容连接 `G` 和 `H`.

### 链接到依赖项 {#linking-to-dependencies}

当客户端库文件夹中的代码引用其他库时，请将其他库标识为依赖项。 此 `ui:includeClientLib` 引用了您的客户端库文件夹的标记会导致HTML代码包含指向生成的库文件以及依赖项的链接。

依赖项必须是另一个 `cq:ClientLibraryFolder`. 要识别依赖关系，请将资产添加到 `cq:ClientLibraryFolder` 节点具有以下属性：

* **名称：** 依赖关系
* **类型：** 字符串[]
* **值：** 当前库文件夹所依赖的cq：ClientLibraryFolder节点的categories属性的值。

例如， `/etc/clientlibs/myclientlibs/publicmain` 依赖于 `cq.jquery` 库。 引用主客户端库的页面会生成包含以下代码的HTML：

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### 嵌入其他库中的代码 {#embedding-code-from-other-libraries}

您可以将来自客户端库的代码嵌入到另一个客户端库中。 在运行时，嵌入库生成的JS和CSS文件包含嵌入库的代码。

嵌入代码可用于提供对存储在存储库安全区域中的库的访问权限。

#### 特定于应用程序的客户端库文件夹 {#app-specific-client-library-folders}

最佳实践是将所有与应用程序相关的文件保存在其应用程序文件夹的下方 `/apps`. 拒绝网站访客访问 `/apps` 文件夹。 为满足这两个最佳实践的要求，请在以下位置创建一个客户端库文件夹： `/etc` 嵌入以下客户端库的文件夹 `/apps`.

使用categories属性可标识要嵌入的客户端库文件夹。 要嵌入库，请向嵌入中添加属性 `cq:ClientLibraryFolder` 节点，使用以下属性属性：

* **名称：** 嵌入
* **类型：** 字符串[]
* **值：** 的类别属性的值 `cq:ClientLibraryFolder` 要嵌入的节点。

#### 使用嵌入功能将请求数降至最低 {#using-embedding-to-minimize-requests}

在某些情况下，您可能会发现发布实例为典型页面生成的最终HTML包含相对大量的 `<script>` 元素。

在这种情况下，将所有所需的客户端库代码合并到一个文件中会很有用，从而减少页面加载上的来回请求数。 要执行此操作，您可以 `embed` 所需的库将放入特定于应用程序的客户端库中，使用的嵌入属性 `cq:ClientLibraryFolder` 节点。

#### CSS文件中的路径 {#paths-in-css-files}

嵌入CSS文件时，生成的CSS代码使用相对于嵌入库的资源的路径。 例如，可公开访问的库 `/etc/client/libraries/myclientlibs/publicmain` 嵌入 `/apps/myapp/clientlib` 客户端库：

此 `main.css` 文件包含以下样式：

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

CSS文件， `publicmain` 节点使用原始图像的URL生成包含以下样式：

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

#### 请参阅HTML输出中的嵌入式文件 {#see-embedded-files}

要跟踪嵌入代码的来源，或确保嵌入的客户端库产生预期结果，您可以在运行时查看嵌入文件的名称。 要查看文件名，请附加 `debugClientLibs=true` 参数到网页URL。 生成的库包含 `@import` 语句而不是嵌入代码。

在上一个示例中 [嵌入其他库中的代码](#embedding-code-from-other-libraries) 部分， `/etc/client/libraries/myclientlibs/publicmain` 客户端库文件夹嵌入了 `/apps/myapp/clientlib` 客户端库文件夹。 将参数附加到网页会在网页的源代码中生成以下链接：

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

打开 `publicmain.css` 文件将显示以下代码：

```javascript
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. 在Web浏览器的地址框中，将以下文本附加到HTML的URL：
   * `?debugClientLibs=true`
1. 加载页面时，查看页面源。
1. 单击作为链接元素的href提供的链接，以打开文件并查看源代码。

### 使用预处理器 {#using-preprocessors}

AEM允许使用可插拔的预处理器，并且附带支持 [YUI压缩程序](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) 适用于CSS和JavaScript和 [Google Closure Compiler (GCC)](https://developers.google.com/closure/compiler/) YUI设置为AEM默认预处理器的JavaScript。

可插拔预处理器允许灵活使用，包括：

* 定义可以处理脚本源的ScriptProcessors
* 处理器可通过选项进行配置
* 处理器可用于缩小，也可用于非缩小情况
* clientlib可以定义要使用的处理器

>[!NOTE]
>
>默认情况下，AEM使用YUI压缩程序。 请参阅 [YUI压缩程序GitHub文档](https://github.com/yui/yuicompressor/issues) 以获取已知问题的列表。 为特定clientlibs切换到GCC压缩器可以解决使用YUI时观察到的一些问题。

>[!CAUTION]
>
>请勿将缩小的库放置在客户端库中。 而是提供原始库，如果需要缩小，请使用预处理器的选项。

#### 用途 {#usage}

您可以选择按clientlibrary或系统范围配置预处理器配置。

* 添加多值属性 `cssProcessor` 和 `jsProcessor` 在客户端库节点上
* 或通过定义系统默认配置 **HTML库管理器** OSGi配置

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

##### 适用于CSS缩小和GCC for JS的YUI压缩程序 {#yui-compressor-for-css-minification-and-gcc-for-js}

```javascript
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

##### 用于预处理的Typescript，然后用于缩小和模糊处理的GCC {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

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

有关GCC选项的更多详细信息，请参见 [GCC文档](https://developers.google.com/closure/compiler/docs/compilation_levels).

#### 设置系统默认缩小器 {#set-system-default-minifier}

在AEM中，YUI被设置为默认小型化器。 要将其更改为GCC，请执行以下步骤。

1. 转到Apache Felix配置管理器，网址为(`http://<host>:<portY/system/console/configMgr`)
1. 查找并编辑 **AdobeGraniteHTML库管理器**.
1. 启用 **Minify** 选项（如果尚未启用）。
1. 设置值 **JS处理器默认配置** 到 `min:gcc`.
   * 如果用分号分隔，则可以传递选项，例如， `min:gcc;obfuscate=true`.
1. 单击 **保存** 以保存更改。
