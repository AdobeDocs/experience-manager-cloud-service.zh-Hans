---
title: 配置帐户环境
description: Adobe Experience Manager (AEM)允许您配置帐户和创作环境的某些方面。
exl-id: 1b948f0b-85b9-478a-8b7e-61495c1d57b6
source-git-commit: 78ead5f15c2613d9c3bed3025b43423a66805c59
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 60%

---

# 配置帐户环境 {#configuring-your-account-environment}

Adobe Experience Manager (AEM)允许您配置帐户和创作环境的某些方面。

通过使用[标题](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header)和关联的[我的首选项](#my-preferences)对话框中的[用户](#user-settings)选项，您可以修改用户选项。

首先，访问标题中的[用户](#user-settings)选项。

## 用户设置 {#user-settings}

在&#x200B;**用户**&#x200B;设置对话框中，您可以访问：

* 模拟为
   * 借助“模拟为”功能，用户可以代表其他用户工作。<!--With the [Impersonate as](/help/sites-administering/security.md#impersonating-another-user) functionality, a user can work on behalf of another user.-->
* 配置文件
   * 它提供了一个指向您的用户设置的便捷链接 <!--Offers a convenient link to your [user settings](/help/sites-administering/security.md))-->
* [我的偏好设置](#my-preferences)
   * 指定用户特有的各种首选项设置

![用户设置](/help/sites-cloud/authoring/assets/user-settings.png)

### 我的偏好设置 {#my-preferences}

此 **我的首选项** 对话框可通过 [用户](#user-settings) 选项来识别。

每个用户可以设置自己的首选属性。

![我的首选项](/help/sites-cloud/authoring/assets/user-preferences.png)

* **语言**

  此选项定义要用于创作环境 UI 的语言。从可用列表中选择所需语言。

* **窗口管理**

  此选项定义打开窗口的行为。选择：

   * **多窗口**（默认）

      * 页面会在新窗口中打开。

   * **单窗口**

      * 页面会在当前窗口中打开。

* **显示适用于资产的桌面操作**

  此选项需要使用AEM桌面应用程序。

* **注释颜色**

  此选项定义创建注释时使用的默认颜色。

   * 单击颜色块，以便打开样本选择器来选择颜色。
   * 或者，可在字段中输入所需颜色的十六进制代码。

* **相对日期显示**

  为了提高可读性，AEM将过去七天内的日期渲染为相对日期（例如，三天前），将更早的日期渲染为确切日期（例如，2017年3月20日）。

  此选项定义系统中日期的显示方式。以下选项可供选择：

   * **始终显示确切日期**：将始终显示确切日期（从不显示相对日期）。
   * **1 天**：对于一天内的日期显示相对日期，其他情况则显示确切日期。
   * **7 天（默认）**：对于七天内的日期显示相对日期，其他情况则显示确切日期。
   * **1 个月**：对于一个月内的日期显示相对日期，其他情况则显示确切日期。
   * **1 年**：对于一年内的日期显示相对日期，其他情况则显示确切日期。
   * **始终显示相对日期**：从不显示确切日期，只显示相对日期。

* **启用快捷键**

  AEM支持各种键盘快捷键，以提高创作效率。

   * [用于编辑页面的键盘快捷键](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
   * [控制台的键盘快捷键](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)

  此选项可启用键盘快捷键。默认情况下，这些功能处于启用状态，但可以禁用，例如，如果用户有特定的辅助功能要求。

* **启用资产主页**

  仅当系统管理员为整个组织启用了资产主页体验时，此选项才可用。

* **Stock 配置**

  此选项可让您指定首选的Adobe Stock配置，并且仅在系统管理员已启用时才可用 [Adobe Stock集成](/help/assets/aem-assets-adobe-stock.md).
