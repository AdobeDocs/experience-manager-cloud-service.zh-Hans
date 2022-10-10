---
title: 在AEMas a Cloud Service上使用客户端库
description: AEM提供客户端库文件夹，利用该文件夹可将客户端代码(clientlibs)存储在存储库中，将其整理为各个类别，并定义何时以及如何将每个类别的代码提供给客户端
exl-id: 370db625-09bf-43fb-919d-4699edaac7c8
source-git-commit: 51933d1ed509117f1ed0488900807b74f55ef46b
workflow-type: tm+mt
source-wordcount: '2568'
ht-degree: 1%

---


# 在AEMas a Cloud Service上使用客户端库 {#using-client-side-libraries}

数字体验严重依赖由复杂的JavaScript和CSS代码驱动的客户端处理。 AEM客户端库(clientlibs)允许您组织这些客户端库并将其集中存储在存储库中。 与 [AEM项目原型中的前端构建流程，](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) 为AEM项目管理前端代码变得简单。

在AEM中使用clientlibs的优势包括：

* 客户端代码与所有其他应用程序代码和内容一样存储在存储库中
* AEM中的Clientlib可将所有CSS和JS聚合到一个文件中
* 通过可通过访问的路径显示clientlib [dispatcher](/help/implementing/dispatcher/disp-overview.md)
* 允许重写引用文件或图像的路径

Clientlibs是用于从AEM交付CSS和Javascript的内置解决方案。

>[!TIP]
>
>为AEM项目创建CSS和Javascript的前端开发人员还应熟悉 [AEM项目原型及其自动化前端构建过程。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)

## 什么是客户端库 {#what-are-clientlibs}

站点需要JavaScript和CSS以及静态资源（如要在客户端处理的图标和Web字体）。 clientlib是AEM机制，可引用（如果需要，按类别）并提供此类资源。

AEM将网站的CSS和Javascript收集到一个位于中心位置的文件中，以确保HTML输出中只包含任何资源的一个副本。 这样可最大程度地提高交付效率，并允许通过代理在存储库中集中维护此类资源，从而保持访问安全。

## AEMas a Cloud Service的前端开发 {#fed-for-aemaacs}

所有JavaScript、CSS和其他前端资产都应在 [AEM项目原型的ui.frontend模块。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) 原型的灵活性允许您使用所选的现代Web工具创建和管理这些资源。

然后，原型可以将资源编译为单个CSS和JS文件，并自动将它们嵌入到 `cq:clientLibraryFolder` 中。

## 客户端库文件夹结构 {#clientlib-folders}

客户端库文件夹是类型的存储库节点 `cq:ClientLibraryFolder`. 其定义见 [CND符号](https://jackrabbit.apache.org/node-type-notation.html) is

```text
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

* `cq:ClientLibraryFolder` 节点可置于 `/apps` 存储库的子树。
* 使用 `categories` 节点的属性，以标识它所属的库类别。

每个 `cq:ClientLibraryFolder` 中填充了一组JS和/或CSS文件，以及一些支持文件（请参阅下文）。 的重要属性 `cq:ClientLibraryFolder` 配置如下：

* `allowProxy`:由于所有clientlib都必须存储在 `apps`，此属性允许通过代理servlet访问客户端库。 请参阅部分 [查找客户端库文件夹并使用代理客户端库Servlet](#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) 下。
* `categories`:标识此文件中JS和/或CSS文件集所属的类别 `cq:ClientLibraryFolder` 摔倒。 的 `categories` 属性具有多值，允许库文件夹包含在多个类别中（请参阅下文，了解这种属性的用法）。

如果客户端库文件夹包含一个或多个在运行时会合并到单个JS和/或CSS文件中的源文件。 生成的文件的名称是节点名称，其中节点名称的 `.js` 或 `.css` 文件扩展名。 例如，名为的库节点 `cq.jquery` 结果生成的文件名为 `cq.jquery.js` 或 `cq.jquery.css`.

客户端库文件夹包含以下项目：

* JS和/或CSS源文件
* 支持CSS样式的静态资源，如图标、Web字体等。
* 一个 `js.txt` 文件和/或一个 `css.txt` 用于标识要合并到生成的JS和/或CSS文件中的源文件的文件

![Clientlib架构](assets/clientlib-architecture.drawio.png)

## 创建客户端库文件夹 {#creating-clientlib-folders}

客户端库必须位于 `/apps`. 这是为了更好地将代码与内容和配置隔离开来。

为了在 `/apps` 若要访问，请使用代理服务器。 ACL仍对客户端库文件夹强制执行，但Servlet允许通过读取内容 `/etc.clientlibs/` 如果 `allowProxy` 属性设置为 `true`.

1. 在Web浏览器中打开CRXDE Lite(`https://<host>:<port>/crx/de`)。
1. 选择 `/apps` 文件夹，单击 **创建>创建节点**.
1. 在库文件夹的名称中，输入 **类型** 列表选择 `cq:ClientLibraryFolder`. 单击 **确定** 然后单击 **全部保存**.
1. 要指定库所属的类别或类别，请选择 `cq:ClientLibraryFolder` 节点中，添加以下属性，然后单击 **全部保存**:
   * 名称: `categories`
   * 类型：字符串
   * 值：类别名称
   * 多：已选择
1. 为了通过下的代理访问客户端库， `/etc.clientlibs`，选择 `cq:ClientLibraryFolder` 节点中，添加以下属性，然后单击 **全部保存**:
   * 名称: `allowProxy`
   * 类型：布尔型
   * 值: `true`
1. 如果需要管理静态资源，请创建一个名为 `resources` 客户端库文件夹下。
   * 如果将静态资源存储在文件夹以外的任意位置 `resources`，则无法在发布实例上引用这些参数。
1. 将源文件添加到库文件夹。
   * 这通常由的前端构建过程来完成 [AEM项目原型。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)
   * 您可以根据需要将源文件组织在子文件夹中。
1. 选择客户端库文件夹，然后单击 **创建>创建文件**.
1. 在文件名框中，键入以下文件名之一，然后单击“确定”：
   * **`js.txt`:** 使用此文件名生成JavaScript文件。
   * **`css.txt`:** 使用此文件名生成层叠样式表。
1. 打开文件并键入以下文本以标识源文件路径的根：
   * `#base=*[root]*`
   * 替换 `[root]` 包含源文件的文件夹路径（相对于TXT文件）。 例如，当源文件与TXT文件位于同一文件夹时，请使用以下文本：
      * `#base=.`
   * 以下代码会将根目录设置为 `cq:ClientLibraryFolder` 节点：
      * `#base=mobile`
1. 在以下行中 `#base=[root]`，键入源文件相对于根的路径。 将每个文件名放在单独的行上。
1. 单击 **全部保存**.

## 提供客户端库 {#serving-clientlibs}

在您的客户端库文件夹 [根据需要进行配置，](#creating-clientlib-folders) 您的clientlib可以通过代理进行请求。 例如：

* 您的 `/apps/myproject/clientlibs/foo`
* 您的 `/apps/myprojects/clientlibs/foo/resources/icon.png`

的 `allowProxy` 属性允许您请求：

* 通过j的clientlib`/etc.clientlibs/myprojects/clientlibs/foo.js`
* 静态图像通过 `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

### 通过HTL加载客户端库 {#loading-via-htl}

在客户端库文件夹中成功存储和管理客户端库后，即可通过HTL访问它们。

客户端库通过AEM提供的帮助程序模板加载，该模板可通过 `data-sly-use`. 此文件中提供了帮助程序模板，可通过 `data-sly-call`.

每个帮助程序模板都需要一个 `categories` 选项来引用所需的客户端库。该选项可以是字符串值的数组，也可以是包含逗号分隔值列表的字符串。

[请参阅HTL文档](https://experienceleague.adobe.com/docs/experience-manager-htl/using/getting-started/getting-started.html#loading-client-libraries) 有关通过HTL加载clientlibs的更多详细信息。

<!--
### Setting Cache Timestamps {#setting-cache-timestamps}

This is possible. Still need detail.
-->

## 创作与发布上的客户端库 {#clientlibs-author-publish}

在AEM发布实例上，将需要使用大多数clientlib。 也就是说，大多数clientlibs的目的都是为内容提供最终用户体验。 对于发布实例上的clientlib， [前端构建工具](#fed-for-aemaacs) 可通过使用和部署 [客户端库文件夹，如上所述。](#creating-clientlib-folders)

但是，有时可能需要客户端库来自定义创作体验。 例如，自定义对话框可能需要将少量CSS或JS部署到AEM创作实例。

### 管理作者上的客户端库 {#clientlibs-on-author}

如果您需要在创作时使用客户端库，可以在 `/apps` 使用与发布相同的方法，但直接在 `/apps/.../clientlibs/foo` 而不是创建用于管理项目的整个项目。

然后，您可以通过将客户端库添加到即装即用的客户端库类别，将其“挂接”到创作JS中。

## 调试工具 {#debugging-tools}

AEM提供了多种工具来调试和测试客户端库文件夹。

### 发现客户端库 {#discover-client-libraries}

的 `/libs/cq/granite/components/dumplibs/dumplibs` 组件会生成有关系统上所有客户端库文件夹的信息页面。 的 `/libs/granite/ui/content/dumplibs` 节点将组件作为资源类型。 要打开页面，请使用以下URL（根据需要更改主机和端口）：

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

该信息包括库路径和类型（CSS或JS），以及库属性的值，如类别和依赖关系。 页面上的后续表显示了每个类别和渠道中的库。

### 请参阅生成的输出 {#see-generated-output}

的 `dumplibs` 组件包含测试选择器，该测试选择器显示为 `ui:includeClientLib` 标记。 页面包含js、css和主题属性的不同组合的代码。

1. 使用以下方法之一打开“测试输出”页：
   * 从 `dumplibs.html` 页面上的 **单击此处进行输出测试** 文本。
   * 在Web浏览器中打开以下URL（根据需要使用其他主机和端口）：
      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`
   * 默认页面显示类别属性没有值的标记的输出。
1. 要查看类别的输出，请键入客户端库的 `categories` 属性并单击 **提交查询**.

## 其他客户端库文件夹功能 {#additional-features}

AEM中的客户端库文件夹还支持许多其他功能。 但是，AEMas a Cloud Service中不要求使用这些函数，因此不鼓励使用这些函数。 这里列出的是完整的。

>[!WARNING]
>
>AEMas a Cloud Service上不需要客户端库文件夹的这些附加功能，因此不建议使用这些功能。 这里列出的是完整的。

### AdobeGraniteHTML库管理器 {#html-library-manager}

其他客户端库设置可通过 **AdobeGraniteHTML库管理器** 系统控制台的面板(位于 `https://<host>:<port>/system/console/configMgr`)。

### 其他文件夹属性 {#additional-folder-properties}

其他文件夹属性包括允许控制依赖项和嵌入，但通常不再需要，也不建议使用：

* `dependencies`:这是此库文件夹所依赖的其他客户端库类别的列表。 例如，给定两个 `cq:ClientLibraryFolder` 节点 `F` 和 `G`，如果文件位于 `F` 需要另一个文件 `G` 为了正常运行， `categories` of `G` 应该属于 `dependencies` of `F`.
* `embed`:用于嵌入来自其他库的代码。 如果节点 `F` 嵌入节点 `G` 和 `H`，则生成的HTML将是节点中的内容的拼接 `G` 和 `H`.

### 链接到依赖项 {#linking-to-dependencies}

当客户端库文件夹中的代码引用其他库时，请将其他库标识为依赖项。 的 `ui:includeClientLib` 引用客户端库文件夹的标记会导致HTML代码包含指向您生成的库文件的链接以及依赖关系。

依赖项必须是另一个 `cq:ClientLibraryFolder`. 要识别依赖项，请向 `cq:ClientLibraryFolder` 具有以下属性的节点：

* **名称：** 依赖
* **类型：** 字符串[]
* **值：** 当前库文件夹所依赖的cq:ClientLibraryFolder节点的categories属性的值。

例如， `/etc/clientlibs/myclientlibs/publicmain` 对 `cq.jquery` 库。 引用主客户端库的页面会生成HTML，该页面包含以下代码：

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### 从其他库嵌入代码 {#embedding-code-from-other-libraries}

您可以将来自客户端库的代码嵌入到其他客户端库中。 在运行时，嵌入库生成的JS和CSS文件包含嵌入库的代码。

嵌入代码对于提供对存储在存储库安全区域中的库的访问权限非常有用。

#### 特定于应用程序的客户端库文件夹 {#app-specific-client-library-folders}

最佳做法是将所有与应用程序相关的文件保留在其应用程序文件夹下 `/apps`. 此外，最好还是拒绝网站访客访问 `/apps` 文件夹。 要满足这两个最佳实践，请在 `/etc` 嵌入下面客户端库的文件夹 `/apps`.

使用类别属性标识要嵌入的客户端库文件夹。 要嵌入库，请向嵌入中添加资产 `cq:ClientLibraryFolder` 节点，使用以下属性属性：

* **名称：** 嵌入
* **类型：** 字符串[]
* **值：** 的类别属性的值 `cq:ClientLibraryFolder` 要嵌入的节点。

#### 使用嵌入最小化请求 {#using-embedding-to-minimize-requests}

在某些情况下，您可能会发现，由发布实例为典型页面生成的最终HTML包含的页面数量相对较多 `<script>` 元素。

在这种情况下，将所有必需的客户端库代码合并到单个文件中，以减少页面加载时来回请求的数量，这非常有用。 为此，您可以 `embed` 使用的embed属性将所需的库放入特定于应用程序的客户端库中 `cq:ClientLibraryFolder` 节点。

#### CSS文件中的路径 {#paths-in-css-files}

嵌入CSS文件时，生成的CSS代码会使用指向与嵌入库相关的资源的路径。 例如，可公开访问的库 `/etc/client/libraries/myclientlibs/publicmain` 嵌入 `/apps/myapp/clientlib` 客户端库：

的 `main.css` 文件包含以下样式：

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

用于 `publicmain` 节点使用原始图像的URL生成包含以下样式：

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

#### 请参阅HTML输出中的嵌入文件 {#see-embedded-files}

要跟踪嵌入代码的源，或确保嵌入的客户端库生成预期结果，您可以在运行时查看正在嵌入的文件的名称。 要查看文件名，请在 `debugClientLibs=true` 参数。 生成的库包含 `@import` 语句，而不是嵌入代码。

在上一个示例中 [从其他库嵌入代码](#embedding-code-from-other-libraries) , `/etc/client/libraries/myclientlibs/publicmain` 客户端库文件夹嵌入了 `/apps/myapp/clientlib` 客户端库文件夹。 将参数附加到网页后，会在网页的源代码中生成以下链接：

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

打开 `publicmain.css` 文件会显示以下代码：

```javascript
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. 在Web浏览器的地址框中，将以下文本附加到HTML的URL:
   * `?debugClientLibs=true`
1. 页面加载时，查看页面源。
1. 单击作为链接元素的href提供的链接以打开文件并查看源代码。

### 使用预处理器 {#using-preprocessors}

AEM允许可插拔的预处理器，并支持 [YUI压缩机](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) （对于CSS和JavaScript）和 [Google关闭编译器(GCC)](https://developers.google.com/closure/compiler/) (对于将YUI设置为AEM默认预处理器的JavaScript)。

可插拔预处理器允许灵活使用，包括：

* 定义可处理脚本源的ScriptProcessors
* 处理器可通过选项进行配置
* 处理器可用于缩小，但也可用于未缩小的情况
* clientlib可定义要使用的处理器

>[!NOTE]
>
>默认情况下，AEM使用YUI压缩程序。 请参阅 [YUI压缩程序GitHub文档](https://github.com/yui/yuicompressor/issues) 列出已知问题。 在使用YUI时，切换到特定客户端的GCC压缩程序可能会解决一些观察到的问题。

>[!CAUTION]
>
>请勿在客户端库中放置缩小的库。 请改为提供原始库，如果需要缩小，请使用预处理器的选项。

#### 用途 {#usage}

您可以选择为每个客户端库或系统范围配置预处理器配置。

* 添加多值属性 `cssProcessor` 和 `jsProcessor` 在clientlibrary节点上
* 或通过 **HTML库管理器** OSGi配置

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

##### 用于CSS缩小的YUI压缩程序和用于JS的GCC压缩程序 {#yui-compressor-for-css-minification-and-gcc-for-js}

```javascript
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

##### 对GCC进行预处理，然后对GCC进行缩小和模糊处理 {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

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

有关GCC选项的更多详细信息，请参阅 [GCC文档](https://developers.google.com/closure/compiler/docs/compilation_levels).

#### 设置系统默认缩小器 {#set-system-default-minifier}

在AEM中，YUI设置为默认的缩小符。 要将此代码更改为GCC，请执行以下步骤。

1. 转到Apache Felix配置管理器(`http://<host>:<portY/system/console/configMgr`)
1. 查找和编辑 **AdobeGraniteHTML库管理器**.
1. 启用 **缩小** 选项（如果尚未启用）。
1. 设置值 **JS处理器默认配置** to `min:gcc`.
   * 如果以分号分隔，则可以传递选项，例如， `min:gcc;obfuscate=true`.
1. 单击 **保存** 以保存更改。
