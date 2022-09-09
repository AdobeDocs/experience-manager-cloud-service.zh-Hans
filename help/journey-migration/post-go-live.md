---
title: 上线后
description: 了解如何监控问题并提高性能
exl-id: 487f0b51-501b-48fc-a796-3cb8a6d64462
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 23%

---

# 上线后 {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="故障诊断AEM"
>abstract="查看持续开发的最佳实践并管理日志，以及诸如开发人员控制台和CRXDE Lite之类的工具，以帮助解决AEM问题"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html" text="访问和管理日志"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools" text="AEMas a Cloud Service开发工具"

这是历程的最后一部分，因此您将学习如何在迁移完成后监控问题并提高性能。 您应确保清理临时文件，审查持续开发的最佳实践并管理日志。

## 迄今为止的故事 {#story-so-far}

在历程的上一步中，您学习了如何执行迁移和 [上线](/help/journey-migration/go-live.md) 代码和内容准备好移到AEM  as a Cloud Service后。

## 目标 {#objective}

本文档介绍可用于对AEMas a Cloud Service环境进行故障诊断的工具：

* **开发人员控制台**
* **CRXDE Lite**
* **管理日志**

## 开发人员控制台 {#developer-console}

开发人员控制台中提供了调试AEMas a Cloud Service开发人员环境的功能，可用于开发、暂存和生产环境。

请参阅[实施 AEM as a Cloud Service](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools)，了解有关开发工具的更多信息。

## CRXDE Lite {#crxde-lite}

作为用户，您可以在开发环境中访问 CRXDE Lite，但不能在暂存或生产环境中访问。

>[!IMPORTANT]
>写入不可变存储库，例如 `/libs` 和 `/apps` 运行时会导致错误。 此外，您还无法访问用于暂存和生产环境的开发人员工具。

请参阅[使用 CRXDE Lite 进行开发](/help/implementing/developing/tools/crxde.md)，了解如何使用 CRXDE Lite 来开发 AEM 应用程序。

## 管理日志 {#managing-logs}

用户可以访问选定环境的可用日志文件列表。

请参阅[访问和管理日志](/help/implementing/cloud-manager/manage-logs.md)，了解如何通过 UI 或通过 Cloud Manager 从 API 访问和管理日志。

## 联系支持人员 {#contacting-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="帮助和支持"
>abstract="请联系我们的AEM支持团队，以获取说明或解决任何问题。"
>additional-url="https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html" text="支持Experience Cloud"

如果您对访问Cloud Service有任何疑问，请联系您的Adobe代表或 [支持Experience Cloud](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html) 以了解更多详细信息。

## 文档学习 {#document-learnings}

迁移完成后，您应记录在此过程中获得的知识。 一些可能有助于文档处理的问题包括：

* 什么管用，什么管用？
* 主要的痛点是什么？
* Recommendations，以防将来迁移。

然后，您应该与组织内的利益相关方和团队共享这些迁移后学习内容。

## 历程结束了？ {#journey-ends}

恭喜！您已完成AEMas a Cloud Service迁移历程! 您应该了解如何：

* 开始迁移到AEMas a Cloud Service
* 确定您的部署是否已准备好移至AEMas a Cloud Service
* 使代码和内容云就绪
* 执行迁移
* 监控问题并提高性能
