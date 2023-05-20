---
title: 為行動裝置編寫頁面
description: 為行動裝置製作時，您可以在數個模擬器之間切換，以檢視一般使用者看到的內容
exl-id: fabd4468-3304-402f-9522-342da3bbae94
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 52%

---

# 為行動裝置編寫頁面 {#authoring-a-page-for-mobile-devices}

Adobe Experience Manager 页面基于响应式布局。[响应式布局可自动调整内容以适合目标设备，而无需为特定设备创作内容。](/help/sites-cloud/authoring/features/responsive-layout.md)

編寫行動頁面時，頁面會以模擬行動裝置的方式顯示。 編寫頁面時，您可以在多個模擬器之間切換，以檢視一般使用者在存取頁面時看到的內容。

系統會根據裝置轉譯頁面的功能，將裝置分組為類別功能、智慧型和觸控。 當一般使用者存取行動頁面時，AEM會偵測裝置並傳送與其裝置群組相對應的表現。

>[!NOTE]
>
>若要根據現有的標準網站建立行動網站，請建立標準網站的即時副本。 请参阅[创建 Live Copy](/help/sites-cloud/administering/msm/creating-live-copies.md)。
>
>AEM 开发人员可以创建新设备组。请参阅“创建设备组过滤器”。

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
