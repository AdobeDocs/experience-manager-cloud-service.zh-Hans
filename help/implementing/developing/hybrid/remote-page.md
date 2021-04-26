---
title: RemotePage组件
description: RemotePage组件是一个自定义页面组件，用于在AEM中编辑远程React SPA。
exl-id: d3465592-0392-49b0-b49d-de93983c1d6e
translation-type: tm+mt
source-git-commit: a46a2b3951d2fcc8468b29b4fa2c1faada643243
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# RemotePage组件{#remote-page-component}

当决定[您希望在外部SPA和AEM之间具有哪个级别的集成](/help/implementing/developing/headful-headless.md)时，您通常可以清楚地看到，您需要能够在AEM内视图和编辑SPA。 RemotePage组件是一个自定义页面组件，仅用于此用途。

## 概述 {#overview}

RemotePage组件从应用程序生成的`asset-manifest.json`中获取所有必需的资产，并使用它在AEM中呈现SPA。

* RemotePage允许您将SPA的脚本和样式表注入AEM页面组件的正文中。
* 虚拟前端组件允许将部分标记为在AEM SPA编辑器中可编辑。
* 同时，可以在AEM中编辑托管在其他域上的SPA。

有关可编辑的AEM(中的外部SPA的详细信息，请参阅文章[在AEM中编辑外部SPA。](editing-external-spa.md)

## 要求{#requirements}

* 使CORS能够开发
* 在页面属性中配置远程URL
* 在AEM中渲染SPA
* Web应用程序必须像以下任一操作那样使用bundler资源清单，并在`entrypoints property`中列表要加载的所有CSS和JS文件的域根目录下公开`asset-manifest.json`文件：
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest
      ![entrypoints属性示例](assets/asset-manifest-entrypoints.png)
* 应用程序必须能够在`body`元素下方的`<div id="root"></div>`中进行初始化。 如果应用程序要实例化需要其他标记，则必须在具有`sling:resourceSuperType="spa-project-core/components/remotepage`的代理组件的HTL脚本中相应地调整此标记。

## 限制 {#limitations}

* 在AEM中进行远程渲染时，应用程序的根HTML文件中定义的内部CSS以及根DOM节点上的内联CSS将不可用。

## 技术详细信息{#technical-details}

与AEM SPA项目的其余部分一样，RemotePage组件是开放源。 有关RemotePage组件的完整技术详细信息，请参阅GitHub存储库。](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)[
