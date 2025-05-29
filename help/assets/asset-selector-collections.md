---
title: 资产选择器收藏集
description: 使用资产选择器收藏集。
role: Admin,User
exl-id: 1687e7d5-eb7e-4eb7-8747-e5dc6afacd5b
source-git-commit: 08fc43bc8edeea91bfeb01f053d435e136658e7f
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 15%

---

# 资产选择器收藏集 {#asset-selector-collections}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime 和 Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets 与 Edge Delivery Services 集成</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 可扩展性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup><a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>启用 Dynamic Media Prime 和 Ultimate</b></a>
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

收藏集是Asset Selector中的一组资源、文件夹或其他收藏集。 使用收藏集可在用户之间共享资源。收藏集与文件夹的不同之处是可包含来自不同位置的资源。

资产选择器中的微型前端收藏集在只读模式下开箱即用。 它直接从您有权访问的[!DNL Experience Manager Assets]存储库获取资源和收藏集。

>[!NOTE]
>
>确保您有权访问[!DNL Experience Manager Assets] [imsOrg](/help/assets/asset-selector-properties.md)和收藏集。

资产选择器中的微型前端收藏集在只读模式下开箱即用。 它直接从您有权访问的Experience Manager Assets存储库获取资源和收藏集，并从您的Experience Manager Assets存储库继承公用文件夹和专用文件夹的属性。 查看有关[在Assets视图](/help/assets/manage-collections-assets-view.md#create-collection)中创建公共或私有收藏集的更多信息。

您可以在边栏视图和模式视图的资源选择器中查看收藏集。

边栏视图中的![收藏集](assets/collections-rail-modal-view.png)

<!--
Additionally, you can [customize](/help/assets/asset-selector-customization.md) the `featureSet` property to enable or disable collections in Asset Selector. See [enable or disable Collections tab](#enable-disable-collections-tab).-->

此外，您还可以自定义收藏集选项卡下的资源选择。 为此，您可以使用`handleSelection`对其进行自定义。 请参阅[使用对象架构](/help/assets/asset-selector-customization.md#handling-selection)处理对Assets的选择。

## 查看收藏集 {#view-collections}

资产选择器允许您在![列表视图](assets/do-not-localize/list-view.png)列表视图或![网格视图](assets/do-not-localize/grid-view.png)网格视图中查看集合。 查看资产选择器](overview-asset-selector.md#types-of-view)中的[视图类型。

## 将资产拖放到收藏集 {#collection-drag-and-drop}

您可以在创作环境中直接从[!DNL Assets as a Cloud Service]视图将资产拖放到收藏集。 为此，请将资源从Assets选项卡拖到Asset Selector应用程序的收藏集工作区，以构建丰富的应用程序。

>[!NOTE]
>
>* 只能在边栏视图中拖放资产。
>* 您只能拖放文件（资源），不能拖放文件夹。

另一方面，您还可以直接[启用或禁用收藏集](asset-selector-customization.md#enable-disable-drag-and-drop)中的拖放资产。

## 禁止选择收藏集中的资源 {#disable-selection-collection}

禁用选择用于隐藏或禁用资源或文件夹不可选择。 它会隐藏信息卡或资源中的选择复选框，以防被选择。 请参阅[禁用选择](/help/assets/asset-selector-customization.md#disable-selection)。

## 启用或禁用“收藏集”选项卡 {#enable-disable-collections-tab}

资产选择器允许您根据需求和可用性自定义组件。 要启用或禁用Asset Selector中的“收藏集”选项卡，您可以按以下方式使用`featureSet`属性：

* **启用“收藏集”选项卡：**&#x200B;要启用“收藏集”选项卡，需要提供`collections`作为数组的值。 默认情况下，会开箱即用地为所有用户启用“收藏集”选项卡。 例如，`featureSet:["collections"]`
* **禁用“收藏集”选项卡：**&#x200B;要禁用“收藏集”选项卡，需要提供一个空数组作为其值。 例如，`featureSet:[ ]`

>[!MORELIKETHIS]
>
>* [资产选择器自定义](/help/assets/asset-selector-customization.md)
>* [将资产选择器与各种应用程序集成](/help/assets/integrate-asset-selector.md)
>* [资产选择器属性](/help/assets/asset-selector-properties.md)
