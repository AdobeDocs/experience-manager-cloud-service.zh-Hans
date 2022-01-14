---
title: 与 Adobe Analytics 集成
description: '与 Adobe Analytics 集成 '
feature: Administering
role: Admin
source-git-commit: 4bf5ee1218f775efdc7829b790360033ad756c9a
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 2%

---


# 将Adobe Analytics与Experience Cloud设置自动化集成 {#integrate-adobe-analytics-automation-setup}

>[!CAUTION]
>
> 此功能当前为内部测试版。 Target版本发布于2022年第1季度。

Experience Cloud设置自动化提供了一种简单且自动的方式，通过简单的UI向导界面将Experience Manager Sites与Experience Platform Launch和Adobe Analytics集成并设置仪器。

将Adobe Analytics与AEM Sites集成从未像现在这样简单。 借助Experience Cloud设置自动化，只需单击几下即可设置、集成和检测您的网站以捕获性能分析，从而了解客户的参与度和转化情况。

本视频探讨如何使用“AEM设置自动化”将Experience Cloud网站与Experience Platform Launch和Analytics集成：

>[!VIDEO](https://video.tv.adobe.com/v/339605/?quality=12)

## 要求

自动化设置旨在开箱即用，并使用 [AEM核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 和 [Adobe客户端数据层](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html) 已启用。 您可以使用 [AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 或通过使用 [网站模板](/help/journey-sites/quick-site/create-site.md).

## 如何设置

1. 导航到 **站点** 并选择要与Adobe Analytics集成的站点的根。
1. 展开侧边栏菜单，然后点按 **设置分析**.

   这是侧边栏中的一个新选项，它将打开一个面板，其中提供Experience Cloud设置自动化的控件和状态。
1. 点按 **集成Analytics** 按钮。
1. 在结果对话框中，为 **报表包ID**.

   此字符串将用于创建新 [报表包ID](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html?lang=en) 在Adobe Analytics中作为选定AEM网站的analytics数据的数据存储。 提供的字符串将附加环境和层标识符，以确保唯一性。

1. 刷新页面和面板，然后点按 **检查集成状态** 以检查自动化的状态。

   自动化设置是异步进行的。 的 **检查集成状态** 将显示集成的当前状态。

   * **正在进行**  — 指示作业正在运行。
   * **集成完成**  — 表示作业已完成Analytics和Launch集成、设置Launch扩展和Launch规则，以及在Adobe Analytics中创建新报表包。
   * **失败**  — 表示自动作业无法成功完成。 单击日志链接，检查此作业的日志文件。

## 验证AEM设置

自动化完成后，验证您的网站是否现在触发Analytics事件。

1. 使用 **站点编辑器**.
1. 使用 **查看已发布的项目** 选项来加载页面的已发布版本。
1. 使用浏览器的开发人员工具检查网络流量，以及 **Launch** 和 `AppMeasurement.js` 文件正在加载。
1. Inspect是浏览器的控制台，用于查看Adobe客户端数据层触发和收集的页面和组件级别事件。

## 验证Analytics设置

接下来，导航到Adobe Analytics以查看从AEM网站上的事件流入的数据。

1. 在与您的AEM网站相同的IMS组织中导航到Adobe Analytics。
1. 为AEM Sites导航到 **报表** > **参与度** > **Adobe Experience Manager** > **网站性能概述**.
1. 点按 **打开报表**.
1. 选择 **报表包ID** 与上一个练习中使用的报表包名称匹配。
1. 查看一段时间内流入新模板的分析数据流。

   >[!NOTE]
   >
   > 使用新集成，可能需要几个小时才能将报表填充到数据中。
