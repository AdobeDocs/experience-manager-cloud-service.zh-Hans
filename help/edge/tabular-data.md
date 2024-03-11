---
title: 使用电子表格管理表格数据
description: 了解如何使用电子表格来管理各种值(如带有Edge Delivery Services网站的AEM的元数据和重定向)的表格数据。
feature: Edge Delivery Services
source-git-commit: 0fa88453a7d7c58a3ccb2a4baf7d2b143acf7ad5
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 2%

---


# 使用电子表格管理表格数据 {#tabular-data}

了解如何使用电子表格来管理各种值(如带有Edge Delivery Services网站的AEM的元数据和重定向)的表格数据。

{{aem-authoring-edge-early-access}}

## 用例 {#use-cases}

对于任何具有Edge Delivery Services网站的AEM，都需要维护表格式数据列表，如键值映射的数据列表。 这些可以是许多不同值的列表，例如元数据和重定向。 Edge Deliver Services允许您使用直观的工具（电子表格）维护此类表格列表。 AEM将这些电子表格转换为JSON文件，以便您的网站或Web应用程序轻松使用。

常见用例包括：

* [占位符](/help/edge/docs/placeholders.md)
* [元数据](/help/edge/docs/bulk-metadata.md)
* [标头](/help/edge/docs/custom-headers.md)
* [重定向](/help/edge/docs/redirects.md)
* [配置](/help/edge/docs/setup-byo-cdn-push-invalidation.md) 例如，用于CND设置

此外，您还可以 [创建电子表格](#own-spreadsheet) 的任何结构的映射，用于存储您自己的映射。

本文档使用重定向示例来说明如何创建此类电子表格。 有关每个用例的详细信息，请参阅Edge Delivery Services文档中先前链接的主题。

>[!TIP]
>
>有关电子表格如何与Edge Delivery Services一起使用的更多信息，请参阅文档 [电子表格和JSON。](/help/edge/developer/spreadsheets.md)

>[!TIP]
>
>电子表格只应用于维护表格式数据。 用于存储结构化数据， [查看AEM headless功能。](/help/headless/introduction.md)

## 先决条件 {#prerequisites}

要使用AEM中的电子表格与Edge Delivery Services项目创建映射，您需要使用最新的站点模板创建站点。

请参阅文档 [使用Edge Delivery Services进行AEM创作的开发人员快速入门指南](/help/edge/edge-dev-getting-started.md) 以了解更多信息。

## 创建电子表格 {#spreadsheet}

在本例中，您将创建一个电子表格来管理带有Edge Delivery Services网站的AEM的重定向。 这些步骤同样适用于 [其他电子表格类型](#other) 您希望创建的。

1. 登录到您的AEMas a Cloud Service创作实例，转到 **站点** ，然后导航到需要电子表格的站点的根。 点击或单击 **创建** -> **页面**.

   ![创建页面](assets/tabular-data/tabular-data-create-page.png)

1. 在 **模板** 创建页面向导的选项卡，点按或单击 **重定向** 模板以将其选中，然后点按或单击 **下一个**.

   ![选择模板](assets/tabular-data/tabular-data-create-page-teamplate-redirects.png)

1. 此 **属性** 向导的选项卡将显示重定向电子表格的默认值。 点按或单击&#x200B;**创建**。

   * **标题**  — 将此值保持原样。
   * **列**  — 预填充重定向所需的最少列。
      * **源**  — 要重定向的页面
      * **目标**  — 要重定向到的页面

   ![电子表格的属性](assets/tabular-data/tabular-data-create-page-properties-redirects.png)

1. 在 **成功** 对话框，点击或单击 **打开**.

   ![“成功”对话框](assets/tabular-data/tabular-data-success.png)

1. 此时将打开一个新选项卡，电子表格将加载到具有预定义属性的编辑器中 **源** 和 **目标** 列。 要定义重定向，请点按或单击 **源** 列。 编辑电子表格时，会自动保存更改。

   ![编辑电子表格](assets/tabular-data/tabular-data-edit-redirects.png)

   * 此 **源** 相对于网站的域，因此它仅包含相对路径。
   * 此 **目标** 如果要重定向到其他网站，则可以是完全限定的URL；如果您在自己的网站中重定向，则可以是相对路径。
   * 使用Tab键将焦点移动到下一个单元格。
   * 编辑器会根据需要向电子表格中添加新行。
   * 要删除或移动行，请使用 **删除** 图标和拖动手柄分别位于每行末尾和每行开头。

1. 定义完重定向后，关闭选项卡并返回到 **站点** 控制台。

1. 点按或单击以选择您在控制台中创建的重定向电子表格，然后点按或单击 **快速发布** 以发布电子表格。

   ![在站点控制台中选择电子表格](assets/tabular-data/tabular-data-select-publish.png)

1. 在 **快速发布** 对话框，点击或单击 **Publish**.

   ![确认发布](assets/tabular-data/tabular-data-quick-publish.png)

1. 一条横幅用于确认发布。

   ![发布的横幅确认](assets/tabular-data/tabular-data-publish-banner.png)

重定向电子表格现已发布并可供公众访问。

## 更新paths.json {#paths-json}

为了使AEM能够在电子表格中使用数据，您还需要更新 `paths.json` 您的项目的文件。

1. 在GitHub中打开项目的根。

1. 点按或单击 `paths.json` 文件以打开其详细信息，然后 **编辑** 图标。

   ![paths.json文件](assets/tabular-data/tabular-data-paths-json.png)

1. 添加一行以将新电子表格映射到 `redirects.json` 资源。

   ```json
   {
     "mappings": [
      "/content/<site-name>/:/",
      "/content/<site-name>/redirects:/redirects.json"
     ]
   }
   ```

1. 单击 **提交更改……** 将更改保存到 `main`.

   * 提交到 `main` 或根据流程创建拉取请求。

将更改到 `paths.json` 合并后，您的站点将启用重定向。

## 其他电子表格类型 {#other}

现在您已经知道如何创建重定向电子表格，您可以创建任何其他标准电子表格类型：

* 占位符
* 元数据
* 标头
* 配置

只需执行部分中的相同步骤即可 [创建电子表格](#spreadsheet) 和 [更新paths.json](#paths-json) 并选择相应的模板并更新 `paths.json` 文件设置正确。

此外，您可以 [创建自己的电子表格](#own-spreadsheet) 任意列供您自己使用。

>[!NOTE]
>
>您无需创建电子表格即可管理与Edge Delivery Services项目as a Cloud Service的AEM索引。
>
>如果您希望创建自己的索引， [请按照此文档操作](https://www.aem.live/developer/indexing#setting-up-more-index-configurations) 创建您自己的 `helix-query.yaml` 文件。

## 创建自己的电子表格 {#own-spreadsheet}

1. 执行部分中的相同步骤 [创建电子表格。](#spreadsheet)

1. 选择模板时，选择 **电子表格**.

1. 在 **属性** 选项卡中，您可以添加自己的列。

   ![添加您自己的列](assets/tabular-data/tabular-data-own-spreadsheet.png)

   * 在 **列** 部分，点击或单击 **添加** 以添加新列。
   * 提供列的名称。
   * 使用删除或重新组织列 **删除** 和拖动手柄图标。

1. 按照重定向电子表格的说明创建电子表格并发布。

1. 将映射添加到 `paths.json` 文件，按照重定向电子表格的说明执行。
