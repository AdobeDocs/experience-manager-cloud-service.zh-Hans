---
title: 在Cloud Manager中添加外部存储库（早期采用者）
description: 了解如何将外部存储库添加到Cloud Manager。 Cloud Manager支持与GitHub、GitLab和Bitbucket存储库集成。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 9cde6e63ec452161dbeb1e1bfb10c75f89e2692c
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 4%

---


# 在Cloud Manager中添加外部存储库 {#external-repositories}

了解如何将外部存储库添加到Cloud Manager。 Cloud Manager支持与GitHub、GitLab和Bitbucket存储库集成。

>[!NOTE]
>
>此功能仅适用于[早期采用计划](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)。

## 配置外部存储库

Cloud Manager中外部存储库的配置包括三个步骤：

1. [将外部存储库](#add-external-repo)添加到所选程序。
1. 提供对外部存储库的访问令牌。
1. 验证私有GitHub存储库的所有权。


## 添加外部存储库 {#add-ext-repo}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择要将外部存储库链接到的程序。

1. 在侧菜单的&#x200B;**服务**&#x200B;下，选择![文件夹图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **存储库**。

   ![存储库页面](/help/implementing/cloud-manager/managing-code/assets/repositories-tab.png)

1. 在&#x200B;**存储库**&#x200B;页面的右上角附近，单击&#x200B;**添加存储库**。

1. 在&#x200B;**添加存储库**&#x200B;对话框中，选择&#x200B;**专用存储库**&#x200B;以将外部Git存储库链接到您的项目。

   ![添加自己的存储库](/help/implementing/cloud-manager/managing-code/assets/repositories-private-repo-type.png)

1. 在每个相应的字段中，提供有关存储库的以下详细信息：

   | 字段 | 描述 |
   | --- | --- |
   | **存储库名称** | 必需。 新存储库的表示性名称。 |
   | **存储库URL** | 必需。 存储库的URL。<br><br>如果您使用的是GitHub托管的存储库，则路径必须以`.git`结尾。<br>例如，*`https://github.com/org-name/repo-name.git`* （URL路径仅供说明之用）。<br><br>如果您使用的是外部存储库，则必须使用以下URL路径格式：<br>`https://git-vendor-name.com/org-name/repo-name.git`<br>或<br>`https://self-hosted-domain/org-name/repo-name.git`<br>并且与您的Git供应商匹配。 |
   | S **选择存储库类型** | 必需。 选择您正在使用的存储库类型： **GitHub**、**GitLab**&#x200B;或&#x200B;**BitBucket**。 如果上述存储库URL路径包含Git供应商名称（如GitLab或Bitbucket），则已为您预先选择存储库类型。 |
   | **描述** | 可选。 存储库的详细说明。 |

1. 选择&#x200B;**保存**&#x200B;以添加存储库。

1. 在&#x200B;**私有存储库所有权验证**&#x200B;对话框中，提供访问令牌以验证外部存储库的所有权，以便您可以访问它。

   ![选择存储库的现有访问令牌](/help/implementing/cloud-manager/managing-code/assets/repositories-exisiting-access-token.png)
   *为BitBucket存储库选择现有的访问令牌。*

   | 令牌类型 | 描述 |
   | --- | --- |
   | **使用现有的访问令牌** | 如果您已经为您的组织提供了存储库访问令牌，并且有权访问多个存储库，则可以选择现有令牌。 使用&#x200B;**令牌名称**&#x200B;下拉列表选择要应用于存储库的令牌。 否则，请添加新访问令牌。 |
   | **添加新的访问令牌** | **存储库类型：GitHub**<br>·在&#x200B;**令牌名称**&#x200B;文本字段中，键入您创建的访问令牌的名称。<br>·按照[GitHub文档](https://docs.github.com/en/enterprise-server@3.14/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)中的说明创建个人访问令牌。<br>·所需的权限：<br>  · `Read access to metadata`。<br>  · `Read and write access to code and pull requests`。<br>·在&#x200B;**访问令牌**&#x200B;字段中，粘贴您刚刚创建的令牌。 |
   |  | **存储库类型： GitLab**<br>·在&#x200B;**令牌名称**&#x200B;文本字段中，键入您创建的访问令牌的名称。<br>·按照[GitLab文档](https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html)中的说明创建个人访问令牌。<br>·所需的权限：<br>  · `api`<br>  · `read_api`<br>  · `read_repository`<br>  · `write_repository`<br>·在&#x200B;**访问令牌**&#x200B;字段中，粘贴您刚刚创建的令牌。 |
   |  | **存储库类型： Bitbucket**<br>·在&#x200B;**令牌名称**&#x200B;文本字段中，键入您创建的访问令牌的名称。<br>·使用[Bitbucket文档](https://support.atlassian.com/bitbucket-cloud/docs/create-a-repository-access-token/)创建存储库访问令牌。<br>·所需的权限：<br>  · `Read and write access to code and pull requests`。 |

   >[!NOTE]
   >
   >功能&#x200B;**添加新访问令牌**&#x200B;当前处于早期采用者阶段。 正在计划其他功能。 因此，访问令牌所需的权限可能会发生更改。 此外，可以更新用于管理令牌的用户界面，可能包括令牌过期日期等功能。 此外，还会自动检查以确保链接到存储库的令牌保持有效。

1. 单击&#x200B;**验证**。

验证后，外部存储库即可使用并链接到管道。

## 将经过验证的外部存储库链接到管道 {#validate-ext-repo}

1. 添加或编辑管道：
   * [添加生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)
   * [添加非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)
   * [编辑管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#editing-pipelines)

   ![管道的源代码存储库和Git分支](/help/implementing/cloud-manager/managing-code/assets/pipeline-repo-gitbranch.png)
   *添加非生产管道对话框，其中包含选定的存储库和Git分支，*

1. 添加或编辑管道时，要为新管道或现有管道指定&#x200B;**Source代码**&#x200B;位置，请从&#x200B;**存储库**&#x200B;下拉列表中选择要使用的外部存储库。

1. 在&#x200B;**Git分支**&#x200B;下拉列表中，选择分支作为管道的源。

1. 单击&#x200B;**保存**。


>[!TIP]
>
>有关在 Cloud Manager 中管理存储库的详细信息，请参阅 [Cloud Manager 存储库](/help/implementing/cloud-manager/managing-code/managing-repositories.md)。


## 限制

* 外部存储库无法链接到配置管道。
* 使用外部存储库（不包括GitHub托管存储库）和&#x200B;**部署触发器**&#x200B;选项&#x200B;[!UICONTROL **的管道（在Git更改上**]）不会自动启动触发器。 必须手动启动它们。




