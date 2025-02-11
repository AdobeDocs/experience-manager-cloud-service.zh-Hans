---
title: 管理分类数据
description: 了解如何管理分类数据，以便在 AEM with Edge Delivery Services Sites 上使用标签。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 017982e4-a4c8-4097-8751-9619cc4639d0
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 75%

---


# 管理分类数据 {#managing-taxonomy-data}

了解如何管理分类数据，以便在 AEM with Edge Delivery Services Sites上使用标签。

## 简介 {#introduction}

标记是一项重要功能，可帮助您组织和管理页面。[AEM 中的标记控制台](/help/sites-cloud/administering/tags.md#tagging-console)允许您创建丰富的标记分类来组织您的页面。

这些标签不仅对您和您的作者组织内容有用，而且对您的读者也很有用。标签及其分类法可用于页面上的组件，以帮助读者浏览您的内容。

通用编辑器仅适用于您的标签 ID。通过为您的内容创建一个分类页面，您可以将这些标签的描述以各种语言形式向通用编辑器公开，以便它在呈现内容时可以使用这些信息。

## 创建分类页面 {#creating}

在AEM](/help/sites-cloud/authoring/sites-console/creating-pages.md)中创建的分类，类似于[任何其他页面。

1. 导航到&#x200B;[**站点**&#x200B;控制台](/help/sites-cloud/authoring/sites-console/introduction.md)。

1. 选择您想要创建分类的位置。

1. 点击或单击&#x200B;**创建**-> **页面**。

   ![创建页面](assets/taxonomy/create-page.png)

1. 在&#x200B;**创建页面**&#x200B;向导的&#x200B;**模板**&#x200B;选项卡上，选择&#x200B;**分类**&#x200B;模板，然后点击或单击&#x200B;**下一步**。

   ![分类模板](assets/taxonomy/taxonomy-template.png)

1. 在&#x200B;**创建页面**&#x200B;向导的&#x200B;**属性**&#x200B;选项卡上，为页面提供一个有意义的&#x200B;**标题**，并在&#x200B;**标签**&#x200B;字段中，[使用标签选择器](/help/sites-cloud/authoring/sites-console/tags.md)选择您想要包含在分类中的标签或命名空间。

   ![分类属性](assets/taxonomy/create-page-wizard-properties.png)

1. 点击或单击&#x200B;**创建**。

分类页面已创建。在&#x200B;**成功**&#x200B;对话框中，您可以点按或单击&#x200B;**完成**&#x200B;对话框以关闭消息，或者点按或单击&#x200B;**打开**&#x200B;以在[页面编辑器](/help/sites-cloud/authoring/page-editor/introduction.md)中编辑页面。

记下分类页面生成的页面名称，以便在后续步骤中使用。

## 创建分类页面 {#editing}

您可以像编辑 AEM 中的其他页面一样开始编辑分类页面。

1. 导航到&#x200B;[**站点**&#x200B;控制台](/help/sites-cloud/authoring/sites-console/introduction.md)。

1. 选择您想要编辑的分类。

1. 在操作栏中点击或单击&#x200B;**编辑**。

1. 页面编辑器打开并显示分类。

   * 分类页面在页面编辑器中是只读的。

   ![编辑分类](assets/taxonomy/edit-page.png)

1. 点击或单击工具栏中的&#x200B;**页面信息**&#x200B;图标，然后选择&#x200B;**打开属性**。

   ![打开属性](assets/taxonomy/open-properties.png)

1. 在&#x200B;**页面属性**&#x200B;窗口内，您可以更新页面名称并使用标签选择器来更新分类中包含的标签和命名空间。

   ![编辑页面属性](assets/taxonomy/edit-properties.png)

1. 点击或单击&#x200B;**保存并关闭**。

页面编辑器中显示的页面是只读的，因为分类的内容是根据所选标签和命名空间自动生成的。它们起到一种过滤器的作用，可以自动生成分类的内容。因此，没有理由直接在编辑器中编辑页面。

当您更新底层标签和命名空间时，AEM 会自动更新分类页面的内容。但是您必须在进行任何更改之后[重新发布分类](#publishing)，以便您的用户能够看到这些更改。

## 更新分类发布的 paths.json {#paths-json}

就像在[管理和发布Edge Delivery Services站点](/help/edge/wysiwyg-authoring/tabular-data.md)的表格数据时一样，您需要更新项目的`paths.json`文件以允许发布分类数据。

1. 在 GitHub 中打开您的项目的根目录。

1. 点击或单击 `paths.json` 文件以打开其详细信息，然后点击“**编辑**”图标。

   ![paths.json 文件](assets/taxonomy/paths-json.png)

1. 添加一行以将新分类页面映射到 `.json` 资产。

   ```json
   {
     "mappings": [
      "/content/<site-name>/:/",
      "/content/<site-name>/<taxonomy-page-name>:/<taxonomy-json-name>.json"
     ]
   }
   ```

   * `<taxonomy-page-name>`必须与您创建的[分类页面](#creating)的名称匹配。
   * `<taxonomy-json-name>` 可以是您选择的任何有效名称。

1. 单击“**提交更改...**”将更改保存到 `main`。

   * 根据您的流程提交`main`或创建拉取请求。

每个分类页面只需执行一次此过程。完成后，您可以发布您的分类。

>[!TIP]
>
>有关路径映射的详细信息，请参阅文档[Edge Delivery Services的路径映射](/help/edge/wysiwyg-authoring/path-mapping.md)。

## 发布分类 {#publishing}

分类在发布之前不可供通用编辑器或您的用户使用。

分类页面由[使用工具栏中的&#x200B;**快速发布**&#x200B;或&#x200B;**管理发布**&#x200B;图标像任何其他页面一样发布](/help/sites-cloud/authoring/sites-console/publishing-pages.md)。

每次执行以下操作时，都必须重新发布分类页面：

* 编辑分类页面。
* 编辑或添加分类页面中包含的标签和命名空间。

如果您创建新的分类页面，则必须先[将映射添加到项目](#paths-json)中的`paths.json`文件。

## 访问分类信息 {#accessing}

在发布分类后，通用编辑器就可以利用其信息并将其显示给您的用户。

您可以通过以下地址以 JSON 数据的形式访问分类。

`https://<branch>--<repository>--<owner>.aem.page/<taxonomy-json-name>.json`

使用您在[将分类映射到项目](#paths-json)中的`paths.json`文件时定义的`<taxonomy-json-name>`。 分类数据作为JSON数据返回，如下例所示。

```json
{
  "total": 3,
  "offset": 0,
  "limit": 3,
  "data": [
    {
      "tag": "default:",
      "title": "Standard Tags"
    },
    {
      "tag": "do-not-translate",
      "title": "Do Not Translate"
    },
    {
      "tag": "translate",
      "title": "Translate"
    }
  ],
  "columns": [
    "tag",
    "title"
  ],
  ":type": "sheet"
}
```

当您更新分类并重新发布时，此 JSON 数据将自动更新。您的应用程序可以通过编程方式为用户获取这些信息。

[如果您维护多种语言的标记](/help/sites-cloud/administering/tags.md#managing-tags-in-different-languages)，您可以通过将ISO2语言代码作为`sheet=`参数的值传递来访问这些语言。

## 公开其他标记属性 {#additional-properties}

默认情况下，您的分类将包含`tag`和`title`值，如上一个示例](#accessing)中的[所示。 您可以配置分类以公开其他标记属性。 在这个示例中，我们将公开标记描述。

1. 使用 Sites 控制台选择您创建的分类。
1. 点击或单击工具栏中的&#x200B;**属性**&#x200B;图标。
1. 在&#x200B;**其他属性**&#x200B;部分，点击或单击&#x200B;**添加**&#x200B;来添加字段。
1. 在新字段中，输入 JRC 属性名称公开。在这种情况下，输入 `jcr:description` 用于标记描述。
1. 点击或单击&#x200B;**保存并关闭**。
1. 在分类仍处于选定状态的情况下，在工具栏中点击或单击&#x200B;**快速发布**。

现在[当您访问分类](#accessing)时，标记描述（或您选择公开的任何属性）包含在JSON中。

```json
{
  "total": 3,
  "offset": 0,
  "limit": 3,
  "data": [
    {
      "tag": "default:",
      "title": "Standard Tags",
      "jcr:description": "These are the standard tags"
    },
    {
      "tag": "do-not-translate",
      "title": "Do Not Translate",
      "jcr:description": "Tag to mark pages that should not be translated"
    },
    {
      "tag": "translate",
      "title": "Translate",
      "jcr:description": "Tag to mark pages that should be translated"
    }
  ],
  "columns": [
    "tag",
    "title",
    "jcr:description"
  ],
  ":type": "sheet"
}
```
