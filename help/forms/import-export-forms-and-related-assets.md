---
title: 如何将资产导入和导出到 [!DNL AEM Forms]？
description: 了解如何将DocuSign与自适应表单一起使用来收集电子签名。
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '1313'
ht-degree: 0%

---


# 导入和导出资源 {#importing-and-exporting-assets-to-aem-forms}

您可以在不同[!DNL AEM Forms]实例之间移动表单、主题、模板、文档片段、主题和其他资源。 将系统或从开发或暂存服务器向生产服务器迁移表单时，需要执行此类移动。

对于支持通过[!DNL AEM Forms] UI上载和导入的资源，建议使用Forms UI进行导出或导入。 不建议使用AEM包管理器导出或导入此类资源。

## 下载或上传Forms &amp; Documents资源 {#download-or-upload-forms-amp-documents-assets}

通过[!DNL AEM Forms]用户界面，您可以通过将资源下载为AEM CRX包或二进制文件来从AEM实例导出资源。 然后，您可以将下载的AEM CRX包或二进制文件导入到另一个AEM实例中。

除自适应表单模板和自适应表单内容策略之外，所有资产都支持通过[!DNL AEM Forms]用户界面导出和导入。 因此，在从[!DNL AEM Forms] UI导出自适应表单时，不会像其他相关的资产一样自动导出相关的自适应表单模板和内容策略。

对于这些资源类型，必须使用AEM包管理器在源AEM服务器上创建CRX包，并在目标服务器上安装该包。 有关创建和安装包的信息，请参阅[部署到AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html)。

### 下载Forms和文档资源 {#download-forms-amp-documents-assets}

要下载Forms和文档资源，请执行以下操作：

1. 登录到[!DNL AEM Forms]实例。
1. 选择Experience Manager![adobeexperiencemanager](assets/adobeexperiencemanager.png)图标>导航![compass](assets/Smock_Compass_18_N.svg)图标> **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
1. 选择表单资源并选择&#x200B;**[!UICONTROL 下载]**&#x200B;图标。
1. 在下载资产中，选择以下选项之一，然后选择&#x200B;**[!UICONTROL 下载]**。

   * **下载为CRX包：**&#x200B;使用选项从[!DNL AEM Forms]实例下载所有选定的资源和相关依赖项并将其移动到另一个实例。 它将所有资源和文件夹下载为crx包。 任何表单资源，包括在AEM(Adaptive Forms和自适应表单片段)、PDF文档和资源（XSD、XFS、图像）中创作的表单，都可以从[!DNL AEM Forms] UI中作为包下载。
将资源下载为包的优势在于，它还可以下载选定要下载的资源已使用的资源。 例如，如果您有一个自适应表单，该表单使用表单模板、XSD和图像。 当您选择此自适应表单并将其下载为包时，下载的包中还包含表单模板、XSD和图像。 与资源关联的所有元数据属性（包括自定义属性）也会下载。

   * **将资源下载为二进制文件：**使用选项仅下载表单模板(XDP)、PDF forms(PDF)、文档(PDF)和资源（图像、架构、样式表）。 您可以使用外部应用程序编辑这些资源。 它将具有二进制文件的表单资源(如XSD、XDP、图像、PDF和XDP)下载为.zip文件。
无法使用**[!UICONTROL 以二进制文件格式下载资源]**&#x200B;选项下载自适应Forms、自适应表单片段和主题。 要下载这些资源，您应该使用&#x200B;**[!UICONTROL 下载为CRX包]**&#x200B;选项。

   选定的资产将下载为存档（.zip文件）。

   >[!NOTE]
   >
   >AEM包和二进制文件都将作为存档（.zip文件）下载。 资产的模板不会与资产一起下载。 您需要单独导出资产模板。

### 上传资源 {#upload-forms-amp-documents-assets}

要上传Forms和文档资源，请执行以下操作：

1. 登录到[!DNL AEM Forms]实例。
1. 选择Experience Manager![adobeexperiencemanager](assets/adobeexperiencemanager.png)图标>导航![compass](assets/Smock_Compass_18_N.svg)图标> **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
1. 选择&#x200B;**创建** >**文件上传**。 此时会显示上传表单或资源包对话框。
1. 在对话框中，浏览并选择要导入的软件包或存档。 您还可以选择PDF文档、XSD、图像、样式表和XDP表单。 选择&#x200B;**[!UICONTROL 打开]**。 您选择的文件夹或文件名不得包含任何特殊字符。

   在该对话框中，验证要上传的资源的详细信息，然后选择&#x200B;**[!UICONTROL 上传]**。

   如果上传现有的表单资源，则会更新该资源。

   >[!NOTE]
   >
   >上传包不会替换现有文件夹层次结构。 例如，如果一台服务器上位于/content/dam/formsanddocuments的位置有一个名为“Training”的自适应表单。 您下载自适应表单并将表单上传到其他服务器。 第二台服务器还在同一位置/content/dam/formsanddocuments具有一个名为“Training”的文件夹。 上传失败。

## 下载或上传主题 {#downloading-or-uploading-a-theme}

通过[!DNL AEM Forms]，您可以创建、下载或上传主题。 创建主题的方式与创建表单、文档和信件等其他资产类似。 您可以创建主题，下载主题，然后将其上传到单独的实例上以重复使用。 有关主题的更多信息，请参阅[!DNL AEM Forms]中的[主题](themes.md)。

### 下载主题 {#downloading-a-theme}

您可以导出[!DNL AEM Forms]中在其他项目或实例中使用的主题。 AEM允许您将主题下载为zip文件，并可在实例上上上传。

要下载主题，请执行以下操作：

1. 登录到[!DNL AEM Forms]实例。
1. 选择Experience Manager![adobeexperiencemanager](assets/adobeexperiencemanager.png)图标>导航![compass](assets/Smock_Compass_18_N.svg)图标> **[!UICONTROL Forms]** > **[!UICONTROL 主题]**。
1. 选择主题，然后选择&#x200B;**[!UICONTROL 下载]**。 主题将下载为存档（.zip文件）。

### 上传主题 {#uploading-a-theme}

您可以在项目中将创建的主题与样式预设一起使用。 您可以通过将其他人创建的主题包上传到您的项目来导入这些主题包。

要上传主题，请执行以下操作：

1. 在Experience Manager中，导航到&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms主题]**。
1. 在“主题”页面中，单击&#x200B;**[!UICONTROL Forms创建]** > **[!UICONTROL Forms文件上传]**。
1. 在“文件上传”提示下，浏览并选择计算机上的主题包，然后单击&#x200B;**[!UICONTROL Forms上传]**。 主题已上传。

<!--

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

### Import Document Fragments, Letters and/or Data Dictionaries into Correspondence Management {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

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
   >For you to be able to upload XDPs (as part of the cmp file or otherwise), you need to be a part of forms-power-users group. For access rights, contact the administrator.
-->

## 导出工作流应用程序 {#export-a-workflow-application}

您可以使用AEM包管理器导出工作流应用程序。 此过程如下所示：

1. 打开[!DNL AEM Forms]包管理器。
1. 单击&#x200B;**[!UICONTROL 创建包]**。 出现&#x200B;**[!UICONTROL 新包]**&#x200B;对话框。
1. 指定包的名称、版本和组。 单击&#x200B;**[!UICONTROL 确定]**。
1. 单击&#x200B;**[!UICONTROL 编辑]**&#x200B;并打开&#x200B;**[!UICONTROL 筛选器]**&#x200B;选项卡。 单击&#x200B;**[!UICONTROL 添加筛选器]**。 指定工作流应用程序的路径。 例如，/etc/fd/dashboard/startpoints/homemortgage。 单击&#x200B;**[!UICONTROL 添加规则]**。

1. 打开&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡。 在ACL处理字段中选择&#x200B;**[!UICONTROL 合并]**&#x200B;或&#x200B;**[!UICONTROL 覆盖]**。 单击&#x200B;**[!UICONTROL 保存]**。
1. 单击&#x200B;**[!UICONTROL 生成]**&#x200B;以创建包。

   生成包后，您可以下载包并将其导入其他服务器。 工作流应用程序会出现在上传包的服务器上。

   >[!NOTE]
   >
   >为使工作流应用程序正常工作，还应将相应的自适应表单和工作流模型导出到工作应用程序。

## 文件夹和组织资源 {#folders-and-organizing-assets}

[!DNL AEM Forms]用户界面使用文件夹排列资源。 这些文件夹用于排列在[!DNL AEM Forms]用户界面中创建的资源。 您可以重命名、创建子文件夹并将资源和文档存储在这些文件夹中。 在文件夹中组织文档和资产，可让您将文件分组在一起以便于管理。 您可以选择文件夹，然后选择下载或删除该文件夹。

要创建文件夹，请完成以下步骤：

### 创建文件夹 {#create-a-folder}

1. 登录到`https://<server>:<port>/aem/forms.html`上的[!DNL AEM Forms]用户界面。
1. 导航到要创建文件夹的位置。
1. 选择&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 文件夹]**。
1. 输入以下详细信息：

   * **标题：**&#x200B;文件夹的显示名称
   * **名称：** *（必需）*&#x200B;要将文件夹存储在存储库中的节点名称

   >[!NOTE]
   >
   >默认情况下，“名称”字段的值会自动从标题中填充。 名称只能包含字母数字字符，或连字符(-)和下划线(_)特殊字符。 在标题中输入的任何其他特殊字符都会自动替换为连字符，并提示您确认新名称。 您可以选择使用建议的名称继续操作或进一步编辑它。

1. 具有您定义的标题的新文件夹将显示在资产列表中的当前位置。

   如果存在具有指定名称的文件夹，则提交会失败并出现错误。 您可以将鼠标悬停在名称字段旁边显示的错误![aem6forms_error_alert](assets/Smock_Alert_18_N.svg)图标上，以查看错误消息。

   您可以选择创建的文件夹，以进入该文件夹，并在该文件夹中创建资源或文件夹。 此外，您还可以选择一个文件夹，并选择将该文件夹排入下载队列、删除或编辑其名称。

<!-- ### Create copies of one or more assets or letters {#create-copies-of-one-or-more-assets-or-letters}

You can use an existing assets and letters to quickly create a assets and letters with similar properties, content, and inherited assets. You can copy and paste data dictionaries, document fragments, and letters.

Complete the following steps to create copies of assets and letters:

1. In the relevant Assets or Letters page, select one or more assets/letters. The UI displays the Copy icon.
1. Select Copy. The UI displays the Paste icon. You can also choose to go/navigate inside a folder before you paste. Different folders can contain assets with same names. For more information on folders, see [Folders and organizing assets](#folders-and-organizing-assets).
1. Select Paste. The Paste dialog appears. The system auto generates names and titles to the new copies of assets/letters, but you can edit the titles and names of the assets/letters.

   If you are copying and pasting the assets/letters at the same place, a suffix "-CopyXX" gets added to the existing name of the asset/letter. If no title existed for the copied asset/letter, the auto generated title field remains blank.

1. If necessary, edit the Title and Name with which you want to save the copy of the asset/letter.
1. Select Paste. New copies of the copied assets are created.

## Search {#search-forms}

[!DNL AEM Forms] UI lets you search your content. Using the top bar, you can select Search **[A]** to search your content for resources such as assets and documents.

When you search for assets, [!DNL AEM Forms] displays the side panel. You can also select ![assets-browser-content-only](assets/assets-browser-content-only.png) &gt; Filter **[B]** to invoke the side panel. Using the various filters in the side panel, you can narrow down your search. The side panel also lets you save your searches.

![search_topbar](assets/search_topbar.png)

**A.** Search **B.** Filter

![Side panel - Filters](assets/search_sidepanel.png)

Side panel - Filters

On the side panel, you can use the following to narrow down your search results:

* Search Directory
* Tags
* Search Criteria; for example, Modified Dates, Publish Status, LiveCopy Status.

The side panel also lets you save your search settings with names of your choice.

For more information and instructions on using search, filters, saved search, and side panel, see [Search](/help/sites-authoring/search.md).

-->

>[!MORELIKETHIS]
>
>* [导入导出表单模板](/help/forms/import-export-forms-templates.md)
>* [在自适应表单核心组件中使用主题](/help/forms/using-themes-in-core-components.md)