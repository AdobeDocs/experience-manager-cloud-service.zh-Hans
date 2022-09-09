---
title: 导入和导出资产
seo-title: Import and export assets to [!DNL AEM Forms]
description: 您可以将自适应Forms和相关资产导入和导出到AEM实例。 这有助于迁移表单或跨系统移动表单。
seo-description: You can import and export Adaptive Forms and templates from and in to AEM instances. This helps in migrating forms or moving them across systems.
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1325'
ht-degree: 1%

---


# 导入和导出资产 {#importing-and-exporting-assets-to-aem-forms}

您可以在不同的资产之间移动表单、主题、模板、文档片段、主题和其他资产 [!DNL AEM Forms] 实例。 在将系统迁移或表单从开发或暂存服务器移动到生产服务器时，需要进行此类移动。

对于通过上传和导入的资产 [!DNL AEM Forms] 支持UI，建议导出或导入Forms UI。 不建议使用AEM包管理器导出或导入此类资产。

## 下载或上传Forms和文档资产 {#download-or-upload-forms-amp-documents-assets}

[!DNL AEM Forms] 用户界面允许您通过将资产下载为AEM CRX包或二进制文件，从AEM实例导出资产。 然后，您可以将下载的AEM CRX包或二进制文件导入另一个AEM实例。

通过导出和导入 [!DNL AEM Forms] 除自适应表单模板和自适应表单内容策略外，所有资产均支持用户界面。 因此，在从 [!DNL AEM Forms] 与其他相关资产一样，UI、相关的自适应表单模板和内容策略不会自动导出。

对于这些资产类型，您必须使用AEM Package Manager在源AEM服务器上创建CRX包，并将该包安装到目标服务器上。 有关创建和安装包的信息，请参阅 [部署到AEMas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html).

### 下载Forms和文档资产 {#download-forms-amp-documents-assets}

要下载Forms和文档资产，请执行以下操作：

1. 登录到 [!DNL AEM Forms] 实例。
1. 点按Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 图标>导航 ![指南](assets/Smock_Compass_18_N.svg) 图标> **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.
1. 选择表单资产，然后点按 **[!UICONTROL 下载]** 图标。
1. 在下载资产中，选择以下选项之一，然后点按 **[!UICONTROL 下载]**.

   * **下载为CRX包：** 使用选项可从 [!DNL AEM Forms] 实例到其他实例。 它会将所有资产和文件夹下载为crx包。 任何表单资产(包括在AEM(自适应Forms和自适应表单片段)中创作的表单)、PDF文档和资源（XSD、XFS、图像）均可从以下位置以包形式下载 [!DNL AEM Forms] UI。
将资产下载为包的好处是，它还会下载选定要下载的资产所使用的资产。 例如，如果您的自适应表单使用表单模板、XSD和图像。 当您选择此自适应表单并将其下载为包时，下载的包中还包含表单模板、XSD和图像。 与资产关联的所有元数据属性（包括自定义属性）也会下载。

   * **将资产下载为二进制文件：** 使用选项可仅下载表单模板(XDP)、PDF forms(PDF)、文档(PDF)和资源（图像、架构、样式表）。 您可以使用外部应用程序编辑这些资产。 它将下载包含二进制文件的表单资产(如XSD、XDP、图像、PDF和XDP)，作为.zip文件。
您无法下载自适应Forms、自适应表单片段和主题， **[!UICONTROL 将资产下载为二进制文件]** 选项。 要下载这些资产，您应使用 **[!UICONTROL 下载为CRX包]** 选项。

   选定资产将作为存档文件（.zip文件）下载。

   >[!NOTE]
   >
   >AEM包和二进制文件均下载为存档文件（.zip文件）。 不会随资产一起下载资产的模板。 您需要单独导出资产模板。

### 上传资产 {#upload-forms-amp-documents-assets}

要上传Forms和文档资产，请执行以下操作：

1. 登录到 [!DNL AEM Forms] 实例。
1. 点按Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 图标>导航 ![指南](assets/Smock_Compass_18_N.svg) 图标> **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.
1. 点按 **创建** >**文件上传**. 将显示上载表单或包对话框。
1. 在对话框中，浏览并选择要导入的包或存档。 您还可以选择PDF文档、XSD、图像、样式表和XDP表单。 点按 **[!UICONTROL 打开]**. 您选择的文件夹或文件名不得包含任何特殊字符。

   在对话框中，验证所上传资产的详细信息，然后点按 **[!UICONTROL 上传]**.

   如果您上传现有的表单资产，则资产会进行更新。

   >[!NOTE]
   >
   >上传资源包不会替换现有文件夹层次结构。 例如，如果您有一个名为“培训”的自适应表单，该表单位于一个服务器上的/content/dam/formsanddocuments位置。 您下载自适应表单，然后将表单上传到其他服务器。 第二台服务器在同一位置/content/dam/formsanddocuments还有一个名为“Training”的文件夹。 上传失败。

## 下载或上传主题 {#downloading-or-uploading-a-theme}

使用 [!DNL AEM Forms]，则可以创建、下载或上传主题。 与其他资产（如表单、文档和信件）一样，创建主题。 您可以创建主题、下载它，然后将其上传到单独的实例以重复使用。 有关主题的更多信息，请参阅 [主题](themes.md) in [!DNL AEM Forms].

### 下载主题 {#downloading-a-theme}

您可以在 [!DNL AEM Forms] 在其他项目或实例中使用的ID、ID和ID。 AEM允许您以zip文件的形式下载主题，您可以在实例上传该主题。

要下载主题，请执行以下操作：

1. 登录到 [!DNL AEM Forms] 实例。
1. 点按Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 图标>导航 ![指南](assets/Smock_Compass_18_N.svg) 图标> **[!UICONTROL Forms]** > **[!UICONTROL 主题]**.
1. 选择主题并点按 **[!UICONTROL 下载]**. 主题将下载为存档文件（.zip文件）。

### 上传主题 {#uploading-a-theme}

您可以在项目中将创建的主题与样式预设结合使用。 您可以通过在您的项目上上传他人创建的主题包来导入这些主题包。

要上传主题，请执行以下操作：

1. 在Experience Manager中，导航到 **[!UICONTROL Forms]** > **[!UICONTROL Forms主题]**.
1. 在“主题”页面中，单击 **[!UICONTROL Forms创建]** > **[!UICONTROL Forms文件上传]**.
1. 在“文件上载”提示中，浏览并选择您计算机上的主题包，然后单击 **[!UICONTROL Forms上传]**. 主题已上传。

<!--

## Import and export assets in Correspondence Management {#import-and-export-assets-in-correspondence-management}

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

### Import Document Fragments, Letters and/or Data Dictionaries into Correspondence Management {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

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
   >For you to be able to upload XDPs (as part of the cmp file or otherwise), you need to be a part of forms-power-users group. For access rights, contact the administrator.
-->

## 导出工作流应用程序 {#export-a-workflow-application}

您可以使用AEM包管理器导出工作流应用程序。 程序如下：

1. 打开 [!DNL AEM Forms] 包管理器。
1. 单击 **[!UICONTROL 创建资源包]**. 的 **[!UICONTROL 新包]** 对话框。
1. 指定包的名称、版本和组。 单击&#x200B;**[!UICONTROL 确定]**。
1. 单击 **[!UICONTROL 编辑]** 打开 **[!UICONTROL 过滤器]** 选项卡。 单击 **[!UICONTROL 添加过滤器]**. 指定工作流应用程序的路径。 例如， /etc/fd/dashboard/startpoints/homemortgage。 单击 **[!UICONTROL 添加规则]**.

1. 打开&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡。选择 **[!UICONTROL 合并]** 或 **[!UICONTROL 覆盖]** 在ACL处理字段中。 单击“**[!UICONTROL 保存]**”。
1. 单击 **[!UICONTROL 生成]** 创建资源包。

   生成包后，您可以下载该包并将其导入到其他服务器。 工作流应用程序将显示在上传包的服务器上。

   >[!NOTE]
   >
   >为了使工作流应用程序正常工作，还将相应的自适应表单和工作流模型与工作应用程序一起导出。

## 文件夹和组织资产 {#folders-and-organizing-assets}

[!DNL AEM Forms] 用户界面使用文件夹来排列资产。 这些文件夹用于排列在 [!DNL AEM Forms] 用户界面。 您可以重命名子文件夹，并存储这些文件夹中的资产和文档。 通过在文件夹中组织文档和资产，可以将文件分组在一起，以便轻松管理。 您可以选择文件夹并选择下载或删除它。

要创建文件夹，请完成以下步骤：

### 创建文件夹 {#create-a-folder}

1. 登录到 [!DNL AEM Forms] 用户界面位于 `https://<server>:<port>/aem/forms.html`.
1. 导航到要创建文件夹的位置。
1. 点按 **[!UICONTROL 创建]** > **[!UICONTROL 文件夹]**.
1. 输入以下详细信息：

   * **标题：** 文件夹的显示名称
   * **名称：** *（必需）* 要在存储库中存储文件夹的节点名称

   >[!NOTE]
   >
   >默认情况下，会从标题中自动填充name字段的值。 名称只能包含字母数字字符，或连字符(-)和下划线(_)特殊字符。 在标题中输入的任何其他特殊字符会自动替换为连字符，系统会提示您确认新名称。 您可以选择继续使用建议的名称，也可以进一步对其进行编辑。

1. 资产列表中的当前位置将显示一个新文件夹，其中包含您定义的标题。

   如果存在具有指定名称的文件夹，则提交会失败，并出现错误。 您可以通过将鼠标悬停在错误上来查看错误消息 ![aem6forms_error_alert](assets/Smock_Alert_18_N.svg) 图标。

   您可以点按新创建的文件夹，以转到文件夹内，并在文件夹中创建资产或文件夹。 此外，您还可以选择文件夹并选择将其排入队列进行下载、删除或编辑其名称。

<!-- ### Create copies of one or more assets or letters {#create-copies-of-one-or-more-assets-or-letters}

You can use an existing assets and letters to quickly create a assets and letters with similar properties, content, and inherited assets. You can copy and paste data dictionaries, document fragments, and letters.

Complete the following steps to create copies of assets and letters:

1. In the relevant Assets or Letters page, select one or more assets/letters. The UI displays the Copy icon.
1. Tap Copy. The UI displays the Paste icon. You can also choose to go/navigate inside a folder before you paste. Different folders can contain assets with same names. For more information on folders, see [Folders and organizing assets](#folders-and-organizing-assets).
1. Tap Paste. The Paste dialog appears. The system auto generates names and titles to the new copies of assets/letters, but you can edit the titles and names of the assets/letters.

   If you are copying and pasting the assets/letters at the same place, a suffix "-CopyXX" gets added to the existing name of the asset/letter. If no title existed for the copied asset/letter, the auto generated title field remains blank.

1. If required, edit the Title and Name with which you want to save the copy of the asset/letter.
1. Tap Paste. New copies of the copied assets are created.

## Search {#search-forms}

[!DNL AEM Forms] UI allows you to search your content. Using the top bar, you can tap Search **[A]** to search your content for resources such as assets and documents.

When you search for assets, [!DNL AEM Forms] displays the side panel. You can also tap ![assets-browser-content-only](assets/assets-browser-content-only.png) &gt; Filter **[B]** to invoke the side panel. Using the various filters in the side panel, you can narrow down your search. The side panel also allows you to save your searches.

![search_topbar](assets/search_topbar.png)

**A.** Search **B.** Filter

![Side panel - Filters](assets/search_sidepanel.png)

Side panel - Filters

On the side panel, you can use the following to narrow down your search results:

* Search Directory
* Tags
* Search Criteria; for example, Modified Dates, Publish Status, LiveCopy Status.

The side panel also allows you to save your search settings with names of your choice.

For more information and instructions on using search, filters, saved search, and side panel, see [Search](/help/sites-authoring/search.md).

-->
