---
title: 创建沙盒程序
description: 了解如何使用 Cloud Manager 创建自己的沙盒程序，用于培训、演示、POC 或其他非生产目的。
exl-id: 10011392-3059-4bb0-88db-0af1d390742e
source-git-commit: b916bf5b252045120659600293e004fc34b96e7a
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 67%

---

# 创建沙盒程序 {#create-sandbox-program}

通常，创建沙盒程序是为了提供培训、运行演示、支持、概念验证 (POC) 或归档等目的，并不意味着要承载实时流量。

请参阅文档[解程序和程序类型](program-types.md)，了解有关程序类型的更多信息。

## 创建沙盒程序 {#create}

按照以下步骤创建沙盒程序。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 从 Cloud Manager 的登陆页面，单击屏幕右上角的&#x200B;**添加程序**。

   ![Cloud Manager 登陆页面](assets/cloud-manager-my-programs.png)

1. 從建立計畫精靈中，選擇 **設定沙箱** 並提供計畫名稱。

   ![程序类型创建](assets/create-sandbox.png)

1. 或者，您也可以拖放影像檔案至 **新增程式影像** 或按一下以從檔案瀏覽器中選取影像。 点按或单击&#x200B;**继续**。

   * 此影像僅可作為計畫總覽視窗中的圖磚，並有助於識別計畫。

1. 在 **設定您的沙箱** 對話方塊中，勾選「 」選項中的「 」，選擇您要在沙箱程式中啟用的解決方案。 **解決方案和附加元件** 表格。

   * 使用解決方案名稱旁的>形箭號，顯示解決方案的其他可選附加元件。

   * 此 **網站** 和 **資產** 解決方案一律包含在沙箱程式中，且無法取消選取。

   ![為沙箱選取解決方案和附加元件](assets/sandbox-solutions-add-ons.png)

1. 為您的沙箱計畫選取解決方案和附加元件後，點選按一下 **建立**.

随着安装过程的进行，您将在登陆页面上看到一个带有状态指示器的新沙盒程序信息卡。

![从概述页面创建沙盒](assets/sandbox-setup.png)

## 沙箱存取 {#access}

您可以查看沙盒设置的详细信息，也可以通过查看程序概述页面访问环境（一旦可用）。

1. 从 Cloud Manager 登陆页面中，单击新创建程序上的省略号按钮。

   ![访问程序概述](assets/program-overview-sandbox.png)

1. 项目创建步骤完成后，您可以访问&#x200B;**访问存储库信息**&#x200B;链接，以便能够使用您的 Git 存储库。

   ![程序配置](assets/create-program4.png)

   >[!TIP]
   >
   >要了解有关访问和管理 Git 存储库的更多信息，请参阅文档[访问 Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md)。

1. 创建开发环境后，您可以使用 **Access AEM** 链接登录 AEM。

   ![访问 AEM 链接](assets/create-program-5.png)

1. 完成非生产管道部署到开发后，向导将指导您访问 AEM 开发环境或将代码部署到开发环境。

   ![部署沙盒](assets/create-program-setup-deploy.png)

如果在任何时候您需要切换到另一个程序或返回概述页面创建另一个程序，请单击屏幕左上角的程序名称，可显示&#x200B;**导航到**&#x200B;选项。

![导航至](assets/create-program-a1.png)
