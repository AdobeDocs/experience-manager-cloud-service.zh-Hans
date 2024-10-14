---
title: Cloud Manager中的管道变量
description: 了解如何在Cloud Manager中使用管道变量来管理内部版本的特定配置变量。
exl-id: cfcef2e2-0590-457d-a0f9-6092a6d9e0e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 40a76e39750d6dbeb03c43c8b68cddaf515a2614
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 14%

---

# Cloud Manager中的管道变量 {#configuring-pipeline-variables}

您的构建过程可能依赖于不应存储在Git存储库中的特定配置变量。 或者，您可能需要在同一分支上的管道运行之间调整它们。 通过Cloud Manager，可将这些设置作为管道变量进行管理。

## 关于管道变量 {#pipeline-variables}

使用Cloud Manager，您可以通过多种不同的方式配置管道变量。

* [使用Cloud Manager用户界面](#ui)
* [使用Cloud Manager CLI](#cli)
* [使用Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Variables/operation/getPipelineVariables)

可将变量以纯文本或静态加密形式存储。在任一情况下，变量都将在构建环境中用作环境变量，之后可以从 `pom.xml` 文件或其他构建脚本中引用这些变量。

## 通过Cloud Manager添加管道变量 {#ui}

可通过Cloud Manager用户界面配置和管理管道变量。 它们有助于简化管道管理，尤其是在不同步骤中需要不同配置时。

您必须具有编辑管道的权限才能添加、编辑和删除管道变量。

如果管道正在运行，则变量管理会被阻止。

**要通过Cloud Manager添加管道变量：**

1. 在[管理您的管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)时，单击要为其创建管道变量的管道的![省略号 — 更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 从下拉菜单中，单击&#x200B;**查看/编辑变量**。

   ![查看/编辑管道变量](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. 在&#x200B;**变量配置**&#x200B;对话框中，在表的第一行中输入详细信息。

   | 字段 | 描述 |
   | --- | --- |
   | 名称 | 配置变量的唯一名称。 它标识在管道中使用的特定变量。 它必须遵循以下命名惯例：<ul><li>变量只能包含字母数字字符和下划线(`_`)。</li><li>名称应全部大写。</li><li>每个管道最多有 200 个变量。</li><li>每个名称的长度必须等于或少于100个字符。</li><li>每个`string`变量值的长度必须少于 2048 个字符。</li><li>每个`secretString`类型变量值的长度必须等于或少于500个字符。</li></ul> |
   | 价值 | 变量保存的值。 |
   | 已应用步骤 | 必需。变量应用于的管道中的步骤：<ul><li>**生成** — 变量在生成过程中应用。</li><li>**功能测试** — 该变量在功能测试步骤中使用。</li><li>**UI测试** — 变量在UI测试阶段使用。</li></ul> |
   | 类型 | 选择变量是纯文本还是加密为密钥。 |

   ![添加变量](/help/implementing/cloud-manager/assets/pipeline-variables-add-variable.png)

1. 单击&#x200B;**添加**。

   根据需要添加其他变量。

1. 单击&#x200B;**保存**。

## 编辑管道变量 {#edit-ui}

1. 当[管理您的管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)时，单击要编辑其管道变量的![省略号 — 更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 在下拉菜单中，单击&#x200B;**查看/编辑变量**。

   ![查看/编辑管道变量](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. 在&#x200B;**变量配置**&#x200B;对话框中，单击要更改的变量的![省略号 — 更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 在下拉菜单中，单击&#x200B;**编辑**。

   ![编辑变量](/help/implementing/cloud-manager/assets/pipeline-variables-edit.png)

1. 根据需要更新变量的值。

   只能更改变量的值。

1. 执行下列操作之一：

   * 单击![应用 — 复选标记图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg)以应用更改。
   * 单击![撤消图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Undo_18_N.svg)以还原更改。

1. 单击&#x200B;**保存**。


## 删除管道变量 {#delete-ui}

1. 当[管理您的管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)时，单击要删除其管道变量的![省略号 — 更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 在下拉菜单中，单击&#x200B;**查看/编辑变量**。

   ![查看/编辑管道变量](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. 在&#x200B;**变量配置**&#x200B;对话框中，单击要删除的变量的![省略号 — 更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，然后单击&#x200B;**删除**。

## 使用Cloud Manager CLI设置管道变量 {#cli}

CLI（命令行界面）中的此命令可设置变量。

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test
```

此命令列出变量。

```shell
$ aio cloudmanager:list-pipeline-variables PIPELINEID
```

在Maven `pom.xml`文件中使用时，使用与以下示例类似的语法将这些变量链接到Maven属性通常很有用：

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
