---
title: 生产程序简介
description: 了解什么是生产程序以及如何设置程序的建议。
exl-id: bb8d4a5a-b26a-4718-9327-149fedb87e6a
source-git-commit: a6152a1529b5c70bcf056857204e7ff97fc614e4
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 100%

---


# 生产程序简介 {#production-programs}

生产程序面向准备好开始编写、构建和测试代码的团队，目的是将其部署到托管实时流量。

[创建生产程序](creating-production-programs.md)后，[程序创建向导](using-the-wizard.md)将根据用户创建程序的目标指导用户进行选择。

## 项目创建选项 {#program-creation-options}

您与 Adobe 的合同协议定义了在创建生产程序时特定组织可用的解决方案的数量和类型。 您可以控制如何将可用解决方案映射到 Cloud Manager 程序。

下表描述了可用解决方案的常见场景以及基于这些场景创建的典型生产程序。

| 可用的解决方案 | 程序选项 | 包含的内容 | 使用时间 | 示例 |
|--- |--- |--- |--- |---|
| 1 个 Sites 解决方案 | 仅创建 1 个 Sites 程序 | 1 个生产 + 1 个暂存，1 个开发 | 不适用 | 不适用 |
| 1 个 Assets 解决方案 | 仅创建 1 个 Assets 程序 | 1 个生产 + 1 个暂存，1 个开发 | 不适用 | 不适用 |
| 1 Sites +1 Assets | 创建一个程序：<br>1 个 Sites 和 Assets 程序 | 1 个生产 + 1 个暂存，2 个开发 | 当大多数数字资产用于支持 Sites 实施时。<br>在这种情况下，大多数数字资产都处于完成状态，可以通过 Sites 进行跨渠道体验。<br>通常，一个团队负责管理 Sites 和 Assets 的内容。 | 主要用于网站的图像。<br>将通过 AEM Sites 内置的内部门户分发的 PDF。 |
| 1个站点+1个资产 | 创建单独的程序：<br>1 个仅限 Sites 的程序和 1 个仅限于Assets 的程序 | 1 个生产 + 1 个暂存，1 个开发<br>1 个生产 + 1 个暂存，1 个开发 | 当许多数字资产不直接支持 Sites 实施时。<br>在这种情况下，资产处于各种状态，包括原始文件类型和正在进行的工作。<br>一个专门的创意团队在其自身的生命周期中管理数字资产，并且与 Sites 内容管理团队相比，拥有单独的工作流程和发布周期。 | 照片拍摄的原始图像存储在 Assets 程序中，只有少数几个将用于 Sites 实施。<br>许多 Creative Cloud 文件类型，如 Photoshop 和 Illustrator，在 AEM Assets 中进行管理，并在生成成品资产之前通过其自己的审批工作流。<br>在这种情况下，请考虑使用[连接 Assets](/help/assets/use-assets-across-connected-assets-instances.md#overview-of-connected-assets) |
| 1 Sites + 1 Sites | 创建单独的程序：<br>1 个仅限 Sites 的程序和 1 个仅限于Sites 的程序 | 1 个生产 + 1 个暂存，1 个开发<br>1 个生产 + 1 个暂存，1 个开发 | 对于多租户 Sites 实施。<br>在这种情况下，必须管理多个站点，它们有自己的发布时间表和专门的开发和内容团队。 | 两个零售品牌，拥有专门的网站和独立的开发团队 |

>[!NOTE]
>
>生产程序[可以编辑，但无法删除](editing-programs.md)。
