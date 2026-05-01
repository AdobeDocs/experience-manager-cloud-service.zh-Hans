---
title: 将视频智能裁剪应用于批准的视频
description: 通过具有OpenAPI功能的Dynamic Media ，您可以在Adobe Experience Manager (AEM)中为批准的视频资源自动生成视频智能裁剪输出。
role: Admin, User
badgeSaas: label="AEM Assets" type="Positive" tooltip="适用于AEM Assets)。"
exl-id: video-smartcrop-dmwoapi
source-git-commit: 8ddd2ade491069e4592becf3b77c04e6bbb2c06a
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 2%

---


# 将视频智能裁剪应用于批准的视频 {#apply-video-smart-crops-dmwoapi}

[!DNL Dynamic Media with OpenAPI capabilities]允许您在[!DNL Adobe Experience Manager (AEM)]中自动生成视频资产的视频智能裁剪输出。 视频智能裁剪可分析视频内容并动态调整帧以保持不同宽高比和设备中的关键主题聚焦。

启用该功能并批准视频资产后，将自动生成视频智能裁剪

## 开始之前 {#prerequisites-for-video-smart-crops}

确保您具有：

* 访问[!DNL AEM Assets as a Cloud Service]。
* 编辑元数据架构的权限。
* 为您的环境启用了OpenAPI功能的Dynamic Media 。
* 可标记为&#x200B;**[!UICONTROL 已批准]**&#x200B;的视频资产。

## 为视频启用视频智能裁剪 {#enable-video-smart-crops}

要启用视频智能裁剪，请配置用于视频资产的元数据架构：

1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 元数据架构]**。
2. 打开适用的元数据架构（例如，**默认**）。
3. 选择&#x200B;**视频**&#x200B;表单，然后单击&#x200B;**[!UICONTROL 编辑]**。
4. 添加新的&#x200B;**[!UICONTROL 下拉字段]**&#x200B;并配置以下内容：

   * **字段标签**：创建视频智能裁剪
   * **映射到属性**： `./jcr:content/dam:applyVideoSmartCrop`

5. 手动添加以下值：

   * 是→真
   * 否→假

6. 保存架构。

现在，视频资源元数据表单中提供了&#x200B;**创建视频智能裁剪**&#x200B;选项。

![创建视频智能裁剪字段](/help/assets/assets/video-smartcrop-metadata-field.png)

## 将视频智能裁剪应用于批准的视频 {#apply-video-smart-crops}

您可以通过启用元数据字段并批准资产，将视频智能裁剪应用于视频资产。

执行以下步骤：

1. 在[!DNL Assets View]中，选择&#x200B;**[!UICONTROL Assets]**&#x200B;并导航到您的文件夹。
2. 选择视频资产。
3. 单击&#x200B;**[!UICONTROL 详细信息]**。
4. 在元数据面板中，找到&#x200B;**[!UICONTROL 创建视频智能裁剪]**。
5. 将该值设置为&#x200B;**是**，然后单击&#x200B;**[!UICONTROL 保存]**。
6. 将资源状态设置为&#x200B;**[!UICONTROL 已批准]**。

资源获得批准后，将自动生成视频智能裁剪输出。

## 查看视频智能裁剪输出 {#view-video-smart-crops}

生成视频智能裁剪后：

* 输出在视频播放期间可用。
* Dynamic Media查看器会根据设备和长宽比自动选择最合适的裁切。
* 视频播放会动态调整以保持关键主题聚焦。

## 使用视频智能裁剪的视频 {#use-video-smart-crops}

无论在何处交付视频资产，您都可以使用“视频智能裁剪”输出，例如：

* 网页
* 应用程序
* 嵌入式视频播放器

查看器会在播放期间自动应用相应的智能裁切。

>[!NOTE]
>
>* 仅为&#x200B;**已批准**&#x200B;个视频资产生成视频智能裁剪。
>* 在批准资产之前，请确保&#x200B;**创建视频智能裁剪**&#x200B;字段设置为&#x200B;**是**。
>* 视频智能裁剪不会修改原始资产。 裁剪在播放期间动态应用。