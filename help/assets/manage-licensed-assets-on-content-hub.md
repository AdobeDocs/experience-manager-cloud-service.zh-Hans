---
title: 在Content Hub上管理许可的Assets
description: 了解如何将许可证字段添加到资源元数据表单、将许可证元数据属性应用于资源文件夹以及审批具有许可证的资源以供使用。
exl-id: ac3aad9f-c7b3-47a7-9314-a2f8277f0d3e
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 1%

---

# 在Content Hub上管理许可的Assets {#manage-licensed-assets-on-content-hub}

>[!AVAILABILITY]
>
>Content Hub指南现在提供了PDF格式。 下载整个指南，并使用Adobe Acrobat AI Assistant来回答您的疑问。
>
>[!BADGE Content Hub指南PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

作为管理员，编辑元数据表单以包含资源许可证字段，以便该字段显示在AEM创作环境的资源属性中。 然后，您可以批准资源及其许可证，以使资源获得许可并在Content Hub上可用。

执行以下步骤：

1. 编辑元数据表单以包含新文本字段以包含许可证详细信息。 将文本字段映射到`dc:license`属性。 有关如何向元数据表单添加字段和定义属性的详细信息，请参阅[设置元数据Forms](/help/assets/metadata-assets-view.md#metadata-forms)。
   ![zip提取](/help/assets/assets/metadata-form-edit.png)
1. 将元数据表单应用于资源文件夹，以应用步骤1中包含的设置。 有关如何将元数据表单分配给资源文件夹的信息，请参阅[将元数据表单分配给文件夹](/help/assets/metadata-assets-view.md#metadata-forms)。
1. [批准许可的PDF](/help/assets/manage-organize-assets-view.md#set-asset-status)
1. 选择资产并单击&#x200B;**详细信息**&#x200B;以查看其属性。 在步骤1中添加的许可证字段中，定义已在步骤3中批准或之前已批准的资产许可证的绝对路径。 Content Hub绝对路径遵循此标准模式： `/content/dam/(The asset's folder hierarchy within the DAM repository)/(asset_name).(file_extension)`。 例如， /content/dam/teamA/projects/documents/file1.pdf
   ![绝对路径](/help/assets/assets/absolute-path.png)
1. 批准资源以使其在Content Hub中可用，然后单击&#x200B;**保存**。 有关如何批准资产的信息，请参阅[设置资产状态](/help/assets/manage-organize-assets-view.md#set-asset-status)。
