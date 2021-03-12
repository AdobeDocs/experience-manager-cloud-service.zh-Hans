---
title: '生产项目简介 '
description: '生产项目简介 '
translation-type: tm+mt
source-git-commit: 5773683a75254855687266929a3e1876c8f06e61
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---


# 生产项目简介{#production-programs}

*Production*&#x200B;项目适用于熟悉AEM和Cloud Manager的用户，可以开始编写、构建和测试代码，以将其部署到生产。

>[!NOTE]
>您无法删除生产项目。

项目创建向导将根据用户在创建项目时的目标引导用户进行选择。 根据特定客户或组织可用的未使用解决方案授权，用户可以控制如何将可用（未使用）解决方案授权映射到Cloud Manager项目。

## 项目创建注意事项{#program-creation-considerations}

下表描述在Cloud Manager中创建项目时要考虑的常见方案：

| 组织中提供的未使用的解决方案授权 | 创建项目选项 | 包含的内容 | 何时使用和其他注意事项 |
|--- |--- |--- |--- |
| 1个站点解决方案 | 仅创建1个站点项目 | 1个生产+1个阶段，1个开发 | NA |
| 1个资产解决方案 | 仅创建1个资产项目 | 1个生产+1个阶段，1个开发 | NA |
| 1个站点+1个资产 | 创建一个项目:1个站点和资产项目 | 1个生产+1个阶段，2个开发 | 大部分数字资产用于支持站点实施。 大多数数字资产处于已完成状态，随时可用于通过Sites实现跨渠道体验。通常，一个团队负责管理站点和资产的内容。 **常见示例**:主要用于网站的图像。将通过内置于AEM Sites中的内部门户分发的PDF。 |
| 1个站点+1个资产 | 创建单独的项目:仅限1个站点项目和1个仅限资产项目 | 1个生产+ 1阶段，1个开发<br> 1个生产+ 1阶段，1个开发 | 许多数字资产并不直接支持站点实施。 受管理的资产处于各种状态，包括原始文件类型和正在进行中的工作。 专业的创意团队在数字资产的整个生命周期中进行管理，与Sites内容管理团队相比，该团队具有不同的工作流和发布周期。 *常见示例*:照片拍摄中的原始图像存储在“资源”项目中，站点实施中只使用少数几张图像。在AEM Assets中管理大量Creative Cloud文件类型(如Photoshop和Illustrator)，并在生成完成的资产之前执行其自己的批准工作流。 可利用的功能：[已连接资产](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html?lang=en#overview-of-connected-assets) |
| 1个站点+ 1个站点 | 创建单独的项目:1个仅站点项目和1个仅站点项目 | 1个生产+1个阶段，1个开发<br>1个生产+1个阶段，1个开发 | 多租户站点实现。 多个站点拥有自己的发布计划和专门的开发和内容团队。 *常见示例*:两个零售品牌，设有专用网站和独立的开发团队 |


