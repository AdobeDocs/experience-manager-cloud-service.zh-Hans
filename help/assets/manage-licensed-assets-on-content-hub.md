---
title: 管理 Content Hub 上的许可资产
description: 了解如何将许可证字段添加到资源元数据表单、将许可证元数据属性应用于资源文件夹以及审批具有许可证的资源以供使用。
exl-id: ac3aad9f-c7b3-47a7-9314-a2f8277f0d3e
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 19%

---

# 管理 Content Hub 上的许可资产 {#manage-licensed-assets-on-content-hub}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime和Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup><a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets与Edge Delivery Services的集成</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI可扩展性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新建</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>启用Dynamic Media Prime和Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜索最佳实践</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>元数据最佳实践</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 开发人员文档</b></a>
        </td>
    </tr>
</table>

>[!AVAILABILITY]
>
>Content Hub 指南现以 PDF 格式提供。下载完整指南并使用 Adobe Acrobat AI 助手来回答您的疑问。
>
>[!BADGE Content Hub 指南 PDF]{type=Informative url="https://helpx.adobe.com/cn/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

作为管理员，编辑元数据表单以包含资源许可证字段，以便该字段显示在AEM创作环境的资源属性中。 然后，您可以批准资源及其许可证，以使资源获得许可并在Content Hub上可用。

执行以下步骤：

1. 编辑元数据表单以包含新文本字段以包含许可证详细信息。 将文本字段映射到`dc:license`属性。 有关如何向元数据表单添加字段和定义属性的详细信息，请参阅[设置元数据Forms](/help/assets/metadata-assets-view.md#metadata-forms)。
   ![zip提取](/help/assets/assets/metadata-form-edit.png)
1. 将元数据表单应用于资源文件夹，以应用步骤1中包含的设置。 有关如何将元数据表单分配给资源文件夹的信息，请参阅[将元数据表单分配给文件夹](/help/assets/metadata-assets-view.md#metadata-forms)。
1. [批准许可的PDF](/help/assets/manage-organize-assets-view.md#set-asset-status)
1. 选择资产并单击&#x200B;**详细信息**&#x200B;以查看其属性。 在步骤1中添加的许可证字段中，定义已在步骤3中批准或之前已批准的资产许可证的绝对路径。 Content Hub绝对路径遵循此标准模式： `/content/dam/(The asset's folder hierarchy within the DAM repository)/(asset_name).(file_extension)`。 例如， /content/dam/teamA/projects/documents/file1.pdf
   ![绝对路径](/help/assets/assets/absolute-path.png)
1. 批准资源以使其在Content Hub中可用，然后单击&#x200B;**保存**。 有关如何批准资产的信息，请参阅[设置资产状态](/help/assets/manage-organize-assets-view.md#set-asset-status)。
