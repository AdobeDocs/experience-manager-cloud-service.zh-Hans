---
title: 使用电子表格管理表格数据
description: 了解如何使用电子表格来管理各种值的表格数据，例如利用 Edge Delivery Services Site 为您的 AEM 提供元数据和重定向。
feature: Edge Delivery Services
exl-id: 26d4db90-3e4b-4957-bf21-343c76322cdc
role: Admin, Architect, Developer
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: ht
source-wordcount: '1294'
ht-degree: 100%

---


# 使用电子表格管理表格数据 {#tabular-data}

了解如何使用电子表格来管理各种值的表格数据，例如利用 Edge Delivery Services Site 为您的 AEM 提供元数据和重定向。

## 用例 {#use-cases}

对于任何使用 Edge Delivery Services Site 的 AEM，都需要维护表格数据列表，例如键值映射列表。这些可以是许多不同值的列表，例如元数据和重定向。Edge Deliver Services 允许您使用直观的工具（电子表格）维护此类表格列表。AEM 将这些电子表格转换为 JSON 文件，您的网站或 Web 应用程序可以轻松使用这些文件。

常见的用例包括：

* [占位符](/help/edge/docs/placeholders.md)
* [元数据](/help/edge/docs/bulk-metadata.md)
* [标头](/help/edge/docs/custom-headers.md)
* [重定向](/help/edge/docs/redirects.md)
* [配置](/help/edge/docs/setup-byo-cdn-push-invalidation.md)例如 CND 设置

此外，您可以[创建任何结构的电子表格](#own-spreadsheet)来存储映射，以满足自己的需要。

本文档使用重定向示例来说明如何创建此类电子表格。有关每个用例的详细信息，请参阅边 Edge Delivery Services 文档中先前链接的主题。

>[!TIP]
>
>有关电子表格通常如何与 Edge Delivery Services 配合使用的详细信息，请参阅文档[电子表格和 JSON](/help/edge/developer/spreadsheets.md)。

>[!TIP]
>
>电子表格只能用于维护表格数据。要存储结构化数据，[请查看 AEM 的 Headless 功能](/help/headless/introduction.md)。

## 前提条件 {#prerequisites}

为了在具有 Edge Delivery Services 的 AEM 项目中使用电子表格创建映射，您需要使用最新的 Site 模板创建 Site。

请参阅文档[使用 Edge Delivery Services 进行所见即所得创作的开发人员快速入门指南](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)，以了解更多信息。

## 创建电子表格 {#spreadsheet}

在此示例中，您将创建一个电子表格来管理利用 Edge Delivery Services Site 为您的 AEM 重定向。相同的步骤适用于您想要创建的[其他电子表格类型](#other)。

1. 登录到 AEM as a Cloud Service 创作实例，进入 **Site** 控制台，然后导航到需要电子表格的 Site 的根目录。点击或单击&#x200B;**创建**-> **页面**。

   ![创建页面](assets/tabular-data/tabular-data-create-page.png)

1. 在创建页面向导的“**模板**”选项卡上，点击或单击“**重定向**”模板将其选中，然后点击或点击“**下一步**”。

   ![选择模板](assets/tabular-data/tabular-data-create-page-teamplate-redirects.png)

1. 向导的“**属性**”选项卡显示重定向电子表格的默认值。点击或单击“**创建**”。

   * **标题** - 保留此值不变。
   * **列** - 预先填充重定向所需的最少列。
      * **源** - 要重定向的页面
      * **目标** - 重定向到的页面

   ![电子表格的属性](assets/tabular-data/tabular-data-create-page-properties-redirects.png)

1. 在&#x200B;**“成功”**&#x200B;对话框中，点击或单击&#x200B;**“打开”**。

   ![“成功”对话框](assets/tabular-data/tabular-data-success.png)

1. 将打开一个新选项卡，其中电子表格已加载到编辑器中，并包含预定义的&#x200B;**源列**&#x200B;和&#x200B;**目标列**。要定义重定向，请点击或单击&#x200B;**源**&#x200B;列的空行。当您编辑电子表格时，更改会自动保存。

   ![编辑电子表格](assets/tabular-data/tabular-data-edit-redirects.png)

   *  **源**&#x200B;与您网站的域相关，因此它仅包含相对路径。
   * 如果您重定向到其他网站，**目标**&#x200B;可以是完全限定的 URL；如果您在自己的网站内重定向，目标可以是相对路径。
   * 使用 Tab 键将焦点移至下一个单元格。
   * 编辑器根据需要向电子表格添加新行。
   * 要删除或移动行，请分别使用每行末尾的&#x200B;**“删除”**&#x200B;图标和每行开头的拖动手柄。

## 导入电子表格数据 {#importing}

除了在 AEM 页面编辑器中编辑电子表格之外，您还可以从 CSV 文件导入数据。

1. 在 AEM 中编辑电子表格时，点击或单击屏幕左上角的&#x200B;**上传**&#x200B;按钮。
1. 在下拉菜单中，选择您想要如何导入数据。
   * 使用&#x200B;**替换文档**&#x200B;功能将整个电子表格的内容替换为您要上传的 CSV 文件的内容。
   * 使用&#x200B;**附加到文档**&#x200B;功能将您要上传的 CSV 文件的数据附加到现有电子表格内容中。
1. 在打开的对话框中，选择您的 CSV 文件，然后点击或单击&#x200B;**打开**。

在导入过程中会打开一个对话框。完成后，CSV 文件中的数据将会被添加到电子表格中或替换电子表格的内容。如果遇到任何错误（例如列不匹配），则会报告这些错误，以便更正 CSV 文件。

>[!NOTE]
>
>* CSV 文件中的标题必须与电子表格中的列完全匹配。
>* 导入整个 CSV 不会修改列标题，只会修改内容行。
>* 如果需要更新列，则必须在执行 CSV 导入之前在 AEM 页面编辑器中执行此操作。
>* 导入的 CSV 文件不能大于 10 MB。

根据您选择的 `mode`，您还可以使用类似于以下内容的 CSV 和 cURL 命令 `create`、`replace` 或 `append` 到电子表格。

```text
curl --request POST \
  --url http://<aem-instance>/bin/asynccommand \
  --header 'content-type: multipart/form-data' \
  --form file=@/path/to/your.csv \
  --form spreadsheetPath=/content/<your-site>/<your-spreadsheet> \
  --form 'spreadsheetTitle=Your Spreadsheet' \
  --form cmd=spreadsheetImport \
  --form operation=asyncSpreadsheetImport \
  --form _charset_=utf-8 \
  --form mode=append
```

该调用会返回一个包含有关作业 ID 的信息的 HTML 页面。

```text
Message | Job(Id:2024/9/18/15/27/5cb0cacc-585d-4176-b018-b684ad2dfd02_90) created successfully. Please check status at Async Job Status Navigation.
```

[您可以使用&#x200B;**作业**&#x200B;控制台](/help/operations/asynchronous-jobs.md)来查看作业的状态，或者使用返回的 ID 进行查询。

```text
https://<aem-instance>/bin/asynccommand?optype=JOBINF&jobid=2024/10/24/14/1/8da63f9e-066b-4134-95c9-21a9c57836a5_1
```

## 发布电子表格 paths.json {#paths-json}

为了使 AEM 能够发布您的电子表格中的数据，您还需要更新项目的 `paths.json` 文件。

1. 在 GitHub 中打开您的项目的根目录。

1. 点击或单击 `paths.json` 文件以打开其详细信息，然后点击&#x200B;**编辑**&#x200B;图标。

   ![paths.json 文件](assets/tabular-data/tabular-data-paths-json.png)

1. 添加一行以将新电子表格映射到`redirects.json`资产。

   ```json
   {
     "mappings": [
      "/content/<site-name>/:/",
      "/content/<site-name>/redirects:/redirects.json"
     ]
   }
   ```

   >[!NOTE]
   >
   >该 `paths.json` 条目基于使用表格数据创建重定向的示例。确保更新与[您正在创建的电子表格类型](#other)相对应的路径。

1. 单击“**提交更改...**”将更改保存到 `main`。

   * 根据您的流程提交`main`或创建拉取请求。

1. 定义完重定向并更新路径映射后，返回 **Site** 控制台。

1. 点击或单击以选择您在控制台中创建的重定向电子表格，然后点击或单击操作栏中的&#x200B;**“快速发布”**&#x200B;发布电子表格。

   ![在 Site 控制台中选择电子表格](assets/tabular-data/tabular-data-select-publish.png)

1. 在&#x200B;**“快速发布”**&#x200B;对话框中，点击或单击&#x200B;**“发布”**。

   ![确认发布](assets/tabular-data/tabular-data-quick-publish.png)

1. 横幅确认了该出版物。

   ![横幅确认发布](assets/tabular-data/tabular-data-publish-banner.png)

重定向电子表格现已发布并可供公众访问。

>[!TIP]
>
>有关路径映射的更多信息，请参阅文档 [Edge Delivery Services 的路径映射](/help/edge/wysiwyg-authoring/path-mapping.md)。

## 其他电子表格类型 {#other}

现在您已经知道如何创建重定向电子表格，您可以创建任何其他标准电子表格类型：

* [占位符](https://www.aem.live/docs/placeholders)
* [元数据](https://www.aem.live/docs/bulk-metadata)
* [标头](https://www.aem.live/docs/custom-headers)
* [配置](https://www.aem.live/docs/configuration)——例如用于[缓存失效](https://www.aem.live/docs/byo-cdn-adobe-managed#setup-push-invalidation)
* [分类](/help/edge/wysiwyg-authoring/taxonomy.md)

只需按照各部分中的相同步骤操作即可[创建电子表格](#spreadsheet)和[更新 paths.json](#paths-json)，选择合适的模板并`paths.json`相应地更新文件。

对于[配置](https://www.aem.live/docs/configuration)、[标头](https://www.aem.live/docs/custom-headers)和[元数据](https://www.aem.live/docs/bulk-metadata)，请确保添加一项映射，以将其发布到默认位置：

* 配置：`/.helix/config.json`
* 标头：`/.helix/headers.json`
* 元数据：`/metadata.json`
* 分类：请参阅文档[管理分类数据](/help/edge/wysiwyg-authoring/taxonomy.md)，以了解更多信息。

此外，您还可以用任意列[创建您自己的电子表格](#own-spreadsheet)供您自己使用。

>[!NOTE]
>
>您无需创建电子表格来管理带有 Edge Delivery Services 项目的 AEM as a Cloud Service 的索引。
>
>如果您想创建自己的索引，[请遵循此文档](https://www.aem.live/developer/indexing#setting-up-more-index-configurations) 创建您自己的`helix-query.yaml`文件。

## 创建您自己的电子表格 {#own-spreadsheet}

1. 请按照本节中的相同步骤进行操作[创建电子表格](#spreadsheet)。

1. 选择模板时，选择&#x200B;**电子表格**。

1. 在向导的“**属性**”选项卡中，您可以添加自己的列。

   ![添加您自己的列](assets/tabular-data/tabular-data-own-spreadsheet.png)

   * 在&#x200B;**列** 部分，点击或单击&#x200B;**“添加”**&#x200B;添加新列。
   * 提供该列的名称。
   * 分别使用&#x200B;**“删除”**&#x200B;和拖动手柄图标进行删除或重新组织列。

1. 创建电子表格并按照重定向电子表格的说明进行发布。

1. 按照重定向电子表格的说明将映射添加到`paths.json`文件。

