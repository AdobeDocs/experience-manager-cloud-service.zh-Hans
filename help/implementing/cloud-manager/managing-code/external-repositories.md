---
title: 在Cloud Manager中添加外部存储库
description: 了解如何将外部存储库添加到 Cloud Manager。Cloud Manager支持与GitHub Enterprise、GitLab、Bitbucket和Azure DevOps存储库集成。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="私人测试版" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md网站#gitlab-bitbucket"
exl-id: aebda813-2eb0-4c67-8353-6f8c7c72656c
source-git-commit: 54f86f7bc204c6171fb031ecb94dd3da0379dacf
workflow-type: tm+mt
source-wordcount: '2298'
ht-degree: 28%

---

# 在 Cloud Manager 中添加外部存储库 {#external-repositories}

了解如何将外部存储库添加到 Cloud Manager。Cloud Manager支持与GitHub Enterprise、GitLab和Bitbucket存储库集成。

客户现在还可以将其Azure DevOps Git存储库载入到Cloud Manager中，并支持现代Azure DevOps和旧版VSTS (Visual Studio Team Services)存储库。

* Edge Delivery Services 用户可以使用已加入的存储库来同步和部署网站代码。
* 对于 AEM as a Cloud Service 和 Adobe Managed Services (AMS) 用户，该存储库可以链接到全栈和前端两种管道。

>[!NOTE]
>
>本文中介绍的功能只能通过私有Beta版计划获得。 有关更多详细信息以及注册私人测试版，请参阅[自带Git](/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket)。


## 配置外部存储库

在Cloud Manager中配置外部存储库包括以下步骤：

1. [将外部存储库](#add-external-repo)添加到所选程序
1. [将经过验证的外部存储库链接到管道](#validate-ext-repo)
   <!-- 1. Provide an access token to the external repository.
    1. Validate ownership of the private GitHub repository. -->
1. [将webhook](#configure-webhook)配置为外部存储库。


## 添加一个外部存储库 {#add-ext-repo}

>[!NOTE]
>
>外部存储库无法链接到配置管道。

<!-- THIS BULLET REMOVED AS PER https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2024.12.0+Release. THEY CAN NOW START AUTOMATICALLY>
* Pipelines using external repositories (excluding GitHub-hosted repositories) and the **Deployment Trigger** option [!UICONTROL **On Git Changes**], triggers are not automatically started. They must be manually started. -->


1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择要将外部存储库链接到的程序。

1. 在侧菜单的&#x200B;**程序**&#x200B;下，单击![文件夹大纲图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_FolderOutline_18_N.svg) **存储库**。

   ![存储库页面](/help/implementing/cloud-manager/managing-code/assets/repositories-tab.png)

1. 在&#x200B;**存储库**&#x200B;页面的右上角附近，点击&#x200B;**添加存储库**。

1. 在&#x200B;**添加存储库**&#x200B;对话框中，选择&#x200B;**专用存储库**，将外部 Git 存储库链接到您的程序。

   ![添加自己的存储库](/help/implementing/cloud-manager/managing-code/assets/repositories-private-repo-type.png)

1. 在每个相应的字段中，提供有关存储库的以下详细信息：

   | 字段 | 描述 |
   | --- | --- |
   | **存储库名称** | 必需。为您的新存储库取一个富有表现力的名称。 |
   | **存储库 URL** | 必需。存储库的 URL。<br><br>如果您使用的是GitHub托管的存储库，则路径必须以`.git`结尾。<br>例如，*`https://github.com/org-name/repo-name.git`*（URL 路径仅用于说明目的）。<br><br>如果您使用外部存储库，则必须使用以下 URL 路径格式：<br>`https://git-vendor-name.com/org-name/repo-name.git`<br> 或 <br>`https://self-hosted-domain/org-name/repo-name.git`<br>，并与您的 Git 供应商匹配。 |
   | **选择存储库类型** | 必需。选择您正在使用的存储库类型。 如果存储库URL路径包含Git供应商名称（如GitLab或Bitbucket），则已为您预先选择存储库类型。: <ul><li>**GitHub**（GitHub Enterprise和GitHub的自托管版本）</li><li>**GitLab**（`gitlab.com`和GitLab的自托管版本） </li><li>支持&#x200B;**Bitbucket**（仅`bitbucket.org` — 云版本）。 Bitbucket的自托管版本从2024年2月15日开始被弃用。)</li><li>**Azure DevOps** (`dev.azure.com`) </ul> |
   | **描述** | 可选。存储库的详细描述。 |

1. 选择&#x200B;**保存**&#x200B;以添加存储库。

   现在，提供访问令牌以验证外部存储库的所有权。

1. 在&#x200B;**私有存储库所有权验证**&#x200B;对话框中，提供用于验证外部存储库所有权的访问令牌，以便您能够访问它，然后单击&#x200B;**验证**。

   ![为存储库选择现有的访问令牌](/help/implementing/cloud-manager/managing-code/assets/repositories-exisiting-access-token.png)
   *为Bitbucket存储库选择现有的访问令牌（仅供说明）。*

>[!BEGINTABS]

>[!TAB GitHub企业版]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/github -->

| 访问令牌选项 | 描述 |
| --- | --- |
| **使用现有的访问令牌** | 如果您已经为贵组织提供了存储库访问令牌，并且有权访问多个存储库，则可以选择一个现有令牌。使用&#x200B;**令牌名称**&#x200B;下拉列表，选择要应用到存储库的令牌。否则，添加一个新的访问令牌。 |
| **添加新的访问令牌** | <ul><li> 在&#x200B;**令牌名称**&#x200B;文本字段中，键入要创建的访问令牌的名称。<li>按照[GitHub文档](https://docs.github.com/en/enterprise-server@3.14/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)中的说明创建个人访问令牌。<li>GitHub企业个人访问令牌(PAT)所需的权限<br>这些权限确保Cloud Manager可以验证拉取请求、管理提交状态检查以及访问必要的存储库详细信息。<br>在GitHub Enterprise中生成PAT时，请确保它包含以下存储库权限：<ul><li>拉取请求（读取和写入）<li>提交状态（读取和写入）<li>存储库元数据（只读）</li></li></ul></li></ul></ul></ul><ul><li>在&#x200B;**访问令牌**&#x200B;字段中，粘贴刚刚创建的令牌。 |

验证后，外部存储库即可使用并链接到管道。

另请参阅[管理访问令牌](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md)。

>[!TAB GitLab]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/gitlab -->

| 访问令牌选项 | 描述 |
| --- | --- |
| **使用现有的访问令牌** | 如果您已经为贵组织提供了存储库访问令牌，并且有权访问多个存储库，则可以选择一个现有令牌。使用&#x200B;**令牌名称**&#x200B;下拉列表，选择要应用到存储库的令牌。否则，添加一个新的访问令牌。 |
| **添加新的访问令牌** | <ul><li>在&#x200B;**令牌名称**&#x200B;文本字段中，键入要创建的访问令牌的名称。<li>按照[GitLab文档](https://docs.gitlab.com/user/profile/personal_access_tokens/)中的说明创建个人访问令牌。<li>GitLab个人访问令牌(PAT)所需的权限<br>这些范围允许Cloud Manager访问验证和webhook集成所需的存储库数据和用户信息。<br>在GitLab中生成PAT时，请确保它包括以下令牌范围：<ul><li>api<li>read_user</li></li></ul></li></li></ul></ul></ul><ul><li>在&#x200B;**访问令牌**&#x200B;字段中，粘贴刚刚创建的令牌。 |

验证后，外部存储库即可使用并链接到管道。

另请参阅[管理访问令牌](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md)。

>[!TAB 比特桶]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/bitbucket -->

| 访问令牌选项 | 描述 |
| --- | --- |
| **使用现有的访问令牌** | 如果您已经为贵组织提供了存储库访问令牌，并且有权访问多个存储库，则可以选择一个现有令牌。使用&#x200B;**令牌名称**&#x200B;下拉列表，选择要应用到存储库的令牌。否则，添加一个新的访问令牌。 |
| **添加新的访问令牌** | <ul><li>在&#x200B;**令牌名称**&#x200B;文本字段中，键入要创建的访问令牌的名称。<li>使用[Bitbucket文档](https://support.atlassian.com/bitbucket-cloud/docs/create-a-repository-access-token/)创建存储库访问令牌。<li>Bitbucket个人访问令牌(PAT)所需的权限<br>这些权限允许Cloud Manager访问存储库内容、管理拉取请求以及配置或响应webhook事件。<br>在Bitbucket中创建应用程序密码时，请确保它包含以下必需的应用程序密码权限：<ul><li>存储库（只读）<li>拉取请求（读取和写入）<li>Webhook（读写）</li></li></ul></li></li></ul></ul></ul><ul><li>在&#x200B;**访问令牌**&#x200B;字段中，粘贴刚刚创建的令牌。 |

验证后，外部存储库即可使用并链接到管道。

另请参阅[管理访问令牌](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md)。

>[!TAB Azure DevOps]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/azure_devops -->

| 访问令牌选项 | 描述 |
| --- | --- |
| **使用现有的访问令牌** | 如果您已经为贵组织提供了存储库访问令牌，并且有权访问多个存储库，则可以选择一个现有令牌。使用&#x200B;**令牌名称**&#x200B;下拉列表，选择要应用到存储库的令牌。否则，添加一个新的访问令牌。 |
| **添加新的访问令牌** | <ul><li>在&#x200B;**令牌名称**&#x200B;文本字段中，键入要创建的访问令牌的名称。<li>使用[Azure DevOps文档](https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate?view=azure-devops&tabs=Windows)创建存储库访问令牌。<li>Azure DevOps个人访问令牌(PAT)所需的权限。<br>这些权限允许Cloud Manager访问存储库内容、管理拉取请求以及配置或响应webhook事件。<br>当您在Azure DevOps中创建应用程序密码时，请确保它包含以下必需的应用密码权限：<ul><li>存储库（只读）</li></ul></li></li></ul></ul></ul><ul><li>在&#x200B;**访问令牌**&#x200B;字段中，粘贴刚刚创建的令牌。 |

验证后，外部存储库即可使用并链接到管道。

另请参阅[管理访问令牌](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md)。

>[!ENDTABS]


## 将经过验证的外部存储库链接到管道 {#validate-ext-repo}

1. 添加或编辑管道：
   * [添加生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)
   * [添加非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)
   * [编辑管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#editing-pipelines)

   <!-- Add an Edge Delivery Pipeline -->

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

对于已载入访问令牌的所有其他外部存储库 — 例如GitHub Enterprise、GitLab、Bitbucket和Azure DevOps - webhook配置可用，必须手动设置。

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
1. 导航到您的Git供应商解决方案（GitHub Enterprise、GitLab、Bitbucket或Azure DevOps）。

   有关webhook配置的所有详细信息以及每个供应商所需的事件均可在[添加外部存储库](#add-ext-repo)中获取。 在步骤8下，请参见选项卡表。

1. 找到解决方案的&#x200B;**Webhook**&#x200B;设置部分。
1. 将之前复制的Webhook URL粘贴到URL文本字段中。
   1. 将Webhook URL中的`api_key`查询参数替换为您自己的实际API密钥。

      要生成API密钥，您必须在Adobe Developer Console中创建集成项目。 有关完整详细信息，请参阅[创建API集成项目](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/)。

1. 将您之前复制的Webhook密码粘贴到&#x200B;**密码**（或&#x200B;**密钥**，或&#x200B;**密码令牌**）文本字段中。
1. 配置webhook以发送Cloud Manager所需的事件。 使用下表确定Git提供商的正确事件。

>[!BEGINTABS]

>[!TAB GitHub企业版]

<!-->
https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-venders/github —>

| 必需的webhook事件 |
| --- |
| 这些事件允许Cloud Manager响应GitHub活动，例如拉取请求验证、管道的基于推送的触发器或Edge Delivery Services代码同步。<br>确保将webhook设置为在下列必需的webhook事件上触发：<ul><li>拉取请求<li>推送<li>问题评论</li></li></li></ul></ul></ul> |

>[!TAB GitLab]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/gitlab -->

| 必需的webhook事件 |
| --- |
| 这些webhook事件允许Cloud Manager在推送代码或提交合并请求时触发管道。 它们还跟踪与拉取请求验证相关的注释（通过注释事件）。<br>确保将webhook设置为在下列必需的webhook事件上触发<ul><li>推送事件<li>合并请求事件<li>注释事件</li></li></li></ul></ul></ul> |

>[!TAB 比特桶]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/bitbucket -->

| 必需的webhook事件 |
| --- |
| 这些事件可确保Cloud Manager能够验证拉取请求、响应代码推送并与注释交互以协调管道。<br>确保将webhook设置为在下列必需的webhook事件上触发<ul><li>拉取请求：已创建<li>拉取请求：已更新<li>拉取请求：已合并<li>拉取请求：评论<li>存储库：推送</li></li></li></ul></ul></ul> |

>[!TAB Azure DevOps]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/azure_devops -->

| 必需的webhook事件 |
| --- |
| 这些事件可确保Cloud Manager能够验证拉取请求、响应代码推送并与注释交互以协调管道。<br>确保将webhook设置为在下列必需的webhook事件上触发<ul><li>存储库：推送</li></li></ul></ul></ul> |

>[!ENDTABS]


### 使用Webhook验证拉取请求

正确配置Webhook后，Cloud Manager会自动触发对存储库的管道执行或PR验证检查。

具体行为因您使用的Git提供商而异，如下所述。

>[!BEGINTABS]


>[!TAB GitHub企业版]

<!-->
https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-venders/github —>

创建检查后，它类似于下面的屏幕快照。 与`GitHub.com`的主要区别在于`GitHub.com`使用检查运行，而GitHub Enterprise（使用个人访问令牌）生成提交状态：

![提交状态以指示GitHub Enterprise上的PR验证过程](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-github-pr-validation.png)


>[!TAB GitLab]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/gitlab -->

GitLab交互仅依赖于评论。 验证开始时，将添加注释。 验证完成（无论成功还是失败）后，将移除初始注释，并替换为包含验证结果或错误详细信息的新注释。

运行代码质量验证时：

![运行代码质量验证时](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab1.png)

完成冷质量验证时：

![冷质量验证完成后](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab2.png)

当代码质量验证失败并出现错误时：

![当代码质量验证失败并出现错误](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab3.png)时

当代码质量验证因客户问题而失败时：

![当代码质量验证因客户问题而失败时](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab4.png)


>[!TAB 比特桶]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/bitbucket -->

运行代码质量验证时：

正在运行代码质量验证时的![状态](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-bitbucket1.png)

使用提交状态来跟踪PR验证进度。 在以下示例中，屏幕截图显示了当代码质量验证因客户问题而失败时将发生的情况。 添加带有详细错误信息的注释，并创建提交检查，其中显示故障（在右侧可见）：

Bitbucket的![拉取请求验证状态](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-bitbucket2.png)



>[!ENDTABS]


## webhook问题疑难解答

* 确保Webhook URL包含有效的API密钥。
* 检查是否在Git供应商设置中正确配置了webhook事件。
* 如果PR验证或管道触发器不起作用，请验证Cloud Manager和Git供应商中的Webhook密码是否为最新。


