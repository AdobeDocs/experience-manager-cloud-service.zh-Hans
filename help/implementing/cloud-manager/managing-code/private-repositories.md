---
title: 在 Cloud Manager 中添加专用存储库
description: 了解如何设置 Cloud Manager 以使用您自己的专用 GitHub 存储库。
exl-id: 5232bbf5-17a5-4567-add7-cffde531abda
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 77%

---

# 在 Cloud Manager 中添加专用存储库 {#private-repositories}

通过将 Cloud Manager 配置为使用您自己的专用 GitHub 存储库，您可以通过 Cloud Manager 直接在 GitHub 存储库中验证代码，而无需始终将代码与 Adobe 存储库同步。

>[!NOTE]
>
>此功能为公共 GitHub 所独有。不支持自托管 GitHub。

## 配置 {#configuration}

配置包含两个主要步骤：

1. [添加存储库](#add-repo)
1. [专用存储库所有权验证](#validate-ownership)

### 添加存储库 {#add-repo}

1. 在Cloud Manager中，从 **项目概述** 页面上，选择 **存储库** 制表符以切换到 **存储库** 页面并单击 **添加存储库**.

1. 在&#x200B;**添加存储库**&#x200B;对话框中，选择&#x200B;**专用存储库**&#x200B;作为存储库类型。

1. 提供您的存储库的详细信息

   * **存储库名称** - 一个富有表现力的名称
   * **存储库 URL** - 存储库的 URL，它必须以 `.git` 结尾
   * **描述**（可选）- 存储库的更详细描述（如有必要）

   ![添加自己的存储库](/help/implementing/cloud-manager/assets/repos/add-own-github.png)

1. 选择&#x200B;**保存**。

>[!TIP]
>
>有关在Cloud Manager中管理存储库的详细信息，请参阅 [Cloud Manager存储库](/help/implementing/cloud-manager/managing-code/managing-repositories.md).

### 专用存储库所有权验证 {#validate-ownership}

Cloud Manager 现已知道您的 GitHub 存储库，但它仍需要其访问权限。要授予访问权限，您需要安装 Adobe GitHub 应用程序并验证您是否拥有指定的存储库。

1. 添加您自己的存储库后， **私有存储库所有权验证** 对话框打开。

   ![专用存储库所有权验证](/help/implementing/cloud-manager/assets/repos/private-repo-validate.png)

1. Cloud Manager 使用 GitHub 应用程序与您的存储库安全地交互。
   * 您的 GitHub 组织的所有者必须安装位于 `https://github.com/apps/cloud-manager-for-aem` 的应用程序并授予对存储库的访问权限。
   * 有关如何完成此操作的详细信息，请参阅GitHub的文档。

1. 为了增强安全性，您必须在存储库的默认分支中创建秘密文件。选择 **生成**.

1. 通过点按或单击&#x200B;**确认**&#x200B;以确认秘密文件的生成。

   ![确认密码生成](/help/implementing/cloud-manager/assets/repos/confirm-generation.png)

1. 返回&#x200B;**专用存储库所有权验证**&#x200B;窗口中，Cloud Manager 已在&#x200B;**秘密文件内容**&#x200B;字段中生成私有文件内容。复制该字段中的内容。

   * 秘密文件的内容仅显示一次。如果在关闭此窗口之前未复制内容，请重新生成密码。

   ![复制秘密文件内容](/help/implementing/cloud-manager/assets/repos/new-secret.png)

1. 在 GitHub 存储库的默认分支中创建一个名为 `.well-known/adobe/cloud-manager-challenge` 的新文件，将秘密文件内容粘贴到该文件中并进行保存。

1. 安装应用程序且存储库中存在机密文件后，您可以选择 **验证** 在 **私有存储库所有权验证** 对话框。

可以按任意顺序安装应用程序并创建秘密文件。但必须先完成这两个步骤，之后才能进行验证。

在验证之前，存储库将以红色图标列出，表示它尚未验证且尚无法使用。

![未经验证的存储库](/help/implementing/cloud-manager/assets/repos/unvalidated-repo.png)

此 **类型** 列可以轻松识别Adobe提供的存储库(**Adobe**)和您自己的GitHub存储库(**GitHub**)。

如果您稍后需要返回到存储库以完成验证，请在 **存储库** 页面上，选择代表您刚刚添加的GitHub存储库的行中的省略号按钮，然后选择 **所有权验证** 从下拉菜单中。

## 将专用存储库与 Cloud Manager 结合使用 {#using}

在 Cloud Manager 中验证 GitHub 存储库后，便已完成集成，您可以在 Cloud Manager 中使用该存储库。

1. 在创建提取请求时，GitHub 检查将自动启动。

   ![GitHub 检查](/help/implementing/cloud-manager/assets/repos/github-checks.png)

1. 对于每个提取请求，将自动创建[全栈代码质量管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)。每次更新提取请求时，此管道将启动。

1. GitHub 检查保持正在运行状态，直到代码质量检查完成。之后，代码质量结果将传播到 GitHub 检查。

   ![GitHub 代码质量检查](/help/implementing/cloud-manager/assets/repos/github-code-quality.png)

在关闭或合并提取请求时，将自动删除创建的全栈代码质量管道。

>[!TIP]
>
>有关运行拉取请求检查时通过 GitHub 提供信息的详细信息，请参阅文档 [GitHub 检查批注](github-annotations.md)。

>[!TIP]
>
>您可以控制自动创建的管道，验证对专用存储库的每个拉取请求。请参阅文档 [GitHub 检查专用存储库的配置](github-check-config.md)，了解更多信息。

## 将私有存储库与管道关联 {#pipelines}

经过验证的专用存储库可以与[全栈和前端管道相关联](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)。

>[!NOTE]
>
>专用存储库不支持 Web 层和配置管道。

## 限制 {#limitations}

在 Cloud Manager 中使用专用存储库时会受到某些限制。

* 无法使用Cloud Manager中的GitHub检查暂停拉取请求验证。
   * 如果在 Cloud Manager 中验证 GitHub 存储库，则 Cloud Manager 将始终尝试验证为该存储库创建的提取请求。
* 如果从您的 GitHb 组织中删除 Adobe GitHub 应用程序，这将删除所有存储库的提取请求验证功能。
* 专用存储库不支持 Web 层和配置管道。
* 在生产全栈管道上使用专用存储库时，不会创建和推送任何 Git 标记。
* 当新的提交被推送到选定的分支时，使用专用存储库和提交构建触发器的管道不会自动启动。
* [工件重用功能](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse)不适用于专用存储库。
