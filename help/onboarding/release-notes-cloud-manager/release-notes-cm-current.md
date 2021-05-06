---
title: AEM中Cloud Manager作为Cloud Service版本2021.5.0的发行说明
description: AEM中Cloud Manager作为Cloud Service版本2021.5.0的发行说明
feature: 发行信息
translation-type: tm+mt
source-git-commit: 29bc3d02295fb04f3aacda41c43d1733092e1f27
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 3%

---


# Adobe Experience Manager中Cloud Manager作为Cloud Service 2021.5.0 {#release-notes}的发行说明

本页概述了AEM中作为Cloud Service 2021.5.0的Cloud Manager发行说明。

>[!NOTE]
>要将当前的Adobe Experience Manager发行说明作为Cloud Service查看，请单击[此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hans)。

## 发布日期 {#release-date}

AEM中Cloud Manager作为Cloud Service 2021.5.0的发布日期为2021年5月06日。
下一版本计划于2021年6月03日发布。

### 新增功能 {#what-is-new}

* PackageOverlaps质量规则现在检测在同一部署的包集中多次部署同一包的情况，即在多个嵌入式位置中部署同一包。

* 公共API中的存储库端点现在包括Git URL。

* 由Cloud Manager用户下载的部署日志将更直观，现在将包含有关失败和成功方案的详细信息。

* 现在，已解决将代码推送到Adobe Git时遇到的间歇性故障。

* Commerce add-on现在可以在“编辑”项目工作流程中应用到沙箱项目。

* *编辑项目*&#x200B;体验已刷新。

* “环境详细信息”页中的“域名”表将通过分页显示多达250个域名。

* **添加项目**&#x200B;和&#x200B;**编辑项目**&#x200B;工作流中的&#x200B;**解决方案和加载项**&#x200B;选项卡将显示解决方案，即使项目仅提供一个解决方案也是如此。

* 生成未生成任何已部署内容包时生成步骤日志中的错误消息不清楚。

### 错误修复 {#bug-fixes}

* 有时，即使未部署IP允许列表，用户也可能在IP配置旁看到绿色的“活动”状态。

* 管道变量API将仅以状态&#x200B;**DELETED**&#x200B;标记它们，而不是删除“deleted”变量。

* 某些“代码气味”类型的质量问题错误地影响了“可靠性等级”。

* 由于不支持通配符域，因此UI将禁止用户提交通配符域。

* 当在午夜和凌晨1点之间启动管道执行时，Cloud Manager生成的伪像版本不能保证大于前一天创建的版本。

* 在沙箱项目设置过程中，成功创建包含示例代码的项目后，“管理Git”将显示为“概述”页面中主题卡中的链接。