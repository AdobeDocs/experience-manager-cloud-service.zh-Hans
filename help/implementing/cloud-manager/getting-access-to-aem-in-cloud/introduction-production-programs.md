---
title: '生产计划简介 '
description: 生产计划简介
exl-id: bb8d4a5a-b26a-4718-9327-149fedb87e6a
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---

# 生产计划简介 {#production-programs}

*生产*&#x200B;程序面向熟悉AEM和Cloud Manager的用户，该用户可以开始编写、构建和测试代码，以将代码部署到生产环境。

>[!NOTE]
>您将无法删除生产程序。

项目创建向导将根据用户在创建项目时的目标引导用户进行选择。 根据特定客户或组织可用的未使用的解决方案权限，用户可以控制如何将可用（未使用）的解决方案权限映射到Cloud Manager程序。

## 程序创建注意事项 {#program-creation-considerations}

下表介绍了在Cloud Manager中创建程序时要考虑的常见情况：

| 组织中提供的未使用的解决方案授权 | 创建程序选项 | 包含的内容 | 何时使用和其他注意事项 |
|--- |--- |--- |--- |
| 1个Sites解决方案 | 仅创建1个站点项目 | 1个生产+1个阶段，1个开发 | NA |
| 1个资产解决方案 | 仅创建1个资产程序 | 1个生产+1个阶段，1个开发 | NA |
| 1个站点+1个资产 | 创建一个程序：1个站点和资产计划 | 1个生产+1个阶段，2个开发 | 大多数数字资产都用于支持网站实施。 大多数数字资产处于已完成状态，可通过站点用于跨渠道体验。通常，由一个团队负责管理站点和资产的内容。 **常见示例**:主要用于网站的图像。PDF将通过内置于AEM Sites中的内部门户分发。 |
| 1个站点+1个资产 | 创建单独的程序：1个仅站点计划和1个仅资产计划 | 1个生产+1个阶段，1个开发<br> 1个生产+1个阶段，1个开发 | 许多数字资产不直接支持站点实施。 管理的资产处于各种状态，包括原始文件类型和正在进行的工作。 专门的创意团队通过其自身的生命周期管理数字资产，与Sites内容管理团队相比，他们的工作流程和发布周期也各不相同。 *常见示例*:照片拍摄中的原始图像会存储在Assets程序中，并且在Sites实施中只会使用少数几幅图像。大量Creative Cloud文件类型(如Photoshop和Illustrator)在AEM Assets中进行管理，并在生成完成的资产之前，先经过他们自己的审批工作流程。 要利用的功能：[连接的资产](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html?lang=en#overview-of-connected-assets) |
| 1个站点+ 1个站点 | 创建单独的程序：1个仅站点计划1个仅站点计划 | 1个生产+1个阶段，1个开发<br>1个生产+1个阶段，1个开发 | 多租户站点实施。 多个网站，有其各自的发行计划以及专门的开发和内容团队。 *常见示例*:两个零售品牌，具有专门的网站和独立的开发团队 |
