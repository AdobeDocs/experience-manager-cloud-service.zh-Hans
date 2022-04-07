---
title: Adobe Experience Manager as a Cloud Service中的Cloud Manager 2022.4.0发行说明
description: 以下是AEM as a Cloud Service中Cloud Manager 2022.4.0的发行说明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: e448ee4ee2928a136bdab382c67104bedce28732
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 1%

---


# Adobe Experience Manager as a Cloud Service中的Cloud Manager 2022.4.0发行说明 {#release-notes}

本页记录了AEMas a Cloud Service中Cloud Manager 2022.4.0的发行说明。

>[!NOTE]
>
>请参阅 [本页](/help/release-notes/release-notes-cloud/release-notes-current.md) ，以了解Adobe Experience Manager as a Cloud Service的最新发行说明。

## 发布日期 {#release-date}

AEM 2022年4月7日as a Cloud Service的Cloud Manager 2022.4.0版的发布日期。 下一版本计划于2022年5月5日发布。

## 新增功能 {#what-is-new}

* 已实施管道构建步骤的持续时间和成功率的改进，并将在4月之前逐步推广到所有客户。
* 现在，您可以通过在添加和编辑管道向导的输入字段中键入名称的前几个字符，然后从两者的建议匹配中进行选择，轻松找到git分支 [生产](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) 和 [非生产](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) 管道。
* 4月版发布后不久，在环境创建过程中定义云区域时，印度将可供选择。
* 的 **管道** 现在，页面已进行分页，以提高具有大量管道的程序的可用性。
   * 表中将显示每页50行。
* 的版本 [AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) Cloud Manager使用的已更新到版本36。
* OracleJDK现在是用于开发和操作AEM应用程序的默认JDK。 即使在Maven工具链中明确选择了替代选项，Cloud Manager构建过程仍会自动切换到使用OracleJDK。
   * 要详细了解如何切换到OracleJDK，请参阅 [构建环境文档。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)
   * 请参阅 [Adobe Experience Manager的Java支持策略常见问题解答](https://experienceleague.adobe.com/docs/experience-manager-65/assets/Java_Policy_for_Adobe_Experience_Manager.pdf) 以解决有关此更改的常见问题。
* 现在，通过在验证步骤中检测旧版AEM，可以更快地执行管道。 用户将在UI中看到一条消息来指导他们。

## 错误修复 {#bug-fixes}

* 现在，可通过UI下载在UI测试步骤中创建的日志。
* Web层配置管道现在只能重复执行Web层配置中的包。
* 为UI中的消息添加了关于如何在过时环境中更新AEM的更清晰说明。
