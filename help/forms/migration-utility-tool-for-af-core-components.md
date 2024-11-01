---
title: 迁移实用程序工具/AEM现代化工具，用于将基于基础组件的自适应Forms转换为基于核心组件的表单
description: 了解如何安装并使用迁移实用程序/AEM现代化工具将基于基础组件的自适应Forms转换为基于核心组件的表单。
Keywords: Migration Utility Tool, Convert Adaptive Forms based on Foundation Components to Core Component based forms, Convert Foundation forms to Core Components forms, Using Modernizer Tool to convert Foundation Components to Core Components in forms.
role: User, Developer, Admin
features: core components
hide: true
hidefromtoc: true
exl-id: ee71a576-96a7-4c81-b3a3-1d678f010cba
feature: Adaptive Forms, Core Components
source-git-commit: c52d649e569ef427e70c85a88fa0f48fcc534e9e
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 4%

---

# 简介

<span class="preview">该功能在早期采用者计划下可用。 您可以使用官方电子邮件 ID 写信给 aem-forms-ea@adobe.com，加入早期采用者计划并申请使用该功能。</span>

Forms转换实用程序是[AEM现代化工具](https://opensource.adobe.com/aem-modernize-tools/)套件的一部分，可帮助您轻松地将使用旧的基础组件构建的自适应Forms转换为利用核心组件的现代、受支持功能的表单。

## 什么是AEM现代化工具？

[AEM现代化工具](https://opensource.adobe.com/aem-modernize-tools/)是指一组旨在促进现代化或更新Adobe Experience Manager (AEM)项目的实用程序或软件应用程序。 这些工具通常有助于将AEM中的旧组件或功能转换为更新、更高效且受支持的替代项。 Forms转换实用程序安装在“AEM现代化工具”下，用于将基于基础组件的自适应Forms转换为基于核心组件的表单。

Forms转换实用程序将基于旧版基础组件的自适应Forms转换为基于新版核心组件的表单。 此转换过程可确保表单符合现代标准和功能，从而潜在地提高AEM环境中的性能、兼容性和易维护性。

![AEM现代化工具](/help/forms/assets/aem-modernize-tools.png)

>[!NOTE]
> 
> 建议在本地AEM设置中安装AEM现代化工具。 将基于基础组件的自适应Forms迁移到基于核心组件的表单。 下载表单及其资产。 然后，将表单及其资源上传到所需的环境。

## 使用AEM现代化工具时的注意事项 {#considerations}

* 成功转换后，将删除应用于表单的所有规则。 规则不会自动迁移。 您应该手动重新创建这些规则，并将其应用到转换后的表单。
* 原始表单中使用的翻译设置不会延续。 为转换后的表单重新配置翻译。
  <!-- * If the form built on Foundation Components contains custom function rules, you have to rewrite these rules for the converted form based on Core Components.-->

## 使用AEM现代化工具的先决条件

* [为AEM Forms设置本地开发环境](/help/forms/setup-local-development-environment.md)
* [为您的环境启用自适应Forms核心组件。](/help/forms/enable-adaptive-forms-core-components.md)

* 将您的用户添加到[!DNL forms-users]组。 [!DNL forms-users]组的成员有权创建自适应表单。

* 具有以下角色的用户有权在AEM环境中安装AEM现代化工具：
   * 开发人员角色
   * 管理员角色

有关特定于表单的用户组的详细列表，请参阅[组和权限](forms-groups-privileges-tasks.md)。

## 安装和配置AEM现代化工具

安装和配置AEM现代化工具：

1. [将AEM现代化工具安装到本地AEM Forms环境](#install-aem-modernize-Tools)
2. [为本地AEM Forms环境启用AEM现代化工具](#enable-aem-modernize-Tools)

### 将AEM现代化工具安装到本地AEM Forms环境 {#install-aem-modernize-Tools}

执行以下步骤，将AEM现代化工具安装到本地AEM Forms环境：

1. 打开命令提示符或终端。
1. 启动本地AEM创作服务。 例如，从执行以下代码以启动本地AEM创作实例：

   `java -jar aem-author-p4502.jar`

1. 在本地系统中克隆[AEM Modernize Tool](/help/journey-migration/refactoring-tools/aem-modernization-tools.md)存储库。

   ```Shell
   git clone [Path of Git repository of AEM Modernize Tool]
   ```

   成功执行该命令后，您的计算机上即存在AEM Modernize Tool存储库的本地副本。

1. 导航到本地系统中的`[AEM Modernize Tool Repository]`。
1. 运行以下命令：

   ```Shell
       mvn clean install 
   ```
![成功安装映像](/help/forms/assets/aem-modernize-install-steps.png)

成功安装后，AEM现代化工具将可用于您的环境。

![启用AEM迁移实用工具工具](/help/forms/assets/enable-aem-modernizer-tools.png)


### 为本地AEM Forms环境启用AEM现代化工具{#enable-aem-modernize-Tools}

要为您的AEM环境启用和使用AEM现代化工具，请务必映射用于将Foundation组件迁移到核心组件的规则：

1. 登录到您的创作实例。
1. 导航到`http://[host]:[port]/system/console/configMgr`
1. 查找并编辑`AEM Modernize Tools - Component Rewrite Rule Service`。
1. 将`Component Rule Paths`添加为`/apps/forms-modernizer/rules`。
1. 单击&#x200B;**保存**&#x200B;以保存更改。

![AEM现代化组件规则](/help/forms/assets/aem-modernize-tools-component-rule.png)

## 运行表单转换实用程序，将基于基础组件的表单转换为基于核心组件的表单

1. 转到&#x200B;**[!UICONTROL 工具> AEM现代化工具> Forms转换]**。

   ![选择AEM现代化工具](/help/forms/assets/aem-modernize-tools-select-form.png)

1. 选择&#x200B;**[!UICONTROL Forms转换]**&#x200B;选项。

   ![选择Forms转换选项](/help/forms/assets/aem-modernize-forms-conversion.png)

1. 单击&#x200B;**创建**&#x200B;以创建新作业。

   ![AEM现代化工具创建作业](/help/forms/assets/aem-modernize-tools-create-job.png)

1. 指定&#x200B;**[!UICONTROL 作业名称]**。
1. 在&#x200B;**[!UICONTROL 表单]**&#x200B;选项卡中，您可以选择以下选项之一：
   * **无** ：如果不想在开始表单转换之前创建基于Foundation组件的表单的副本，请选择选项。
   * **还原** ：选择选项以将表单还原到开始表单转换之前的状态。
   * **复制到Target**：选择相应选项以在开始表单转换之前创建基于Foundation组件的表单的副本。
在本例中，已选择**复制到目标**&#x200B;选项。 如果选择了&#x200B;**复制到目标**&#x200B;选项，则&#x200B;**[!UICONTROL Source路径]**&#x200B;和&#x200B;**[!UICONTROL 目标路径]**&#x200B;选项将变为可见。

1. 在&#x200B;**[!UICONTROL Source路径]**&#x200B;中指定`source folder`名称。
1. 在&#x200B;**[!UICONTROL 目标路径]**&#x200B;中指定`target folder`名称。
1. 选择&#x200B;**[!UICONTROL 下一步]**。
1. 单击&#x200B;**[!UICONTROL 添加Forms]**。 `source folder`中的所有表单都会显示在屏幕上。
1. 选择基于基础组件的自适应Forms以将其转换为基于核心组件的表单。 您还可以选择多个表单。

   ![AEM现代化工具选择表单](/help/forms/assets/aem-modernize-tools-select-form.png)

1. 单击&#x200B;**[!UICONTROL 选择]**。
1. 单击&#x200B;**[!UICONTROL 计划作业]**&#x200B;开始转换过程。
1. 在&#x200B;**[!UICONTROL 转换页面]**&#x200B;对话框中单击&#x200B;**[!UICONTROL 转换]**。

   ![AEM现代化工具转换页面](/help/forms/assets/aem-modernize-tools-convert-form.png)

   进程状态更改为`success`时。 导航到`target folder`以查看转换后的表单。

   ![AEM现代化工具成功](/help/forms/assets/aem-modernize-tools-success.png)

1. 选择自适应表单，然后选择> **[!UICONTROL 属性]**。 这将打开“表单属性”页面。
   ![AEM现代化工具目标文件夹](/help/forms/assets/aem-modernize-tools-destination-folder.png)

1. 选择&#x200B;**[!UICONTROL 保存并关闭]**以再次保存已转换表单的属性。
   ![AEM现代化工具自适应表单属性](/help/forms/assets/aem-modernize-tools-af-properties.png)

现在，您可以看到基于基础组件构建的自适应表单已转换为基于核心组件构建的自适应表单。

## 最佳实践 {#best-practices}

* 确保您的基于基础组件的表单，仅使用具有等效的[核心组件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction#available-components-a-breakdown-by-component-type)的组件。 如果您使用的基础组件没有等效的核心组件，则不会转换基础组件。 因此，它在创作表单时无法正常运行
* 确保将基础组件转换为核心组件的规则采用XML格式。
