---
title: AEM 2020.6.0版中Cloud Manager的发行说明
description: AEM 2020.6.0版中Cloud Manager的发行说明
feature: Release Information
exl-id: 879a5025-f94f-4549-bf6e-e1cc6b6a7b58
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 83%

---

# Adobe Experience Manager as a Cloud Service 2020.6.0版中的Cloud Manager发行说明 {#release-notes}

本页概述了AEM 2020.6.0版中Cloud Manager的发行说明。

## 发布日期 {#release-date}

AEM 2020.6.0版中Cloud Manager的发布日期是2020年6月4日。

## 新增功能 {#whats-new-cloud-manager}

* 在 Cloud Manager 中，具有“业务所有者”**&#x200B;角色的用户现在可以从登陆页面（通过项目卡上的快速操作按钮）或项目中删除沙盒项目。

   有关更多详细信息，请参阅[删除沙盒项目](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html)。

* 在 Cloud Manager 中，具有“业务所有者”**&#x200B;或“部署管理者”**&#x200B;角色的沙盒项目用户现在可以通过 Cloud Manager UI 删除其生产和暂存环境集。删除选项现在可从&#x200B;**项目概述**&#x200B;页面和&#x200B;**环境**&#x200B;页面上的环境卡中使用。在生产或暂存环境中选择删除选项也会删除环境集中的另一个环境。

   有关更多详细信息，请参阅[删除沙盒项目](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html)。

* 在登陆页面上显示引导标记，以告知和指示用户如何进行基本导航。

* 在&#x200B;**项目概述**&#x200B;页面上显示引导标记，以告知和指示用户如何在 Cloud Manager 中进行基本导航，以便开始操作。

* 现在 Cloud Manager 中提供了&#x200B;**学习**&#x200B;页面，可通过顶部导航访问该页面。该页面包含可帮助用户了解与他们在 Cloud Manager 中分配的角色相关的最常用工作流的资源。

* 沙盒项目现在通过&#x200B;**沙盒**&#x200B;徽章进行标识，该徽章将显示在登陆页面的项目卡上，以及&#x200B;**项目概述**&#x200B;页面中项目名称的旁边。

* 具有 SysAdmin 角色的用户现在通过一次单击即可访问 Admin Console 中的相应位置，以管理用户角色或 Cloud Manager 权限。现在，登陆页面上的&#x200B;**添加项目**&#x200B;按钮旁边提供了&#x200B;**管理访问权限**&#x200B;按钮。

   有关更多详细信息，请参阅 [SysAdmin 任务](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html#sysadmin-tasks)。

* 具有 SysAdmin 角色的用户现在通过一次单击即可直接从 Cloud Manager 中访问创作实例。

   有关更多详细信息，请参阅[管理对创作实例的访问](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html#manage-access-aem)。

* “生成”日志现在包含已发现项目的列表，包括跳过的内容包。

* “生成”步骤现在会验证所有生成的内容包是否包含所有必需属性 - 名称、组和版本。

* “生成”步骤现在会验证是否生成了至少一个内容包。

### 错误修复 {#bug-fixes-cm}

* 在某些情况下，**创建项目**&#x200B;对话框中的图标未对齐。

* AEM 版本标识符在&#x200B;**项目概述**&#x200B;页面上显示不一致。

* 配置生产管道时，某些客户看不到&#x200B;**计划部署**&#x200B;选项。

### 已知问题 {#known-issues-cm}

* 在某一特定时间段内未检测到活动时，沙盒项目内的环境将会休眠。在 Cloud Manager 中不会观察到此状态。但是，可通过开发人员控制台观察到此状态。即将发布的版本中将解决此问题。

* 直接从 Cloud Manager 链接到开发人员控制台不会显示用于将沙盒项目的环境解除休眠/休眠的选项。要解决此问题，请在开发人员控制台中，将模式 `#release-cm-p1234-e5678` 添加到 URL 的末尾，其中 *1234* 是项目 ID，*5678* 是环境 ID。即将发布的版本中将解决此问题。
