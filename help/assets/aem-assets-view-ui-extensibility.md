---
title: 在 [!DNL AEM Assets View]中启用用户界面可扩展性
description: 了解 [!DNL AEM Assets View]. [!DNL AEM Assets View] UI的UI可扩展性功能，该功能允许添加自定义UI组件以满足特定业务需求。
feature: App Builder
role: User, Developer
exl-id: a11f7043-17cf-4331-b76c-d3db099c2411
source-git-commit: 2de6352363959f4258c0786910eaef7babe68f15
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 3%

---

# 在[!DNL AEM Assets View]中启用用户界面可扩展性 {#AEM-Assets-View-UI-Extensibility}

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
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新建</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>启用Dynamic Media Prime和Ultimate</b></a>
        </td>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜索最佳实践</b></a>
        </td>
    </tr>
    <tr>
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

[!DNL AEM Assets View]支持UI可扩展性，使您能够为[!DNL AEM Assets View]的开箱即用功能无法满足的特定工作流和业务要求将自定义UI组件添加到[!DNL Assets View] UI。 [!DNL AEM Assets View]的这个UI可扩展性功能增强了它的灵活性，使组织能够针对特定的工作流和要求调整界面。\
您可以将扩展添加到&#x200B;**Asset**、**Folder**&#x200B;和&#x200B;**Collection**&#x200B;级别。 添加的扩展显示在&#x200B;**Asset**、**Collection**&#x200B;或&#x200B;**Folder** **[!UICONTROL Details]**&#x200B;页面的专用面板上。

>[!IMPORTANT]
>
> * [!DNL AEM Assets View] UI可扩展性在[[!DNL Assets Ultimate]](/help/assets/assets-ultimate-overview.md)中可用。
> * 要访问[!DNL Assets view] UI扩展性，[创建并提交 [!DNL Adobe] 客户支持案例](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html)。
> * 您可以通过展开&#x200B;**[!UICONTROL 详细反馈选项]**&#x200B;并单击&#x200B;**[!UICONTROL 报告问题]**&#x200B;来提供文档反馈。

## <a id="1"></a>访问Assets视图{#add-UI-Extensibility-in-AEM-Assets-View}

按照下图中所述的步骤访问[!DNL Assets View]：
![access-assets-view-ui](/help/assets/assets/access-assets-view.jpg)

## 在[!DNL Assets View]中查看UI扩展 {#ui-extensibility-panel-assets-view}

在[!DNL Assets View]内，导航到资产、文件夹或收藏集的&#x200B;**[!UICONTROL 详细信息]**&#x200B;页面。 **[!UICONTROL 详细信息]**页面在专用面板上显示添加的UI扩展。
![我的工作区](/help/assets/assets/my-workspace-assets-view3.png)

## 添加可扩展性组件的先决条件{#assets-view-ui-extensibility}

满足以下要求以开始在[!DNL Assets View UI]上添加可扩展性组件：

* [访问 [!DNL Assets View]](#1)。
* 访问[[!DNL Adobe app builder]](https://developer.adobe.com/app-builder/docs/overview/)。
* 组织中具有系统管理员角色的开发人员的权利。 有关详细信息，请参阅[此文档](https://developer.adobe.com/uix/docs/guides/get-access/)。
* [!DNL Adobe IO command line tool (AIO CLI)]已安装在您的本地计算机上。 此工具对于创建和部署扩展项目至关重要。 有关详细信息，请参阅[此文档](https://developer.adobe.com/app-builder/docs/getting_started/#local-environment-set-up)。
* 很好地了解[!DNL JavaScript]、[!DNL Node.js]和[!DNL React]技术。

## 将UI可扩展性组件添加到[!DNL Assets View] {#ui-extensibility-in-assets-view}

1. 有关UI扩展和[!DNL Adobe App Builder]框架的基本信息，请参阅[快速入门](https://developer.adobe.com/uix/docs/getting-started/)。 了解UI可扩展性如何实现[!DNL Adobe Experience Cloud services]中的自定义逻辑和UI集成，并了解用于实施UI扩展的架构和工作流。
1. 有关UI可扩展性的常规信息，包括本地环境设置、本地预览、发布和管理，请参阅[指南](https://developer.adobe.com/uix/docs/guides/)。
1. 请参阅创建扩展中的[常见概念](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/commons/)，了解为[!DNL AEM Assets View]开发UI扩展所需的基础。
1. 将自定义侧面板添加到[!DNL Assets View]界面。 主机应用程序([!DNL Assets View])管理这些面板以处理UI交互，如切换和深层链接。 扩展使用`aem/assets/details/1`扩展点来集成指定属性的自定义面板，如面板ID、标题和内容URL。 开发人员使用`getPanels()`方法注册自定义面板，并构建显示自定义内容的路由。 有关详细实施（包括API引用和代码示例），请参阅[详细信息视图](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/details-view/)。
1. 设置您的本地环境并创建您的第一个UI扩展，以在[!DNL Assets View]中亲身体验开发UI扩展的过程。 有关更多详细信息，请参阅[AEM Assets分步查看扩展开发](https://developer.adobe.com/uix/docs/services/aem-assets-view/extension-development/)。
1. 使用AIO CLI设置应用程序以生成基本扩展结构和所需代码。 有关详细信息，请参阅 [!DNL AEM Assets View]](https://developer.adobe.com/uix/docs/services/aem-assets-view/code-generation/)的[代码生成。
1. 在本地测试您的扩展，以确保它们在部署之前可按预期工作。 在完全隔离的环境中或以部分隔离的方式运行扩展，并将扩展连接到生产[!DNL AEM Assets View]以进行测试。 有关详细信息，请参阅[疑难解答 —  [!DNL AEM Assets View] 可扩展性](https://developer.adobe.com/uix/docs/services/aem-assets-view/debug/)。
