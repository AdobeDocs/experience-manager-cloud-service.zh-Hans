---
description: 本教程包含使表单的部分可重复使用的说明
title: Edge Delivery Services中的可重复部分
feature: Edge Delivery Services
source-git-commit: fd2e5df72e965ea6f9ad09b37983f815954f915c
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 1%

---


# Edge投放中的可重复部分

可重复部分是表单的一个组件，该组件可多次复制或复制以收集同一数据的多次出现的信息。

例如，考虑使用表单从申请贷款的用户那里收集信息。 该表单允许用户提供个人信息，包括共同贷款人的详情。 用户可以输入共同申请人的详细信息，此部分可重复。

![表单中的可重复部分](/help/forms/assets/eds-repeatable.png)

## 先决条件

使用AEM样板设置边缘交付服务(EDS) GitHub项目，并在本地计算机上克隆相应的GitHub存储库。 有关详细信息，请参阅[开发者教程](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/build/tutorial.html)。

## Edge投放中的可重复部分

让我们以贷款申请表为例。 用户可通过该表单提交个人信息。 您可以使用可重复部分包含共同申请人详细信息，并且可以选择至少和最多添加三个共同申请人部分。

>[!NOTE]
>
> * 您可以在Microsoft Site或SharePoint Drive上创作Google Excel，以使字段集在表单中可重复。
> * 在本例中，我们以Microsoft SharePoint为例。 要将您的SharePoint文件夹作为内容源，请按照中所述的步骤操作 [如何使用Sharepoint](https://www.aem.live/docs/setup-customer-sharepoint).


要在Edge Delivery中添加可重复的部分，请执行以下操作：

1. [使用Microsoft Excel创作表单](#author-form)
2. [预览和发布表单](#preview-form)

### 使用Microsoft Excel创作表单 {#author-form}

1. 转到您的Microsoft SharePoint帐户，然后打开或创建AEM Edge交付项目目录。
2. 打开现有的Microsoft Excel文件或新建。
在本例中，我们使用了一个名为的Excel工作表 `loan-application.xlsx` 在Microsoft SharePoint站点中创建。
3. 添加标记为的新列 `Repeatable`， `Min`、和 `Max` 在Microsoft Excel文件中。
4. 指定值 `Repeatable` 列为 `True` 用于要使其可重复的字段集。
5. 指定值 `Min` 和 `Max` 列。 此 `Min` 值表示面板重复出现的最小次数，而 `Max` 值表示面板重复出现的最大次数。
6. 保存Microsoft Excel文件。

>[!NOTE]
>
> 这是 [贷款申请](/help/forms/assets/loan-application.xlsx) excel工作表以供您参考。

### 使用您的边缘交付服务预览/发布表单

1. 在Microsoft SharePoint站点中打开或创建新文档文件，以使用 `Form Block`. 例如，打开 `index` 文件并添加 `Form Block`.
2. 打开命令提示符，导航到本地计算机上的AEM Edge Delivery项目目录，然后如下所示执行命令 `aem up`.

可在以下位置访问该表单： `https://localhost:3000`，其中单击 `Add` 按钮添加新的可重复部分，用于输入共同申请人详细信息。 您也可以通过单击 `Delete` 按钮。

>[!NOTE]
>
> 如果在本地主机访问您的表单时遇到“页面未找到”错误，请将Microsoft SharePoint站点的目录名称添加到表单所在的URL前面。 例如，`http://localhost:3000/<dir-name>/`




