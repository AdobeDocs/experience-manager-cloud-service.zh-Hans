---
title: 在AEM as a Cloud Service上使用客户端库
description: AEM提供了客户端库文件夹，允许您在存储库中存储客户端代码(clientlibs)，将其组织为不同类别，并定义何时以及如何向客户端提供每种类别的代码
exl-id: 370db625-09bf-43fb-919d-4699edaac7c8
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '2497'
ht-degree: 1%

---


# 在AEM as a Cloud Service上使用客户端库 {#using-client-side-libraries}

数字体验在很大程度上依赖于由复杂的JavaScript和CSS代码驱动的客户端处理。 AEM客户端库(clientlibs)允许您在存储库中组织和集中存储这些客户端库。 结合AEM项目原型中的[前端构建过程，](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)可以轻松管理AEM项目的前端代码。

在AEM中使用clientlibs的优点包括：

* 客户端代码与所有其他应用程序代码和内容一样存储在存储库中
* AEM中的Clientlibs可以将所有CSS和JS聚合到一个文件中
* 通过可通过[调度程序](/help/implementing/dispatcher/disp-overview.md)访问的路径公开clientlibs
* 允许重写引用的文件或图像的路径

Clientlibs是内置解决方案，用于从AEM提供CSS和JavaScript。

>[!TIP]
>
>为AEM项目创建CSS和JavaScript的前端开发人员还应熟悉[AEM项目原型及其自动前端构建过程。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)

## 什么是客户端库 {#what-are-clientlibs}

站点需要在客户端处理JavaScript和CSS以及静态资源，例如图标和Web字体。 clientlib是AEM的机制，用于引用（如有必要，按类别分类）并为此类资源提供服务。

AEM将站点的CSS和JavaScript收集到一个位于中心位置的文件中，以确保HTML输出中仅包含任何资源的一个副本。 这样可以最大限度地提高交付效率，并通过代理在存储库中集中维护此类资源，从而确保访问安全。

## AEM as a Cloud Service的前端开发 {#fed-for-aemaacs}

所有JavaScript、CSS和其他前端资源都应在AEM项目原型的[ui.frontend模块中进行维护。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)原型的灵活性允许您使用所选择的现代Web工具来创建和管理这些资源。

然后，原型可以将资源编译为单个CSS和JS文件，并将它们自动嵌入存储库中的`cq:clientLibraryFolder`中。

## 客户端库文件夹结构 {#clientlib-folders}

客户端库文件夹是`cq:ClientLibraryFolder`类型的存储库节点。 [CND表示法](https://jackrabbit.apache.org/node-type-notation.html)中的定义为

```text
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

* `cq:ClientLibraryFolder`节点可以放置在存储库`/apps`子树中的任意位置。
* 使用节点的`categories`属性标识它所属的库类别。

每个`cq:ClientLibraryFolder`都填充了一组JS和/或CSS文件以及几个支持文件（见下文）。 `cq:ClientLibraryFolder`的重要属性配置如下：

* `allowProxy`：由于所有clientlib都必须存储在`apps`下，因此此属性允许通过代理servlet访问客户端库。 请参阅下面的[查找客户端库文件夹和使用代理客户端库Servlet](#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet)部分。
* `categories`：标识此`cq:ClientLibraryFolder`内的JS和/或CSS文件集所属的类别。 `categories`属性是多值属性，它允许库文件夹成为多个类别的一部分（请参阅下面的内容，了解其用处）。

如果client library文件夹包含一个或多个源文件，则在运行时这些文件将合并到单个JS和/或CSS文件中。 生成的文件的名称是具有`.js`或`.css`文件扩展名的节点名称。 例如，名为`cq.jquery`的库节点会生成名为`cq.jquery.js`或`cq.jquery.css`的文件。

客户端库文件夹包含以下项目：

* JS和/或CSS源文件
* 支持CSS样式的静态资源，例如图标、Web字体等。
* 一个`js.txt`文件和/或一个`css.txt`文件，它们标识要合并到生成的JS和/或CSS文件中的源文件

![Clientlib体系结构](assets/clientlib-architecture.drawio.png)

## 创建客户端库文件夹 {#creating-clientlib-folders}

客户端库必须位于`/apps`下。 此规则是更好地将代码与内容和配置隔离所必需的。

为了能够访问`/apps`下的客户端库，使用了代理servelt。 仍在客户端库文件夹上强制执行ACL，但如果`allowProxy`属性设置为`true`，则servlet允许通过`/etc.clientlibs/`读取内容。

1. 在Web浏览器(`https://<host>:<port>/crx/de`)中打开CRXDE Lite。
1. 选择`/apps`文件夹并单击&#x200B;**创建>创建节点**。
1. 输入库文件夹的名称，然后在&#x200B;**类型**&#x200B;列表中选择`cq:ClientLibraryFolder`。 单击&#x200B;**确定**，然后单击&#x200B;**全部保存**。
1. 要指定库所属的类别，请选择`cq:ClientLibraryFolder`节点，添加以下属性，然后单击&#x200B;**全部保存**：
   * 名称：`categories`
   * 类型：字符串
   * 值：类别名称
   * 多：已选择
1. 若要通过`/etc.clientlibs`下的代理访问客户端库，请选择`cq:ClientLibraryFolder`节点，添加以下属性，然后单击&#x200B;**全部保存**：
   * 名称：`allowProxy`
   * 类型：布尔值
   * 值： `true`
1. 如果您需要管理静态资源，请在客户端库文件夹下创建名为`resources`的子文件夹。
   * 如果您将静态资源存储在文件夹`resources`下以外的任何位置，则无法在发布实例上引用这些资源。
1. 将源文件添加到库文件夹中。
   * 这通常由[AEM项目原型的前端构建过程完成。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)
   * 如果需要，可以在子文件夹中组织源文件。
1. 选择客户端库文件夹，然后单击&#x200B;**创建>创建文件**。
1. 在“文件名”框中，键入以下文件名之一，然后单击“确定”：
   * **`js.txt`：**&#x200B;使用此文件名生成JavaScript文件。
   * **`css.txt`：**&#x200B;使用此文件名生成层叠样式表。
1. 打开文件并键入以下文本以标识源文件路径的根：
   * `#base=*[root]*`
   * 将`[root]`替换为包含源文件的文件夹相对于TXT文件的路径。 例如，当源文件与TXT文件位于同一文件夹时，请使用以下文本：
      * `#base=.`
   * 以下代码将根设置为`cq:ClientLibraryFolder`节点下名为mobile的文件夹：
      * `#base=mobile`
1. 在`#base=[root]`下面的行中，键入源文件相对于根的路径。 将每个文件名放在单独的一行中。
1. 单击&#x200B;**全部保存**。

## 为客户端库提供服务 {#serving-clientlibs}

在[根据需要配置您的客户端库文件夹后，](#creating-clientlib-folders)可以通过代理请求您的clientlibs。 例如：

* 您在`/apps/myproject/clientlibs/foo`中有一个clientlib
* 您在`/apps/myprojects/clientlibs/foo/resources/icon.png`中有一个静态图像

`allowProxy`属性允许您请求：

* clientlib通过`/etc.clientlibs/myprojects/clientlibs/foo.js`
* 通过`/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`的静态图像

### 通过HTL加载客户端库 {#loading-via-htl}

成功将clientlibs存储和管理在其客户端库文件夹中后，可以通过HTL访问它们。

客户端库是通过AEM提供的帮助程序模板加载的，可通过`data-sly-use`访问该模板。 帮助程序模板在此文件中可用，可通过`data-sly-call`调用这些模板。

每个帮助程序模板都需要一个 `categories` 选项来引用所需的客户端库。该选项可以是字符串值的数组，也可以是包含逗号分隔值列表的字符串。

[有关通过HTL加载clientlibs的更多详细信息，请参阅HTL文档](https://experienceleague.adobe.com/docs/experience-manager-htl/using/getting-started/getting-started.html#loading-client-libraries)。

<!--
### Setting Cache Timestamps {#setting-cache-timestamps}

This is possible. Still need detail.
-->

## 创作实例与Publish上的客户端库 {#clientlibs-author-publish}

AEM发布实例上需要大多数clientlibs。 也就是说，大多数clientlibs的目的是生成内容的最终用户体验。 对于发布实例上的clientlibs，[前端生成工具](#fed-for-aemaacs)可以通过[客户端库文件夹使用和部署，如上所述。](#creating-clientlib-folders)

但是，有时可能需要使用客户端库来自定义创作体验。 例如，自定义对话框可能需要将少量CSS或JS部署到AEM创作实例。

### 管理有关作者的客户端库 {#clientlibs-on-author}

如果您需要在创作中使用客户端库，则可以使用与发布相同的方法在`/apps`下创建客户端库，但直接在`/apps/.../clientlibs/foo`下写入客户端库，而不是创建整个项目来管理它。

然后，您可以通过将客户端库添加到现成的客户端库类别来“挂接”到创作JS中。

## 调试工具 {#debugging-tools}

AEM提供了几种用于调试和测试客户端库文件夹的工具。

### 发现客户端库 {#discover-client-libraries}

`/libs/cq/granite/components/dumplibs/dumplibs`组件生成系统上所有客户端库文件夹的信息页面。 `/libs/granite/ui/content/dumplibs`节点将组件作为资源类型。 要打开该页面，请使用以下URL（根据需要更改主机和端口）：

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

该信息包括库路径和类型（CSS或JS）以及库属性的值（如类别和依赖项）。 页面上的后续表将显示每个类别和渠道中的库。

### 查看生成的输出 {#see-generated-output}

`dumplibs`组件包括一个测试选择器，该选择器显示为`ui:includeClientLib`标记生成的源代码。 该页面包含用于不同js、css和主题属性组合的代码。

1. 使用以下方法之一打开“测试输出”页：
   * 从`dumplibs.html`页面，单击&#x200B;**单击此处进行输出测试**&#x200B;文本中的链接。
   * 在Web浏览器中打开以下URL（根据需要使用不同的主机和端口）：
      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`
   * 默认页面显示没有categories属性值的标记的输出。
1. 要查看类别的输出，请键入客户端库的`categories`属性的值，然后单击&#x200B;**提交查询**。

## 其他客户端库文件夹功能 {#additional-features}

AEM中的客户端库文件夹支持其他一些功能。 但是，AEM as a Cloud Service上不需要这些变量，因此建议不要使用这些变量。 为了完整起见，此处列出了它们。

>[!WARNING]
>
>AEM as a Cloud Service上不需要客户端库文件夹的这些附加功能，因此建议不要使用这些功能。 为了完整起见，此处列出了它们。

### AdobeGraniteHTML库管理器 {#html-library-manager}

其他客户端库设置可以通过位于`https://<host>:<port>/system/console/configMgr`的系统控制台的&#x200B;**AdobeGraniteHTML库管理器**&#x200B;面板进行控制。

### 其他文件夹属性 {#additional-folder-properties}

其他文件夹属性包括允许控制依赖项和嵌入，但通常不再需要这些属性，因此建议不要使用这些属性：

* `dependencies`：这是此库文件夹所依赖的其他客户端库类别的列表。 例如，在给定两个`cq:ClientLibraryFolder`节点`F`和`G`的情况下，如果`F`中的某个文件需要`G`中的另一个文件才能正常工作，则`G`的`categories`中至少有一个应属于`F`的`dependencies`中。
* `embed`：用于嵌入来自其他库的代码。 如果节点`F`嵌入了节点`G`和`H`，则生成的HTML是来自节点`G`和`H`的内容串联。

### 链接到依赖项 {#linking-to-dependencies}

当客户端库文件夹中的代码引用其他库时，将其他库标识为依赖项。 引用您的客户端库文件夹的`ui:includeClientLib`标记会导致HTML代码包含指向生成的库文件和依赖项的链接。

依赖项必须是另一个`cq:ClientLibraryFolder`。 要识别依赖关系，请使用以下属性向您的`cq:ClientLibraryFolder`节点添加属性：

* **名称：**&#x200B;依赖项
* **类型：**&#x200B;字符串[]
* **值：**&#x200B;当前库文件夹所依赖的cq：ClientLibraryFolder节点的categories属性值。

例如，`/etc/clientlibs/myclientlibs/publicmain`依赖于`cq.jquery`库。 引用主客户端库的页面会生成包含以下代码的HTML：

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### 嵌入来自其他库的代码 {#embedding-code-from-other-libraries}

您可以将来自客户端库的代码嵌入到另一个客户端库中。 在运行时，生成的嵌入库的JS和CSS文件包含嵌入库的代码。

嵌入代码可用于提供对存储在存储库安全区域中的库的访问权限。

#### 特定于应用程序的客户端库文件夹 {#app-specific-client-library-folders}

最佳做法是将应用程序文件夹中所有与应用程序相关的文件保留在`/apps`以下。 拒绝网站访客访问`/apps`文件夹也是最佳实践。 为满足这两个最佳实践，请在`/etc`文件夹下创建一个客户端库文件夹，该文件夹嵌入了`/apps`下的客户端库。

使用类别属性可标识要嵌入的客户端库文件夹。 要嵌入库，请使用以下属性将属性添加到嵌入`cq:ClientLibraryFolder`节点：

* **名称：**&#x200B;已嵌入
* **类型：**&#x200B;字符串[]
* **值：**&#x200B;要嵌入的`cq:ClientLibraryFolder`节点的categories属性值。

#### 使用嵌入以最大限度地减少请求 {#using-embedding-to-minimize-requests}

在某些情况下，您可能会发现发布实例为典型页面生成的最终HTML包含相对大量的`<script>`元素。

在这种情况下，有必要将所有所需的客户端库代码合并到单个文件中，以便减少页面加载上的来回请求数量。 为此，您可以使用`cq:ClientLibraryFolder`节点的嵌入属性，将所需的库`embed`到特定于应用程序的客户端库中。

#### CSS文件中的路径 {#paths-in-css-files}

嵌入CSS文件时，生成的CSS代码使用相对于嵌入库的资源路径。 例如，可公开访问的库`/etc/client/libraries/myclientlibs/publicmain`嵌入了`/apps/myapp/clientlib`客户端库：

`main.css`文件包含以下样式：

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

`publicmain`节点生成的CSS文件包含以下样式（使用原始图像的URL）：

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

#### 请参阅HTML输出中的嵌入式文件 {#see-embedded-files}

要跟踪嵌入代码的来源，或确保嵌入的客户端库产生预期的结果，您可以查看运行时嵌入的文件的名称。 要查看文件名，请将`debugClientLibs=true`参数附加到网页的URL。 生成的库包含`@import`语句，而不是嵌入的代码。

在上一个[嵌入来自其他库的代码](#embedding-code-from-other-libraries)部分的示例中，`/etc/client/libraries/myclientlibs/publicmain`客户端库文件夹嵌入了`/apps/myapp/clientlib`客户端库文件夹。 将参数附加到网页会在网页的源代码中生成以下链接：

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

打开`publicmain.css`文件将显示以下代码：

```javascript
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. 在Web浏览器的地址框中，将以下文本附加到HTML的URL：
   * `?debugClientLibs=true`
1. 加载页面时，查看页面源。
1. 单击提供为链接元素的href链接，以打开文件并查看源代码。

### 使用预处理器 {#using-preprocessors}

AEM允许可插拔预处理器，并且为CSS和JavaScript提供了[YUI Compressor](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor)支持，为JavaScript提供了[Google Closure Compiler (GCC)](https://developers.google.com/closure/compiler/)支持，并将YUI设置为AEM的默认预处理器。

可插拔预处理器允许灵活使用，包括：

* 定义可以处理脚本源的ScriptProcessors
* 处理器可通过选项进行配置
* 处理器可用于缩小，也可用于非缩小情况
* clientlib可以定义要使用的处理器

>[!NOTE]
>
>默认情况下，AEM使用YUI压缩程序。 有关已知问题的列表，请参阅[YUI压缩程序GitHub文档](https://github.com/yui/yuicompressor/issues)。 为特定clientlibs切换到GCC压缩程序可以解决使用YUI时观察到的一些问题。

>[!CAUTION]
>
>请勿将缩小的库放置在客户端库中。 而是提供原始库，如果需要缩小，请使用预处理器的选项。

#### 用途 {#usage}

您可以选择为每个客户端库或系统范围配置预处理器配置。

* 在clientlibrary节点上添加多值属性`cssProcessor`和`jsProcessor`
* 或通过&#x200B;**HTML库管理器** OSGi配置定义系统默认配置

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

##### 用于CSS缩小和GCC用于JS的YUI压缩器 {#yui-compressor-for-css-minification-and-gcc-for-js}

```javascript
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

##### 使用Typescript进行预处理，然后使用GCC进行缩小和模糊处理 {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

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

有关GCC选项的更多详细信息，请参阅[GCC文档](https://developers.google.com/closure/compiler/docs/compilation_levels)。

#### 设置系统默认缩小器 {#set-system-default-minifier}

在AEM中，YUI被设置为默认小型化器。 要将其更改为GCC，请执行以下步骤。

1. 转到位于(`http://<host>:<port/system/console/configMgr`)的Apache Felix配置管理器
1. 查找并编辑&#x200B;**AdobeGraniteHTML库管理器**。
1. 启用&#x200B;**最小化**&#x200B;选项（如果尚未启用）。
1. 将&#x200B;**JS处理器默认配置**&#x200B;的值设置为`min:gcc`。
   * 如果用分号分隔，例如`min:gcc;obfuscate=true`，则可以传递选项。
1. 单击&#x200B;**保存**&#x200B;以保存更改。
