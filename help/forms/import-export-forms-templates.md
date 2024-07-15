---
title: 如何在AEM Forms实例上导入、导出和组织自适应Forms或PDF forms？
description: 了解如何在AEM实例之间迁移自适应Forms、PDF forms、主题和其他支持资源。
topic-tags: forms-manager
role: Admin, User
feature: Adaptive Forms
exl-id: f5105fb7-b8c0-4656-8095-b21d392746c0
source-git-commit: 6f547bd743932d45e45e0a3c47ff5eb2129cb664
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 3%

---



| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/manage-administer-aem-forms/import-export-forms-templates) |
| AEM as a Cloud Service | 本文 |

# 导入或导出自适应Forms和AEM Forms资源 {#importing-and-exporting-assets-to-aem-forms}

您可以在[!DNL AEM Forms]实例之间移动自适应Forms和相关资源，例如自适应表单主题、表单数据模型(FDM)、自适应表单模板、片段和PDF forms。

## 下载自适应Forms、PDF forms或相关资源 {#download-forms-amp-documents-assets}

要下载表单或相关资源，请执行以下操作：

1. 登录到您的[!DNL Experience Manager Forms]实例。
1. 选择&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。

   ![选择Forms](/help/forms/assets/select-forms.png)

1. 选择资源，然后单击上边栏中的&#x200B;**[!UICONTROL 下载]**&#x200B;图标。

   ![下载Forms](/help/forms/assets/download-form.png)

   下载表单时，出现&#x200B;**[!UICONTROL 下载资源]**&#x200B;对话框。

   ![下载表单资源](/help/forms/assets/download-form-assets.png)

1. 单击&#x200B;**[!UICONTROL “下载”。]**

选定的资产将下载为存档（.zip文件）。

## 上传自适应Forms、PDF forms或相关资源 {#upload-forms-amp-documents-assets}

您可以单独上传支持的资源类型，也可以以ZIP存档的形式上传。 对于ZIP文件，将显示所有受支持资源的相对路径。 ZIP文件中不受支持的资源将被忽略并且不会列出。 但是，如果ZIP存档仅包含不支持的资源，则会显示错误消息，而不是弹出对话框。
要上传表单或相关资源，请执行以下操作：

1. 登录到您的[!DNL Experience Manager Forms]实例。
1. 选择&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。

   ![选择Forms](/help/forms/assets/select-forms.png)

1. 选择&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 文件上传]**。 将显示一个对话框。

   ![上传Forms](/help/forms/assets/form-upload.png)

1. 在对话框中，浏览并选择要导入的软件包或存档。 您还可以选择其他支持的文件类型。 选择&#x200B;**[!UICONTROL 打开]**。 您选择的文件夹或文件名不得包含任何特殊字符。

   在该对话框中，验证要上传的资源的详细信息，然后选择&#x200B;**[!UICONTROL 上传]**。

   如果上传现有的表单资源，则会更新该资源。

   >[!NOTE]
   >
   > 当名称与不同的资源类型冲突时，上传包不会替换现有的文件夹层次结构。 例如，如果一台服务器上的位置`/content/dam/formsanddocuments`有一个名为“Training”的自适应表单。 您可以下载自适应表单并将表单上传到其他服务器。 第二台服务器也在同一位置`/content/dam/formsanddocuments`有一个名为“Training”的文件夹。 上传失败。

## 下载主题

您可以导出[!DNL AEM Forms]中在其他项目或实例中使用的主题。 AEM允许您将主题下载为zip文件，并可在实例上上传这些主题。
要下载主题，请执行以下操作：

1. 登录到您的[!DNL Experience Manager Forms]创作实例。
1. 选择&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL 主题]**。

   ![选择主题](/help/forms/assets/select-theme.png)

1. 在主题页面上，选择主题，然后单击上边栏中的&#x200B;**[!UICONTROL 下载]**&#x200B;图标。

   ![下载主题](/help/forms/assets/download-theme.png)

   下载主题时，出现&#x200B;**[!UICONTROL 下载资源]**&#x200B;对话框。

   ![下载主题资产](/help/forms/assets/download-theme-asset.png)

1. 单击&#x200B;**[!UICONTROL “下载”。]**

选定的资产将下载为存档（.zip文件）。

## 上传主题 {#uploading-a-theme}

您可以上传和使用其他人在您的表单中创建的主题。
要上传主题，请执行以下操作：

1. 登录到您的[!DNL Experience Manager Forms]实例。
1. 在Experience Manager中，导航到&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL 主题]**。

   ![选择主题](/help/forms/assets/select-theme.png)

1. 在“主题”页面上，单击&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 文件上传]**。

   ![上载主题](/help/forms/assets/theme-upload.png)

1. 浏览并选择计算机上的主题包，然后单击&#x200B;**[!UICONTROL 上传]**。 上传的主题将显示在“主题”页面上。

## 使用文件夹整理自适应Forms、PDF forms和相关资源  {#folders-and-organizing-assets}

您可以使用文件夹来排列和组织资源。 在文件夹中组织文档和资产可让您将文件分组以便于管理。 您可以选择文件夹，然后选择下载或删除该文件夹。

### 创建文件夹 {#create-a-folder}

要创建文件夹，请执行以下操作：

1. 登录到您的[!DNL Experience Manager Forms]实例。
1. 选择&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。

   ![选择表单](/help/forms/assets/select-forms.png)

1. 选择&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 文件夹]**。

   ![创建文件夹](/help/forms/assets/create-folder.png)

   出现&#x200B;**[!UICONTROL 添加文件夹]**&#x200B;对话框。
1. 输入&#x200B;**[!UICONTROL 标题]**。 在您键入&#x200B;**[!UICONTROL 标题]**&#x200B;时，**[!UICONTROL 名称]**&#x200B;会自动填充。

   ![添加文件夹](/help/forms/assets/add-folder.png)

1. 单击&#x200B;**[!UICONTROL 创建]**。

   >[!NOTE]
   >
   >默认情况下，名称字段的值会自动从标题中填充。 名称只能包含字母数字字符，或连字符(-)和下划线(_)特殊字符。 在标题中输入的任何其他特殊字符都会自动替换为连字符，并提示您确认新名称。 您可以选择继续使用建议的名称或对其进行编辑。

具有您定义的标题的新文件夹将显示在资产列表中的当前位置。

如果存在具有指定名称的文件夹，则提交会失败并出现错误。 您可以将鼠标悬停在名称字段旁边显示的错误![aem6forms_error_alert](assets/Smock_Alert_18_N.svg)图标上，以查看错误消息。

您可以选择创建的文件夹，以进入该文件夹，并在该文件夹中创建资源或文件夹。 此外，您还可以选择一个文件夹，并选择将该文件夹排入下载队列、删除或编辑其名称。

### 创建一个或多个资产的副本 {#create-copies-of-one-or-more-assets-or-letters}

您可以使用现有资源快速创建具有相似属性、内容和继承资源的资源。

要创建资产的副本，请执行以下操作：

1. 登录到您的[!DNL Experience Manager Forms]实例。
1. 在相关资产页面上，选择一个或多个资产。 用户界面显示&#x200B;**[!UICONTROL 复制]**&#x200B;图标。
1. 选择&#x200B;**[!UICONTROL 复制]**。 用户界面显示![粘贴图标](/help/forms/assets/Smock_Paste_18_N.svg)图标。

   ![复制资产](/help/forms/assets/copy-asset.png)

   在粘贴之前，您还可以选择在文件夹内进行导航/导航。 不同的文件夹可以包含具有相同名称的资源。 有关文件夹的详细信息，请参阅[文件夹和组织资源](#folders-and-organizing-assets)。
1. 选择&#x200B;**[!UICONTROL 粘贴]**。

   ![粘贴资产](/help/forms/assets/paste-asset.png)

1. 出现&#x200B;**[!UICONTROL 粘贴]**&#x200B;对话框。 系统会自动为资产的新副本生成名称和标题，但您可以编辑资产的标题和名称。

   如果您在同一位置复制和粘贴资产，则会将后缀“ — CopyXX”添加到`asset`的现有名称中。 如果复制的资产不存在标题，则自动生成的标题字段将保留为空。

   ![将资产粘贴到新位置](/help/forms/assets/paste-click-asset.png)

   如有必要，请编辑要用于保存资产副本的&#x200B;**[!UICONTROL 标题]**。 在您键入&#x200B;**[!UICONTROL 标题]**&#x200B;时，**[!UICONTROL 名称]**&#x200B;会自动填充。
1. 选择&#x200B;**[!UICONTROL 粘贴]**。 将创建复制资产的新副本。

## 搜索 {#search-forms}

当您拥有大量资源时，搜索合适的资源非常耗时。 您可以在资源页面上执行基于文本的搜索。

要搜索资源，请执行以下操作：

1. 登录到您的[!DNL Experience Manager Forms]实例。
1. 单击![搜索图标](assets/folder-search-icon.svg)搜索图标。

   ![搜索表单](/help/forms/assets/search-form.png)

1. 在搜索栏中输入要搜索的资源的名称。

1. 此时将显示相关资源的列表。 从显示的资源列表中选择所需的资源。

   ![搜索资产](/help/forms/assets/search-bar.png)

有关使用搜索功能的更多信息和说明，请参阅[搜索](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html)。

<!--
## Export or create a package {#export-a-workflow-application}

You can use packages to install new content, install new functionality, transfer content between instances, and back up content.
To export or create a package:

1. Log in to your [!DNL Experience Manager Forms] instance.
1. Navigate to **[!UICONTROL Tools]** ![hammer](assets/hammer.png) &gt; **[!UICONTROL Deployment]** &gt; **[!UICONTROL Packages]**.

   ![Package Manager](/help/forms/assets/package-manager.png)

1. Click **[!UICONTROL Create Package]**.

   ![Create package](/help/forms/assets/create-package.png)   
   
   When **[!UICONTROL Create Package]** is clicked, the **[!UICONTROL New Package]** dialog box appears.
1. Specify the package name, version, and group for the package. 
   
   ![New package](/help/forms/assets/new-package.png)  

   * **Package Name** - Select a descriptive name to help you identify the contents of the package.

   * **Version** - It is a textual field to indicate a version. This is appended to the package name to form the name of the zip file.

   * **Group** - This is the target group (or folder) name. Groups help you organize your packages. A folder is created for the group if it does not already exist. If you leave the group name blank, it creates the package in the main package list.

1. Click **[!UICONTROL OK]**.

   Once the package is created, it appears at the top of the list of packages.

1. Click **[!UICONTROL Edit]**.
   
   ![Edit Package](/help/forms/assets/edit-package.png)
    
1. Open the **[!UICONTROL Filters]** tab.
   
   ![Open filter tab](/help/forms/assets/add-filter-package.png)
   
1.  Click **[!UICONTROL Add Filter]**. 
   
      ![Add filter](/help/forms/assets/add-filter.png)

      You can specify the path of the package. You can also add rules and other validations for the package.

      ![Add path](/help/forms/assets/add-path.png)

1. Click **[!UICONTROL Save]** after you are finished editing the settings.
1. Click **[!UICONTROL Build]** to create the package.
    
     ![Build path](/help/forms/assets/build-package.png)

   After the package is built, you can download the package and import it to the other server. The workflow application appears on the server where the package is uploaded.

   >[!NOTE]
   >
   >For the workflow application to work properly, also export the corresponding Adaptive Form and workflow model with the work application.

   Once a package is uploaded to AEM, you can modify its settings. You can also download or delete the package.

## Import and export assets in Correspondence Management {#import-and-export-assets-in-correspondence-management}

To share assets, such as data dictionaries, letters, and document fragments, between two different implementations of Correspondence Management, you can create and share .cmp files. A .cmp file can include one or more data dictionaries, letters, document fragments, and forms.

### Export Document Fragments, Letters, and/or Data Dictionaries {#export-document-fragments-letters-and-or-data-dictionaries}

1. In the letters, document fragments, or data dictionary pages, select and select the assets you want to export to a single package, and then select Queue For Download. The assets are lined-up for export.
1. As required, repeat the above step to add letters, document fragments, and data dictionaries.
1. Select **Download**.
1. Correspondence Management displays Download Asset(s) dialog with a list of assets in the export list.

   ![export](assets/export.png)

1. To view the dependencies that are exported, Select Resolve. Or skip to the next step. Even if you do not select resolve, the dependencies are still exported.
1. To download the .cmp file, select **OK**.
1. Correspondence Management downloads a .cmp file to your computer.

   The .cmp file includes the exported assets. You can share the .cmp file with others. Other users can import the .cmp file in a different server to get all the assets in the new server.

### Export all the Correspondence Management assets as a package {#export-all-the-correspondence-management-assets-as-a-package}

Use this option to download all the Correspondence Management assets and related dependencies as a package from an [!DNL AEM Forms] instance.

For example, if Correspondence Management has a letter that uses an image and text, the downloaded package also contains the image and the text related to the letter. All the metadata properties (including custom properties) associated with the asset are also downloaded. Once you have downloaded the package (.cmp), you can [import the package to a different [!DNL AEM Forms] instance](import-export-forms-templates.md#p-upload-forms-documents-assets-p).

To download all the Correspondence Management assets and related dependencies as a package, complete the following steps:

1. Log in to [!DNL AEM Forms] server as a forms user.
1. Select **Adobe Experience Manager** in the Global Navigation bar.
1. Select tools ( ![tools](assets/tools.png)) and then select **Forms**.
1. Select **Export Correspondence Management Assets**.

   ![publish-cmp-assets-1](assets/publish-cmp-assets-1.png)

   ( ``The Export All Correspondence Management Assets page appears and displays the information about the last time the Export process was attempted and a link to download the last successfully exported package.

   ![export-last-run-details](assets/export-last-run-details.png)

1. Select **Export** and, in the confirm message, select **OK**.

   After a batch process is complete, the last run details and the link to download the package are updated. This includes information such as the Administrator login and if the batch run successfully or failed. The assets are exported to a package and the Download Exported Package link appears.

   >[!NOTE]
   >
   >The Export All Assets process cannot be canceled once initiated. Also, while the export all operation is in process, do not create, delete, modify, or publish any assets or initiate Publish All Assets process.a

1. Select the **Download Exported Package** link to download the package file.

   To add the assets in the package to another instance of Correspondence Management, [import the package to an [!DNL AEM Forms] instance](import-export-forms-templates.md#p-upload-forms-documents-assets-p).

<!-- ### Import Document Fragments, Letters and/or Data Dictionaries into Correspondence Management {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

You can import assets that are exported into a .cmp file. A .cmp file can have one or more letters, data dictionaries, document fragments, and dependent assets.

>[!NOTE]
>
>While importing old Correspondence Management assets for migration, log in using an Admin account. For more information on Migrating old Correspondence Management assets, see [Migrate Correspondence Management assets to AEM 6.1 forms](migration-utility.md).

1. On the data dictionary, letters, or document fragments page, select **Create &gt; File Upload** and select the .cmp file.
1. Correspondence Management displays the Import Assets dialog with the list of assets that are imported. Select **Import**.

   After importing the assets, the following properties of the assets are updated while the other properties remain the same:

    * Author: Displays the ID of the user that imported the asset to the server
    * Modified: The time when the asset was imported to the server

   >[!NOTE]
   >
   >For you to be able to upload XDPs (as part of the cmp file or otherwise), you need to be a part of forms-power-users group. For access rights, contact the administrator. -->

## 另请参阅 {#see-also}

{{see-also}}
