---
title: 创建和管理多语言的数字资产并运行翻译工作流程
description: 了解如何自动化将资产（包括二进制文件、元数据和标记）翻译为多种语言的工作流程。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# 多语言资源 {#multilingual-assets}

多语言资源是指具有多语言二进制文件、元数据和标记的资源。 通常，资产的二进制文件、元数据和标记以一种语言存在，然后将它们翻译为其他语言，以便在多语言项目中使用。 Adobe Experience Manager(AEM)资产可让您自动处理资产（包括二进制文件、元数据和标记）的翻译工作流程，以生成其他语言的资产，以便在多语言项目中使用。

要实现翻译工作流程的自动化，您可以将翻译服务提供商与AEM集成，并创建将资产翻译为多种语言的项目。 AEM支持人工和机器翻译工作流程。

人文翻译：转换后的资产将返回并导入到AEM中。 将翻译提供商与AEM集成后，资产会在AEM和翻译提供商之间自动发送。

机器翻译：机器翻译服务会立即翻译资产的元数据和标记。

<!--
We have multiple articles around translation of assets. For now, dumping all content in this article to remove others and create only 1 master article.

https://docs.adobe.com/content/help/en/experience-manager-65/assets/managing/translation-projects.html
https://docs.adobe.com/content/help/en/experience-manager-65/assets/managing/preparing-assets-for-translation.html
[Apply translation cloud services to folders](https://docs.adobe.com/content/help/en/experience-manager-65/assets/managing/transition-cloud-services.html)

One of these articles is a copy of [Preparing Content for Translation](https://docs.adobe.com/content/help/en/experience-manager-65/administering/introduction/tc-prep.html

-->

<!-- 
Translating assets includes the following:

1. [Connecting AEM with the translation service provider](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [Creating translation integration framework configurations](/help/sites-administering/tc-tic.md)
1. [Preparing assets for translation](prepare-assets-for-translation.md)
1. [Applying translation cloud services to folders](transition-cloud-services.md)
1. [Create translation projects](translation-projects.md)

If your translation service provider does not provide a connector to integrate with AEM, use an [alternative process](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

Also see, [Creating translation projects for content fragments](creating-translation-projects-for-content-fragments.md).

-->

## 准备要翻译的资产 {#prepare-assets-for-translation}

多语言资源是指具有多语言二进制文件、元数据和标记的资源。 通常，资产的二进制文件、元数据和标记以一种语言存在，然后将它们翻译为其他语言，以便在多语言项目中使用。

在Adobe Experience Manager(AEM)资产中，多语言资产包含在文件夹中，其中每个文件夹都包含不同语言的资产。

每个语言文件夹都称为语言副本。 语言副本的根文件夹（称为语言根）标识语言副本中内容的语言。 例如， `/content/dam/it` 意大利语副本的意大利语根。 语言副本必须使用 [正确配置的语言根目录](#create-a-language-root) ，以便在执行源资产翻译时瞄准正确的语言。

您最初为其添加资产的语言副本是语言母版。 语言母版是翻译成其他语言的源。 示例文件夹层次结构包括多个语言根：

```
/content
&nbsp; &nbsp; /- dam
&nbsp; &nbsp; &nbsp; |- en
&nbsp; &nbsp; &nbsp; |- fr
&nbsp; &nbsp; &nbsp; |- de
&nbsp; &nbsp; &nbsp; |- es
&nbsp; &nbsp; &nbsp; |- it
&nbsp; &nbsp; &nbsp; |- ja
&nbsp; &nbsp; &nbsp; |- zh
```

执行以下步骤以准备要翻译的资产：

1. 创建语言母版的语言根。 例如，示例文件夹层次结构中英语副本的语言根目录为 */content/dam/en*。 确保根据创建语言根中的信息正确配置 [了语言根](#create-a-language-root)。

1. 将资源添加到您的语言母版。
1. 创建您需要语言副本的每个目标语言的语言根。

### 创建语言根 {#create-a-language-root}

要创建语言根目录，请创建一个文件夹，并使用ISO语言代码作为“名称”属性的值。 创建语言根目录后，可以在语言根目录的任何级别创建语言副本。

例如，示例层次结构的意大利语语言副本的根页面 `it` 作为“名称”属性。 名称属性将用作存储库中资产节点的名称，因此会确定资产的路径。 (*&lt;server>:&lt;port>/assets.html/content/dam/it/*)

1. 在资产控制台中，单击／点按创 **[!UICONTROL 建]** ，然后从 **[!UICONTROL 菜单中选]** 择文件夹。
1. 在“名称”字段中，键入国家／地区代码，格式为 `<language-code>`。
1. 单击或点按&#x200B;**[!UICONTROL 创建]**。将在“资产”控制台中创建语言根目录。

### 查看语言根 {#view-language-roots}

触屏优化UI提供了一个“引用”面板，其中显示在AEM资产中创建的语言根列表。

1. 在“资产”控制台中，选择要为其创建语言副本的语言母版。
1. 单击或点按GlobalNav图标，然后选择“ **[!UICONTROL 引用]** ”以打开“引用”窗格。
1. 在“引用”窗格中，单击或点按 **[!UICONTROL 语言副本]**。 “语言副本”面板显示资产的语言副本。

### 创建新翻译项目 {#create-a-new-translation-project}

如果您使用此选项，则要翻译的资产将复制到您要翻译的语言的语言的语言根目录中。 根据您选择的选项，系统会在“项目”控制台中为资产创建一个翻译项目。 根据设置，可以手动启动翻译项目，或在创建翻译项目后自动运行。

1. 在资产UI中，选择要为其创建语言副本的源文件夹。
1. 打开“ **[!UICONTROL 引用]** ”窗格，然后单击／点按“副本” **[!UICONTROL 下的“语言副本]** ” ****。
1. 单击／点按 **[!UICONTROL 底部的创建]** 和翻译。
1. 从“目 **[!UICONTROL 标语言]** ”列表中，选择要为其创建文件夹结构的语言。
1. 从“项 **[!UICONTROL 目]** ”列表中，选 **[!UICONTROL 择“创建新翻译项目”]**。
1. 在“项 **[!UICONTROL 目标题]** ”字段中，输入项目标题。
1. 单击／点按创 **[!UICONTROL 建]**。 源文件夹中的资产将复制到您在步骤4中选择的区域设置的目标文件夹。
1. 要导航到文件夹，请选择语言副本，然后单击“在资 **[!UICONTROL 产中显示”]**。
1. 导航到项目控制台。 翻译文件夹会被复制到项目控制台。
1. 打开文件夹以查看翻译项目。
1. 单击／点按项目以打开详细信息页面。
1. 要查看翻译作业的状态，请单击“翻译作业”拼贴底部的省略 **[!UICONTROL 号]** 。 <!-- For more details around job statuses, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job). -->
1. 在“资产”用户界面中，打开每个已翻译资产的“属性”页面以查看已翻译的元数据。

>[!NOTE]
>
>此功能适用于资产和文件夹。 选择资产而不是文件夹后，系统会复制文件夹的整个层次结构（直至语言根目录），为资产创建语言副本。

### Add to an existing translation project {#add-to-existing-translation-project}

如果您使用此选项，则在运行以前的翻译工作流之后，将为添加到源文件夹的资产运行翻译工作流。 只有新添加的资产才会复制到包含先前已翻译资产的目标文件夹中。 在这种情况下，不会创建新的翻译项目。

1. 在资产UI中，导航到包含未翻译资产的源文件夹。
1. 选择要翻译的资产，然后打开“引用” **[!UICONTROL 窗格]**。 “语 **[!UICONTROL 言副本]** ”部分显示当前可用的翻译副本数。
1. 单击／点按副 **[!UICONTROL 本下的语言副]****[!UICONTROL 本]**。 此时将显示可用翻译副本列表。
1. 单击／点按 **[!UICONTROL 底部的创建]** 和翻译。
1. 从“目 **[!UICONTROL 标语言]** ”列表中，选择要为其创建文件夹结构的语言。
1. 从“项 **[!UICONTROL 目]** ”列表中，选择 **[!UICONTROL 添加到现有翻译项目]** ，以在文件夹上运行翻译工作流。
   >[!NOTE]
   >
   >如果选择“ **[!UICONTROL 添加到现有翻译项目”选项]** ，则只有在项目设置与现有项目的设置完全匹配时，翻译项目才会添加到预先存在的项目。 否则，将创建新项目。
1. 从“现 **[!UICONTROL 有翻译项目]** ”列表中，选择要添加要翻译的资产的项目。
1. Click/tap **[!UICONTROL Create]**. 要翻译的资产将添加到目标文件夹。 更新的文件夹列在“语言副 **[!UICONTROL 本”部分下]** 。
1. 导航到项目控制台，然后打开您添加到的现有翻译项目。
1. 单击／点按转换项目视图中的项目详细信息页面。
1. Click/tap the ellipsis at the bottom of the **Translation Job** tile to view the assets in the translation workflow. 转换作业列表还显示资产元数据和标记的条目。 这些条目指示资产的元数据和标记也会被翻译。

   >[!NOTE]
   >
   >* 如果删除标记或元数据的条目，则不会为任何资产转换标记或元数据。
   >* 如果使用机器翻译，则资产二进制文件不会翻译。
   >* 如果您添加到翻译作业的资产包含子资产，请选择子资产并删除这些子资产，以便翻译继续，而不会出现任何故障。


1. 要开始资产的转换，请单击／点按转换作业拼贴上的箭 **[!UICONTROL 头]** ，然后从列 **[!UICONTROL 表中选择开始]** 。 系统会显示一条消息，通知翻译作业的开始。
1. 要查看翻译作业的状态，请单击／点按翻译作业拼贴底部的省略 **[!UICONTROL 号]** 。 <!-- For more details, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job). -->
1. 翻译完成后，状态将变为“准备审阅”。 导航到资产UI，然后打开每个已翻译资产的“属性”页面以查看已翻译的元数据。

### 更新语言副本 {#update-language-copies}

运行此工作流以翻译任何其他资产集并将其包含在特定区域设置的语言副本中。 在这种情况下，已翻译的资产会添加到已包含先前已翻译资产的目标文件夹中。 根据选项的选择，系统会创建翻译项目或更新新资产的现有翻译项目。 更新语言副本工作流包含以下选项：

* 创建新翻译项目
* 添加到现有翻译项目

### 添加到现有翻译项目 {#add-to-existing-translation-project-1}

如果您使用此选项，则资产集会添加到现有翻译项目中，以更新您选择的区域设置的语言副本。

1. 从资产UI中，选择您添加资产文件夹的源文件夹。
1. 打开“ **[!UICONTROL 引用”窗格]**，单击／点按“副本”下 **[!UICONTROL 的“语言副本]** ”以 **** 显示语言副本列表。
1. 选中“语言副本”( **[!UICONTROL Language Copy]**)前面的复选框，该复选框将选择所有语言副本。 取消选择其他副本，但与您要翻译的区域设置对应的语言副本（副本）除外。
1. 单击／点按 **[!UICONTROL 底部的“更新语言副本]** ”。
1. 从“项 **[!UICONTROL 目]** ”列表中，选 **[!UICONTROL 择“添加到现有翻译项目”]**。
1. 从“现 **[!UICONTROL 有翻译项目]** ”列表中，选择要添加要翻译的资产的项目。
1. 单击／点按 **[!UICONTROL 开始]**。
1. 请参阅添加到现有翻译 [项目中的步骤](#add-to-existing-translation-project) 9-14以完成其余步骤。

### 创建临时语言副本 {#creating-temporary-language-copies}

运行翻译工作流以使用已编辑版本的原始资产更新语言副本时，将保留现有语言副本，直到您批准已翻译的资产。 AEM资产会将新翻译的资产存储在临时位置，并在您明确批准资产后更新现有语言副本。 如果您拒绝资产，则语言副本将保持不变。

1. 单击／点按您已为其创建语言副本的 **[!UICONTROL 语言副本下的源根文件夹]** ，然后单击／点按资产中的 **[!UICONTROL 显示]** ，以在AEM资产中打开该文件夹。
1. 在资产UI中，选择已翻译的资产，然后单击／点按工具栏中的编辑 **[!UICONTROL 图标]** ，以在编辑模式下打开资产。
1. 编辑资产，然后保存更改。
1. 执行添加到现有翻译项目 [过程的步骤](#add-to-existing-translation-project) 2-14以更新语言副本。
1. 单击／点按翻译作业拼贴底部的 **[!UICONTROL 省略号]** 。 从“翻译作业”页面的 **[!UICONTROL 资产列表中]** ，您可以清楚地查看存储资产翻译版本的临时位置。
1. 选中“标题”旁边的复 **[!UICONTROL 选框]**。
1. 在工具栏中，单击／点按 **[!UICONTROL 接受翻译]****** ，然后单击／点按对话框中的接受，以使用已编辑资产的已翻译版本覆盖目标文件夹中的已翻译资产。

   >[!NOTE]
   >
   >要启用翻译工作流来更新目标资产，请接受资产和元数据。

   单击／点按 **[!UICONTROL 拒绝翻译]** ，以在目标区域设置根目录中保留资产的最初翻译版本并拒绝编辑的版本。

1. 导航到资产控制台，然后打开每个已翻译资产的“属性”页面以查看已翻译的元数据。

有关有效翻译资产元数据的提示，请参 [阅有效翻译元数据的5个步骤](https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/)。

## 创建翻译项目 {#creating-translation-projects}

要创建语言副本，请触发资产UI中引用边栏下可用的以下语言副本工作流之一：

**创建和翻译**

在此工作流中，要翻译的资产会被复制到您要翻译的语言的语言的语言根目录中。 此外，根据您选择的选项，系统会在“项目”控制台中为资产创建一个转换项目。 根据设置，可以手动启动翻译项目，也可以允许翻译项目在创建后立即自动运行。

**更新语言副本**

您可以运行此工作流来翻译另一组资产，并将其包含在特定区域设置的语言副本中。 在这种情况下，已翻译的资产会添加到已包含先前已翻译资产的目标文件夹中。

>[!NOTE]
>
>仅当翻译服务提供商支持二进制的翻译时，资产二进制才被翻译。

>[!NOTE]
>
>如果您为复杂资产（如PDF文件和Adobe inDesign文件）启动了翻译工作流程，则不会提交其子资产或演绎版（如果有）进行翻译。

### 创建和翻译工作流 {#create-and-translate-workflow}

您首次使用创建和翻译工作流为特定语言生成语言副本。 该工作流提供以下选项：

* 只创建结构
* 创建新翻译项目
* 添加到现有翻译项目

### 只创建结构 {#create-structure-only}

使用“ **仅创建结构** ”选项可在目标语言根目录中创建目标文件夹层次结构，以匹配源语言根目录中源文件夹的层次结构。 在这种情况下，源资产会复制到目标文件夹。 但是，不会生成翻译项目。

1. 在资产UI中，选择要在目标语言根目录中创建其结构的源文件夹。
1. 打开“ **[!UICONTROL 引用]** ”窗格，然后单击／点按“副本” **[!UICONTROL 下的“语言副本]** ” ****。
1. 单击／点按 **[!UICONTROL 底部的创建]** 和翻译。
1. 从“目 **[!UICONTROL 标语言]** ”列表中，选择要为其创建文件夹结构的语言。
1. 从“项 **[!UICONTROL 目]** ”列表中，选择“ **[!UICONTROL 仅创建结构”]**。
1. Click/tap **[!UICONTROL Create]**. 目标语言的新结构列在“语言副本” **[!UICONTROL 下]**。
1. 单击／点按列表中的结构，然后单击／点按资产中 **[!UICONTROL 的显示]** ，以导航到目标语言中的文件夹结构。

## 将翻译云服务应用到文件夹 {#applying-translation-cloud-services-to-folders}

Adobe Experience Manager(AEM)允许您从您选择的翻译提供商那里获得基于云的翻译服务，以确保您的资产已根据您的要求进行翻译。

您可以将翻译云服务直接应用到您的资产文件夹，以便在翻译工作流程中使用这些服务。

### 应用翻译服务 {#applying-the-translation-services}

将翻译云服务直接应用到您的资产文件夹，无需在创建或更新翻译工作流程时配置翻译服务。

1. 从“资产”用户界面中，选择要将翻译服务应用到的文件夹。
1. 在工具栏中，单击／点按属 **[!UICONTROL 性图标]** ，以显示“文件 **[!UICONTROL 夹属性]** ”页面。

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. 导航到云服 **[!UICONTROL 务选项卡]** 。
1. 从云服务配置列表中，选择所需的翻译提供商。 例如，如果要使用Microsoft的翻译服务，请选择“ **[!UICONTROL Microsoft Translator”]**。

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. 为翻译提供者选择连接器。

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. 在工具栏中，单击／点 **[!UICONTROL 按保存]**，然后单击确定以关 **** 闭对话框。翻译服务将应用于文件夹。

### 应用自定义翻译连接器 {#applying-custom-translation-connector}

如果要为要在翻译工作流程中使用的翻译服务应用自定义连接器。 要应用自定义连接器，请首先从“包管理器”安装连接器。 然后，从云服务控制台配置连接器。 配置连接器后，该连接器会显示在应用转换服务中所述云服务选项卡的 [连接器列表中](#applying-the-translation-services)。 应用自定义连接器并运行翻译工作流后，翻译项目的“ **[!UICONTROL Translation]** Summary”（翻译摘要）拼贴会在heads **[!UICONTROL Provider]** and **[!UICONTROL Method（提供者和方法）下显示连接器详细信息]**。

1. 从包管理器安装连接器。
1. 单击／点按AEM徽标，然后导航到工 **[!UICONTROL 具>部署>云服务]**。
1. 在“云服务”页面的“ **[!UICONTROL 第三方服务]** ”下找 **[!UICONTROL 到您安装的连接器]** 。

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. 单击／点按 **[!UICONTROL 立即配置]** ，打开创建配 **[!UICONTROL 置对话框]** 。

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. 指定连接器的标题和名称，然后单击／点按创 **[!UICONTROL 建]**。 自定义连接器位于应用翻译服务步骤5中所述的 **[!UICONTROL 云服务]** ，该连接器列 [表中](#applying-the-translation-services)。
1. 在应用自定义连接器后，运行创建翻译项目中描述的任何翻译工作流。 在“项目”控制台中验证翻译项 **[!UICONTROL 目的“翻译摘要]** ”拼贴中连接器的 **[!UICONTROL 详细信息]** 。

   ![chlimage_1-220](assets/chlimage_1-220.png)
