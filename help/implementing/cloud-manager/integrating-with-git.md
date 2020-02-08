---
title: 与Git集成
description: 与Git集成——云服务
translation-type: tm+mt
source-git-commit: 57206e36725e28051b2468d47da726e318bd763b

---


# 将Git与Adobe Cloud Manager集成 {#git-integration}

Adobe Cloud Manager提供了单个git存储库，用于使用Cloud Manager的CI/CD管道部署代码。 客户可以立即使用Cloud Manager的git存储库。 客户还可以选择将内部部署或客户管 **理的** Git存储库与Cloud manager集成。

## Git集成概述 {#git-integration-overview}

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

此视频系列探讨了在将客户管理的Git存储库与Cloud manager集成时的几个使用案例，包括：

* [初始同步](#initial-sync)
* [基本分支策略](#branching-strategy)
* [功能分支开发](#feature-development)
* [生产部署](#production-deployment)
* [同步发行标记](#sync-tags)

该视频系列假设您对git和源代码控制管理有基本的了解。 有关git的 [更多详细信息](#additional-resources) ，请参阅以下资源。

>[!NOTE]
>
> 此视频系列中概述的步骤和命名约定代表了使用客户管理的Git存储库和Cloud Manager的一些最佳实践。 预计所描述的公约和工作流程将适用于个别开发小组。

## 初始同步 {#initial-sync}

将客户管理的Git存储库与Cloud Manager的Git存储库同步的最初步骤。

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## 基本分支策略 {#branching-strategy}

请观看以下视频，了解基本的分支策略。

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## 功能分支开发 {#feature-development}

使用功能分支隔离客户管理的git存储库中的代码更改并与Cloud Manager的git存储库同步，以便使用非生产渠道进行代码质量和验证测试。

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## 生产部署 {#production-deployment}

在客户管理的git存储库中为生产版本准备代码，并与Cloud Manager的git存储库同步，以便部署到舞台和生产环境。

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## 同步发行标记 {#sync-tags}

将Cloud Manager Git存储库中的发行标记同步到客户管理的git存储库中，以便查看已部署到舞台和生产环境的代码。

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## 其他资源 {#additional-resources}

* [GitHub资源](https://try.github.io)
* [Atlassian Git教程](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git备忘单](https://education.github.com/git-cheat-sheet-education.pdf)