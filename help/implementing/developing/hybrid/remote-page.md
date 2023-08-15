---
title: RemotePage 组件
description: RemotePage组件是一个自定义页面组件，用于在AEM中编辑远程React SPA。
exl-id: d3465592-0392-49b0-b49d-de93983c1d6e
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 2%

---

# RemotePage 组件 {#remote-page-component}

在决定时 [什么级别的集成](/help/implementing/developing/headful-headless.md) 您希望在外部SPA和AEM之间切换，但通常情况下，您需要能够在AEM中查看和编辑SPA。 RemotePage组件只是用于此目的的自定义页面组件。

## 概述 {#overview}

RemotePage组件从应用程序生成的中提取所有必需的资源 `asset-manifest.json` 和使用此项在AEM中呈现SPA。

* RemotePage允许您将SPA的脚本和样式表插入AEM Page组件的正文中。
* 虚拟前端组件允许在AEM SPA编辑器中将部分标记为可编辑。
* 托管在不同域上的SPA可以一起在AEM中编辑。

请参阅文章 [在AEM中编辑外部SPA](editing-external-spa.md) 有关AEM中可编辑的外部SPA的更多详细信息。

## 要求 {#requirements}

* 在开发中启用CORS
* 在页面属性中配置远程URL
* 在AEM中渲染SPA
* Web应用程序必须使用类似以下内容的捆绑包资产清单，并公开 `asset-manifest.json` 位于域根目录中的文件，该文件在 `entrypoints property` 要加载的所有CSS和JS文件：
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest
     ![entrypoints属性示例](assets/asset-manifest-entrypoints.png)
* 应用程序必须能够在 `<div id="root"></div>` 在 `body` 元素。 如果应用程序实例化需要不同的标记，则必须在具有的代理组件的HTL脚本中相应地调整此标记 `sling:resourceSuperType="spa-project-core/components/remotepage`.

## 限制 {#limitations}

* RemotePage组件希望实施提供类似于资产清单的资产清单 [此处找到。](https://github.com/shellscape/webpack-manifest-plugin) 但是，RemotePage组件仅经过测试可用于React框架（以及通过remote-page-next组件的Next.js），因此不支持从其他框架(如Angular)远程加载应用程序。
* 在AEM中执行远程渲染时，在应用程序的根HTML文件中定义的内部CSS和根DOM节点上的内联CSS将不可用。

## 技术详细信息 {#technical-details}

与AEM SPA项目的其余部分一样，RemotePage组件是开源的。 有关RemotePage组件的完整技术详细信息， [请参阅GitHub存储库。](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
