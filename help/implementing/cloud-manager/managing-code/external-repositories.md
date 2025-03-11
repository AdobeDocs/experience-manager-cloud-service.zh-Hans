---
title: 在Cloud Manager — 有限测试版中添加外部存储库
description: 了解如何将外部存储库添加到 Cloud Manager。Cloud Manager支持与GitHub Enterprise Server、GitLab和Bitbucket存储库集成。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: aebda813-2eb0-4c67-8353-6f8c7c72656c
source-git-commit: 7ce39020870943243e2d48aa66370f2cca9c2ac0
workflow-type: tm+mt
source-wordcount: '1618'
ht-degree: 37%

---

# 在Cloud Manager — 有限测试版中添加外部存储库 {#external-repositories}

了解如何将外部存储库添加到 Cloud Manager。Cloud Manager支持与GitHub Enterprise Server、GitLab和Bitbucket存储库集成。

>[!NOTE]
>
>此功能仅通过早期采用计划提供。 有关更多详细信息，以及要注册为早期采用者，请参阅[自带Git — 现在支持GitLab和Bitbucket](/help/implementing/cloud-manager/release-notes/2024/2024-10-0.md#gitlab-bitbucket)。

## 配置外部存储库

在 Cloud Manager 中配置外部存储库包括三个步骤：

1. [将外部存储库 ](#add-external-repo) 添加到选择的程序。
1. 向外部存储库提供访问令牌。
1. 验证私有GitHub存储库的所有权。



## 添加一个外部存储库 {#add-ext-repo}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择要将外部存储库链接到的程序。

1. 在侧菜单的&#x200B;**服务**&#x200B;下，单击![文件夹大纲图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_FolderOutline_18_N.svg) **存储库**。

   ![存储库页面](/help/implementing/cloud-manager/managing-code/assets/repositories-tab.png)

1. 在&#x200B;**存储库**&#x200B;页面的右上角附近，点击&#x200B;**添加存储库**。

1. 在&#x200B;**添加存储库**&#x200B;对话框中，选择&#x200B;**专用存储库**，将外部 Git 存储库链接到您的程序。

   ![添加自己的存储库](/help/implementing/cloud-manager/managing-code/assets/repositories-private-repo-type.png)

1. 在每个相应的字段中，提供有关存储库的以下详细信息：

   | 字段 | 描述 |
   | --- | --- |
   | **存储库名称** | 必需。为您的新存储库取一个富有表现力的名称。 |
   | **存储库 URL** | 必需。存储库的 URL。<br><br>如果您使用的是GitHub托管的存储库，则路径必须以`.git`结尾。<br>例如，*`https://github.com/org-name/repo-name.git`*（URL 路径仅用于说明目的）。<br><br>如果您使用外部存储库，则必须使用以下 URL 路径格式：<br>`https://git-vendor-name.com/org-name/repo-name.git`<br> 或 <br>`https://self-hosted-domain/org-name/repo-name.git`<br>，并与您的 Git 供应商匹配。 |
   | **选择存储库类型** | 必需。选择正在使用的存储库类型：<ul><li>**GitHub**（GitHub企业服务器和GitHub的自托管版本）</li><li>**GitLab**（`gitlab.com`和GitLab的自托管版本） </li><li>**Bitbucket**（`bitbucket.org`和Bitbucket Server，以及Bitbucket的自托管版本）</li></ul>如果上面的存储库 URL 路径包含 Git 供应商名称，例如 GitLab 或 Bitbucket，则存储库类型已为您预先选择。 |
   | **描述** | 可选。存储库的详细描述。 |

1. 选择&#x200B;**保存**&#x200B;以添加存储库。

1. 在&#x200B;**专用存储库所有权验证**&#x200B;对话框中，提供访问令牌来验证外部存储库的所有权，以便您可以访问它。

   ![为存储库选择现有的访问令牌](/help/implementing/cloud-manager/managing-code/assets/repositories-exisiting-access-token.png)
   *为Bitbucket存储库选择现有的访问令牌。*

   | 令牌类型 | 描述 |
   | --- | --- |
   | **使用现有的访问令牌** | 如果您已经为贵组织提供了存储库访问令牌，并且有权访问多个存储库，则可以选择一个现有令牌。使用&#x200B;**令牌名称**&#x200B;下拉列表，选择要应用到存储库的令牌。否则，添加一个新的访问令牌。 |
   | **添加新的访问令牌** | **存储库类型：GitHub**<br>• 在&#x200B;**令牌名称**&#x200B;文本字段中，键入您正在创建的访问令牌的名称。<br>• 按照 [GitHub 文档](https://docs.github.com/en/enterprise-server@3.14/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)中的说明创建个人访问令牌。<br>·有关所需权限，请参阅以下信息： ![为GitHub创建新PAT](/help/implementing/cloud-manager/managing-code/assets/webhook-github-enterprise-server.png)<br>·在&#x200B;**访问令牌**&#x200B;字段中，粘贴您刚刚创建的令牌。 |
   |  | **存储库类型：GitLab**<br>• 在&#x200B;**令牌名称**&#x200B;文本字段中，键入您正在创建的访问令牌的名称。<br>• 按照 [GitLab 文档](https://docs.gitlab.com/user/profile/personal_access_tokens/)中的说明创建个人访问令牌。<br>·有关所需权限，请参阅以下信息： ![为GitLab创建新的PAT](/help/implementing/cloud-manager/managing-code/assets/webhook-gitlab.png)<br>·在&#x200B;**访问令牌**&#x200B;字段中，粘贴刚刚创建的令牌。 |
   |  | **存储库类型：Bitbucket**<br>• 在&#x200B;**令牌名称**&#x200B;文本字段中，键入您正在创建的访问令牌的名称。<br>• 使用 [Bitbucket 文档](https://support.atlassian.com/bitbucket-cloud/docs/create-a-repository-access-token/)创建存储库访问令牌。<br>·有关所需权限，请参阅以下信息![为Bitbucket创建新PAT](/help/implementing/cloud-manager/managing-code/assets/webhook-bitbucket.png)。 |

   >[!NOTE]
   >
   >**添加新的访问令牌**&#x200B;功能目前处于早期采用者阶段。正在规划其他功能。因此，访问令牌所需的权限可能会发生更改。此外，用于管理令牌的用户界面（包括令牌有效期限等功能）可能会被更新。而且，还将进行自动检查，以确保与存储库链接的令牌保持有效。

1. 点击&#x200B;**验证**。

验证后，外部存储库即可使用并链接到管道。

## 将经过验证的外部存储库链接到管道 {#validate-ext-repo}

1. 添加或编辑管道：
   * [添加生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)
   * [添加非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)
   * [编辑管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#editing-pipelines)

   ![管道的源代码存储库和 Git 分支](/help/implementing/cloud-manager/managing-code/assets/pipeline-repo-gitbranch.png)
   *添加非生产管道对话框，其中包含选择的存储库和 Git 分支，*

1. 添加或编辑管道时，要指定新管道或现有管道的&#x200B;**源代码**&#x200B;位置，请从&#x200B;**存储库**&#x200B;下拉列表中选择要使用的外部存储库。

1. 在 **Git 分支**&#x200B;下拉列表中，选择该分支作为管道的源。

1. 单击&#x200B;**保存**。


>[!TIP]
>
>有关在 Cloud Manager 中管理存储库的详细信息，请参阅 [Cloud Manager 存储库](/help/implementing/cloud-manager/managing-code/managing-repositories.md)。

## 为外部存储库配置webhook {#configure-webhook}

Cloud Manager允许您为已添加的外部Git存储库配置webhook。 请参阅[添加外部存储库](#add-ext-repo)。 这些Webhook允许Cloud Manager接收与Git供应商解决方案中的其他操作相关的事件。

例如，Webhook允许Cloud Manager根据以下事件触发操作：

* 创建拉取请求(PR) — 启动PR验证功能。
* 推送事件 — 在“在Git上提交”触发器打开（启用）时启动管道。
* 未来基于评论的操作 — 允许工作流，例如直接从PR部署到快速开发环境(RDE)。

在`GitHub.com`上托管的存储库不需要Webhook配置，因为Cloud Manager直接通过GitHub应用程序集成。
对于已载入访问令牌的所有其他外部存储库（例如GitHub Enterprise Server、GitLab和Bitbucket），webhook配置可用，必须手动设置。

**要为外部存储库配置webhook：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择要为其配置外部Git存储库的webhook的程序。

1. 在页面左上角，单击![显示菜单图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以显示左侧菜单。

1. 在左侧菜单的&#x200B;**项目**&#x200B;标题下，单击![文件夹大纲图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_FolderOutline_18_N.svg) **存储库**。

1. 在&#x200B;**存储库**&#x200B;页面上，使用&#x200B;**类型**&#x200B;列引导您进行选择，找到所需的存储库，然后单击其旁边的![省略号 — 更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

   ![在下拉菜单中配置选定存储库的Webhook选项](/help/implementing/cloud-manager/managing-code/assets/repository-config-webhook.png)

1. 从下拉菜单中，单击&#x200B;**配置Webhook**。

   ![配置Webhook对话框](/help/implementing/cloud-manager/managing-code/assets/config-webhook.png)

1. 在&#x200B;**配置Webhook**&#x200B;对话框中，执行以下操作：

   1. 在&#x200B;**Webhook URL**&#x200B;字段旁边，单击![复制图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)。
将URL粘贴为纯文本文件。 您的Git供应商的Webhook设置需要复制的URL。
   1. 在&#x200B;**Webhook密码**&#x200B;令牌/密钥字段旁边，单击&#x200B;**生成**，然后单击![复制图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)。
将密码粘贴为纯文本文件。 您的Git供应商的Webhook设置需要复制的密钥。
1. 单击&#x200B;**关闭**。
1. 导航到您的Git供应商解决方案（GitHub Enterprise、GitLab或Bitbucket）。
1. 找到解决方案的&#x200B;**Webhook**&#x200B;设置部分。
1. 将之前复制的Webhook URL粘贴到URL文本字段中。
   1. 将Webhook URL中的`api_key`查询参数替换为您自己的实际API密钥。

      要生成API密钥，您必须在Adobe Developer Console中创建集成项目。 有关完整详细信息，请参阅[创建API集成项目](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/)。

1. 将您之前复制的Webhook密码粘贴到&#x200B;**密码**（或&#x200B;**密钥**，或&#x200B;**密码令牌**）文本字段中。
1. 配置webhook以发送Cloud Manager期望的适当事件。

   以下网页提供了有关webhook配置和每个供应商所需事件的所有详细信息：

   * [为GitHub Enterprise Server](https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-venders/create-new-github-pat？id=webhook-events)设置Webhook。
   * [为GitLab设置Webhook](https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-venders/create-new-gitlab-pat？id=webhook-events)。
   * [为Bitbucket](https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-venders/create-new-bitbucket-pat？id=webhook-events)设置Webhook。

### 使用Webhook验证拉取请求

正确配置Webhook后，Cloud Manager会自动触发对存储库的管道执行或PR验证检查。

以下行为适用：

* **GitHub企业服务器**

  创建检查后，它类似于下面的屏幕快照。 与`GitHub.com`的主要区别在于`GitHub.com`使用检查运行，而GitHub Enterprise Server（使用个人访问令牌）生成提交状态：

  ![提交状态以指示GitHub企业服务器上的PR验证过程](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-github-pr-validation.png)

* **比特桶**

  运行代码质量验证时：

  正在运行代码质量验证时的![状态](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-bitbucket1.png)

  使用提交状态来跟踪PR验证进度。 在以下示例中，屏幕截图显示了当代码质量验证因客户问题而失败时将发生的情况。 添加带有详细错误信息的注释，并创建提交检查，其中显示故障（在右侧可见）：

  Bitbucket的![拉取请求验证状态](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-bitbucket2.png)

* **GitLab**

  GitLab交互仅依赖于评论。 验证开始时，将添加注释。 验证完成（无论成功还是失败）后，将移除初始注释，并替换为包含验证结果或错误详细信息的新注释。

  运行代码质量验证时：

  ![运行代码质量验证时](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab1.png)

  完成冷质量验证时：

  ![冷质量验证完成后](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab2.png)

  当代码质量验证失败并出现错误时：

  ![当代码质量验证失败并出现错误](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab3.png)时

  当代码质量验证因客户问题而失败时：

  ![当代码质量验证因客户问题而失败时](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab4.png)


## webhook问题疑难解答

* 确保Webhook URL包含有效的API密钥。
* 检查是否在Git供应商设置中正确配置了webhook事件。
* 如果PR验证或管道触发器不起作用，请验证Cloud Manager和Git供应商中的Webhook密码是否为最新。








## 限制

* 外部存储库无法链接到配置管道。
* 具有外部存储库（未在GitHub上托管）和“在Git发生更改时”触发器的管道不会自动启动。 它们只能手动启动。


<!-- THIS BULLET REMOVED AS PER https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2024.12.0+Release. THEY CAN NOW START AUTOMATICALLY>
* Pipelines using external repositories (excluding GitHub-hosted repositories) and the **Deployment Trigger** option [!UICONTROL **On Git Changes**], triggers are not automatically started. They must be manually started. -->


