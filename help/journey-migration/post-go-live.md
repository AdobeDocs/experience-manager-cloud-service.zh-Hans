---
title: 上线后
description: 了解如何监测问题并提高性能
exl-id: 487f0b51-501b-48fc-a796-3cb8a6d64462
feature: Migration
role: Admin
source-git-commit: 13a2386c099624a46e84126a939a9470e9b3a5f2
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 16%

---

# 上线后 {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="AEM 故障排除"
>abstract="审查持续开发的最佳实践并管理日志，以及开发人员控制台和CRXDE Lite等工具，以帮助对AEM问题进行故障诊断"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html#" text="访问和管理日志"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools" text="AEM as a Cloud Service 开发工具"

此历程是最后一部分，您将了解如何监测问题并在迁移完成后提高性能。 您应确保清理临时文件，审查持续开发的最佳实践并管理日志。

## 迄今为止的故事 {#story-so-far}

在历程的上一步中，您已了解如何在代码和内容准备好移至AEM as a Cloud Service后执行迁移和[上线](/help/journey-migration/go-live.md)。

## 目标 {#objective}

本文档介绍了可用于对AEM as a Cloud Service环境进行故障排除的工具：

* **开发人员控制台**
* **CRXDE Lite**
* **管理日志**

## 开发人员控制台 {#developer-console}

Developer Console中提供了调试AEM as a Cloud Service开发人员环境的功能，可用于开发、暂存和生产环境。

请参阅[为AEM as a Cloud Service实施](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools)，了解有关开发工具的更多信息。

## CRXDE Lite {#crxde-lite}

作为用户，您可以在开发环境中访问CRXDE Lite，但不能在暂存或生产环境中访问。

>[!IMPORTANT]
>在运行时写入不可变存储库（如`/libs`和`/apps`）会导致错误。 此外，您无法访问用于暂存和生产环境的开发人员工具。

有关如何使用CRXDE Lite开发AEMCRXDE Lite的详细信息，请参阅[使用Application](/help/implementing/developing/tools/crxde.md)。

## 管理日志 {#managing-logs}

用户可以访问选定环境的可用日志文件列表。

请参阅[访问和管理日志](/help/implementing/cloud-manager/manage-logs.md)，了解如何通过用户界面或通过Cloud Manager从API访问和管理日志。

## 联系支持 {#contacting-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="帮助与支持"
>abstract="请联系 Adobe 的 AEM 支持团队，获取说明或解决任意问题。"
>additional-url="https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html" text="Experience Cloud 支持"

如果您对访问Cloud Service有任何疑问，请联系您的Adobe代表或[Experience Cloud支持](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html)以获取更多详细信息。

## 文档学习 {#document-learnings}

迁移完成后，记录在此过程中获得的知识。 一些可能对文档流程有所帮助的问题包括：

* 哪些方法行之有效，哪些方法无效？
* 主要棘手问题有哪些？
* 如果将来发生迁移，则使用Recommendations。

与组织中的利益相关者和团队共享这些迁移后学习。

## 历程结束 - 是吗？ {#journey-ends}

恭喜！您已完成AEM as a Cloud Service迁移历程！ 您应该了解如何：

* AEM as a Cloud Service迁移入门
* 确定您的部署是否已准备好移至AEM as a Cloud Service
* 使您的代码和内容云准备就绪
* 执行迁移
* 监控问题并提高性能
