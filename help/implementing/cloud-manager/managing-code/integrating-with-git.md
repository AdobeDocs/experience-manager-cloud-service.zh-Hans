---
title: 将Git用于Cloud Manager
description: 了解如何使用 Cloud Manager 的 Git 存储库，以及如何将您自己的本地客户管理的 Git 储存库与 Cloud Manager 集成。
exl-id: 57e71b8a-4546-4d7f-825c-a1637d08e608
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 80206fc1396896fe45e2c959c78a0bf30eba71c5
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 95%

---

# 将Git用于Cloud Manager {#git-integration}

Adobe Cloud Manager 附带了一个 Git 存储库，用于使用 Cloud Manager 的 CI/CD 管道部署代码。

您可以使用现成的 Cloud Manager 的 Git 存储库，但也可以选择将客户管理的 Git 存储库与 Cloud Manager 集成。

## Git 集成概述 {#git-integration-overview}

本视频系列探讨了将客户管理的 Git 存储库与 Cloud Manager 集成时的几个用例，包括：

* [初始同步](#initial-sync)
* [基本分支策略](#branching-strategy)
* [功能分支开发](#feature-development)
* [生产部署](#production-deployment)
* [同步版本标记](#sync-tags)

本视频系列假定您具有 Git 和源代码控制管理的基本知识。 有关 Git 的更多详细信息，请参阅[以下附加资源](#additional-resources)。

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

本视频系列中概述的步骤和命名惯例代表了有关使用 Cloud Manager 中客户管理的 Git 存储库一些最佳实践。预计所描述的惯例和工作流适用于各个用例。

## 初始同步 {#initial-sync}

在本视频中，了解将客户管理的 Git 存储库与 Cloud Manager 的 Git 存储库同步的第一步。

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## 基本分支策略 {#branching-strategy}

在本视频中，了解基本分支策略。

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## 功能分支开发 {#feature-development}

使用功能分支隔离客户管理的 Git 存储库中的代码更改，并与 Cloud Manager 的 Git 存储库同步，以便使用非生产管道进行代码质量和验证测试。

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## 生产部署 {#production-deployment}

在客户管理的 Git 存储库中为生产版本准备代码，并与 Cloud Manager 的 Git 存储库同步，以便部署到暂存和生产环境。

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## 同步版本标记 {#sync-tags}

将 Cloud Manager Git 存储库中的版本标记同步到客户管理的 Git 存储库中，以便公开已将哪些代码部署到暂存和生产环境。

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## 其他资源 {#additional-resources}

* [GitHub 资源](https://docs.github.com/en/get-started/getting-started-with-git/set-up-git)
* [Atlassian Git 教程](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git 备忘单](https://education.github.com/git-cheat-sheet-education.pdf)
