---
title: 配置管道变量
description: 了解如何在Cloud Manager中使用管道变量来管理内部版本的特定配置变量。
exl-id: cfcef2e2-0590-457d-a0f9-6092a6d9e0e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 20%

---

# 配置管道变量 {#configuring-pipeline-variables}

您的构建过程可能取决于特定的配置变量，这些变量不适合放置在Git存储库中，或者您可能需要在使用同一分支的管道执行之间切换这些变量。 利用Cloud Manager，可将这些数据作为管道变量进行管理。

## 管道变量 {#pipeline-variables}

使用Cloud Manager，您可以通过多种不同的方式配置管道变量。

* [通过Cloud Manager UI](#ui)
* [使用Cloud Manager CLI](#cli)
* [使用Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Variables/operation/getPipelineVariables)

可将变量以纯文本或静态加密形式存储。在任一情况下，变量都将在构建环境中用作环境变量，之后可以从 `pom.xml` 文件或其他构建脚本中引用这些变量。

### 管道变量命名约定 {#naming-conventions}

变量名必须遵守以下约定。

* 变量只能包含字母数字字符和下划线 (`_`)。
* 名称应全部大写。
* 每个管道最多有 200 个变量。
* 每个名称的长度必须等于或少于100个字符。
* 每个`string`变量值的长度必须少于 2048 个字符。
* 每个`secretString`类型变量值的长度必须等于或少于500个字符。

## 通过Cloud Manager UI {#ui}

可通过Cloud Manager UI配置和管理管道变量。 您必须具有编辑管道的权限才能添加、编辑和删除管道变量。

如果管道正在运行，则变量管理会被阻止。

### 添加管道变量 {#add-ui}

1. 在[管理管道时，](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)点按或单击要为其创建管道变量的管道的省略号按钮，然后从上下文菜单中选择&#x200B;**查看/编辑变量**。

   ![查看/编辑管道变量](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. 将打开&#x200B;**变量配置**&#x200B;窗口。 在表的第一行中输入变量详细信息，然后点按或单击&#x200B;**添加**。

   * **配置名称**&#x200B;是变量的唯一标识符，它必须遵循[管道变量命名约定](#naming-conventions)。
   * **Value**&#x200B;是变量保存的值。
   * **应用的步骤**&#x200B;是管道中变量应用的步骤。 它是必需的。
      * **生成**
      * **功能测试**
      * **UI测试**
   * **Type**&#x200B;定义变量是纯文本还是加密为密钥。

   ![添加变量](/help/implementing/cloud-manager/assets/pipeline-variables-add-variable.png)

1. 随即会添加到表中。 根据需要添加其他变量，然后点按或单击&#x200B;**保存**&#x200B;以保存添加到管道的变量。

### 编辑管道变量 {#edit-ui}

1. 在[管理管道时，](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)点按或单击要为其创建管道变量的管道的省略号按钮，然后从上下文菜单中选择&#x200B;**查看/编辑变量**。

   ![查看/编辑管道变量](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. 将打开&#x200B;**变量配置**&#x200B;窗口。 点按或单击要编辑的变量的省略号按钮，然后选择&#x200B;**编辑**。

   ![编辑变量](/help/implementing/cloud-manager/assets/pipeline-variables-edit.png)

1. 根据需要更新变量的值，然后点按或单击&#x200B;**应用**（行末尾的复选标记）以应用更改，或者点按或单击&#x200B;**放弃**（返回箭头）以还原更改。

   * 只能编辑变量的值。

   ![编辑变量](/help/implementing/cloud-manager/assets/pipeline-variables-edit-save.png)

1. 点按或单击&#x200B;**保存**&#x200B;以将您对变量所做的更改保存到管道。

如果要删除变量，请在&#x200B;**变量配置**&#x200B;窗口中从管道变量的省略号菜单中选择&#x200B;**删除**，而不是&#x200B;**编辑**。

## 使用Cloud Manager CLI {#cli}

此 CLI 命令用于设置变量。

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test
```

此命令列出变量。

```shell
$ aio cloudmanager:list-pipeline-variables PIPELINEID
```

通常，在 Maven `pom.xml` 文件中使用变量时，使用与该内容类似的语法将这些变量映射到 Maven 属性会很有用。

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
            </activation>
            <properties>
                <my.custom.property>${env.MY_CUSTOM_VARIABLE}</my.custom.property> 
            </properties>
        </profile>
```
