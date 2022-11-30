---
title: 通过GraphQL API提取内容
description: 了解如何将内容片段和GraphQL API用作无头内容管理系统。
hidefromtoc: true
index: false
source-git-commit: a832ed1d81866a6470b47d8e30f5c242b10d1422
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 1%

---


# 通过GraphQL API提取内容 {#extract-content}

迄今为止，在AEM Trials for headless中，您已 [创建了您自己的内容片段模型](content-structure.md) 并创建您自己的无头内容 [内容片段。](create-content.md) 现在，您可以了解如何将内容片段和GraphQL API用作无头内容管理系统来交付内容。

GraphQL提供了一个基于查询的API，允许外部客户端应用程序使用单个API调用仅查询AEM所需的内容。

首先，您将学习如何运行两种不同类型的查询： **列表** 和 **byPath** 查询。 然后，您将学习如何从之前创建的内容片段中检索内容。 本文档是交互式导览的补充，涵盖相同的步骤，并酌情链接到其他资源。

>[!TIP]
>
>如果要了解有关GraphQL API的更多详细信息，请参阅 [“其他资源”部分](#additional-resources) 在本模块末尾，阅读GraphQL API指南。

## GraphQL Explorer {#graphql-explorer}

从GraphQL资源管理器启动。 在此，您可以针对无头内容构建和运行查询。

![GraphQL查询编辑器](assets/extract-content/query-editor.png)

如果您希望自己在应用程序内指南之外导航到GraphQL资源管理器，可使用页面左上角的Adobe图标找到该资源管理器。 此时将打开AEM的全局导航。 从此处，您选择 **工具** 选项卡，然后 **常规** -> **GraphQL查询编辑器**.

>[!TIP]
>
>如果您想进一步了解在AEM中导航的信息，请参阅 [“其他资源”部分](#additional-resources) 的文档，以了解有关AEM基本操作的更多信息。

AEM试用版附带一个预加载内容的端点，您可以从中提取内容以进行测试。

![选择端点](assets/extract-content/select-endpoint.png)

选择 **AEM演示资产** 来自的端点 **端点** （如果尚未找到）位于编辑器右上角的下拉菜单。

## 复制并运行列表查询 {#list-query}

首先从简单的列表查询开始，以便掌握AEMas a Cloud ServiceGraphQL API的工作方式。 此列表查询示例将返回使用特定内容片段模型的所有内容的列表。 库存页面和类别页面通常使用此查询格式。

1. 复制以下代码片段。

   ```text
   {
       adventureList {
         items {
            _path
            adventureTitle
            adventurePrice
            adventureTripLength
            adventurePrimaryImage {
              ... on ImageRef {
               _path
               mimeType
               width
               height
             }
           }
         }
      }
    }
   ```

1. 然后，通过粘贴复制的代码来替换查询编辑器中的现有内容。

   ![列表查询](assets/extract-content/list-query.png)

1. 粘贴后，单击 **播放** 按钮以执行查询。

1. 成功执行查询后，结果将显示在查询编辑器旁边的右侧面板中。 如果查询不正确，则右侧面板中会显示错误。

   ![列出查询结果](assets/extract-content/list-query-results.png)

您刚刚验证了列表查询，以获取所有内容片段的完整列表。 此过程有助于确保响应符合应用程序的预期，并通过说明应用程序和网站将如何检索在AEM中创建的内容的结果。

您需要显示内容的不同渠道和平台现在可以使用此查询或类似方法来检索您的无标题内容。

## 复制并运行byPath查询 {#bypath-query}

运行byPath查询允许您检索特定内容片段的资产。 产品详细信息页面和侧重于特定内容集的页面通常需要此类型的查询。

1. 复制以下代码片段。

   ```text
    {
     adventureByPath(
       _path: "/content/dam/aem-demo-assets/en/adventures/bali-surf-camp/bali-surf-camp"
     ) {
       item {
         _path
         adventureTitle
         adventureDescription {
           json
         }
         adventurePrimaryImage {
           ... on ImageRef {
             _path
             width
             height
           }
         }
       }
     }
   }
   ```

1. 然后，通过粘贴复制的代码来替换查询编辑器中的现有内容。

   ![byPath查询](assets/extract-content/bypath-query.png)

1. 粘贴后，单击 **播放** 按钮以执行查询。

1. 成功执行查询后，结果将显示在查询编辑器旁边的右侧面板中。 如果查询不正确，则右侧面板中会显示错误。

1. 成功执行查询后，结果将显示在查询编辑器旁边的右侧面板中。 如果查询不正确，则右侧面板中会显示错误。

   ![byPath查询结果](assets/extract-content/bypath-query-results.png)

您刚刚验证了列表查询，以获取所有内容片段的完整列表。 此过程有助于确保响应符合应用程序的预期，并通过说明应用程序和网站将如何检索在AEM中创建的内容的结果。

您需要显示内容的不同渠道和平台现在可以使用此查询或类似方法来检索您的无标题内容。

## 对您自己的内容运行查询 {#own-queries}

现在，您已运行两种主要类型的查询，接下来便可以为自己创建的内容设置和运行查询。

1. 要针对您自己的内容片段运行查询，请从 **AEM演示资产** 文件夹 **您的项目** 文件夹。

   ![选择您自己的端点](assets/extract-content/select-endpoint.png)

1. 首先，在查询编辑器中选择并删除所有现有内容。 然后键入开括号 `{` 并按Ctrl+空格键或Option+空格键可自动完成在内容片段模型中定义的模型列表。 选择您创建的以 `List` 列表。

   ![在查询编辑器中自动完成模型](assets/extract-content/auto-complete-models.png)

1. 为所选内容片段模型定义查询应包含的项目。 再次键入开括号 `{`，然后按Ctrl+空格键或Option+空格键可显示自动完成列表。 选择 `items` 列表。

   ![在查询编辑器中自动完成项目](assets/extract-content/auto-complete-items.png)

1. 为所选内容片段模型定义查询应包含的字段。 再次键入开括号 `{`，然后按Ctrl+空格键或Option+空格键可自动完成内容片段模型中可用字段的列表。 从列表中选择您希望从模型中选择的字段。

   ![查询编辑器中的自动完成字段](assets/extract-content/auto-complete-fields.png)

1. 用逗号(`,`)或空格键，然后再次按Ctrl+空格键或Option+空格键以选择其他字段。

1. 在工作时，您可以点按或单击 **美化** 按钮以自动设置代码格式，以便于阅读。

   ![美化](assets/extract-content/prettify.png)

1. 完成后，点按或单击 **播放** 按钮来运行查询。

   ![您自己的查询结果](assets/extract-content/custom-query-results.png)

这就是如何将内容交付到全渠道数字体验。 请参阅 [“其他资源”部分](#additional-resources) 以了解其他示例查询，并了解使用GraphQL API可以执行的更多操作。

## 您已学会如何查询内容！ {#conclusion}

干得好！ 您已经了解了两种基本类型的查询以及如何查询您自己的内容。 请务必查看 [“其他资源”部分](#additional-resources) 以了解其他示例查询，并了解使用GraphQL API可以执行的更多操作。

如果您想要了解如何在自定义React应用程序中使用提取的内容，请务必查看模块 [自定义示例React应用程序中的内容。](customize-app.md)

您可以通过单击返回到试用版主屏幕 **解决方案** 按钮，然后选择 **Experience Manager**.

![导航主页](assets/extract-content/home.png)

## 其他资源 {#additional-resources}

有关内容片段和AEM的更多信息，请考虑查看此附加文档。

* [GraphQL API指南](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/explore-graphql-api.html)
* [基本操作](/help/sites-cloud/authoring/getting-started/basic-handling.md)  — 有关如何导航和为新用户使用AEM的文档
* [了解如何将 GraphQL 与 AEM 结合使用 – 示例内容和查询](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/headless/graphql-api/sample-queries.html)
