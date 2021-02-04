---
title: RemotePage组件
description: RemotePage组件是用于编辑AEM中的远程React SPA的自定义页面组件。
translation-type: tm+mt
source-git-commit: 6a88b93a4005b858eec222fd7ae15df9db269d31
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 1%

---

# RemotePage组件{#remote-page-component}

在决定[外部SPA和AEM之间希望具有的集成级别](/help/implementing/developing/headful-headless.md)时，您通常需要能够在AEM内视图和编辑SPA。 RemotePage组件是一个自定义页面组件，仅用于此用途。

## 概述 {#overview}

RemotePage组件从应用程序生成的`asset-manifest.json`中获取所有必需的资产，并使用它在AEM中呈现SPA。

## 要求{#requirements}

* 在开发中启用CORS
* 在页面属性中配置远程URL
* 在AEM中呈现SPA

## 限制 {#limitations}

* RemotePage组件的当前实现仅支持远程React应用程序。
* 在AEM中进行远程渲染时，应用程序的根HTML文件中定义的内部CSS以及根DOM节点上的内联CSS将不可用。

## 技术详细信息{#technical-details}

与AEM SPA项目的其余部分一样，RemotePage组件是开放源。 有关RemotePage组件的完整技术详细信息，请[参阅GitHub存储库。](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
