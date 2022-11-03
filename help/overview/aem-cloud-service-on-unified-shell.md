---
title: Unified Shell 上的 AEM as a Cloud Service
description: Unified Shell 上的 AEM as a Cloud Service
exl-id: ea739307-dc99-4621-a239-dbe60ab6b52e
source-git-commit: 53e22737e62835872e47ac07530078c3d1dfcf31
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 71%

---

# Unified Shell 上的 AEM as a Cloud Service {#aem-as-a-cloud-service-on-unified-shell}

>[!NOTE]
>该功能将在 2022 年 7 月的预发布渠道中发布。
>
>其目的是推出新的功能，该功能将会在 2022 年 8 月发布。
>
>有关如何为您的环境启用该功能的信息，请参阅[预发布渠道文档](/help/release-notes/prerelease.md#enable-prerelease)。

## 概述 {#overview}

AEMas a Cloud Service（创作服务）与Unified Shell集成，以改进用户体验并将其与所有其他Experience Cloud应用程序相统一。 此集成的影响可在应用程序的顶部标题中查看，如下所示。

![图像](/help/overview/assets/unifiedshell_header.png)

其好处包括：

* 跨所有 Experience Cloud 应用程序进行单点登录
* 在组织之间轻松切换或切换到其他应用程序
* 改进了产品帮助
* 简单的产品内反馈按钮，用于报告问题或与 Adobe 分享想法
* 除了特定于AEM as a Cloud Service的通知之外，还可以访问全球产品公告和通知

## 禁用 Unified Shell {#disabling-unified-shell}

开箱即用地，AEM as a Cloud Service 已启用 Unified Shell。 但是，如果已自定义顶部标头，则建议禁用 Unified Shell 以避免自定义项出现任何问题。 要禁用 Unified Shell，请执行以下步骤：

>[!NOTE]
>只有具有管理权限的帐户才能禁用统一Shell。

1. 导航到&#x200B;**工具 – Cloud Services**。

   管理员用户将看到 Unified Shell 配置信息卡，如下所示：

   ![图像](/help/overview/assets/unifiedshell2.png)

1. 单击 **Unified Shell 配置**。 然后，取消选中下面显示的复选框以禁用 Unified Shell：

   ![图像](/help/overview/assets/unifiedshell3.png)

## 更改为深色主题 {#changing-to-dark-theme}

要更改为深色主题，请单击您的用户档案图标。 此时将显示一个弹出窗口，如下所示。 您可以使用切换开关切换到 Unified Shell 程序的深色主题。

>[!INFO]
>
>深色主题仅适用于 Unified Shell（顶栏）。

![图像](/help/overview/assets/unifiedshell4.png)

## 识别AEMas a Cloud Service环境 {#identify-aemaacs-environment}

AEMas a Cloud Service提供了三种类型的环境：生产、暂存和开发。 请参阅 [环境类型](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=en) 以了解更多详细信息。 通过与Unified Shell的此集成，用户在创作服务中登录的环境类型将通过标签显示在顶部标题中，如下所示。

![图像](/help/overview/assets/unifiedshell_header_label.png)


## 访问 AEM 收件箱 {#accessing-the-aem-inbox}

单击 Unified Shell 中的铃铛图标，即可访问 AEM 收件箱。

>[!INFO]
>
> 铃铛图标上指示的编号包括该 IMS 组织内所有解决方案的未读通知以及 AEM 收件箱中列出的任务。

![图像](/help/overview/assets/unifiedshell5.png)

单击弹出窗口中的收件箱按钮，以转到您的 AEM 收件箱：

![图像](/help/overview/assets/unifiedshell6.png)
