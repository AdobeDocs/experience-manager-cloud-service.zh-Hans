---
title: AEM Assets与Adobe Express的本机集成
description: AEM Assets与Adobe Express本机集成允许您从Adobe Express用户界面中直接访问AEM Assets中存储的资源。
exl-id: d43e4451-da2a-444d-9aa4-4282130ee44f
source-git-commit: 8bbf9a2ba8f708a5a03d11bc0388d39b32d4c7b3
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 30%

---

# 与Adobe Express的本机集成 {#native-integration-adobe-express}

AEM Assets与Adobe Express进行原生集成，这使您能够从Adobe Express用户界面中直接访问存储在AEM Assets中的资源。 可将在 AEM Assets 中管理的内容放入 Express 画布，然后将新内容或经过编辑的内容保存在 AEM Assets 存储库中。该集成具有以下主要优势：

* 通过在AEM中编辑和保存新资源提高了内容重复使用率。

* 减少了创建新资产或创建新版本现有资产的总体时间和工作量。

## 先决条件 {#prerequisites}

有权访问AEM Assets中的Adobe Express和至少一个环境。 该环境可以是 Assets as a Cloud Service 或 Assets Essentials 中的任何存储库。


## 在 Adobe Express 编辑器中使用 AEM Assets {#use-aem-assets-in-express}

执行以下步骤以开始在Adobe Express编辑器中使用AEM Assets：

1. 打开 Adobe Express Web 应用程序。

1. 通过加载新模板或项目或创建资源来打开新的空白画布。

1. 单击 **[!UICONTROL 资产]** 在左侧导航窗格中可用。 Adobe Express显示您有权访问的存储库列表，以及在根级别可用的资源和文件夹列表。

1. 浏览或搜索存储库中的资产以拖放到画布上。 您可以使用各种可用的过滤器来筛选资源，例如文件类型、MIME类型和维度。

   ![从 Assets 加载项纳入资源](assets/adobe-express-native-integration.png)


## 将 Adobe Express 项目保存在 AEM Assets 中 {#save-express-projects-in-assets}

在 Express 画布中纳入适当的修改后，即可将该画布保存在 AEM Assets 存储库中。

1. 单击 **[!UICONTROL 共享]** 以打开 **[!UICONTROL 共享]** 对话框。

   ![将资源保存在 AEM 中](assets/adobe-express-share.png)

1. 选择 **[!UICONTROL AEM Assets]** 从 **[!UICONTROL 存储]** 部分在右侧窗格中可用。 Adobe Express显示“上载”对话框。
1. 指定资源的名称和格式。可将画布的内容保存为 PNG 或 JPEG 格式类型。

1. 单击&#x200B;**[!UICONTROL 位置]**&#x200B;字段旁的文件夹图标，导航到要保存资源的位置，然后单击&#x200B;**[!UICONTROL 选择]**。随后在&#x200B;**[!UICONTROL 位置]**&#x200B;字段中显示该文件夹的名称。

   ![将资源保存在 AEM 中](assets/adobe-express-upload.png)

1. 可选：您可以使用为上传添加营销活动元数据 **[!UICONTROL 项目或营销活动名称]** 字段。 您可以使用现有名称或创建新名称。 您可以为上传定义多个项目或营销策划名称。 键入名称时，单击对话框中的其它位置或按 `,` （逗号）密钥以注册名称。

   作为最佳实践，Adobe建议在其他字段中指定值，并且为上传的资源创建增强的搜索体验。
1. 同样，定义 **[!UICONTROL 关键字]** 和 **[!UICONTROL 渠道]** 字段。

1. 单击&#x200B;**[!UICONTROL 上传]**&#x200B;以将资源上传到 AEM Assets。




## 限制 {#limitations}

某些具有多个Assets存储库访问权限的用户在保存具有多个存储库的资产的文档时遇到了已知错误。
