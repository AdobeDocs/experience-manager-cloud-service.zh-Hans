---
title: 如何在AEM Forms实例上导入、导出和组织自适应Forms或PDF forms？
description: 了解如何在AEM实例之间迁移自适应Forms、PDF forms、主题和其他支持资源。
topic-tags: forms-manager
exl-id: f5105fb7-b8c0-4656-8095-b21d392746c0
source-git-commit: d33c7278d16a8cce76c87b606ca09aa91f1c3563
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 1%

---

# 导入或导出自适应Forms和AEM Forms资源 {#importing-and-exporting-assets-to-aem-forms}

您可以在以下位置移动自适应Forms和相关资源，例如自适应表单主题、表单数据模型、自适应表单模板、文档片段和PDF forms [!DNL AEM Forms] 实例。 您可以导入和导出CRX包或二进制文件格式的资产。

导出自适应表单时，不会导出内容策略和模板。 使用 [包管理器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#how-rolling-deployments-work) 以导出此类资产。

## 下载自适应Forms、PDF forms或相关资源 {#download-forms-amp-documents-assets}

要下载表单或相关资源，请执行以下操作：

1. 登录 [!DNL AEM Forms] 实例。
1. 点按 **[!UICONTROL Adobe Experience Manager]** ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 图标> **[!UICONTROL 导航]** ![指南针](assets/Smock_Compass_18_N.svg) 图标> **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.
1. 选择资产并点按 **[!UICONTROL 下载]** 图标。
1. 在下载资产中，选择以下选项之一，然后点按 **[!UICONTROL 下载]**.

   * **下载为CRX包：** 使用选项从下载和移动所有选定的资源和相关依赖项 [!DNL AEM Forms] 实例到另一个实例。 它以CRX包形式下载所有资源和文件夹，包括在AEM中创作的表单(自适应Forms和自适应表单片段)、表单集、表单数据模型、表单模板、PDF文档以及引用的资源（XSD和图像）。
将资源下载为资源包的优势在于它还可以下载选定资源引用的资源。 例如，如果您有一个使用表单模板、XSD和图像的自适应表单。 当您选择此自适应表单并将其下载为包时，下载的包中还包含表单模板、XSD和图像。 与资源关联的所有元数据属性（包括自定义属性）也会下载。

   * **将资产下载为二进制文件：** 使用选项可仅下载表单模板(XDP)、PDF forms(PDF)、文档(PDF)和资源（图像、架构、样式表）。 您可以使用外部应用程序编辑这些资源。 它会将具有二进制文件的资源(例如图像、PDF和其他支持的格式)下载为.zip文件。
您无法使用以下内容下载自适应Forms、自适应表单片段、主题和表单集 **[!UICONTROL 将资产下载为二进制文件]** 选项。 要下载这些资源，您应使用 **[!UICONTROL 下载为CRX包]** 选项。

   选定的资产将下载为存档（.zip文件）。

   >[!NOTE]
   >
   >AEM包和二进制文件都将作为存档（.zip文件）下载。 资产的模板不会与资产一起下载。 您需要单独导出资产模板。

## 上传自适应Forms、PDF forms或相关资源 {#upload-forms-amp-documents-assets}

您可以单独上传支持的资源类型，也可以以ZIP存档的形式上传。 对于ZIP文件，将显示所有受支持资源的相对路径。 ZIP文件中不受支持的资源将被忽略并且不会列出。 但是，如果ZIP存档仅包含不支持的资源，则会显示错误消息，而不是弹出对话框。
要上传表单或相关资源，请执行以下操作：

1. 登录 [!DNL AEM Forms] 实例。
1. 点按 **[!UICONTROL Adobe Experience Manager]** ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 图标> **[!UICONTROL 导航]** ![指南针](assets/Smock_Compass_18_N.svg) 图标> **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.
1. 点按 **[!UICONTROL 创建]** > **[!UICONTROL 文件上传]**. 将显示一个对话框。
1. 在对话框中，浏览并选择要导入的软件包或存档。 您还可以选择其他支持的文件类型。 点按 **[!UICONTROL 打开]**. 您选择的文件夹或文件名不得包含任何特殊字符。

   在对话框中，验证要上传的资源的详细信息，然后点击 **[!UICONTROL 上传]**.

   如果上传现有的表单资源，则会更新该资源。

   >[!NOTE]
   >
   > * 当名称与不同的资源类型冲突时，上传包不会替换现有的文件夹层次结构。 例如，如果一台服务器上位于/content/dam/formsanddocuments的位置有一个名为“Training”的自适应表单。 您下载自适应表单并将表单上传到其他服务器。 第二台服务器还在同一位置/content/dam/formsanddocuments具有一个名为“Training”的文件夹。 上传失败。
   > * 仅属于 `form-power-user` 组可以上传XDP文件。


## 下载主题 {#downloading-a-theme}

您可以在中导出主题 [!DNL AEM Forms] 您可在其他项目或实例中使用的任何其他插件。 AEM允许您将主题下载为zip文件，并可在实例上上传这些主题。

要下载主题，请执行以下操作：

1. 登录 [!DNL AEM Forms] 实例。
1. 点按 **[!UICONTROL Adobe Experience Manager]** ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 图标> **[!UICONTROL 导航]** ![指南针](assets/Smock_Compass_18_N.svg) 图标> **[!UICONTROL Forms]** > **[!UICONTROL 主题]**.
1. 选择主题并点按 **[!UICONTROL 下载]**. 主题将下载为存档（.zip文件）。

## 上传主题 {#uploading-a-theme}

您可以上传和使用其他人在您的表单中创建的主题。 要上传主题，请执行以下操作：

1. 在Experience Manager中，导航到 **[!UICONTROL Forms]** > **[!UICONTROL 主题]**.
1. 在“主题”页面上，单击 **[!UICONTROL 创建]** > **[!UICONTROL 文件上传]**.
1. 在“文件上传”提示符下，浏览并选择计算机上的主题包，然后单击 **[!UICONTROL 上传]**. 上传的主题可在主题页面上找到。

<!-- ## Import and export assets in Correspondence Management {#import-and-export-assets-in-correspondence-management}

To share assets, such as data dictionaries, letters, and document fragments, between two different implementations of Correspondence Management, you can create and share .cmp files. A .cmp file can include one or more data dictionaries, letters, document fragments, and forms.

### Export Document Fragments, Letters, and/or Data Dictionaries {#export-document-fragments-letters-and-or-data-dictionaries}

1. In the letters, document fragments, or data dictionary pages, tap and select the assets you want to export to a single package, and then tap Queue For Download. The assets are lined-up for export.
1. As required, repeat the above step to add letters, document fragments, and data dictionaries.
1. Tap **Download**.
1. Correspondence Management displays Download Asset(s) dialog with a list of assets in the export list.

   ![export](assets/export.png)

1. To view the dependencies that are exported, Tap Resolve. Or skip to the next step. Even if you do not tap resolve, the dependencies are still exported.
1. To download the .cmp file, tap **OK**.
1. Correspondence Management downloads a .cmp file to your computer.

   The .cmp file includes the exported assets. You can share the .cmp file with others. Other users can import the .cmp file in a different server to get all the assets in the new server.

### Export all the Correspondence Management assets as a package {#export-all-the-correspondence-management-assets-as-a-package}

Use this option to download all the Correspondence Management assets and related dependencies as a package from an [!DNL AEM Forms] instance.

For example, if Correspondence Management has a letter that uses an image and text, the downloaded package also contains the image and the text related to the letter. All the metadata properties (including custom properties) associated with the asset are also downloaded. Once you have downloaded the package (.cmp), you can [import the package to a different [!DNL AEM Forms] instance](import-export-forms-templates.md#p-upload-forms-documents-assets-p).

To download all the Correspondence Management assets and related dependencies as a package, complete the following steps:

1. Log in to [!DNL AEM Forms] server as a forms user.
1. Tap **Adobe Experience Manager** in the Global Navigation bar.
1. Tap tools ( ![tools](assets/tools.png)) and then tap **Forms**.
1. Tap **Export Correspondence Management Assets**.

   ![publish-cmp-assets-1](assets/publish-cmp-assets-1.png)

   ( ``The Export All Correspondence Management Assets page appears and displays the information about the last time the Export process was attempted and a link to download the last successfully exported package.

   ![export-last-run-details](assets/export-last-run-details.png)

1. Tap **Export** and, in the confirm message, tap **OK**.

   After a batch process is complete, the last run details and the link to download the package are updated. This includes information such as the Administrator login and if the batch run successfully or failed. The assets are exported to a package and the Download Exported Package link appears.

   >[!NOTE]
   >
   >The Export All Assets process cannot be canceled once initiated. Also, while the export all operation is in process, do not create, delete, modify, or publish any assets or initiate Publish All Assets process.a

1. Tap the **Download Exported Package** link to download the package file.

   To add the assets in the package to another instance of Correspondence Management, [import the package to an [!DNL AEM Forms] instance](import-export-forms-templates.md#p-upload-forms-documents-assets-p).

<!-- ### Import Document Fragments, Letters and/or Data Dictionaries into Correspondence Management {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

You can import assets that are exported into a .cmp file. A .cmp file can have one or more letters, data dictionaries, document fragments, and dependent assets.

>[!NOTE]
>
>While importing old Correspondence Management assets for migration, log in using an Admin account. For more information on Migrating old Correspondence Management assets, see [Migrate Correspondence Management assets to AEM 6.1 forms](migration-utility.md).

1. On the data dictionary, letters, or document fragments page, tap **Create &gt; File Upload** and select the .cmp file.
1. Correspondence Management displays the Import Assets dialog with the list of assets that are imported. Tap **Import**.

   After importing the assets, the following properties of the assets are updated while the other properties remain the same:

    * Author: Displays the ID of the user that imported the asset to the server
    * Modified: The time when the asset was imported to the server

   >[!NOTE]
   >
   >For you to be able to upload XDPs (as part of the cmp file or otherwise), you need to be a part of forms-power-users group. For access rights, contact the administrator. -->

## 导出工作流应用程序 {#export-a-workflow-application}

您可以使用包管理器导出工作流应用程序。 此过程如下所示：

1. 打开 [!DNL AEM Forms] 包管理器。 包管理器的URL为 `https://[server]:[port]/crx/packmgr`.
1. 单击 **[!UICONTROL 创建包]**. 此 **[!UICONTROL 新建包]** 对话框。
1. 指定包的名称、版本和组。 单击&#x200B;**[!UICONTROL 确定]**。
1. 单击 **[!UICONTROL 编辑]** 然后打开 **[!UICONTROL 过滤器]** 选项卡。 单击 **[!UICONTROL 添加筛选器]**. 指定工作流应用程序的路径。 例如，/etc/fd/dashboard/startpoints/homemortgage。 单击 **[!UICONTROL 添加规则]**.

1. 打开&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡。选择 **[!UICONTROL 合并]** 或 **[!UICONTROL 覆盖]** 在ACL处理字段中。 单击&#x200B;**[!UICONTROL 保存]**。
1. 单击 **[!UICONTROL 生成]** 以创建包。

   生成包后，您可以下载包并将其导入其他服务器。 工作流应用程序会出现在上传包的服务器上。

   >[!NOTE]
   >
   >为使工作流应用程序正常工作，还应将相应的自适应表单和工作流模型导出到工作应用程序。

## 使用文件夹整理自适应Forms、PDF forms和相关资源  {#folders-and-organizing-assets}

您可以使用文件夹来排列和组织资源。 在文件夹中组织文档和资产可让您将文件分组以便于管理。 您可以选择文件夹，然后选择下载或删除该文件夹。 要创建文件夹，请完成以下步骤：

### 创建文件夹 {#create-a-folder}

1. 登录 [!DNL AEM Forms] 实例。
1. 点按Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 图标>导航 ![指南针](assets/Smock_Compass_18_N.svg) 图标> **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.
1. 点按 **[!UICONTROL 创建]** > **[!UICONTROL 文件夹]**.
1. 输入以下详细信息：

   * **[!UICONTROL 标题]**：文件夹的显示名称
   * **[!UICONTROL 名称]**： *（必需）* 要在存储库中存储文件夹的节点名称

   >[!NOTE]
   >
   >默认情况下，名称字段的值会自动从标题中填充。 名称只能包含字母数字字符，或连字符(-)和下划线(_)特殊字符。 在标题中输入的任何其他特殊字符都会自动替换为连字符，并提示您确认新名称。 您可以选择继续使用建议的名称或对其进行编辑。

1. 具有您定义的标题的新文件夹将显示在资产列表中的当前位置。

   如果存在具有指定名称的文件夹，则提交会失败并出现错误。 您可以通过将鼠标悬停在错误上来查看错误消息 ![aem6forms_error_alert](assets/Smock_Alert_18_N.svg) 显示在“名称”字段旁边的图标。

   您可以点按新创建的文件夹以进入该文件夹，并在该文件夹中创建资产或文件夹。 此外，您还可以选择一个文件夹，并选择将该文件夹排入下载队列、删除或编辑其名称。


<!-- ### Create copies of one or more assets or letters {#create-copies-of-one-or-more-assets-or-letters}

You can use an existing assets to quickly create an asset with similar properties, content, and inherited assets.

Complete the following steps to create copies of assets and letters:

1. On the relevant assets page, select one or more assets. The UI displays the Copy icon.
1. Tap **[!UICONTROL Copy]**. The UI displays the **[!UICONTROL Paste]** icon. You can also choose to go/navigate inside a folder before you paste. Different folders can contain assets with same names. For more information on folders, see [Folders and organizing assets](#folders-and-organizing-assets).
1. Tap **[!UICONTROL Paste]**. The **[!UICONTROL Paste]** dialog appears. The system auto generates names and titles to the new copies of assets/letters, but you can edit the titles and names of the assets/letters.

   If you are copying and pasting the assets/letters at the same place, a suffix "-CopyXX" gets added to the existing name of the asset/letter. If no title existed for the copied asset/letter, the auto generated title field remains blank.

1. If required, edit the Title and Name with which you want to save the copy of the asset/letter.
1. Tap **[!UICONTROL Paste]**. New copies of the copied assets are created.

## Search {#search-forms}

You ca use the top bar **[A]** to search your content. When you search for assets, a side panel is displayed. You can also tap ![assets-browser-content-only](assets/assets-browser-content-only.png) &gt; Filter **[B]** to invoke the side panel. Using the various filters in the side panel, you can narrow down your search. The side panel also lets you save your searches.

![search_topbar](assets/search_topbar.png)

**A.** Search **B.** Filter

![Side panel - Filters](assets/search_sidepanel.png)

Side panel - Filters

On the side panel, you can use the following to narrow down your search results:

* Search Directory
* Tags
* Search Criteria; for example, Modified Dates, Publish Status, LiveCopy Status.

The side panel also lets you save your search settings with names of your choice.

For more information and instructions on using search, filters, saved search, and side panel, see [Search](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html). -->
