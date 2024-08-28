---
title: 如何发送自适应表单以供审查？
description: 与一个或多个审阅人共享自适应表单以进行审阅。
uuid: 58c8c8fb-9262-4c37-b9b2-e46fe21b77d9
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 71d1aa10-d191-49bc-a50f-1098324f1cfe
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: 937bd4653e454beea3111cfc7ef7b4bbc1ace193
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---


# 将提交审阅人与表单关联 {#associating-submission-reviewers-with-a-form}

在创建表单时，您可以指定审阅通过表单门户提交的表单并提供反馈的用户。 贵组织可以收集反馈并对提交的表单进行返工。

[!DNL AEM Forms]允许您将审核者组与表单关联。 添加到表单审核组的用户，可以查看该表单的提交并提供反馈。

分配给表单的审阅人组只能审阅指定表单的提交。

## 先决条件 {#prerequisite}

### 使用元数据架构编辑器为自适应Forms启用提交审核者组属性 {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

要将审阅者组与表单关联，请编辑自适应Forms的元数据架构。 默认情况下，您无法将审阅者组添加到已提交的表单。

要编辑元数据架构，请执行以下操作：

1. 在创作模式的“Experience Manager”下，单击&#x200B;**工具** > **Assets** > **元数据架构**。
1. 在架构Forms页面中，导航到&#x200B;**Forms** > **在AEM中创作的Forms。**

   页面的URL为：

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. 选择&#x200B;**自适应表单**&#x200B;并单击&#x200B;**编辑**。
1. 在“编辑表单”页中，单击&#x200B;**高级**。
1. 在“高级”选项卡中，拖放“生成表单”下可用的&#x200B;**单行文本**&#x200B;组件。
1. 选择添加的文本组件以查看其设置。

   在“设置”下的“映射到属性”字段中输入`./jcr:content/metadata/form-submission-reviewer-group`。

   自适应表单的高级属性中的提交审核者组字段使用您在字段标签下指定的名称启用。

## 将提交审阅人与表单关联 {#associating-submission-reviewers-with-a-form-1}

要将提交审阅人与自适应表单关联，请创建一个审阅人组并将用户添加到该组。 在表单高级属性的表单提交审阅人字段下添加创建的审阅人组。
通过用户组，您可以将不同的提交审阅人集与不同的自适应Forms关联。 此功能可防止未经授权的用户进行提交审核。

执行以下步骤之前，请参阅[先决条件](adding-reviewers-form.md#prerequisite)。

若要创建组并向其添加成员，请导航到&#x200B;**工具** > **操作** > **安全** > **组**。
有关详细信息，请参阅[用户管理和服务](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html)。
确保将您创建的组添加为现成用户组的成员： **forms-submission-reviewers**。 此用户组随[!DNL AEM Forms]一起提供，它确保将用户添加为提交审核者。

要将用户组与自适应表单关联，请执行以下操作：

1. 在创作模式下，导航到&#x200B;**Forms** > **Forms和文档**。
1. 使用**选择**选项选择自适应表单，然后单击&#x200B;**查看属性**。
1. 在表单的“属性”窗口中，单击&#x200B;**编辑**，然后单击&#x200B;**高级**。
1. 在提交审核者组字段中输入组，然后单击&#x200B;**完成**。

   此时将显示提交审核者组字段，其中包含您在自适应Forms的已编辑元数据架构中指定的名称。

>[!NOTE]
>
>复制用户和表单，以确保[!DNL AEM Forms]的远程实现中的用户和表单可用。
>
>确保所有用户都作为查看远程实施中用户组的成员进行复制。

>[!MORELIKETHIS]
>
>* [创建和管理表单审核](/help/forms/create-reviews-forms.md)
>* [创建和管理自适应表单的审核](/help/forms/review-adaptiveforms-in-sites-page.md)