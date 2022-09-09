---
title: 配置帐户环境
description: AEM 提供了用于配置帐户和创作环境的某些方面的功能
exl-id: 1b948f0b-85b9-478a-8b7e-61495c1d57b6
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 100%

---

# 配置帐户环境 {#configuring-your-account-environment}

AEM 提供了配置帐户和创作环境某些方面的功能。

通过使用[标题](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header)和关联的[我的首选项](#my-preferences)对话框中的[用户](#user-settings)选项，您可以修改用户选项。

首先，访问标题中的[用户](#user-settings)选项。

## 用户设置 {#user-settings}

在&#x200B;**用户**&#x200B;设置对话框中，您可以访问：

* 模拟为
   * 借助“模拟为”功能，用户可以代表其他用户工作。<!--With the [Impersonate as](/help/sites-administering/security.md#impersonating-another-user) functionality, a user can work on behalf of another user.-->
* 配置文件
   * 提供一个指向您的用户设置的便捷链接 <!--Offers a convenient link to your [user settings](/help/sites-administering/security.md))-->
* [我的偏好设置](#my-preferences)
   * 指定用户特有的各种首选项设置

![用户设置](/help/sites-cloud/authoring/assets/user-settings.png)

### 我的偏好设置 {#my-preferences}

**我的首选项**&#x200B;对话框可通过标题中的[用户](#user-settings)选项进行访问。

每个用户都可以为自己设置特定的属性。

![我的首选项](/help/sites-cloud/authoring/assets/user-preferences.png)

* **语言**

   此选项定义要用于创作环境 UI 的语言。从可用列表中选择所需语言。

* **窗口管理**

   此选项定义打开窗口的行为。选择：

   * **多窗口**（默认）

      * 页面将在新窗口中打开。
   * **单一窗口**

      * 页面将在当前窗口中打开。


* **显示适用于资产的桌面操作**

   此选项要求使用 AEM 桌面应用程序。

* **注释颜色**

   此选项定义创建注释时使用的默认颜色。

   * 单击颜色块可打开色板选择器以选择一种颜色。
   * 或者，可在字段中输入所需颜色的十六进制代码。

* **相对日期显示**

   为了提高可读性，AEM 会将过去七天内的日期显示为相对日期（例如三天前），而将更早的日期则显示为确切日期（例如 2017 年 3 月 20 日）。

   此选项定义系统中日期的显示方式。以下选项可供选择：

   * **始终显示确切日期**：将始终显示确切日期（从不显示相对日期）。
   * **1 天**：对于一天内的日期显示相对日期，其他情况则显示确切日期。
   * **7 天（默认）**：对于七天内的日期显示相对日期，其他情况则显示确切日期。
   * **1 个月**：对于一个月内的日期显示相对日期，其他情况则显示确切日期。
   * **1 年**：对于一年内的日期显示相对日期，其他情况则显示确切日期。
   * **始终显示相对日期**：从不显示确切日期，只显示相对日期。

* **启用快捷键**

   AEM 支持使用许多键盘快捷键，以便更高效地进行创作。

   * [用于编辑页面的键盘快捷键](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
   * [控制台的键盘快捷键](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)

   此选项可启用键盘快捷键。默认情况下，这些键盘快捷键处于启用状态，但也可以将其禁用，例如，当用户要求使用特定辅助功能时。

* **启用资产主页**

   仅当系统管理员为整个组织启用了资产主页体验时，此选项才可用。

* **Stock 配置**

   此选项允许指定首选的 Adobe Stock 配置，并且仅在系统管理员已启用 [Adobe Stock 集成](/help/assets/aem-assets-adobe-stock.md)时才可用。
