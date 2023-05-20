---
title: 组件控制台
description: 组件控制台允许您浏览针对实例定义的所有组件
exl-id: f4949331-5302-46d3-a004-b813bb95ec2f
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 81%

---

# 组件控制台 {#components-console}

组件控制台允许您浏览针对实例定义的所有组件，并查看每个组件的关键信息。

该控制台可从&#x200B;**工具** -> **常规** -> **组件**&#x200B;中访问。由于组件没有树结构，因此只有列视图可用。

![组件控制台](/help/sites-cloud/authoring/assets/components-console.png)

>[!NOTE]
>
>组件控制台会显示系统中的所有组件。[组件浏览器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)显示可用于创作的组件，并隐藏任何以句点 (`.`) 开头的组件组。

## 搜索 {#search-field}

通过&#x200B;**仅限内容**&#x200B;图标（左上方），您可以打开&#x200B;**搜索**&#x200B;面板以搜索和/或筛选组件：

![在组件控制台中搜索](/help/sites-cloud/authoring/assets/components-console-search.png)

### 组件详细信息 {#component-details}

若要檢視特定元件的詳細資訊，請點選/按一下所需的資源。 三個索引標籤提供：

* **属性**

   ![组件控制台属性](/help/sites-cloud/authoring/assets/components-console-properties.png)

   在“属性”选项卡上，您可以：

   * 查看组件的常规属性。
      * 查看组件的图标或缩写定义的方式。<!-- View how the [icon or abbreviation has been defined](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) for the component.-->
      * 按一下圖示的來源會前往該元件。
   * 檢視 **資源型別** 和 **資源超級型別** （如果已定義）。
      * 按一下「資源超級型別」即可前往該元件。

   >[!NOTE]
   >
   >由于 `/apps` 在运行时不可编辑，因此组件控制台为只读。

* **策略**

   ![组件控制台策略](/help/sites-cloud/authoring/assets/components-console-policies.png)

* **实时使用情况**

   ![组件的实时使用情况](/help/sites-cloud/authoring/assets/components-console-live-usage.png)

   >[!CAUTION]
   >
   >由于为此视图收集的信息的性质所致，它可能需要一段时间才能进行整理/显示。

* **文档**

   如果开发人员提供了组件相关文档，则该文档将会显示在&#x200B;**文档**&#x200B;选项卡中。如果没有可用文档，则不会显示&#x200B;**文档**&#x200B;选项卡。<!-- If the developer has provided [documentation for the component](/help/sites-developing/developing-components.md#documenting-your-component), it will appear on the **Documentation** tab. If there is no documentation available, the **Documentation** tab will not be shown.-->

   ![组件文档](/help/sites-cloud/authoring/assets/components-console-documentation.png)
