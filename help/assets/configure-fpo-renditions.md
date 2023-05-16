---
title: 为仅用于置入的呈现版本生成Adobe InDesign
description: 使用Experience Manager Assets工作流和ImageMagick生成新资产和现有资产的FPO演绎版。
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
exl-id: 869c1c34-6287-4d62-bb7a-aa4df580ac0e
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 7%

---

# 为仅用于置入的呈现版本生成Adobe InDesign {#fpo-renditions}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/configure-fpo-renditions.html?lang=en) |
| AEM as a Cloud Service | 本文 |

将大型资产从Experience Manager放入Adobe InDesign文档中时，创意专业人士必须等待一段较长的时间 [放置资产](https://helpx.adobe.com/indesign/using/placing-graphics.html). 同时，阻止用户使用InDesign。 这会中断创作流程，并对用户体验造成负面影响。 Adobe允许在InDesign文档中临时放置小型演绎版，以开始。 如果需要最终输出（例如，对于打印和发布工作流），原始的全分辨率资产将替换后台的临时演绎版。 后台的此异步更新可加快设计流程以提高生产效率，同时不会妨碍创作流程。

资产提供仅用于放置(FPO)的演绎版。 这些FPO呈现文件大小较小，但纵横比相同。 如果FPO演绎版不适用于资产，Adobe InDesign会改用原始资产。 此回退机制可确保创意工作流持续进行，不会出现任何中断。

Experience Manageras a Cloud Service提供云原生资产处理功能以生成FPO呈现版本。 使用资产微服务生成演绎版。 您可以为新上传资产和Experience Manager中存在的资产配置演绎版生成。

以下是生成FPO演绎版的步骤：

1. [创建处理配置文件](#create-processing-profile).

1. 配置Experience Manager以使用此配置文件 [处理新资产](#generate-renditions-of-new-assets).
1. 使用用户档案 [处理现有资产](#generate-renditions-of-existing-assets).

## 创建处理配置文件 {#create-processing-profile}

要生成FPO呈现，请创建 **[!UICONTROL 处理配置文件]**. 配置文件使用云原生资产微服务进行处理。 有关说明，请参阅 [为资产微服务创建处理配置文件](asset-microservices-configure-and-use.md).

选择 **[!UICONTROL 创建FPO演绎版]** 生成FPO呈现版本。 （可选）单击 **[!UICONTROL 新增]** 向同一配置文件添加其他演绎版设置。

![create-processing-profile-fpo-renditions](assets/create-processing-profile-fpo-renditions.png)

## 生成新资产的演绎版 {#generate-renditions-of-new-assets}

要生成新资产的FPO演绎版，请应用 **[!UICONTROL 处理配置文件]** 文件夹属性中的文件夹。 在文件夹的“属性”页面中，单击 **[!UICONTROL 资产处理]** 选项卡，选择 **[!UICONTROL FPO配置文件]** as a **[!UICONTROL 处理配置文件]**，然后保存更改。 上传到文件夹的所有新资产都将使用此配置文件进行处理。

![add-fpo-rendition](assets/add-fpo-rendition.png)


## 生成现有资产的演绎版 {#generate-renditions-of-existing-assets}

要生成演绎版，请选择资产，然后按照以下步骤操作。

![fpo-existing-asset-reprocess](assets/fpo-existing-asset-reprocess.gif)


## 查看FPO呈现 {#view-fpo-renditions}

您可以在工作流完成后检查生成的FPO演绎版。 在Experience Manager Assets用户界面中，单击资产以打开大型预览。 打开左边栏并选择 **[!UICONTROL 演绎版]**. 或者，使用键盘快捷键 `Alt + 3` 打开预览时。

单击 **[!UICONTROL FPO呈现]** 来加载其预览。 或者，您也可以右键单击演绎版并将其保存到文件系统。 检查左边栏中的可用演绎版。

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
