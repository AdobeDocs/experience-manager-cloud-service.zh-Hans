---
title: 为Adobe InDesign生成仅用于置入的演绎版
description: 使用Experience Manager Assets工作流和ImageMagick生成新资源和现有资源的FPO演绎版。
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
exl-id: 869c1c34-6287-4d62-bb7a-aa4df580ac0e
source-git-commit: f0e9fe0bdf35cc001860974be1fa2a7d90f7a3a9
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 7%

---

# 为Adobe InDesign生成仅用于置入的演绎版 {#fpo-renditions}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/configure-fpo-renditions.html?lang=en) |
| AEM as a Cloud Service | 本文 |

将大型资源从Experience Manager放入Adobe InDesign文档时，创意专业人士必须等待相当长的时间才能完成这些操作 [放置资产](https://helpx.adobe.com/indesign/using/placing-graphics.html). 同时，用户被阻止使用InDesign。 这会中断创作流并对用户体验产生负面影响。 Adobe功能允许从InDesign文档开始临时放置小型演绎版。 当需要最终输出时（例如，对于打印和发布工作流），原始的全分辨率资产会在后台替换临时演绎版。 这种后台异步更新可加快设计过程以提高生产效率，并且不会妨碍创作过程。

Assets提供仅用于置入的演绎版(FPO)。 这些FPO呈现版本的文件大小较小，但具有相同的纵横比。 如果FPO演绎版不可用于某个资源，Adobe InDesign将改用原始资源。 此回退机制可确保创作工作流不间断地进行。

Experience Manageras a Cloud Service提供云原生资源处理功能以生成FPO演绎版。 使用资源微服务生成节目。 您可以配置新上传的资源以及Experience Manager中存在的资源的演绎版生成。

以下是生成FPO呈现形式的步骤：

1. [创建处理配置文件](#create-processing-profile).

1. 配置Experience Manager以使用此配置文件来 [处理新资产](#generate-renditions-of-new-assets).
1. 使用配置文件可以 [处理现有资产](#generate-renditions-of-existing-assets).

## 创建处理配置文件 {#create-processing-profile}

要生成FPO格式副本，请创建 **[!UICONTROL 处理配置文件]**. 配置文件使用云原生资产微服务进行处理。 有关说明，请参阅 [为资产微服务创建处理配置文件](asset-microservices-configure-and-use.md).

选择 **[!UICONTROL 创建FPO演绎版]** 以生成FPO演绎版。 （可选）单击 **[!UICONTROL 新增]** 以将其他演绎版设置添加到同一配置文件。

![create-processing-profile-fpo-renditions](assets/create-processing-profile-fpo-renditions.png)

## 生成新资产的演绎版 {#generate-renditions-of-new-assets}

要生成新资产的FPO演绎版，请应用 **[!UICONTROL 处理配置文件]** 到文件夹属性中的文件夹。 在文件夹的“属性”页面中，单击 **[!UICONTROL 资产处理]** 选项卡，选择 **[!UICONTROL FPO配置文件]** as a **[!UICONTROL 处理配置文件]**，并保存更改。 使用此配置文件处理上传到文件夹的所有新资源。

![add-fpo-rendition](assets/add-fpo-rendition.png)


## 生成现有资产的演绎版 {#generate-renditions-of-existing-assets}

要生成演绎版，请选择资源并执行以下步骤。

![fpo-existing-asset-reprocess](assets/fpo-existing-asset-reprocess.gif)


## 查看FPO演绎版 {#view-fpo-renditions}

您可以在工作流完成后检查生成的FPO演绎版。 在Experience Manager Assets用户界面中，单击资源以打开大型预览。 打开左边栏并选择 **[!UICONTROL 演绎版]**. 或者，使用键盘快捷键 `Alt + 3` 打开预览时。

单击 **[!UICONTROL FPO演绎版]** 以加载其预览。 或者，您也可以右键单击该演绎版并将其保存到您的文件系统。 检查左边栏中是否有可用的演绎版。

![rendition_list](assets/list-renditions.png)

**另请参阅**

* [翻译资源](translate-assets.md)
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
