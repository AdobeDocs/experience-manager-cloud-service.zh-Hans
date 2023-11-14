---
title: Cloud Manager 存储库
description: 了解如何在 Cloud Manager 中创建、查看和删除 Git 存储库。
exl-id: 6e1cf636-78f5-4270-9a21-38b4d5e5a0b0
source-git-commit: af8ab1f741c658dcb47bdf0d37e403fcb180631a
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 96%

---


# Cloud Manager 存储库 {#cloud-manager-repos}

了解如何在 Cloud Manager 中创建、查看和删除 Git 存储库。

>[!NOTE]
>
>在任何给定公司或 IMS 组织的所有项目中，存储库的数量限制为 300 个。

## 添加和管理存储库 {#add-manage-repos}

按照以下步骤在 Cloud Manager 中查看和管理存储库。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 从 **项目概述** 页面，点按或单击 **存储库** 制表符以切换到 **存储库** 页面。

1. 单击 **添加存储库**.

   ![添加“存储库”按钮](/help/implementing/cloud-manager/assets/repos/create-repo2.png)

1. 输入请求的名称和描述，然后单击&#x200B;**保存**。

   ![添加“存储库”对话框](/help/implementing/cloud-manager/assets/repos/repo-1.png)

向导关闭时，您的新存储库会显示在表中。

您可以在表中选择存储库，然后单击省略号按钮，然后选择&#x200B;**复制存储库 URL**、**查看和更新**&#x200B;或&#x200B;**删除**。

![存储库选项](/help/implementing/cloud-manager/assets/repos/create-repo3.png)

在 Cloud Manager 中创建的存储库也可供您在添加或编辑管道时选择。 请参阅 [CI-CD 管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)，以了解更多信息。

任何给定的管道都有一个主存储库或分支。 通过 [Git 子模块支持](#git-submodule-support)，可以在构建时包括许多二级分支。

>[!NOTE]
>
>用户必须具有&#x200B;**部署管理员**&#x200B;或&#x200B;**业务负责人**&#x200B;角色才能添加存储库。

## 删除存储库 {#delete-repo}

删除存储库将：

* 使删除的存储库名称不可用于将来可能创建的新存储库。
   * 在这种情况下，会显示错误消息 `Repository name should be unique within organization.`。
* 使已删除的存储库在 Cloud Manager 中不可用，并且无法链接到管道。

按照这些步骤删除 Cloud Manager 中的存储库。

1. 从&#x200B;**项目概述**&#x200B;页面中，单击&#x200B;**存储库**&#x200B;选项卡，然后导航到&#x200B;**存储库**&#x200B;页面。

1. 选择存储库并单击省略号按钮，然后选择&#x200B;**删除**&#x200B;存储库。

   ![删除存储库](/help/implementing/cloud-manager/assets/repos/delete-repo.png)

## Git 子模块支持 {#git-submodule-support}

Git 子模块可用于在构建时跨 Git 存储库合并多个分支的内容。

Cloud Manager 的构建流程执行期间，在克隆为管道配置的存储库并签出配置的分支后，如果该分支在根目录中包含 `.gitmodules` 文件，则执行此命令。

以下命令将把每个子模块签出到适当的目录中。

```
$ git submodule update --init
```

这项技术是文档[使用多源 Git 存储库](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md)中所述解决方案的潜在替代方案，适用于习惯使用 Git 子模块且不想管理外部合并过程。

例如，假设有三个存储库，每个存储库均包含一个名为 `main` 的分支。 在“主”存储库（即，在管道中配置的存储库）中，`main` 分支包含一个 `pom.xml` 文件，声明其他两个存储库所包含的项目。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
   
    <groupId>customer.group.id</groupId>
    <artifactId>customer-reactor</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>pom</packaging>
   
    <modules>
        <module>project-a</module>
        <module>project-b</module>
    </modules>
   
</project>
```

之后，您将为其他两个存储库添加子模块。

```shell
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

这会导致 `.gitmodules` 文件类似于以下内容。

```text
[submodule "project-a"]
    path = project-a
    url = https://git.cloudmanager.adobe.com/ProgramName/projectA/
    branch = main
[submodule "project-b"]
    path = project-b
    url = https://git.cloudmanager.adobe.com/ProgramName/projectB/
    branch = main
```

可以在 [Git 参考手册](https://git-scm.com/book/en/v2/Git-Tools-Submodules)中找到有关 Git 子模块的更多信息。

### 限制和建议 {#limitations-recommendations}

使用 Git 子模块时，请注意以下限制。

* Git URL 必须完全遵循上一节所述语法。
* 仅支持分支的根目录中的子模块。
* 为安全起见，请勿在 Git URL 中嵌入凭据。
* 除非另有必要，否则强烈建议使用“浅”子模块。
   * 为此，请为每个子模块运行 `git config -f .gitmodules submodule.<submodule path>.shallow true`。
* Git 子模块引用将存储到特定的 git 承诺中。 因此，在对子模块存储库进行更改时，需要更新引用的承诺。
   * 例如，通过使用 `git submodule update --remote`
