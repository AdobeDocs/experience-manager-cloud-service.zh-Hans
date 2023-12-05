---
title: 开发和页面差异
description: 了解页面差异功能的工作方式以及它如何影响开发人员
exl-id: 03c08616-2203-4b90-bed6-4836266e2507
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 12%

---

# 开发和页面差异 {#developing-and-page-diff}

## 功能概述 {#feature-overview}

内容创建是一个迭代过程。要进行高效创作，需要能够发现从一次迭代到另一次迭代所发生的更改。逐个查看页面版本的方式效率低下且容易出错。作者希望能够并排比较当前页面与先前版本，并突出显示差异。

页面差异允许用户将当前页面与启动项、先前版本等进行比较。 有关此用户功能的详细信息，请参阅 [页面差异](/help/sites-cloud/authoring/features/page-diff.md).

## 操作详细信息 {#operation-details}

在比较页面的版本时，用户要比较的先前版本由AEM在后台重新创建，以便于进行比较。 呈现内容需要此以前的版本 [用于并排比较](/help/sites-cloud/authoring/features/page-diff.md).

此重新创建操作由AEM在内部完成，对用户是透明的，无需干预。 但是，查看存储库的管理员(例如，在CRXDE Lite中)会在内容结构中看到这些重新创建的版本。

比较内容时，会于以下位置重新创建整个树，一直到要比较的页面：

`/tmp/versionhistory/`

自动运行清理任务以清理此临时内容。

## 限制 {#limitations}

比较过程通过DOM比较的方式在客户端进行，使得比较过程变得简单。 但是，开发人员必须考虑以下几个限制。

* 此功能使用的CSS类未与AEM产品进行命名空间。 如果页面上包含其他具有相同名称的自定义CSS类或第三方CSS类，则差异的显示可能会受到影响。

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* 由于diff是客户端并在页面加载时运行，因此不会考虑在客户端差异服务运行后对DOM进行的任何调整。 此过程可能会影响以下内容：

   * 使用AJAX包含内容的组件
   * 单页面应用程序
   * 基于JavaScript的组件，可在用户交互时处理DOM。
