---
title: CI-CD管线
description: CI-CD管线
index: false
source-git-commit: 16e3280d7eaf53d8f944a60ec93b21c6676f0133
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# Cloud Manager CI-CD管道 {#intro-cicd}

## 简介 {#introduction}

>[!NOTE]
>Cloud Manager中的CI/CD管道由事件触发，例如来自源代码存储库的拉取请求（即代码更改），或与发行频率匹配的常规计划。

要配置管道，必须：
* 定义将启动管道的触发器
* 定义控制生产部署的参数
* 配置性能测试参数

在Cloud Manager中，有两种类型的管道：

* [生产管道](#prod-pipeline)
* [非生产管道](#non-prod-pipeline)

## 生产管道 {#prod-pipeline}

生产管道是用于构建管道的目的，管道包括一系列经过编排的步骤，以将源代码一直引入生产环境。 这些步骤包括首先构建、打包、测试、验证并部署到所有Stage环境中。 不用说，只有在创建生产和暂存环境集后，才能添加生产管道。

>[!NOTE]
>有关更多详细信息，请参阅配置生产管道。


## 非生产管道 {#non-prod-pipeline}

非生产管道旨在运行代码质量扫描或将源代码部署到开发环境。

>[!NOTE]
>有关更多详细信息，请参阅非生产和代码仅质量管道。
