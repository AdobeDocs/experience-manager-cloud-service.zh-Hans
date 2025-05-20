---
title: 添加Edge Delivery管道
description: 了解如何添加Edge Delivery管道以生成代码并将其部署到生产环境。
index: true
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="率先采用者" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md网站#gitlab-bitbucket"
hide: true
hidefromtoc: true
source-git-commit: 22289138be1fa63caa1beda83e98ffa75dfabc2a
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# 添加Edge Delivery管道 {#configure-edge-delivery-pipeline}

了解如何配置生产管道以生成代码并将其部署到生产环境。 生产管道首先将代码部署到暂存环境。 在获得批准后，它会将相同的代码部署到生产环境。

用户必须具有&#x200B;**[部署管理员](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**&#x200B;角色才能配置Edge Delivery管道。

>[!NOTE]
>
>本文中介绍的功能只能通过早期采用者计划获得。 有关更多详细信息，以及要注册为早期采用者，请参阅[自带Git](/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket)。