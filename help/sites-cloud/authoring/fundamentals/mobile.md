---
title: 创作适用于移动设备的页面
description: 在为移动设备进行创作时，您可以在多个模拟器之间切换，以查看最终用户看到的内容
exl-id: fabd4468-3304-402f-9522-342da3bbae94
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 98%

---

# 创作适用于移动设备的页面 {#authoring-a-page-for-mobile-devices}

Adobe Experience Manager 页面基于响应式布局。[响应式布局可自动调整内容以适合目标设备，而无需为特定设备创作内容。](/help/sites-cloud/authoring/features/responsive-layout.md)

在创作移动页面时，页面会以模拟移动设备的方式显示。在创作页面时，您可以在多个模拟器之间切换，以查看最终用户在访问页面时看到的内容。

根据设备呈现页面的功能，设备分为功能、智能和触控三个类别。当最终用户访问移动页面时，AEM 会检测设备并发送与其设备组对应的演绎版。

>[!NOTE]
>
>要创建基于现有标准站点的移动站点，请创建标准站点的 Live Copy。请参阅 [创建Live Copy。](/help/sites-cloud/administering/msm/creating-live-copies.md)
>
>AEM 开发人员可以创建新设备组。请参阅“创建设备组筛选器”。

<!--
>AEM developers can create new device groups. (See [Creating Device Group Filters](/help/sites-developing/groupfilters.md).)
-->

请使用以下过程来创作移动页面：

1. 从全局导航中打开&#x200B;**站点**&#x200B;控制台。
1. 编辑内容页面。
1. 单击页面顶部的&#x200B;**模拟器**&#x200B;图标以切换到所需的模拟器。

   ![“模拟器”图标](/help/sites-cloud/authoring/assets/emulator.png)

1. 将组件浏览器或资产浏览器中的组件拖放到页面上。
1. 根据所选设备[修改页面及其组件的响应式布局](/help/sites-cloud/authoring/features/responsive-layout.md)。

该页面将与下图所示类似：

![移动设备示例](/help/sites-cloud/authoring/assets/mobile.png)

>[!NOTE]
>
>从移动设备中请求创作实例上的页面时，会禁用模拟器。
