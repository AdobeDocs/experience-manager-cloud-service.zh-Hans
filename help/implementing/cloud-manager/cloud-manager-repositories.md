---
title: Cloud Manager存储库
description: Cloud Manager存储库
exl-id: Cloud Manager Repositories
source-git-commit: d2a8329fff12be6581f2ee2caf7f9764c765d0e6
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# Cloud Manager存储库 {#cloud-manager-repos}

在Cloud Manager中创建和可用的存储库可通过“存储库”页面查看和管理。

## 添加和管理存储库 {#add-manage-repos}

请按照以下步骤在Cloud Manager中查看和管理存储库：

1. 在&#x200B;**Program Overview**&#x200B;页面中，单击&#x200B;**Repositories**&#x200B;选项卡，然后导航到&#x200B;**Repositories**&#x200B;页面。

1. 单击&#x200B;**添加存储库**&#x200B;以启动向导。

   >[!NOTE]
   >必须登录具有部署管理员或业务所有者角色的用户才能添加存储库。

   ![](assets/repos/create-repo2.png)


1. 根据请求输入名称和描述，然后单击&#x200B;**Save**。

   ![](assets/repos/repo-1.png)

1. 选择&#x200B;**保存**。您新创建的存储库将显示在表中，如下所示。

   ![](assets/repos/create-repo3.png)

   >[!NOTE]
   >在Cloud Manager中创建的存储库也将可供您在添加或编辑管道步骤期间从中进行选择。 请参阅[配置CI-CD管线](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en)以了解更多信息。

1. 您可以选择存储库，然后单击表最右侧的菜单选项&#x200B;**复制存储库URL**、**查看和更新**&#x200B;或&#x200B;**删除**&#x200B;您的存储库，如下图所示。

   ![](assets/repos/create-repo3.png)


## Git子模块支持 {#git-submodule-support}

Git子模块可用于在构建时在git存储库中合并多个分支的内容。 执行Cloud Manager的生成过程时，在克隆了为管道配置的存储库并签出已配置的分支后，如果分支在根目录中包含`.gitmodules`文件，则会执行命令。

```
$ git submodule update --init
```

这会将每个子模块检出到相应的目录中。 对于熟悉使用git子模块且不希望管理外部合并流程的组织而言，此技术是https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/working-with-multiple-source-git-repositories.html的一种潜在替代方法。

例如，假设有三个存储库，每个存储库都包含一个名为main的分支。 在“主”存储库（即在管道中配置的存储库）中，主分支具有一个pom.xml文件，用于声明其他两个存储库中包含的项目：

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

然后，您将为其他两个存储库添加子模块：

```
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

这会生成一个`.gitmodules`文件，如下所示：

```
[submodule "project-a"]
    path = project-a
    url = https://git.cloudmanager.adobe.com/ProgramName/projectA/
    branch = main
[submodule "project-b"]
    path = project-b
    url = https://git.cloudmanager.adobe.com/ProgramName/projectB/
    branch = main
```

有关git子模块的更多信息，请参阅[Git参考手册](https://git-scm.com/book/en/v2/Git-Tools-Submodules)。

使用git子模块时，请牢记以下事项：

* Git URL必须完全采用上述语法。 出于安全考虑，请勿在这些URL中嵌入凭据。
* 仅支持位于分支根的子模块。
* Git子模块引用存储到特定的git提交中。 因此，当对子模块存储库进行更改时，例如，使用`git submodule update --remote` ，需要更新引用的提交。

