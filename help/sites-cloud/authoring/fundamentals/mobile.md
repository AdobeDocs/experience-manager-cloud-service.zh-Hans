---
title: 创作适用于移动设备的页面
description: 在为移动设备进行创作时，您可以在多个模拟器之间切换，以查看最终用户看到的内容
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# 创作适用于移动设备的页面 {#authoring-a-page-for-mobile-devices}

Adobe Experience Manager页面基于响应式布局。 响应式布局可自动调整内容以适合目标设备，无需为特定设备创作内容。

在创作移动页面时，页面会以模拟移动设备的方式显示。在创作页面时，您可以在多个模拟器之间切换，以查看最终用户在访问页面时看到的内容。

根据设备呈现页面的功能，设备分为功能、智能和触控三个类别。当最终用户访问移动页面时，AEM 会检测设备并发送与其设备组对应的演绎版。

>[!NOTE]
>
>要创建基于现有标准站点的移动站点，请创建标准站点的 Live Copy。请参阅为不同渠道创建Live Copy。
>
>AEM开发人员可以创建新设备组。 请参阅创建设备组过滤器。
<!--
>To create a mobile site based on an existing standard site, create a live copy of the standard site. (See [Creating a Live Copy for Different Channels](/help/sites-administering/msm-livecopy.md).)
>
>AEM developers can create new device groups. (See [Creating Device Group Filters](/help/sites-developing/groupfilters.md).)
-->

请使用以下过程来创作移动页面：

1. From global navigation open the **Sites** console.
1. 编辑内容页面。
1. Switch to the desired emulator by clicking the **Emulator** icon at the top of the page.

   ![模拟器图标](/help/sites-cloud/authoring/assets/emulator.png)

1. 将组件浏览器或资产浏览器中的组件拖放到页面上。
1. [根据所选设备](/help/sites-cloud/authoring/features/responsive-layout.md) ，修改页面及其组件的响应式布局。

该页面的外观将类似于以下内容：

![移动示例](/help/sites-cloud/authoring/assets/mobile.png)

>[!NOTE]
>
>从移动设备中请求创作实例上的页面时，会禁用模拟器。
