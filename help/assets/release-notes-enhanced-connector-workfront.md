---
title: ' 版发行说明 [!DNL Workfront for Experience Manager enhanced connector]'
description: ' 版发行说明 [!DNL Workfront for Experience Manager enhanced connector]'
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: 081f7ed8c39382408285887928163e2569c5cbfe
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 4%

---

#  版发行说明[!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

以下部分概述了 [!DNL Workfront for Experience Manager enhanced connector].

## 发布日期 {#release-date}

最新版本1.9.0( [!DNL Workfront for Experience Manager enhanced connector] 是2022年6月16日。

## 发行亮点 {#release-highlights}

的最新版本 [!DNL Workfront for Experience Manager enhanced connector] 包括以下错误修复：

* 当您通过链接的文件夹上传或使用 `Send To` Workfront中可用于将资产上传到Experience Manageras a Cloud Service的操作，导致资产损坏，无法在Adobe Photoshop中打开。

>[!IMPORTANT]
>
>Adobe建议您 [升级到最新的1.9.0版本](../assets/update-workfront-enhanced-connector.md) 的 [!DNL Workfront for Experience Manager enhanced connector].

## 已知问题 {#known-issues}

* 使用AEM 6.4配置项目链接文件夹时，Experience Manager不会保存 **[!UICONTROL 子文件夹]** 和 **[!UICONTROL 在具有项目组合的项目中创建链接文件夹]** 字段。 的值 **[!UICONTROL 子文件夹]** 字段更新至 **[!UICONTROL 未定义]** 和 **[!UICONTROL 在具有项目组合的项目中创建链接文件夹]** 字段更新至 **[!UICONTROL 默认Portfolio]** 自动。

* 当您使用经典Workfront体验时， **[!UICONTROL 发送到]** 选项 **[!UICONTROL 更多]** 下拉列表不允许您在Experience Manager中选择目标目标。 的 **[!UICONTROL 发送到]** 选项可使用 **[!UICONTROL 文档操作]** 下拉列表。 的 **[!UICONTROL 发送到]** 选项可正确用于 **[!UICONTROL 更多]** 下拉列表以及 **[!UICONTROL 文档操作]** 新Workfront体验中提供的下拉列表。

## 以前版本 {#previous-releases}

### 2022年3月版 {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 现在包括以下更新：

* 现在，即使存在多个项目链接文件夹配置，您也可以在Adobe Workfront和AEM Assetsas a Cloud Service之间创建链接文件夹。

* 添加了对事件订阅分页的支持。

* 添加了对AEM 6.4.x的支持。

* 添加了对代理环境的支持。

* 根据合作伙伴和客户反馈进行了若干错误修复。

>[!MORELIKETHIS]
>
>* [集成 [!DNL Workfront for Experience Manager enhanced connector] 与Experience Manager6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=en)
>* [集成 [!DNL Workfront for Experience Manager enhanced connector] 与Experience Manager6.4](https://experienceleague.adobe.com/docs/experience-manager-64/assets/integrations/workfront-integrations.html?lang=en)

