---
title: '将团队成员分配给Cloud Manager产品配置文件 '
description: 可查看本页以了解如何将团队成员分配给Cloud Manager产品配置文件
hide: true
hidefromtoc: true
index: false
source-git-commit: 8b30fc9494e152aa742cf17c02f982f5c9479473
workflow-type: tm+mt
source-wordcount: '1110'
ht-degree: 0%

---


# 将团队成员分配给Cloud Manager产品配置文件 {#assign-team-members}

了解如何登录Admin Console并以系统管理员身份查看您的权限后，您现在可以将团队成员分配给Cloud Manager产品配置文件。

## 目标 {#objective}

本文档概述了如何从Admin Console将团队成员分配给Cloud Manager产品配置文件。

阅读此部分后，您应该能够：

* 了解添加团队成员的原因和方式。
* 了解三个不同的Cloud Manager产品配置文件，如业务所有者、部署管理员和开发人员。
* 将团队成员分配给Cloud Manager产品配置文件（业务所有者、部署管理器和开发人员）。

## 查看Cloud Manager产品配置文件 {#review-product-profiles}

从Admin Console中，您可以看到Cloud Manager配置文件列表。

>[!NOTE]
>在从Admin Console查看Cloud Manager产品配置文件之前，建议先查看可用的Cloud Manager产品配置文件。

请按照以下步骤查看Cloud Manager配置文件列表：

1. 登录Adobe Admin Console。 从&#x200B;**概述**&#x200B;页面中，从“产品和服务”卡中选择Adobe Experience Manager as a Cloud Service 。

   >[!NOTE]
   >请参阅登录到Admin Console，了解如何使用Admin Console。


1. 从包含所有实例列表的表中导航到Cloud Manager实例。 您将看到预配置的Cloud Manager产品配置文件列表。


## 将用户分配给业务所有者产品配置文件 {#assign-users-business-owner}

现在，您可以添加用户并将其分配给Cloud Manager业务所有者产品配置文件。

要成功执行此操作，您必须从Adobe管理控制台将用户添加到产品(在本例中为AEM)和Cloud Manager Business Owner产品配置文件中。

以下步骤将指导您完成此步骤：

1. 确定将管理Cloud Manager程序的用户，并将其添加到业务所有者产品配置文件。 系统管理员必须是第一个访问和登录Cloud Manager的人员。 您必须先将自己（系统管理员）添加到“业务所有者”产品配置文件中。

1. 在Admin Console概述页面中，从产品和服务卡中选择Adobe Experience Manager作为Cloud Service产品，如下所示：

1. 从顶部导航中选择用户选项卡，然后选择添加用户。

1. 在“添加用户”对话框中，键入要添加用户的电子邮件ID。 对于ID类型，如果尚未设置团队成员的Federated ID，请选择Adobe ID。

1. 在“产品”选项中，选择“Adobe Experience Manager as a Product”，并将“业务所有者”产品配置文件分配给用户，如下所示。 请参阅Cloud Manager产品配置文件，以确保在Admin Console中为正确的用户分配正确的角色，如下所示。

1. 将用户至少分配一个产品配置文件，以便用户可以访问Cloud Manager。 请记住将您自己（系统管理员）分配给“业务所有者”。

1. 单击保存。系统会向您添加的用户发送一封欢迎电子邮件。 受邀用户可以通过单击欢迎电子邮件中的链接，然后使用其Adobe ID登录来访问Cloud Manager。

恭喜！ 现在，您新组建的Cloud Manager团队（包括您自己分配给“业务所有者”角色的团队）已经设置完成。 会员将收到一封欢迎电子邮件，邀请他们登录并访问Cloud Manager。 在“业务所有者”角色中，您现在只需一步即可登录到Cloud Manager并启用云资源的创建。

## 将用户分配给Deployment Manager产品配置文件 {#assign-users-deployment-manager}

1. 确定将管理Cloud Manager程序的用户，并将其添加到业务所有者产品配置文件。 系统管理员必须是第一个访问和登录Cloud Manager的人员。 您必须先将自己（系统管理员）添加到“业务所有者”产品配置文件中。

1. 在Admin Console概述页面中，从产品和服务卡中选择Adobe Experience Manager作为Cloud Service产品，如下所示：

1. 从顶部导航中选择用户选项卡，然后选择添加用户。

1. 在“添加用户”对话框中，键入要添加用户的电子邮件ID。 对于ID类型，如果尚未设置团队成员的Federated ID，请选择Adobe ID。

1. 在“产品”选项中，选择“Adobe Experience Manager as a Deployment”，并将“部署管理器”产品配置文件分配给用户，如下所示。 请参阅Cloud Manager产品配置文件，以确保在Admin Console中为正确的用户分配正确的角色，如下所示。

   >[!NOTE]
   >在创建Cloud Manager资源后，可以将用户添加到部署管理器产品配置文件。

## 将用户分配给开发人员产品配置文件 {#assign-users-developer}

1. 确定将管理Cloud Manager程序的用户，并将其添加到业务所有者产品配置文件。 系统管理员必须是第一个访问和登录Cloud Manager的人员。 您必须先将自己（系统管理员）添加到“业务所有者”产品配置文件中。

1. 在Admin Console概述页面中，从产品和服务卡中选择Adobe Experience Manager作为Cloud Service产品，如下所示：

1. 从顶部导航中选择用户选项卡，然后选择添加用户。

1. 在“添加用户”对话框中，键入要添加用户的电子邮件ID。 对于ID类型，如果尚未设置团队成员的Federated ID，请选择Adobe ID。

1. 在“产品”选项中，选择“Adobe Experience Manager as a Product”，并将“开发人员”产品配置文件分配给用户，如下所示。 请参阅Cloud Manager产品配置文件，以确保在Admin Console中为正确的用户分配正确的角色，如下所示。

   >[!NOTE]
   >在创建Cloud Manager资源后，可以将用户添加到开发人员产品配置文件。

## 下一步 {#whats-next}

作为分配给&#x200B;*业务所有者*&#x200B;角色的系统管理员，您必须访问并登录Cloud Manager。
>[!NOTE]
>请参阅导航到Cloud Manager ，以了解如何登录和访问Cloud Manager。

具有“业务所有者”角色的Cloud Manager用户可以登录并设置您的云资源，包括您的项目和环境。 这将确保您的专家团队能够尽快开始访问AEMCloud Service。
在您的业务所有者设置您的云资源后，已成功添加到Cloud Manager产品配置文件的开发人员和部署经理可以访问Cloud Manager并熟悉如何继续其学习路径。

## 其他资源 {#additional-resources}

请查看其他资源以了解：

* Cloud Manager
* Cloud Manager产品配置文件
* Admin Console身份概述
