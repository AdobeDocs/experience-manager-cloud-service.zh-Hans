---
title: 从 URL 加载下拉列表选项
description: 下拉列表选项包含在不同的电子表格中，然后通过提供的 URL 导入到主电子表格中。
feature: Edge Delivery Services
source-git-commit: 2affe155b285986128487043fcc4f2938fc15842
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 59%

---


# 从 URL 加载下拉列表选项

Forms通常包括下拉菜单，供用户从预定义选项中进行选择。 这些选项通常在表单本身中定义，但管理长列表可能会很麻烦。 本指南概述了如何通过通过URL从单独的电子表格加载下拉选项来改进表单创作。


从单独的电子表格加载下拉选项的好处包括：

* 简化的管理：在一个集中的位置维护下拉列表选项，以便更轻松地更新和添加。
* 提高了效率：无需在表单定义中手动添加长选项列表。




![下拉菜单选项](/help/forms/assets/drop-down-options.png)


读完本文后，您将学会：

* [在单独的电子表格中定义选项](#define-options)
* [添加 URL 以加载下拉列表选项](#add-url)

## 在单独的工作表中定义选项 {#define-options}

在单独的电子表格中定义选项

1. 创建电子表格：
   1. 在Microsoft®SharePoint或Google驱动器中找到AEM项目文件夹。
   1. 添加新工作表。 例如，“共享国家/地区”。
1. 定义选项列：添加两列：“选项”和“值”。
   * “选项”定义下拉菜单中显示的文本。
   * “值”定义用户选择该选项时提交的值。

   >[!NOTE]
   >
   >如果选项和值相同，则仅需要“选项”列。

1. 填充电子表格：在“选项”列中输入国家/地区选项（如有必要，请输入“值”列）。

   有关结构，请参阅以下示例。

   ![国家/地区下拉列表](/help/forms/assets/drop-down-country-options.png)

1. 使用 [AEM Sidekick ](https://www.aem.live/developer/tutorial#preview-and-publish-your-content)预览和发布`shared-country`工作表。

   请参阅展示 `shared-country` 表格的 URL：
https://main--wefinance--wkndforms.hlx.live/enquiry.json?sheet=country

>[!NOTE]
>
> `?sheet=country` 是附加到 URL 的查询参数。该参数表示根据 `shared-country` 表过滤后的 JSON。它重定向到包含与不同国家相关的信息的 JSON 文件。

## 添加 URL 以加载下拉列表选项{#add-url}

字段的`Options` 属性 `select` 接受 URL。URL 返回一个 JSON 数组，用作 `Destination` 下拉列表的选项。要添加 URL 以加载下拉列表选项：

1. 转到 Microsoft® SharePoint 或 Google Drive 上的 AEM Project 文件夹并打开电子表格。您还可以为表单创建新的电子表格。
1. 复制 `shared-country` 工作表的 URL，并将其粘贴到 `Options` 字段的 `Destination` 列中。

   ![查询电子表格](/help/forms/assets/drop-down-enquiry.png)

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content)预览和发布工作表。


   ![国家/地区下拉列表](/help/forms/assets/load-dropdown-options-form.png)

您可以参考 [询价电子表格](/help/forms/assets/enquiry-options.xlsx) 将 URL 添加到加载下拉列表选项中。

将 URL 集成到表单定义中以加载下拉列表选项后，`Destination` 下拉列表的选项开始从 URL 中出现。

请参阅下面的 URL，其中显示了保存在单独工作表中的选项的 `enquiry` 表单：

https://main--wefinance--wkndforms.hlx.live/enquiry-form

## 另请参阅

{{see-more-forms-eds}}


