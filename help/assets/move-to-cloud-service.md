---
title: 从Adobe Experience Manager 6.x迁移到云服务
description: 从Adobe Experience Manager 6.x迁移到云服务
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# 将Adobe Experience Manager资产作为云服务移至 {#move-to-assets-cloud-service}

<!-- About the need to move from previous AEM deployment to a cloud service deployment. And how does Adobe help do it OOTB?
-->

## 关于迁移工具 {#migration-tool}

<!-- 
Link back to information about the tool in the Experience Manager as a Cloud Service docs if the tool works the same for Sites and Assets. Document the Assets-specific information here.

* What is the migration tool called? Is there a branding term for it?
* How much do we want to elaborate about the Pattern Detector rules? Is there a branding term for it?
* Before migrating using the tool, is any prepping required?
* See CQ-4271901

-->

迁移工具可帮助您实现以下目标：

* 将现有的工作流模型转换为可与Assets Compute service一起使用的处理配置文件。
* 从工作流模型中删除不支持的步骤。
* 禁用工作流启动程序。
* 在用户确认／验证后，在现有源代码中合并配置。

迁移工具在Maven模块中创建处理配置文件，用户可以通过以下两种方式使用这些配置文件：

* 合并到其现有项目之一。
* 将模块添加为新的子模块。

迁移工具提供其所做更改的报告以及有关更改的信息。

<!--  

What is the output of the tool, besides migrated content.

Give details about reports and logs of the tool. 

* How to access the report, including required permissions.
* How to read/interpret the report.
* Location of logs. How to read the logs.
* What common errors to look for. Troubleshooting for these errors.

-->

## 将内容迁移到新部署 {#content-migration-across-deployments}
