---
title: Git 子模块支持
description: 了解如何使用 Git 子模块在构建时跨 Git 存储库合并多个分支的内容。
exl-id: fa5b0f49-4b87-4f39-ad50-7e62094d85f4
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: dc4008a33f6a786884a9aad30096ff4f0561346c
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 24%

---

# 为 Adobe 存储库提供的 Git 子模块支持 {#git-submodule-support}

Git 子模块可用于在构建时跨 Git 存储库合并多个分支的内容。

Cloud Manager的构建过程运行时，会克隆管道的存储库并签出分支。 如果分支的根目录中存在`.gitmodules`文件，则执行相应的命令。

以下命令将每个子模块签出到适当的目录中。

```
$ git submodule update --init
```

此技术为[使用多个Source Git存储库](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md)中所述的解决方案提供了替代方案。 它非常适合熟悉Git子模块并且更喜欢不管理外部合并流程的组织。

例如，假设有三个存储库。 每个存储库都包含一个名为`main`的分支。 在主存储库（即，在管道中配置的存储库）中，`main`分支包含一个`pom.xml`文件，声明其他两个存储库所包含的项目：

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

之后，您将为其他两个存储库添加子模块：

```shell
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

结果生成了类似于以下内容的`.gitmodules`文件：

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

另请参阅[Git参考手册](https://git-scm.com/book/en/v2/Git-Tools-Submodules)以了解有关Git子模块的更多信息。

## 限制和建议 {#limitations-recommendations}

将Git子模块与Adobe管理的存储库结合使用时，请注意以下限制。

* Git URL必须完全遵循上一节中所述的语法。
* 仅支持分支的根目录中的子模块。
* 为安全起见，请勿在Git URL中嵌入凭据。
* 除非另有必要，否则Adobe建议您通过运行以下命令来使用浅子模块：
  每个子模块的`git config -f .gitmodules submodule.<submodule path>.shallow true`。
* Git 子模块引用将存储到特定的 Git 承诺中。 因此，在对子模块存储库进行更改时，必须更新引用的承诺。
例如，使用以下命令：

  `git submodule update --remote`

## Git 子模块对专用存储库的支持 {#private-repositories}

对[专用存储库](private-repositories.md)中的Git子模块的支持通常与其在Adobe存储库中的使用类似。

但是，在配置`pom.xml`文件并执行`git submodule`命令后，必须将`.gitmodules`文件添加到Cloud Manager的聚合器存储库的根目录，以识别子模块配置。

![.gitmodules 文件](assets/gitmodules.png)

![聚合器](assets/aggregator.png)

### 限制和建议 {#limitations-recommendations-private-repos}

将Git子模块与专用存储库结合使用时，请牢记以下限制：

* 子模块Git URL可以是HTTPS或SSH格式，但必须指向GitHub.com存储库。 不支持将Adobe存储库子模块添加到GitHub聚合器存储库或反之。
* GitHub子模块必须可由AdobeGitHub应用程序访问。
* [使用 Git 子模块与 Adobe 管理的存储库的局限性](#limitations-recommendations)同样适用。
