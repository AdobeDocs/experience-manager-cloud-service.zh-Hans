---
title: 迁移实用程序，用于将基于基础组件的自适应Forms转换为基于核心组件的表单
description: 了解如何安装并使用迁移实用程序将基于基础组件的自适应Forms转换为基于核心组件的表单。
Keywords: Migration Utility tool, Convert Adaptive Forms based on foundation components to core component based forms, Convert Foundation forms to Core components forms, Using Modernizer tool to convert Foundation Components to Core components in forms.
role: User, Developer, Admin
features: core components
hide: true
hidefromtoc: true
source-git-commit: 494e90bd5822495f0619e8ebf55f373a26a3ffe6
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 1%

---


# 简介

您可以使用迁移实用程序将基于基础组件的自适应Forms转换为基于核心组件的表单。 您可以使用 [AEM现代化工具](https://opensource.adobe.com/aem-modernize-tools/) 作为迁移实用工具。 此 [AEM现代化工具](https://opensource.adobe.com/aem-modernize-tools/) 提供了一套实用程序，用于将基于基础组件的自适应Forms转换为核心组件的现代化且受支持的功能。

## 什么是AEM现代化工具？

[AEM现代化工具](https://opensource.adobe.com/aem-modernize-tools/) 指一组实用程序或软件应用程序，旨在促进现代化或更新Adobe Experience Manager (AEM)项目。 这些工具通常有助于将AEM中的旧组件或功能转换为更新、更高效且受支持的替代项。

“AEM现代化工具”将基于旧的基础组件的自适应Forms转换为基于核心组件的较新表单。 此转换过程可确保表单符合现代标准和功能，从而潜在地提高AEM环境中的性能、兼容性和易维护性。

![AEM现代化工具](/help/forms/assets/aem-modernize-tools.png)

>[!NOTE]
> 
> 建议在本地AEM设置中安装AEM现代化工具。 将基于基础的表单迁移到基于核心组件的表单。 下载表单及其资产。 然后，将表单及其资源上传到所需的环境。

## 使用AEM现代化工具的先决条件

* [为AEM Forms设置本地开发环境](/help/forms/setup-local-development-environment.md)
* [为您的环境启用自适应Forms核心组件。](/help/forms/enable-adaptive-forms-core-components.md)

* 将您的用户添加到 [!DNL forms-users] 组。 董事会成员 [!DNL forms-users] 组有权创建自适应表单。

* 具有以下角色的用户有权在AEM环境中安装AEM现代化工具：
   * 开发人员角色
   * 管理员角色有关特定于表单的用户组的详细列表，请参阅 [组和权限](forms-groups-privileges-tasks.md).

## 安装和配置AEM现代化工具

安装和配置AEM现代化工具的步骤：

1. [将AEM现代化工具安装到本地AEM Forms环境](#install-aem-modernize-tools)
2. [为本地AEM Forms环境启用AEM现代化工具](#enable-aem-modernize-tools)

### 将AEM现代化工具安装到本地AEM Forms环境 {#install-aem-modernize-tools}

执行以下步骤，将AEM现代化工具安装到本地AEM Forms环境：

1. 通过从命令行执行以下命令来启动本地AEM Author Service：

   `java -jar aem-author-p4502.jar`

   >[!NOTE]
   >
   > 提供管理员密码作为 `admin`. 任何管理员密码都可以接受，但建议对本地开发使用默认密码以减少重新配置的需要。

1. 克隆 [AEM现代化工具](https://git.corp.adobe.com/livecycle/forms-modernizer/tree/convertForms) 本地系统中的存储库。

   ```Shell
   git clone [Path of Git repository of AEM Modernize Tools]
   ```
   替换 [AEM现代化工具的Git存储库路径] 以及AEM现代化工具的相应Git存储库的实际URL。
成功执行命令后，您的计算机上提供了AEM Modernize Tools存储库的本地副本。

1. 导航至`[AEM Modernize Tools Repository]`  在本地系统中。
1. 运行以下命令：

   ```Shell
       mvn clean install 
   ```
![成功安装映像](/help/forms/assets/aem-modernize-install-steps.png)

成功安装后，AEM现代化工具将可用于您的环境。

![启用AEM现代化工具](/help/forms/assets/enable-aem-modernizer-tools.png)


### 为本地AEM Forms环境启用AEM现代化工具{#enable-aem-modernize-tools}

要为您的AEM环境启用和使用AEM现代化工具，请务必映射将基础组件迁移到核心组件的规则：

1. 登录到您的创作实例。
1. 导航到 `http://[host]:[port]/system/console/configMgr`
1. 查找并编辑 `AEM Modernize Tools - Component Rewrite Rule Service`.
1. 添加 `Component Rule Paths` 作为 `/apps/forms-modernizer/rules`.
1. 单击 **保存** 以保存更改。

![AEM现代化组件规则](/help/forms/assets/aem-modernize-tools-component-rule.png)

## 运行AEM现代化工具以将基于基础组件的表单转换为基于核心组件的表单

1. 转到 **[!UICONTROL “工具”>“AEM现代化工具”>“Forms转化”]**.

   ![选择AEM现代化工具](/help/forms/assets/aem-modernize-tools-select.png)

1. 选择 **[!UICONTROL Forms转换]** 选项。

   ![选择Forms转换选项](/help/forms/assets/aem-modernize-forms-conversion.png)

1. 单击 **创建** 以创建新作业。

   ![AEM现代化工具创建作业](/help/forms/assets/aem-modernize-tools-create-job.png)

1. 指定 **[!UICONTROL 作业名称]**.
1. 在 **[!UICONTROL 表单]** 选项卡中，您可以选择以下选项之一：
   * **无** ：如果不需要表单处理，请选择此选项。
   * **恢复** ：选择此选项以将表单恢复到上次转换前的状态。
   * **复制到目标**：选择此选项可在执行转换之前复制表单。
在我们的例子中， **复制到目标** 已选中选项。 如果 **复制到目标** 选项，则 **[!UICONTROL 源路径]** 和 **[!UICONTROL 目标路径]** 选项将变为可见。

1. 指定 `source folder` 中的名称 **[!UICONTROL 源路径]**.
1. 指定 `target folder` 中的名称 **[!UICONTROL 目标路径]**.
1. 选择&#x200B;**[!UICONTROL 下一步]**。
1. 单击 **[!UICONTROL 添加Forms]**. 此页面中的 `source folder` 屏幕上会显示。
1. 选择基于基础组件的表单以将其转换为基于核心组件的表单。 您还可以选择多个表单。

   ![AEM现代化工具选择表单](/help/forms/assets/aem-modernize-tools-select-form.png)

1. 单击 **[!UICONTROL 选择]**.
1. 单击 **[!UICONTROL 计划作业]** 以开始转换过程。
1. 单击 **[!UICONTROL 转换]** 从 **[!UICONTROL 转换页面]** 对话框。

   ![AEM现代化工具转换页面](/help/forms/assets/aem-modernize-tools-convert-form.png)

   当进程的状态更改为 `success`. 导航至 `target folder` 查看转换后的表单。

   ![AEM现代化工具成功](/help/forms/assets/aem-modernize-tools-success.png)

1. 选择自适应表单，然后选择> **[!UICONTROL 属性]**. 这将打开“表单属性”页面。
   ![AEM现代化工具目标文件夹](/help/forms/assets/aem-modernize-tools-destination-folder.png)

1. 选择 **[!UICONTROL 保存并关闭]** 以再次保存已转换表单的属性。
   ![AEM现代化工具自适应表单属性](/help/forms/assets/aem-modernize-tools-af-properties.png)

现在，您可以看到基于基础组件构建的自适应表单已转换为基于核心组件构建的自适应表单。

## 使用迁移实用程序工具时的注意事项 {#considerations}

* 如果基于基础组件构建的表单包含自定义函数规则，则必须根据核心组件为转换后的表单重写这些规则。
* 转换后的表单在规则编辑器中不包含任何规则，因此需要重写转换后的表单的规则。
* 您必须为已转换的表单重新创建翻译作业。

## 最佳实践 {#best-practices}

* 基于基础组件构建的表单仅包含在基于核心组件的组件中找到的组件。
* 确保规则采用XML格式。


