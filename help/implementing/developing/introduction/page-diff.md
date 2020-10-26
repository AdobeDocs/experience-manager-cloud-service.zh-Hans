---
title: 开发和页面差异
description: 了解页面差异功能的工作原理以及它如何影响开发人员
translation-type: tm+mt
source-git-commit: 57a9026dd944547196e53fecb1cf1213ed793af7
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 11%

---


# 开发和页面差异 {#developing-and-page-diff}

## 功能概述 {#feature-overview}

内容创建是一个迭代过程。要进行高效创作，需要能够发现从一次迭代到另一次迭代所发生的更改。逐个查看页面版本的方式效率低下且容易出错。作者希望能够并排比较当前页面与先前版本的差异。

页面差异允许用户将当前页面与启动项、先前版本等进行比较。 有关此用户功能的详细信息，请参 [阅页面差异](/help/sites-cloud/authoring/features/page-diff.md)。

## 操作详细信息 {#operation-details}

在比较页面版本时，用户希望比较的先前版本由AEM在后台重新创建，以便进行比较。 这需要能够呈现内容 [进行并排比较](/help/sites-cloud/authoring/features/page-diff.md)。

此娱乐操作由AEM内部完成，对用户透明，无需任何干预。 但是，在CRX DE Lite中查看存储库的管理员将在内容结构中看到这些重新创建的版本。

比较内容时，将在以下位置重新创建整个树到要比较的页面：

`/tmp/versionhistory/`

自动运行清除任务以清除此临时内容。

## 限制 {#limitations}

差异通过DOM比较在客户端发生，使差异处理变得简单，但开发人员需要考虑许多限制。

* 此功能使用名称与AEM产品不间隔的CSS类。 如果页面中包含具有相同名称的其他自定义CSS类或第三方CSS类，则差异的显示可能会受到影响。

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* 由于差异是客户端差异，并在页面加载时执行，因此在客户端差异服务运行后对DOM所做的任何调整都不会计入。 这可能会影响

   * 使用AJAX包含内容的组件
   * 单页应用程序
   * 在用户交互时操作DOM的基于Javascript的组件。
