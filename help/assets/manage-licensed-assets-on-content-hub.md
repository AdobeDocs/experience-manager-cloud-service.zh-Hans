---
title: 管理 Content Hub 上的许可资产
description: 了解如何将许可证字段添加到资源元数据表单、将许可证元数据属性应用于资源文件夹以及审批具有许可证的资源以供使用。
badgeSaas: label="AEM Assets" type="Positive" tooltip="适用于AEM Assets)。"
exl-id: ac3aad9f-c7b3-47a7-9314-a2f8277f0d3e
source-git-commit: 59f97fc6ded4274c27400f56b50b4a3329cc471a
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 3%

---

# 管理 Content Hub 上的许可资产 {#manage-licensed-assets-on-content-hub}

作为管理员，编辑元数据表单以包含资源许可证字段，以便该字段显示在AEM创作环境的资源属性中。 然后，您可以批准资源及其许可证，以使资源获得许可并在Content Hub上可用。

执行以下步骤：

1. 编辑元数据表单以包含新文本字段以包含许可证详细信息。 将文本字段映射到`dc:license`属性。 有关如何向元数据表单添加字段和定义属性的详细信息，请参阅[设置元数据Forms](/help/assets/metadata-assets-view.md#metadata-forms)。
   ![zip提取](/help/assets/assets/metadata-form-edit.png)
1. 将元数据表单应用于资源文件夹，以应用步骤1中包含的设置。 有关如何将元数据表单分配给资源文件夹的信息，请参阅[将元数据表单分配给文件夹](/help/assets/metadata-assets-view.md#metadata-forms)。
1. [批准许可的PDF](/help/assets/manage-organize-assets-view.md#set-asset-status)
1. 选择资产并单击&#x200B;**详细信息**&#x200B;以查看其属性。 在步骤1中添加的许可证字段中，定义已在步骤3中批准或之前已批准的资产许可证的绝对路径。 Content Hub绝对路径遵循此标准模式： `/content/dam/(The asset's folder hierarchy within the DAM repository)/(asset_name).(file_extension)`。 例如， /content/dam/teamA/projects/documents/file1.pdf
   ![绝对路径](/help/assets/assets/absolute-path.png)
1. 批准资源以使其在Content Hub中可用，然后单击&#x200B;**保存**。 有关如何批准资产的信息，请参阅[设置资产状态](/help/assets/manage-organize-assets-view.md#set-asset-status)。

## 常见问题解答 {#faqs-manage-licensed-assets-content-hub}

### 在AEM Assets Content Hub上管理许可的资产有何用途？

在AEM Assets Content Hub上管理许可的资产允许管理员确保只有获得批准且许可证有效的资产才可供使用，从而在AEM创作环境中保持合规性和正确的元数据跟踪。

### 如何在Experience Manager as a Cloud Service中将许可证字段添加到资源属性？

在AEM Assets视图中，通过编辑元数据表单以包含映射到`dc:license`属性的新文本字段，可以将许可证字段添加到资源属性。 此字段随后显示在AEM Assets创作环境的资源属性中。

### 如何将元数据表单应用于资源文件夹，以便在AEM Assets的资源属性中包含许可证字段？

在AEM Assets视图中，编辑元数据表单以包含许可证字段。 将此元数据表单应用于所需的资源文件夹，以确保该文件夹中的所有资源都已合并新设置。

### 如何在AEM Assets视图中指定资源的许可证详细信息？

要指定许可证详细信息，请选择该资产，单击&#x200B;**详细信息**&#x200B;查看其属性，然后在添加到元数据表单的许可证字段中输入已批准资产许可证的绝对路径。

### 资源许可证的AEM Assets Content Hub绝对路径所需的格式是什么？

Content Hub绝对路径应遵循以下模式：/content/dam/（DAM存储库中资产的文件夹层次结构）/(asset_name)。（文件扩展名）。 例如 `/content/dam/teamA/projects/documents/file1.pdf`。

### 为何必须批准资源及其许可证，才能使其在AEM Assets Content Hub上可用？

批准资产及其许可证可确保AEM Assets Content Hub上仅提供经过适当许可和授权的资产，从而有助于保持合规性和适当的使用权限。

### 批准资产许可证后，如何在AEM Assets Content Hub中提供该资产？

在资产的属性中定义许可证路径后，批准资产并单击保存。 此操作可使许可的资源在AEM Assets Content Hub中可用。

### 谁将负责管理AEM Assets Content Hub中的许可资产？

管理员负责编辑元数据表单、将元数据表单分配给资源文件夹，以及在AEM Assets Content Hub中审批资源及其许可证。
