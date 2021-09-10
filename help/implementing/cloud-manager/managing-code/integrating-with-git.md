---
title: 与Git集成
description: 与Git集成 — Cloud Services
exl-id: 57e71b8a-4546-4d7f-825c-a1637d08e608
source-git-commit: 21669a29fbfd1072b637f407f5220825c4d1edbb
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 2%

---

# 将 Git 与 Adobe Cloud Manager 集成 {#git-integration}

AdobeCloud Manager配置了单个git存储库，该存储库用于使用Cloud Manager的CI/CD管道部署代码。 客户可以开箱即用地使用Cloud Manager的git存储库。 客户还可以选择将内部部署或&#x200B;**customer-managed** git存储库与Cloud Manager集成。

## Git集成概述 {#git-integration-overview}

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

本视频系列探讨了在将客户管理的git存储库与Cloud Manager集成时的几个用例，包括：

* [初始同步](#initial-sync)
* [基本分支策略](#branching-strategy)
* [功能分支开发](#feature-development)
* [生产部署](#production-deployment)
* [同步发行标记](#sync-tags)

该视频系列假定了有关git和源代码管理的基本知识。 有关git的更多详细信息，请参阅下面的[其他资源](#additional-resources)。

>[!NOTE]
>
>此视频系列中概述的步骤和命名约定体现了使用客户管理的git存储库和Cloud Manager的一些最佳实践。 预计所描述的公约和工作流程将适合各个开发小组。

## 初始同步 {#initial-sync}

将客户管理的Git存储库与Cloud Manager的Git存储库同步的首要步骤。

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## 基本分支策略 {#branching-strategy}

请观看以下视频，了解基本的分支策略。

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## 功能分支开发 {#feature-development}

使用功能分支可隔离客户管理的git存储库中的代码更改，并与Cloud Manager的git存储库同步，以便使用非生产管道进行代码质量和验证测试。

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## 生产部署 {#production-deployment}

在客户管理的git存储库中为生产版本准备代码，并与Cloud Manager的git存储库同步，以便部署到暂存和生产环境。

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## 同步发行标记 {#sync-tags}

将Cloud Manager git存储库中的发行标记同步到客户管理的git存储库中，以便提供有关已部署到暂存和生产环境的代码的可见性。

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## 其他资源 {#additional-resources}

* [GitHub资源](https://try.github.io)
* [Atlassian GitTutorials](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git备忘单](https://education.github.com/git-cheat-sheet-education.pdf)
