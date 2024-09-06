---
title: Git 子模块支持
description: 了解如何使用 Git 子模块在构建时跨 Git 存储库合并多个分支的内容。
exl-id: fa5b0f49-4b87-4f39-ad50-7e62094d85f4
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 90%

---

# Adobe 存储库的 Git 子模块支持 {#git-submodule-support}

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

有关Git子模块的更多信息可在[Git参考手册](https://git-scm.com/book/en/v2/Git-Tools-Submodules)中找到。

### 限制和建议 {#limitations-recommendations}

将Git子模块与Adobe管理的存储库结合使用时，请注意以下限制。

* Git URL 必须完全遵循上一节所述语法。
* 仅支持分支的根目录中的子模块。
* 为安全起见，请勿在 Git URL 中嵌入凭据。
* 除非另有必要，否则强烈建议使用“浅”子模块。
   * 为此，请为每个子模块运行 `git config -f .gitmodules submodule.<submodule path>.shallow true`。
* Git 子模块引用将存储到特定的 git 承诺中。 因此，在对子模块存储库进行更改时，必须更新引用的承诺。
   * 例如，通过使用 `git submodule update --remote`

## Git 子模块对专用存储库的支持 {#private-repositories}

使用[专用存储库](private-repositories.md)时对 Git 子模块的支持与使用 Adobe 存储库时大致相同。

然而，在设置您的 `pom.xml` 文件并运行 `git submodule` 命令之后，您必须添加 `.gitmodules` 文件复制到聚合器存储库的根目录，以便 Cloud Manager 检测子模块设置。

![.gitmodules 文件](assets/gitmodules.png)

![聚合器](assets/aggregator.png)

### 限制和建议 {#limitations-recommendations-private-repos}

使用带有专用存储库的 Git 子模块时，注意以下限制。

* 子模块的 Git URL 可以是 HTTPS 或 SSH 格式，但必须链接到 github.com 存储库
   * 将 Adobe 存储库子模块添加到 GitHub 聚合器存储库或反之亦然不起作用。
* GitHub 子模块必须可供 Adobe GitHub App 访问。
* [使用 Git 子模块与 Adobe 管理的存储库的局限性](#limitations-recommendations)同样适用。
