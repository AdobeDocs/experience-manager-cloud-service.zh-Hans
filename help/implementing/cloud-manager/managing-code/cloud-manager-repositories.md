---
title: Cloud Manager存储库
description: 了解如何在Cloud Manager中创建、查看和删除git存储库。
exl-id: 6e1cf636-78f5-4270-9a21-38b4d5e5a0b0
source-git-commit: 6cf164093cc543fe4847859b248e70efd86efbb1
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---


# Cloud Manager存储库 {#cloud-manager-repos}

了解如何在Cloud Manager中创建、查看和删除git存储库。

>[!NOTE]
>
>任何给定公司或IMS组织中所有程序中的存储库数量限制为300个。

## 添加和管理存储库 {#add-manage-repos}

按照这些步骤在Cloud Manager中查看和管理存储库。

1. 从 **计划概述** 页面，单击 **存储库** 选项卡，然后导航到 **存储库** 页面。

1. 单击 **添加存储库** 来启动向导。

   ![“添加存储库”按钮](/help/implementing/cloud-manager/assets/repos/create-repo2.png)

1. 根据请求输入名称和描述，然后单击 **保存**.

   ![“添加存储库”对话框](/help/implementing/cloud-manager/assets/repos/repo-1.png)

当向导关闭时，您的新存储库将显示在表中。

您可以选择表中的存储库，然后单击省略号按钮并选择 **复制存储库URL**, **查看和更新**&#x200B;或 **删除**.

![存储库选项](/help/implementing/cloud-manager/assets/repos/create-repo3.png)

在Cloud Manager中创建的存储库也将可供您在添加或编辑管道时选择。 请参阅该文档 [CI-CD管线](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 以了解更多。

任何给定管道都有一个主存储库或分支。 使用 [git子模块支持](#git-submodule-support)，在生成时可以包含许多辅助分支。

>[!NOTE]
>
>用户必须具有角色 **部署管理器** 或 **业务所有者** 以添加存储库。

## 删除存储库 {#delete-repo}

删除存储库将：

* 使已删除的存储库名称对将来可能创建的新存储库不可用。
   * 错误消息 `Repository name should be unique within organization.` 中的“隐藏主体”。
* 使已删除的存储库在Cloud Manager中不可用，且无法链接到管道。

按照这些步骤删除Cloud Manager中的存储库。

1. 从 **计划概述** 页面，单击 **存储库** 选项卡，然后导航到 **存储库** 页面。

1. 选择存储库并单击省略号按钮并选择 **删除** 删除存储库。

   ![删除存储库](/help/implementing/cloud-manager/assets/repos/delete-repo.png)

## Git子模块支持 {#git-submodule-support}

Git子模块可用于在构建时在git存储库中合并多个分支的内容。

在执行Cloud Manager的生成过程时，如果为管道配置的存储库包含 `.gitmodules` 文件，将执行命令。

以下命令将每个子模块检出到相应的目录中。

```
$ git submodule update --init
```

此技术是文档中所述解决方案的潜在替代方法 [使用多个源Git存储库](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md) 适用于熟悉使用git子模块且不希望管理外部合并流程的组织。

例如，假设有三个存储库，每个存储库都包含一个名为 `main`. 在主存储库（即在管道中配置的存储库）中， `main` 分支具有 `pom.xml` 文件声明其他两个存储库中包含的项目。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
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

然后，您将为其他两个存储库添加子模块。

```shell
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

这会导致 `.gitmodules` 文件，如下所示。

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

有关git子模块的更多信息，请参阅 [Git参考手册。](https://git-scm.com/book/en/v2/Git-Tools-Submodules)

### 限制和Recommendations {#limitations-recommendations}

使用git子模块时，请注意以下限制。

* Git URL必须完全采用上一节中描述的语法。
* 仅支持位于分支根的子模块。
* 出于安全考虑，请勿在Git URL中嵌入凭据。
* 除非另有必要，否则强烈建议使用浅层子模块。
   * 要执行此操作，请运行 `git config -f .gitmodules submodule.<submodule path>.shallow true` 每个子模块。
* Git子模块引用存储到特定的git提交中。 因此，在对子模块存储库进行更改时，需要更新引用的提交。
   * 例如，使用 `git submodule update --remote`
