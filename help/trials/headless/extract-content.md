---
title: 通过 GraphQL API 提取内容
description: 了解如何使用内容片段和 GraphQL API 作为 Headless 内容管理系统。
hidefromtoc: true
index: false
exl-id: f5e379c8-e63e-41b3-a9fe-1e89d373dc6b
source-git-commit: bcab02cbd84955ecdc239d4166ae38e5f79b3264
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 44%

---


# 通过 GraphQL API 提取内容 {#extract-content}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql"
>title="使用 GraphQL API 提取内容"
>abstract="在本模块中，您将了解如何将内容片段和GraphQL API用作无头内容管理系统。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql_guide"
>title="启动 GraphQL 资源管理器"
>abstract="GraphQL 提供了基于查询的 API，可让外部客户端应用程序使用单个 API 调用，在 AEM 中仅查询所需的内容。请阅读本模块，了解如何运行两种不同类型的查询。 然后，了解如何从您在上一个模块中创建的内容片段中检索内容。<br><br>通过单击下面的，在新选项卡中启动此模块。"
>additional-url="https://video.tv.adobe.com/v/328618" text="提取内容简介视频"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql_guide_footer"
>title="干得好！ 您已了解两种基本类型的查询以及如何查询您自己的内容。现在，您已了解如何使用AEM GraphQL API创建高效查询，以应用程序预期的格式交付内容。"
>abstract=""

## 查询示例内容列表 {#list-query}

单击 **启动GraphQL Explorer** 上方的按钮可在新选项卡中打开GraphQL Explorer。

![GraphQL 查询编辑器](assets/extract-content/query-editor.png)

使用GraphQL Explorer时，您可以针对无头内容构建和验证查询，然后再使用这些内容为应用程序或网站中的内容提供支持。 让我们看看怎么做！

1. 您的AEM无头试用版附带一个预加载了内容片段的端点，您可以从中提取内容以进行测试。 选择 **AEM演示资产** 来自的端点 **端点** 下拉菜单。

   ![选择端点](assets/extract-content/select-endpoint.png)

1. 为预加载的列表查询复制以下代码片段 **AEM演示资产** 端点。 列表查询会返回使用特定内容片段模型的所有内容的列表。 库存和类别页面通常使用此查询格式。

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

1. 通过粘贴复制的代码来替换查询编辑器中的现有内容。

   ![列表查询](assets/extract-content/list-query.png)

1. 粘贴后，单击查询编辑器左上角的&#x200B;**播放**&#x200B;按钮以执行查询。

1. 结果显示在查询编辑器旁边的右侧面板中。 如果查询不正确，右侧面板中将显示错误。

   ![列表查询结果](assets/extract-content/list-query-results.png)

您刚刚验证了列表查询，以获取所有内容片段的完整列表。 此过程可帮助确保响应符合应用程序的预期，其结果说明了您的应用程序和网站将如何检索在 AEM 中创建的内容。

## 查询特定的示例内容 {#bypath-query}

运行byPath查询允许您检索特定内容片段的内容。 产品详细信息页面和专注于一组特定内容的页面通常需要此类查询。让我们看看它的工作原理！

1. 为预加载的byPath查询复制以下代码片段 **AEM演示资产** 端点。

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

1. 通过粘贴复制的代码来替换查询编辑器中的现有内容。

   ![byPath 查询](assets/extract-content/bypath-query.png)

1. 粘贴后，单击查询编辑器左上角的&#x200B;**播放**&#x200B;按钮以执行查询。

1. 结果显示在查询编辑器旁边的右侧面板中。 如果查询不正确，右侧面板中将显示错误。

   ![byPath 查询结果](assets/extract-content/bypath-query-results.png)

您刚刚验证了byPath查询，以检索由该片段的路径标识的特定内容片段。

## 查询您自己的内容 {#own-queries}

现在，您已运行两种主要类型的查询，接下来可以查询您自己的内容了！

1. 要对您自己的内容片段运行查询，请将端点从 **AEM 示范资产**&#x200B;文件夹更改为&#x200B;**您的项目**&#x200B;文件夹。

   ![选择您自己的端点](assets/extract-content/select-endpoint.png)

1. 删除查询编辑器中的所有现有内容。 然后键入开括号 `{` 并按Ctrl+空格键或Option+空格键可自动完成端点中定义的模型列表。 选择您创建的以 `List` 中。

   ![在查询编辑器中自动完成模型](assets/extract-content/auto-complete-models.png)

1. 为您选择的内容片段模型定义查询应包含的项目。 再次键入左方括号 `{`，然后按 Ctrl + 空格键或 Option + 空格键获取自动完成列表。选择 `items` 中。

   ![在查询编辑器中自动完成项目](assets/extract-content/auto-complete-items.png)

1. 为您选择的内容片段模型定义查询应包含的字段。再次键入开括号 `{`，然后按Ctrl+空格键或Option+空格键可自动完成内容片段模型中可用字段的列表。 在该列表中选择所需的模型中的字段。

   ![在查询编辑器中自动完成字段](assets/extract-content/auto-complete-fields.png)

1. 用逗号 (`,`) 或空格分隔多个字段，然后再次按 Ctrl + 空格键或 Option + 空格键选择其他字段。

1. 在工作时，您可以点按或单击&#x200B;**美化**&#x200B;按钮来自动格式化您的代码，使其更易读取。

   ![美化](assets/extract-content/prettify.png)

1. 完成后，点按或单击该编辑器左上角的&#x200B;**播放**&#x200B;按钮以运行查询。

   ![您的查询的结果](assets/extract-content/custom-query-results.png)

1. 结果显示在查询编辑器旁边的右侧面板中。

这就是将您的内容交付给全渠道数字体验的方式。
