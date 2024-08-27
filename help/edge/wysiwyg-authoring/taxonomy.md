---
title: 管理分类数据
description: 了解如何管理分类数据，以便在Edge Delivery Services网站的AEM中使用标记。
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 81aacb0c616490eed4589cb8927ea1316ca1670e
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 8%

---


# 管理分类数据 {#managing-taxonomy-data}

了解如何管理分类数据，以便在Edge Delivery Services网站的AEM中使用标记。

## 简介 {#introduction}

标记是帮助您组织和管理页面的一项重要功能。 [AEM中的“标记控制台”](/help/sites-cloud/administering/tags.md#tagging-console)允许您创建丰富的标记分类来整理您的页面。

这些标记不仅对您和您的作者非常有用，而且对于您的读者也非常有用。 标记及其分类可用于页面上的组件中，以帮助读者导航您的内容。

通用编辑器仅适用于标记的ID。 通过为内容创建分类页面，您可以向通用编辑器公开所有语言中这些标记的描述，以便在呈现内容时使用该信息。

## 创建分类页 {#creating}

在AEM中创建的分类，类似于[任何其他页面。](/help/sites-cloud/authoring/sites-console/creating-pages.md)

1. 导航到&#x200B;[**站点**&#x200B;控制台。](/help/sites-cloud/authoring/sites-console/introduction.md)

1. 选择要创建分类的位置。

1. 点击或单击&#x200B;**创建**-> **页面**。

   ![创建页面](assets/taxonomy/create-page.png)

1. 在&#x200B;**创建页面**&#x200B;向导的&#x200B;**模板**&#x200B;选项卡上，选择&#x200B;**分类**&#x200B;模板，然后点按或单击&#x200B;**下一步**。

   ![分类模板](assets/taxonomy/taxonomy-template.png)

1. 在&#x200B;**创建页面**&#x200B;向导的&#x200B;**属性**&#x200B;选项卡上，为页面提供有意义的&#x200B;**标题**，在&#x200B;**标记**&#x200B;字段中，[使用标记选取器](/help/sites-cloud/authoring/sites-console/tags.md)选择要包含在分类中的标记或命名空间。

   ![分类属性](assets/taxonomy/create-page-wizard-properties.png)

1. 点击或单击“**创建**”。

此时将创建分类页面。 在&#x200B;**成功**&#x200B;对话框中，您可以点按或单击&#x200B;**完成**&#x200B;对话框以关闭消息，或者点按或单击&#x200B;**打开**&#x200B;以在[页面编辑器中编辑页面。](/help/sites-cloud/authoring/page-editor/introduction.md)

记下生成的分类页面名称，以便在以下步骤中使用。

## 编辑分类页面 {#editing}

与AEM中的任何其他页面一样，您开始编辑分类页面。

1. 导航到&#x200B;[**站点**&#x200B;控制台。](/help/sites-cloud/authoring/sites-console/introduction.md)

1. 选择要编辑的分类。

1. 在操作栏中点击或单击&#x200B;**编辑**。

1. 此时将打开页面编辑器，其中显示了分类。

   * 分类页面在页面编辑器中是只读的。

   ![编辑分类](assets/taxonomy/edit-page.png)

1. 点按或单击工具栏中的&#x200B;**页面信息**&#x200B;图标，然后选择&#x200B;**打开属性**。

   ![打开属性](assets/taxonomy/open-properties.png)

1. 在&#x200B;**页面属性**&#x200B;窗口中，您可以更新页面的名称并使用标记选择器更新分类中包含的标记和命名空间。

   ![编辑页面属性](assets/taxonomy/edit-properties.png)

1. 点按或单击&#x200B;**保存并关闭**。

在页面编辑器中显示的页面是只读的，因为分类的内容是从选定的标记和命名空间自动生成的。 它们用作自动生成分类内容的一种过滤器。 因此，没有必要在编辑器中直接编辑页面。

当您更新基础标记和命名空间时，AEM会自动更新分类页面的内容。 但是，您必须在进行任何更改后[重新发布分类](#publishing)，才能将这些更改提供给您的用户。

## 更新分类发布的paths.json {#paths-json}

就像在[管理和发布Edge Delivery Services网站的表格数据时，](/help/edge/wysiwyg-authoring/tabular-data.md)一样，您需要更新项目的`paths.json`文件以允许发布分类数据。

1. 在 GitHub 中打开您的项目的根目录。

1. 点击或单击 `paths.json` 文件以打开其详细信息，然后点击“**编辑**”图标。

   ![paths.json 文件](assets/taxonomy/paths-json.png)

1. 添加一行以将新分类页面映射到`.json`资源。

   ```json
   {
     "mappings": [
      "/content/<site-name>/:/",
      "/content/<site-name>/<taxonomy-page-name>:/<taxonomy-json-name>.json"
     ]
   }
   ```

   * `<taxonomy-page-name>`必须与您创建的[分类页面的名称匹配。](#creating)
   * `<taxonomy-json-name>`可以是您选择的任何有效名称。

1. 单击“**提交更改...**”将更改保存到 `main`。

   * 根据您的流程提交`main`或创建拉取请求。

每个分类页面只需执行一次此过程。 完成后，您可以发布分类。

## 发布分类 {#publishing}

在发布分类之前，该分类将无法供通用编辑器或您的用户使用。

分类页由[使用工具栏中的&#x200B;**快速Publish**&#x200B;或&#x200B;**管理发布**&#x200B;图标像任何其他页一样发布。](/help/sites-cloud/authoring/sites-console/publishing-pages.md)

每次执行以下操作时，您必须重新发布分类页面：

* 编辑分类页面。
* 编辑或添加到分类页面中包含的标记和命名空间。

如果您创建新的分类页面，则必须先[将映射添加到项目中的`paths.json`文件。](#paths-json)

## 访问分类信息 {#accessing}

发布分类后，通用编辑器会利用其信息并使其对用户可见。

您可以在以下地址以JSON数据的形式访问分类。

`https://<branch>--<repository>--<owner>.hlx.page/<taxonomy-json-name>.json`

使用您在[将分类映射到项目中的`paths.json`文件时定义的`<taxonomy-json-name>`。](#paths-json)分类数据作为JSON数据返回，如下例所示。

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
  ":type": "sheet"
}
```

当您更新分类并将其重新发布时，此JSON数据将自动更新。 您的应用程序能够以编程方式为用户访问此信息。

[如果您维护多种语言的标记，](/help/sites-cloud/administering/tags.md#managing-tags-in-different-languages)您可以通过将ISO2语言代码作为`sheet=`参数的值传递来访问这些语言。
