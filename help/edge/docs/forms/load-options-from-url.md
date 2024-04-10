---
title: 从URL加载下拉列表选项
description: 下拉列表选项包含在一个不同的电子表格中，然后通过提供的URL导入到主电子表格中。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: eadfc3d448bd2fadce08864ab65da273103a6212
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 2%

---


# 从URL加载下拉列表选项

在Edge Delivery Services表单中，用户可选择从预定义选项集中选择一个值。 表单作者使用 `select` 元素，提供选项列表。
例如， `enquiry` 表单中有一个下拉菜单用于选择国家/地区，为用户提供了多种预定义的国家/地区以供选择。 您可以看到此列表包含以逗号分隔的一长串国家/地区。

![下拉选项](/help/forms/assets/drop-down-options.png)

直接将下拉菜单中的选项添加到包含表单定义的工作表时，管理这些选项的长列表可能会很麻烦。 创建单独的工作表来存储这些下拉选项可以简化和简化该过程。 此工作表充当所有下拉选项的集中式存储库，以结构化格式排列。 每个选项都列在其各自的行中，从而便于管理和更新。

让我们探讨如何通过通过URL从其他电子表格加载选项列表来改进表单创作过程。

读完本文后，您将学会：

* [在单独的电子表格中定义选项](#define-options)
* [添加URL以加载下拉列表选项](#add-url)

## 在单独的工作表中定义选项 {#define-options}

创建具有两列的工作表：`Option` 和 `Value`，以定义选项：

1. 转到Microsoft®SharePoint或Google Drive文件夹上的“AEM项目”文件夹。
2. 添加名为的工作表 `shared-country` 在Microsoft®SharePoint Site或Google Drive文件夹中，添加以下内容：

   * **选项**：表示下拉菜单中选项的显示值。
   * **值**：表示用户选择选项时提交的值。

   >[!NOTE]
   >
   > 如果下拉选项的值和选项相同，则电子表格只能包含 **选项** 列。

   让我们添加新的工作表， [共享国家/地区](/help/forms/assets/enquiry-options.xlsx) 中显示的选项 `Destination` 中的下拉列表 `enquiry` 表单。

   请参阅下图中的 `shared-country` 电子表格：

   ![国家/地区下拉列表](/help/forms/assets/drop-down-country-options.png)
3. 预览和发布 `shared-country` 工作表使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   请参阅显示的URL `shared-country` 表： https://main--wefinance--wkndforms.hlx.live/enquiry.json?sheet=country

>[!NOTE]
>
> `?sheet=country` 是附加到URL的查询参数。 此参数指示根据 `shared-country` 工作表。 它会重定向到包含与不同国家/地区相关信息的JSON文件。

## 添加URL以加载下拉列表选项{#add-url}

此 `Options` 属性 `select` 字段接受URL。 URL会返回一个用作以下对象选项的JSON数组： `Destination` 下拉列表。 添加URL以加载下拉列表选项：

1. 转到Microsoft®SharePoint或Google驱动器上的AEM项目文件夹，然后打开您的电子表格。 您也可以为表单创建新的电子表格。
1. 复制的URL `shared-country` 将其粘贴到 `Options` 的列 `Destination` 字段。

   ![查询电子表格](/help/forms/assets/drop-down-enquiry.png)

1. 预览和发布工作表，使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).


   ![国家/地区下拉列表](/help/forms/assets/load-dropdown-options-form.png)

您可参阅 [查询电子表格](/help/forms/assets/enquiry-options.xlsx) 以添加URL来加载下拉列表选项。

将URL集成到表单定义中以加载下拉列表选项后， `Destination` 下拉列表从URL开始显示。

请参阅下面的URL，其中显示了 `enquiry` 显示保存在单独工作表中的选项的表单：

https://main--wefinance--wkndforms.hlx.live/enquiry-form

## 另请参阅

{{see-more-forms-eds}}


