---
title: 将 Adobe Analytics 与 Experience Cloud 设置自动化集成
description: Experience Cloud 设置自动化提供了一种简单且自动化的方式，通过简单的 UI 向导界面将 Experience Manager Sites 与 Experience Platform Launch 和 Adobe Analytics 集成和装备到一起。了解如何在您自己的站点上使用自动化设置。
feature: Administering
role: Admin
hide: true
hidefromtoc: true
index: false
exl-id: 351ead2c-7b0d-4bd9-a020-47516948d467
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: ht
source-wordcount: '639'
ht-degree: 100%

---

# 将 Adobe Analytics 与 Experience Cloud 设置自动化集成 {#integrate-adobe-analytics-automation-setup}

>[!CAUTION]
>
> 此功能目前处于内部测试阶段。Target 于 2022 年第 1 季度发行。

Experience Cloud 设置自动化提供了一种简单且自动化的方式，通过简单的 UI 向导界面将 Experience Manager Sites 与 Experience Platform Launch 和 Adobe Analytics 集成和装备到一起。

将 Adobe Analytics 与 AEM Sites 集成从未如此轻松。借助 Experience Cloud 设置自动化，只需单击几下，即可设置、集成和检测您的站点以捕获性能分析，从而了解客户的参与和转换情况。

本视频探讨了如何使用 Experience Cloud 设置自动化将 AEM 站点与 Experience Platform Launch 和 Analytics 集成：

>[!VIDEO](https://video.tv.adobe.com/v/339605/?quality=12)

## 要求

自动化设置旨在即时使用通过启用了 [Adobe 客户端数据层](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html)的 [AEM 核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)构建的 AEM 站点。您可以使用 [AEM 项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 或使用[站点模板](/help/journey-sites/quick-site/create-site.md)创建站点来生成已自动启用这些功能的新站点。

## 如何设置

1. 导航到&#x200B;**站点**，并选择要与 Adobe Analytics 集成的站点的根。
1. 展开侧边栏菜单并点按&#x200B;**设置 Analytics**。

   这是侧边栏中的一个新选项，它将打开一个面板，该面板将为 Experience Cloud 设置自动化提供控件和状态。
1. 点按&#x200B;**基础 Analytics** 按钮。
1. 在生成的对话框中，为&#x200B;**报告包 ID** 提供名称。

   此字符串将用于在 Adobe Analytics 中创建新的[报告包 ID](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html?lang=zh-Hans) 作为选定 AEM 站点的分析数据的数据存储。将为提供的字符串附加环境和层标识符以确保唯一性。

1. 刷新页面和面板，然后点按&#x200B;**查看集成状态**&#x200B;查看自动化的状态。

   自动化设置是异步进行的。**查看集成状态**&#x200B;将显示集成的当前状态。

   * **进行中** – 表明作业正在运行。
   * **集成完成** – 表明作业已将 Analytics 和 Launch 集成、设置 Launch 扩展和 Launch 规则，并在 Adobe Analytics 中创建了新的报告包。
   * **失败** – 表明自动化作业无法成功完成。 单击“日志”链接来查看此作业的日志文件。

## 验证 AEM 设置

自动化完成后，验证您的站点现在是否正在触发 Analytics 事件。

1. 使用&#x200B;**站点编辑器**&#x200B;在您的站点中打开页面。
1. 使用&#x200B;**以发布的形式查看**&#x200B;选项上传页面的发布版本。
1. 使用浏览器的开发人员工具来检查网络流量，并检查是否正在加载 **Launch** 和 `AppMeasurement.js` 文件。
1. 检查浏览器的控制台以查看页面和组件级别的事件是否由 Adobe 客户端数据层触发和收集。

## 验证 Analytics 设置

接下来，导航到 Adobe Analytics 以查看从 AEM 站点上的事件流入的数据。

1. 导航到与您的 AEM 站点相同的 IMS 组织中的 Adobe Analytics。
1. 创建 AEM Sites 的新概述报告，方式是导航到&#x200B;**“报告”**>**“参与”**>**“Adobe Experience Manager”**>**“站点性能概述”**。
1. 点按&#x200B;**打开报告**。
1. 选择与上一个实践中使用的报告包名称匹配的&#x200B;**报告包 ID**。
1. 查看随时间推移流入新模板中的分析数据。

   >[!NOTE]
   >
   > 利用新的集成，可能需要几个小时才能将数据填入报告中。
