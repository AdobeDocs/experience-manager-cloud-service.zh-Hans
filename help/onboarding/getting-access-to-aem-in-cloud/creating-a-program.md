---
title: 创建计划——云服务
description: 创建计划——云服务
translation-type: tm+mt
source-git-commit: 57206e36725e28051b2468d47da726e318bd763b

---


# 创建程序 {#create-a-program}

云本机解决方案为用户提供了必要的权限，并能够在自助服务模型上创建程序。

程序创建向导将要求用户提交详细信息，具体取决于用户在特定客户或组织可用的范围内创建程序的目标。

如果首次访问Cloud manager或租户中不存在程序，用户将看到创建您的第 **一个程序屏幕** 。 如果用户选 *择* Esc或者单击出对话框，将显示以下屏幕：

![](assets/create-program1.png)


## 使用创建程序向导 {#using-create-program-wizard}

根据用户在特定客户／组织可用的范围内创建程序的目标，程序创建向导将要求用户提交一个或多个详细信息。

![](assets/create-program-2.png)

>[!NOTE]
>如果某个程序已存在，您将在登录页面的右 **上方看到** “添加程序”，如下图所示。

![](assets/create-program-add.png)

## 创建演示程序 {#create-demo-program}

>[!NOTE]
>演示程序类似于Cloud Manager UI中的沙箱程序。

请按照以下步骤创建沙箱程序：

1. 从创建程序向导中，选择 **设置演示**。 用户在选择创建之前提交程序 **名称**。

   ![](assets/create-program-setupdemo.png)

1. 用户将在登陆页面上看到新的沙箱程序卡，并可以将鼠标悬停在该卡上以选择云管理器图标以导航到云管理器概述页面。 卡将通知用户新创建的沙箱程序的自动设置状态。 用户将看到进度。

   ![](assets/program-create-setupdemo2.png)

1. 在程序设置和项目创建步骤完成后，用户可以访问“ **Manage Git** ”链接，如下图所示：

   ![](assets/create-program4.png)

   >[!NOTE]
   >
   >要进一步了解如何通过Cloud Manager UI使用自助服务Git帐户管理访问和管理您的Git存储库，请参阅 [访问Git](/help/implementing/cloud-manager/accessing-git.md)。


1. 创建开发环境后，用户便可 **以访问AEM** 链接，如下图所示：

   ![](assets/create-program-5.png)

1. 完成部署到开发的非生产渠道部署后，向导会指导用户访问AEM（在开发中）或将代码部署到开发环境：

   ![](assets/create-program-setup-deploy.png)


## 创建常规程序 {#create-regular-program}

常规 ** 程序适用于熟悉AEM和Cloud manager的用户，他们准备开始编写、构建和测试代码，以将其部署到生产。

请按照以下步骤创建常规计划：

1. 在创 **建程序向导中选择** “为生产设置”以创建常规程序。 用户可以接受默认的程序名称，或在选择“继续”之前对其进行 **编辑**。

   ![](assets/set-up-prod1.png)

1. 用户将在屏幕上选择要包含在程序中的解决方案，该屏幕将在上面的屏幕后显示。



   >[!NOTE]
   >
   >以下屏幕仅针对已购买多个解决方案的客户细分显示。 对于只购买了一个解决方案的客户，将不显示以下解决方案选择屏幕。

   ![](assets/set-up-prod2.png)

1. 选择解决方案后，单击“创 **建”**。

   ![](assets/set-up-prod3.png)

1. 在登录页面上看到您的计划卡后，将指针悬停在该卡片上以选择Cloud Manager图标，以导航到Cloud Manager概 **述页** 。

   ![](assets/set-up-prod4.png)

1. 主行动动员卡将引导用户创建环境，创建非生产管道，最后创建生产管道。
   ![](assets/set-up-prod5.png)


   >[!NOTE]
   >
   >常规程序没有“自 **动设置** ”功能。





