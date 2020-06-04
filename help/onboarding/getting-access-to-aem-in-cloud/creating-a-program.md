---
title: 创建项目-云服务
description: 创建项目-云服务
translation-type: tm+mt
source-git-commit: b2549ac13f996449bc41ac18ba6afbf22e116597
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---


# 创建程序 {#create-a-program}

云本机解决方案为用户提供必要的权限，并能够在自助服务模型上创建项目。

项目创建向导将要求用户提交详细信息，具体取决于用户在特定客户或组织可用内容范围内创建项目的目标。

在首次访问云管理器的事件中，或者如果租户中不存在项目，用户将看到创 **建您的第一个项目屏幕** 。 如果用户选 *择* Esc或者单击出对话框，将显示以下屏幕：

![](assets/create-program1.png)


## 使用创建项目向导 {#using-create-program-wizard}

根据用户在特定客户／组织可用内容范围内创建项目的目标，项目创建向导将要求用户提交一个或多个详细信息。

![](assets/create-sandbox.png)

>[!NOTE]
>If a program already exists, then you will see **Add Program** on the top right of the landing page, as shown in the figure below.

![](assets/create-program-add.png)

## 创建沙箱项目 {#create-sandbox-program}

请按照以下步骤创建沙箱项目:

1. 在创建项目向导中，选 **择设置沙箱**。 用户在选择创建之前提交项目 **名称**。

   ![](assets/create-sandbox.png)

1. 用户将在登陆页上看到新的沙箱项目卡，并可以将鼠标悬停在沙箱卡上，选择云管理器图标，以导航到云管理器概述页面。 卡将通知用户新创建的沙箱项目的自动设置状态。 用户将看到进度。

   ![](assets/program-create-setupdemo2.png)

1. 在项目设置和项目创建步骤完成后，用户可以访 **问“管理** Git”链接，如下图所示：

   ![](assets/create-program4.png)

   >[!NOTE]
   >
   >要进一步了解如何通过云管理器用户界面使用自助Git帐户管理访问和管理您的Git存储库，请参阅 [访问Git](/help/implementing/cloud-manager/accessing-git.md)。


1. 创建开发环境后，用户可 **以访问** AEM链接，如下图所示：

   ![](assets/create-program-5.png)

1. 完成部署到开发的非生产渠道部署后，该向导将指导用户访问AEM（在开发时）或将代码部署到开发环境:

   ![](assets/create-program-setup-deploy.png)

   >[!NOTE]
   >您还可以从Cloud Manager概述页面编辑、切换或添加项目，如下所示：

   ![](assets/create-program-a1.png)

## 删除沙箱项目 {#delete-sandbox-program}

业务所有者或云管 *理器中**的部署管理器角色的沙箱项目* ，可以通过云管理器UI删除其生产环境集和阶段集。

删除选项可从“概述”页面上的 *环境* 卡和环境页 **面使用** 。 在生产或舞台上选择删除选项也会删除集合中的另一个。

## 创建常规项目 {#create-regular-program}

常规 *项目* 适用于熟悉AEM和Cloud Manager并且准备好编写、构建和测试代码并将其部署到生产的用户。

请按照以下步骤创建常规项目:

1. 在创 **建项目向导中** ，选择“为生产设置”以创建常规项目。 用户可以接受默认项目名称，或在选择“继续”之 **前编辑**。

   ![](assets/create-prod1.png)

1. 用户将选择要包含在屏幕上的项目中的解决方案，这些解决方案将在上面的屏幕后显示。



   >[!NOTE]
   >
   >以下屏幕仅针对已购买多个解决方案的客户细分显示。 对于只购买了一个解决方案的客户，将不显示下面的解决方案选择屏幕。

   ![](assets/set-up-prod2.png)

1. 选择解决方案后，单击“ **创建**”。

   ![](assets/set-up-prod3.png)

1. 在项目上看到您的登陆页卡后，将鼠标悬停在该卡上，以选择云管理器图标，以导航至云管理器 **概述** 页。

   ![](assets/set-up-prod4.png)

1. 主行动动员卡将引导用户创建环境、创建非生产管道，最后创建生产管道。
   ![](assets/set-up-prod5.png)


   >[!NOTE]
   >
   >A regular program does not have **Auto-setup** feature.





