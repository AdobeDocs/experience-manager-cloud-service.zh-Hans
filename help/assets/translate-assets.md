---
title: 如何在AEM中翻译资产？
description: 了解如何自动执行工作流，将AEM中的资产（包括二进制文件、元数据和标记）翻译为多种语言。
contentOwner: AG
feature: Asset Management,Translation
role: Admin,User
exl-id: 98df1412-a957-48a3-81c2-7dfe1d5e6d31
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '2642'
ht-degree: 23%

---

# 在AEM中翻译资产 {#multilingual-assets}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/multilingual-assets.html?lang=en) |
| AEM as a Cloud Service | 本文 |

多语言资产是指包含多种语言的二进制文件、元数据和标记的资产。 通常，资产的二进制文件、元数据和标记以一种语言存在，然后将这些语言翻译成其他语言，以用于多语言项目。 Adobe Experience Manager Assets允许您自动执行工作流，以翻译资产（包括二进制文件、元数据和标记），从而生成其他语言的资产，以供在多语言项目中使用。

要自动翻译AEM资产，您需要将翻译服务提供商与Experience Manager集成，并创建项目以将资产翻译成多种语言。 Experience Manager支持人工和机器翻译工作流。

AEM中的人力资产翻译：翻译后的资产会被退回并导入Experience Manager。 将您的翻译提供商与Experience Manager集成后，Experience Manager与翻译提供商之间将自动发送资产。

AEM中的机器资产转换：机器翻译服务会立即翻译资产的元数据和标记。

<!--
We have multiple articles around translation of assets. For now, dumping all content in this article to remove others and create only ONE UBER article.

https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/translation-projects.html
https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/preparing-assets-for-translation.html
[Apply translation cloud services to folders](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/transition-cloud-services.html)

One of these articles is a copy of [Preparing Content for Translation](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/tc-prep.html

-->

<!-- 
Translating assets includes the following:

1. [Connecting Experience Manager with the translation service provider](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [Creating translation integration framework configurations](/help/sites-administering/tc-tic.md)
1. [Preparing assets for translation](prepare-assets-for-translation.md)
1. [Applying translation cloud services to folders](transition-cloud-services.md)
1. [Create translation projects](translation-projects.md)

If your translation service provider does not provide a connector to integrate with Experience Manager, use an [alternative process](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

Also see, [Creating translation projects for content fragments](creating-translation-projects-for-content-fragments.md).

-->

## 准备翻译资产 {#prepare-to-translate-assets}

多语言资产是指包含多种语言的二进制文件、元数据和标记的资产。 通常，资产的二进制文件、元数据和标记以一种语言存在，然后将这些语言翻译成其他语言，以用于多语言项目。

在Adobe Experience Manager Assets中，多语言资产包含在文件夹中，其中每个文件夹都包含使用不同语言的资产。

每个语言文件夹都称为语言副本。 语言副本的根文件夹（称为语言根）可标识语言副本中内容的语言。 例如， `/content/dam/it` 是意大利语副本的意大利语根。 语言副本必须使用 [正确配置的语言根](#create-a-language-root) 以便在执行源资产翻译时定位正确的语言。

最初为其添加资产的语言副本是主要语言。 语言主语是翻译成其他语言的源。 示例文件夹层次结构包括多个语言根：

```shell
/content
    /- dam
        |- en
        |- fr
        |- de
        |- es
        |- it
        |- ja
        |- zh
```

执行以下步骤以准备转换资产：

1. 创建语言主目录的语言根目录。 例如，示例文件夹层次结构中英语副本的语言根目录为 `/content/dam/en`. 确保根据 [创建语言根](#create-a-language-root).

1. 将资产添加到主语言。
1. 创建您需要语言副本的每种目标语言的语言根目录。

### 创建语言根 {#create-a-language-root}

要创建语言根目录，请创建一个文件夹并使用ISO语言代码作为Name属性的值。 创建语言根目录后，可以在语言根目录的任何级别创建语言副本。

例如，示例层次结构的意大利语语言副本的根页面具有 `it` 作为Name属性。 名称属性用作存储库中资产节点的名称，因此可确定资产的路径。 (*&lt;server>:&lt;port>/assets.html*)

1. 在资产控制台中，单击／点按创 **[!UICONTROL 建]** ，然后从 **[!UICONTROL 菜单中选]** 择文件夹。
1. 在“名称”字段中，以 `<language-code>`.
1. 单击或点按&#x200B;**[!UICONTROL 创建]**。语言根目录将在资产控制台中创建。

### 查看语言根 {#view-language-roots}

触屏优化UI提供了一个“引用”面板，其中显示了在中创建的语言根列表 [!DNL Assets].

1. 在资产控制台中，选择要为其创建语言副本的语言主要。
1. 单击或点按GlobalNav图标，然后选择 **[!UICONTROL 引用]** 打开“引用”窗格。
1. 在引用窗格中，单击或点按 **[!UICONTROL 语言副本]**. 语言副本面板会显示资产的语言副本。

### 创建新翻译项目 {#create-a-new-translation-project}

如果您使用此选项，则要翻译的资产将会复制到您要翻译的语言的语言根目录中。 根据您选择的选项，将在“项目”控制台中为资产创建一个翻译项目。 翻译项目可以手动启动，也可以在翻译项目创建后立即自动运行，具体取决于设置。

1. 在资产UI中，选择要为其创建语言副本的源文件夹。
1. 打开&#x200B;**[!UICONTROL 引用]**&#x200B;窗格，单击/点按&#x200B;**[!UICONTROL 副本]**&#x200B;下的&#x200B;**[!UICONTROL 语言副本]**。
1. 单击/点按 **[!UICONTROL 创建和翻译]** 在底部。
1. 从&#x200B;**[!UICONTROL 目标语言]**&#x200B;列表中，选择要为其创建文件夹结构的语言。
1. 从 **[!UICONTROL 项目]** 列表，选择 **[!UICONTROL 创建新的翻译项目]**.
1. 在&#x200B;**[!UICONTROL 项目标题]**&#x200B;字段中，输入项目标题。
1. 单击/点按 **[!UICONTROL 创建]**. 源文件夹中的资产会根据您在步骤4中选择的区域设置复制到目标文件夹。
1. 要导航到文件夹，请选择语言副本，然后单击 **[!UICONTROL 在资产中显示]**.
1. 导航到项目控制台。 翻译文件夹将会复制到项目控制台。
1. 打开文件夹以查看翻译项目。
1. 单击/点按项目以打开详细信息页面。
1. 要查看翻译作业的状态，请单击 **[!UICONTROL 翻译作业]** 拼贴。 <!-- For more details around job statuses, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job). -->
1. 在Assets用户界面中，打开每个已翻译资产的属性页面，以查看已翻译的元数据。

>[!NOTE]
>
>此功能适用于资产和文件夹。 选择资产而不是文件夹后，会复制直至语言根目录的整个文件夹层次结构，以为资产创建语言副本。

### 添加到现有翻译项目 {#add-to-existing-translation-project}

如果您使用此选项，则翻译工作流会为运行之前的翻译工作流后添加到源文件夹的资产运行。 只有新添加的资产才会复制到包含先前翻译过的资产的目标文件夹。 在这种情况下，不会创建新的翻译项目。

1. 在资产UI中，导航到包含未翻译资产的源文件夹。
1. 选择要翻译的资产，然后打开&#x200B;**[!UICONTROL “引用”窗格]**。**[!UICONTROL 语言副本]**&#x200B;部分显示当前可用的翻译副本数。
1. 单击/点按&#x200B;**[!UICONTROL 副本]**&#x200B;下的&#x200B;**[!UICONTROL 语言副本]**。此时将显示可用翻译副本列表。
1. 单击/点按 **[!UICONTROL 创建和翻译]** 在底部。
1. 从&#x200B;**[!UICONTROL 目标语言]**&#x200B;列表中，选择要为其创建文件夹结构的语言。
1. 从“项 **[!UICONTROL 目]** ”列表中，选择 **[!UICONTROL 添加到现有翻译项目]** ，以在文件夹上运行翻译工作流。
   >[!NOTE]
   >
   >如果您选择 **[!UICONTROL 添加到现有翻译项目]** 选项，则仅当项目设置与预先存在的项目的设置完全匹配时，翻译项目才会添加到预先存在的项目。 否则，将创建新项目。
1. 从 **[!UICONTROL 现有翻译项目]** 列表中，选择一个项目以添加要翻译的资产。
1. 单击/点按&#x200B;**[!UICONTROL 创建]**。要翻译的资产将添加到目标文件夹。更新的文件夹列在&#x200B;**[!UICONTROL 语言副本]**&#x200B;部分下。
1. 导航到项目控制台，然后打开您添加到的现有翻译项目。
1. 单击/点按翻译项目查看项目详细信息页面。
1. 单击/点按位于 **翻译作业** 拼贴，以在翻译工作流中查看资产。 翻译作业列表还会显示资产元数据和标记条目。这些条目指示资产的元数据和标记也会被翻译。

   >[!NOTE]
   >
   >* 如果删除标记或元数据的条目，则不会翻译任何资产的标记或元数据。
   >* 如果您使用机器翻译，则不会翻译资产二进制文件。
   >* 如果您添加到翻译作业的资产包含子资产，请选择子资产并将其删除，以便翻译继续，而不会出现任何问题。


1. 要开始翻译资产，请单击/点按 **[!UICONTROL 翻译作业]** 拼贴并选择 **[!UICONTROL 开始]** 列表。 消息会通知翻译作业的开始。
1. 要查看翻译作业的状态，请单击/点按 **[!UICONTROL 翻译作业]** 拼贴。 <!-- For more details, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job). -->
1. 翻译完成后，状态将变为“准备审阅”。 导航到资产UI，然后打开每个已翻译资产的属性页面，以查看已翻译的元数据。

### 更新语言副本 {#update-language-copies}

运行此工作流以翻译任何其他资产集，并将其包含在特定区域设置的语言副本中。 在这种情况下，已翻译的资产会添加到已包含先前已翻译资产的目标文件夹。 根据选项的选择，将创建翻译项目或为新资产更新现有翻译项目。 更新语言副本工作流包含以下选项：

* 创建新翻译项目
* 添加到现有翻译项目

### 添加到现有翻译项目 {#add-to-existing-translation-project-1}

如果您使用此选项，则会将资产集添加到现有翻译项目，以更新所选区域设置的语言副本。

1. 从资产UI中，选择您添加资产文件夹的源文件夹。
1. 打开&#x200B;**[!UICONTROL 引用]**&#x200B;窗格，单击/点按&#x200B;**[!UICONTROL 副本]**&#x200B;下的&#x200B;**[!UICONTROL 语言副本]**，以显示语言副本列表。
1. 选中&#x200B;**[!UICONTROL 语言副本]**&#x200B;前面的复选框，这将选择所有语言副本。除与您要翻译的区域设置对应的语言副本外，取消选择其他副本。
1. 单击/点按 **[!UICONTROL 更新语言副本]** 在底部。
1. 从 **[!UICONTROL 项目]** 列表，选择 **[!UICONTROL 添加到现有翻译项目]**.
1. 从 **[!UICONTROL 现有翻译项目]** 列表中，选择一个项目以添加要翻译的资产。
1. 单击／点按 **[!UICONTROL 开始]**。
1. 参见第9-14步 [添加到现有翻译项目](#add-to-existing-translation-project) 完成其余的程序。

### 创建临时语言副本 {#creating-temporary-language-copies}

当您运行翻译工作流以使用原始资产的编辑版本更新语言副本时，现有语言副本将保留，直到您批准已翻译的资产为止。 [!DNL Assets] 将新翻译的资产存储在临时位置，并在您明确批准资产后更新现有语言副本。 如果您拒绝资产，语言副本将保持不变。

1. 单击/点按下的源根文件夹 **[!UICONTROL 语言副本]** 您已为其创建语言副本，然后单击/点按 **[!UICONTROL 在资产中显示]** 要在中打开文件夹，请执行以下操作 [!DNL Assets].
1. 从资产UI中，选择已翻译的资产，然后单击/点按 **[!UICONTROL 编辑]** 图标以在编辑模式下打开资产。
1. 编辑资产，然后保存更改。
1. 执行 [添加到现有翻译项目](#add-to-existing-translation-project) 更新语言副本的过程。
1. 单击/点按位于 **[!UICONTROL 翻译作业]** 拼贴。 从 **[!UICONTROL 翻译作业]** 页面上，您可以清楚地查看存储资产翻译版本的临时位置。
1. 选中旁边的复选框 **[!UICONTROL 标题]**.
1. 在工具栏中，单击/点按&#x200B;**[!UICONTROL 接受翻译]**，然后单击/点按对话框中的&#x200B;**[!UICONTROL 接受]**，以使用已编辑资产的已翻译版本覆盖目标文件夹中的已翻译资产。

   >[!NOTE]
   >
   >要启用翻译工作流以更新目标资产，请接受资产和元数据。

   单击/点按 **[!UICONTROL 拒绝翻译]** 以在目标区域设置根目录中保留资产的最初翻译版本，并拒绝编辑的版本。

1. 导航到资产控制台，然后打开每个已翻译资产的属性页面，以查看已翻译的元数据。

<!-- TBD: Possibly this blog wasn't migrated. Still try to find from the author. Old one is archived at https://web.archive.org/web/20180423042713/https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/

For tips on translating metadata for assets efficiently, see [5 Steps to efficiently translate metadata](https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/). 
-->

## 创建翻译项目 {#creating-translation-projects}

要创建语言副本，请触发资产UI中引用边栏下可用的以下语言副本工作流之一：

**创建并翻译**

在此工作流中，要翻译的资产将会复制到您要翻译的语言的语言根目录中。 此外，根据您选择的选项，将在“项目”控制台中为资产创建一个翻译项目。 根据设置，可以手动启动翻译项目，也可以在翻译项目创建后立即自动运行翻译项目。

**更新语言副本**

您运行此工作流可翻译另一组资产，并将其包含在特定区域设置的语言副本中。 在这种情况下，已翻译的资产会添加到已包含先前已翻译资产的目标文件夹。

>[!NOTE]
>
>仅当翻译服务提供程序支持二进制文件的翻译时，才会翻译资产二进制文件。

>[!NOTE]
>
>如果您为复杂资产(如PDF文件和Adobe InDesign文件)启动翻译工作流，则不会提交其子资产或演绎版（如果有）以进行翻译。

### 创建和翻译工作流 {#create-and-translate-workflow}

您可以使用创建和翻译工作流首次为特定语言生成语言副本。 工作流提供了以下选项：

* 只创建结构
* 创建新翻译项目
* 添加到现有翻译项目

### 只创建结构 {#create-structure-only}

使用“ **仅创建结构** ”选项可在目标语言根目录中创建目标文件夹层次结构，以匹配源语言根目录中源文件夹的层次结构。 在这种情况下，源资产会复制到目标文件夹。 但是，不会生成翻译项目。

1. 在资产UI中，选择要在目标语言根目录中为其创建结构的源文件夹。
1. 打开&#x200B;**[!UICONTROL 引用]**&#x200B;窗格，单击/点按&#x200B;**[!UICONTROL 副本]**&#x200B;下的&#x200B;**[!UICONTROL 语言副本]**。
1. 单击/点按 **[!UICONTROL 创建和翻译]** 在底部。
1. 从 **[!UICONTROL 目标语言]** 列表中，选择要为其创建文件夹结构的语言。
1. 从&#x200B;**[!UICONTROL 项目]**&#x200B;列表中，选择&#x200B;**[!UICONTROL 仅创建结构]**。
1. 单击/点按&#x200B;**[!UICONTROL 创建]**。目标语言的新结构列在 **[!UICONTROL 语言副本]**.
1. 单击/点按列表中的结构，然后单击/点按 **[!UICONTROL 在资产中显示]** 导航到目标语言中的文件夹结构。

## 将翻译云服务应用到文件夹 {#applying-translation-cloud-services-to-folders}

Adobe Experience Manager允许您使用所选翻译提供商提供的基于云的翻译服务，以确保根据您的要求对资产进行翻译。

您可以将翻译云服务直接应用到您的资产文件夹，以便在翻译工作流程中使用这些服务。

### 应用翻译服务 {#applying-the-translation-services}

将翻译云服务直接应用到您的资产文件夹，无需在创建或更新翻译工作流时配置翻译服务。

1. 从Assets用户界面中，选择要将翻译服务应用到的文件夹。
1. 在工具栏中，单击/点按&#x200B;**[!UICONTROL 属性]**&#x200B;图标，以显示&#x200B;**[!UICONTROL 文件夹属性]**&#x200B;页面。

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. 导航到&#x200B;**[!UICONTROL 云服务]**&#x200B;选项卡。
1. 从Cloud Service配置列表中，选择所需的翻译提供程序。 例如，如果要从Microsoft获取翻译服务，请选择 **[!UICONTROL Microsoft Translator]**.

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. 为翻译提供程序选择连接器。

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. 在工具栏中，单击/点按&#x200B;**[!UICONTROL 保存]**，然后单击&#x200B;**[!UICONTROL 确定]**&#x200B;以关闭对话框。翻译服务将应用于文件夹。

### 应用自定义翻译连接器 {#applying-custom-translation-connector}

如果要为要在翻译工作流程中使用的翻译服务应用自定义连接器。要应用自定义连接器，请先从安装连接器 [包管理器。](/help/implementing/developing/tools/package-manager.md)然后，从云服务控制台配置连接器。配置连接器后，该连接器会显示在[应用翻译服务](#applying-the-translation-services)中所述的“云服务”选项卡的连接器列表中。应用自定义连接器并运行翻译工作流后，翻译项目的&#x200B;**[!UICONTROL 翻译摘要]**&#x200B;拼贴会在&#x200B;**[!UICONTROL 提供程序]**&#x200B;和&#x200B;**[!UICONTROL 方法]**&#x200B;标题下显示连接器详细信息。

1. 从安装连接器 [包管理器。](/help/implementing/developing/tools/package-manager.md)
1. 单击/点按Experience Manager徽标，然后导航到 **[!UICONTROL 工具>部署>Cloud Services]**.
1. 在&#x200B;**[!UICONTROL 云服务]**&#x200B;页面的&#x200B;**[!UICONTROL 第三方服务]**&#x200B;下找到安装的连接器。

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. 单击/点按 **[!UICONTROL 立即配置]** 用于打开的链接 **[!UICONTROL 创建配置]** 对话框。

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. 指定连接器的标题和名称，然后单击/点按&#x200B;**[!UICONTROL 创建]**。自定义连接器位于[应用翻译服务](#applying-the-translation-services)步骤 5 中所述的&#x200B;**[!UICONTROL 云服务]**&#x200B;选项卡的连接器列表中。
1. 在应用自定义连接器后，运行创建翻译项目中描述的任何翻译工作流。 在&#x200B;**[!UICONTROL 项目]**&#x200B;控制台中验证翻译项目的&#x200B;**[!UICONTROL 翻译摘要]**&#x200B;拼贴中连接器的详细信息。

   ![chlimage_1-220](assets/chlimage_1-220.png)

**另请参阅**

* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)
