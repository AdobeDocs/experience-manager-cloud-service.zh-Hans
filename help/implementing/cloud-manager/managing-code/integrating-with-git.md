---
title: 在Cloud Manager中使用Git
description: 了解如何使用Cloud Manager的git存储库，以及如何将您自己的内部部署客户管理的git存储库与Cloud Manager集成。
exl-id: 57e71b8a-4546-4d7f-825c-a1637d08e608
source-git-commit: a9303c659730022b7417fc9082dedd26d7cbccca
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# 在Cloud Manager中使用Git {#git-integration}

AdobeCloud Manager配置了单个git存储库，该存储库用于使用Cloud Manager的CI/CD管道部署代码。

您可以开箱即用地使用Cloud Manager的git存储库，但也可以选择将客户管理的git存储库与Cloud Manager集成。

## Git集成概述 {#git-integration-overview}

本视频系列探讨了在将客户管理的git存储库与Cloud Manager集成时的几个用例，包括：

* [初始同步](#initial-sync)
* [基本分支策略](#branching-strategy)
* [功能分支开发](#feature-development)
* [生产部署](#production-deployment)
* [同步发行标记](#sync-tags)

该视频系列假定了有关git和源代码管理的基本知识。 请参阅 [下文](#additional-resources) 有关git的更多详细信息。

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

此视频系列中概述的步骤和命名约定体现了在Cloud Manager中使用客户管理的git存储库的一些最佳实践。 预计所描述的惯例和工作流会适合单个用例。

## 初始同步 {#initial-sync}

在此视频中，了解将客户管理的Git存储库与Cloud Manager的Git存储库同步的首要步骤。

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## 基本分支策略 {#branching-strategy}

在此视频中，了解基本的分支策略。

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## 功能分支开发 {#feature-development}

使用功能分支可隔离客户管理的git存储库中的代码更改，并与Cloud Manager的git存储库同步，以便使用非生产管道进行代码质量和验证测试。

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## 生产部署 {#production-deployment}

在客户管理的git存储库中为生产版本准备代码，并与Cloud Manager的git存储库同步，以便部署到暂存和生产环境。

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## 同步发行标记 {#sync-tags}

将Cloud Manager git存储库中的发行标记同步到客户管理的git存储库中，以便提供已部署到暂存和生产环境的代码的可见性。

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## 其他资源 {#additional-resources}

* [GitHub资源](https://try.github.io)
* [Atlassian GitTutorials](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git备忘单](https://education.github.com/git-cheat-sheet-education.pdf)
