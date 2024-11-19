---
title: 在 Content Hub 搜索资产
description: 了解如何在 [!DNL Content Hub]中搜索资源
role: User
exl-id: 8578d7d0-32b9-4e5c-80ef-3827e358ac6c
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# 在[!DNL Content Hub]中搜索Assets {#search-assets}

![共享资源横幅图像](assets/search.png)

>[!AVAILABILITY]
>
>Content Hub指南现在提供了PDF格式。 下载整个指南，并使用Adobe Acrobat AI Assistant来回答您的疑问。
>
>[!BADGE Content Hub指南PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

当存储库中有大量资源时，搜索合适的资源会非常耗时。 [!DNL The Content Hub]搜索使您能够查找已批准的资产，以便您可以对其执行其他操作，如下载、共享或创建收藏集。 您可以利用各种功能来缩小搜索结果的范围，例如，执行基于文本的搜索、使用过滤器、执行标记或智能标记特定的搜索、搜索特定的文件格式等。

## 先决条件 {#prerequisites}

[Content Hub用户](deploy-content-hub.md#onboard-content-hub-users)可以执行本文中提到的操作。

## 您可以搜索的内容  {#what-you-can-search}

[!DNL Content Hub]搜索提供的结果基于：

* **匹配文本：** [!DNL Content Hub]搜索允许您使用其名称或描述搜索资源。 您可以执行基于关键字的搜索，将关键字与资源属性中可用的文本进行比较。

* **匹配上下文：** [!DNL Content Hub]搜索结果列表包含您根据匹配上下文获得的资产的近似结果。 例如，如果您在搜索栏中键入`cool`，则与`winter`、`snow`、`cold surroundings`相关的资产将显示在搜索列表中。

* **资产信息（标题、标记或智能标记）：** [!DNL Content Hub]使用智能搜索算法尽可能准确地对搜索结果排名。 [元数据](#asset-properties.md)是某个资源的所有可用数据的集合，但它不一定包含在该资源中。 [它有助于您进一步对资源进行分类，在数字信息量增长时非常有用](/help/assets/configure-content-hub-ui-options.md##configure-metadata-search-content-hub)。

* **上次修改日期：**&#x200B;最近修改的资源显示在搜索结果列表的顶部。 您还可以根据要求筛选日期范围。

* **用法：**&#x200B;常用资源显示在搜索列表的顶部。

* **搜索历史记录：**&#x200B;单击搜索框而不键入字符即可获取搜索历史记录。 您还可以从历史记录中删除任何特定关键字。 搜索历史记录保存在Web浏览器的缓存中，这意味着如果您在其他浏览器中访问[!DNL Content Hub]搜索或清除浏览器的缓存内存，则无法再查看搜索历史记录。

* **键入时进行搜索：** [!DNL Content Hub]搜索可在您开始键入时提供自动完成建议，从而增强您的搜索体验。

## 基本搜索 {#basic-search}

要对[!DNL the Content Hub]执行基本搜索，请导航到搜索栏并指定您需要搜索的关键字。 导航到左窗格中可用的筛选器并应用它们以缩小搜索结果。

例如，搜索包含关键字`architect`的所有&#x200B;**[!UICONTROL JPEG]**&#x200B;图像，该关键字在去年内进行了修改。 要执行此方案，请执行以下步骤：

1. 指定`architect`作为搜索关键词。

1. 导航到筛选器面板> **[!UICONTROL 格式]** >选择&#x200B;**[!UICONTROL JPEG]**。

1. 导航到&#x200B;**[!UICONTROL 已修改]** >指定日期范围。

   ![基本搜索](assets/basic-search.png)

## 使用过滤器缩小搜索结果 {#narrow-down-search-results}

使用过滤器面板根据元数据搜索资源。 您可以根据各种搜索谓词筛选搜索结果。 您可以选择所有适当的谓词，以最小化或缩小搜索结果。 在筛选器中选择多个选项时，Content Hub会显示与筛选器中所选任何选项均匹配的资源。 但是，当您跨筛选器选择多个选项时，Content Hub仅显示与跨筛选器选择的所有选项匹配的资源，以缩小搜索结果的范围。

默认过滤器包括文件格式、批准者、批准日期、已过期和未过期的资源以及过期日期。 管理员还可以配置显示在过滤器列表中的过滤器。 有关详细信息，请参阅[配置Content Hub用户界面](configure-content-hub-ui-options.md#configure-filters-content-hub)。

<!--

<table>
    <tbody>
     <tr>
      <th><strong>Search Predicate</strong></th>
      <th><strong>Description</strong></th>
      <th><strong>Properties</strong></th>
     </tr>
     <tr>
      <td> Campaigns </td>
      <td> Allows you to search using planned activity performed to take any particular action. For example, advertisement campaign run on Ferrari to know the understand the interests of people using number of clicks people perform.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Channels </td>
      <td> Helps you to understand the path from where the asset is coming from. For example, web, social media, books, catalog, etc.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Region </td>
      <td> Helps you to understand the location where the asset is created. For example, Japan, EMEA, Worldwide, etc.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Keywords </td>
      <td> Keyword helps you search using terms or the words that you enter based on the topic. For example, images, low-resolution, etc.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Timeframe </td>
      <td> Helps you search assets using timeline. For example, search by year 2024, Q3 2023, etc.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td>File format</td>
      <td>Composition of an asset. The supported assets include image, document, video, printable media, and so on.</td>
      <td>
        <ul>
            <li>[!UICONTROL JPEG]</li> 
            <li>[!UICONTROL Quicktime]</li> 
            <li>[!UICONTROL PNG]</li> 
            <li>[!UICONTROL WebP]</li> 
            <li>[!UICONTROL MP4]</li> 
            <li>[!UICONTROL Plain]</li> 
            <li>[!UICONTROL PDF]</li>
            <li>[!UICONTROL SVG + XML]</li>
        </ul>
      </td>
     </tr>
     <tr>
      <td>Tags</td>
      <td>Tags help you categorize assets that can be browsed and searched more efficiently based on hierarchical taxonomies.</td>
      <td>
        <ul>
            <li>Field label</li>
            <li>Property name</li>
            <li>Path</li>
            <li>Description</li>
        </ul>
      </td>
     </tr>
     <!--<tr>
      <td>Subject</td>
      <td>Classification of assets based on their theme. For example, colorful, hiking, outdoors.</td>
      <td>NA</td>
     </tr>
          <tr>
      <td>Last modified</td>
      <td>Search assets based on their last modification. Specify the date range using the Start date and End date fields.</td>
      <td>
        <ul>
            <li>Range text (From)</li> 
            <li>Range text (To) </li>
        </ul>
      </td>
     </tr>    
     <!--<tr>
      <td>Asset ID</td>
      <td>Unique number that identifies the asset.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Colors </td>
      <td> Helps you search assets using colors that are automatically identified in an asset using Adobe's Sensei AI capabilities.</td>
      <td>NA</td>
     </tr>  
    </tbody>
   </table>

-->

## 执行更多搜索操作 {#do-more-with-search}

[!DNL The Content Hub]不限于搜索，而是允许您直接从搜索或预览界面执行其他操作，如[下载](download-assets-content-hub.md)、[共享](share-assets-content-hub.md)和[将资产添加到收藏集](collections-content-hub.md)。 选择搜索结果页面上的资源可查看这些选项。
