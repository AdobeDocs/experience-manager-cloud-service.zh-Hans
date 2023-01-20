---
title: 通过 GraphQL API 提取内容
description: 了解如何使用内容片段和 GraphQL API 作为 Headless 内容管理系统。
hidefromtoc: true
index: false
exl-id: f5e379c8-e63e-41b3-a9fe-1e89d373dc6b
source-git-commit: 741fadcffc496cb1c32d1943f7759e8d70cf92ff
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 85%

---


# 通过 GraphQL API 提取内容 {#extract-content}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql"
>title="使用 GraphQL API 提取内容"
>abstract="在本模块中，您将学习如何使用内容片段和 GraphQL API 作为无头内容管理系统。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql_guide"
>title="启动 GraphQL 资源管理器"
>abstract="GraphQL 提供了基于查询的 API，可让外部客户端应用程序使用单个 API 调用，在 AEM 中仅查询所需的内容。按照本模块学习如何运行两种不同类型的查询。之后，您将了解如何从上一个模块中创建的内容片段中检索内容。<br><br>单击下方在新选项卡中启动该模块。"
>additional-url="https://video.tv.adobe.com/v/328618" text="提取内容介绍视频"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql_guide_footer"
>title="做得好！您已了解两种基本类型的查询以及如何查询您自己的内容。现在您了解了如何使用 AEM GraphQL API 创建高效的查询，并且以应用程序期望的格式交付内容。"
>abstract=""

## 查询示例内容列表 {#list-query}

在新选项卡中启动GraphQL Explorer。 在此，您可以针对无头内容构建和验证查询，然后再使用这些内容为应用程序或网站中的内容提供支持。

1. 您的 AEM Headless 试用版附带了一个已预加载内容片段的端点，您可以从中提取内容用于测试。确保 **AEM演示资产** 终结点在 **端点** 下拉菜单。

1. 为预加载的 **AEM 演示资产**&#x200B;端点的列表查询复制以下代码片段。列表查询会返回使用特定内容片段模型的所有内容的列表。库存和类别页面通常使用此查询格式。

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

1. 粘贴后，单击查询编辑器左上角的&#x200B;**播放**&#x200B;按钮以执行查询。

1. 结果会显示在右侧面板中，位于查询编辑器的旁边。如果查询不正确，右侧面板中将显示错误。

   ![列表查询](assets/do-not-localize/list-query-1-3-4-5.png)

您刚刚验证了针对所有内容片段的完整列表的列表查询。此过程可帮助确保响应符合应用程序的预期，其结果说明了您的应用程序和网站将如何检索在 AEM 中创建的内容。

## 查询特定的示例内容 {#bypath-query}

运行 byPath 查询可让您检索特定内容片段的内容。产品详细信息页面和专注于一组特定内容的页面通常需要此类查询。

1. 为预加载的 **AEM 演示资产**&#x200B;端点的 byPath 查询复制以下代码片段。

   ```text
    {
     adventureByPath(
       _path: "/content/dam/aem-demo-assets/en/adventures/bali-surf-camp/bali-surf-camp"
     ) {
       item {
         _path
         title
         description {
           json
         }
         primaryImage {
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

1. 粘贴后，单击查询编辑器左上角的&#x200B;**播放**&#x200B;按钮以执行查询。

1. 结果会显示在右侧面板中，位于查询编辑器的旁边。如果查询不正确，右侧面板中将显示错误。

   ![byPath 查询结果](assets/do-not-localize/bypath-query-2-3-4.png)

您刚刚通过验证 byPath 查询来检索由该片段的路径标识的特定内容片段。

## 查询自己的内容 {#own-queries}

现在，您已运行两种主要类型的查询，接下来可以查询自己的内容。

1. 要对您自己的内容片段运行查询，请将端点从 **AEM 示范资产**&#x200B;文件夹更改为&#x200B;**您的项目**&#x200B;文件夹。

1. 删除查询编辑器中的所有现有内容。然后，键入左方括号 `{` 并按 Ctrl + 空格键或 Option + 空格键，可获取端点中定义的模型的自动完成列表。从选项中选择您创建的以 `List` 结尾的模型。

   ![启动自定义查询](assets/do-not-localize/custom-query-1-2.png)

1. 为您选择的内容片段模型定义查询应包含的项目。再次键入左方括号 `{`，然后按 Ctrl + 空格键或 Option + 空格键获取自动完成列表。从选项中选择 `items`。

1. 点按或单击 **美化** 按钮以自动设置代码格式，以便于阅读。

1. 完成后，点按或单击该编辑器左上角的&#x200B;**播放**&#x200B;按钮以运行查询。编辑器会自动完成 `items` 并运行查询。

1. 结果会显示在右侧面板中，位于查询编辑器的旁边。

   ![运行自定义查询](assets/do-not-localize/custom-query-3-4-5-6.png)

这就是将您的内容交付给全渠道数字体验的方式。
