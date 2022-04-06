---
title: 如何创建表单数据模型？
description: Experience Manager Forms数据集成提供了直观的用户界面，用于创建和使用表单数据模型。 了解如何使用或不使用配置的数据源来创建表单数据模型。
feature: Form Data Model
role: User, Developer
level: Beginner, Intermediate
exl-id: b17b7441-912c-44c7-a835-809f014a8c86
source-git-commit: 1e2b58015453c194af02fdae62c3735727981da1
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 0%

---

# 创建表单数据模型 {#create-form-data-model}

![数据集成](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] 数据集成提供了直观的用户界面，用于创建和使用表单数据模型。 表单数据模型依赖于数据源来交换数据；但是，无论是否具有数据源，您都可以创建表单数据模型。 根据您是否配置了数据源，可以通过两种方法来创建来自数据模型：

* **使用预配置的数据源**:如果您已按照 [配置数据源](configure-data-sources.md)，则可在创建表单数据模型时选择它们。 它从可用于表单数据模型的选定数据源中引入所有数据模型对象、属性和服务。

* **没有数据源**:如果尚未为表单数据模型配置数据源，则仍然可以在没有数据源的情况下创建它。 您可以使用表单数据模型创作自适应Forms <!--and interactive communication--> 然后用样本数据测试。 当数据源可用时，您可以将表单数据模型与数据源绑定，该数据源会自动反映在关联的自适应Forms中<!--and interactive communications-->.

>[!NOTE]
>
>您必须是这两者的成员 **fdm-author** 和 **forms-user** 群组，以便能够创建和使用表单数据模型。 联系您的 [!DNL Experience Manager] 管理员成为组的成员。

## 创建表单数据模型 {#data-sources}

确保已按照 [配置数据源](configure-data-sources.md). 请执行以下操作，以根据配置的数据源创建表单数据模型：

1. 在 [!DNL Experience Manager] 创作实例，导航到 **[!UICONTROL Forms >数据集成]**.
1. 点按 **[!UICONTROL 创建>表单数据模型]**.
1. 在创建表单数据模型对话框中：

   * 指定表单数据模型的名称。
   * (**可选**)为表单数据模型指定标题、描述和标记。
   * (**仅当配置了数据源时，才可选且适用**)点按 **[!UICONTROL 数据源配置]** 字段，然后选择云服务所在的配置节点。 它将下一页可供选择的数据源列表限制为选定配置节点中可用的数据源列表。 但是，任何JDBC数据库和 [!DNL Experience Manager] 默认情况下，会列出用户配置文件数据源。 如果不选择配置节点，则会列出来自所有配置节点的数据源。

1. 点按 **[!UICONTROL 下一个]**.

1. (**仅在配置数据源时适用**) **[!UICONTROL 选择数据源]** 屏幕会列出可用的数据源（如果有）。 选择要在表单数据模型中使用的数据源。
1. 点按 **[!UICONTROL 创建]** 在确认对话框上，点按 **[!UICONTROL 打开]** 打开表单数据模型编辑器。

   让我们查看表单数据模型编辑器UI的不同组件。

   ![具有三个数据源的表单数据模型 — RESTful服务， [!DNL Experience Manager] 用户配置文件和RDBMS。](assets/fdm-ui.png)

   A. **[!UICONTROL 数据源]** 列出表单数据模型中的数据源。 展开数据源以查看其数据模型对象和服务。

   B. **[!UICONTROL 刷新数据源定义]** 从已配置的数据源中获取数据源定义中的任何更改，并在表单数据模型编辑器的“数据源”选项卡中对其进行更新。

   C. **[!UICONTROL 模型]** 显示已添加数据模型对象的内容区域。

   D. **[!UICONTROL 服务]** 显示添加数据源操作或服务的内容区域。

   E. **[!UICONTROL 工具栏]** 用于处理表单数据模型的工具。 工具栏根据表单数据模型中的选定对象显示更多选项。

   F. **[!UICONTROL 添加选定项]** 将所选数据模型对象和服务添加到表单数据模型。

有关表单数据模型编辑器以及如何使用它编辑和配置表单数据模型的更多信息，请参阅 [使用表单数据模型](work-with-form-data-model.md).

## 更新数据源 {#update}

执行以下操作，以向现有表单数据模型添加或更新数据源。

1. 转到 **[!UICONTROL Forms >数据集成]**，选择要在其中添加或更新数据源的表单数据模型，然后点按 **[!UICONTROL 属性]**.
1. 在表单数据模型属性中，转到 **[!UICONTROL 更新源]** 选项卡。

   在 **[!UICONTROL 更新源]** 选项卡：

   * 点按 **[!UICONTROL 上下文感知配置]** 字段，然后选择要添加的数据源的云配置所在的配置节点。 如果您没有选择节点，则云配置仅驻留在 `global` 点按时会列出节点 **[!UICONTROL 添加源]**.

   * 要添加新数据源，请点按 **[!UICONTROL 添加源]** 并选择要添加到表单数据模型的数据源。 在中配置的所有数据源 `global` 将显示选定的配置节点（如果有）。

   * 要将现有数据源替换为同类型的其他数据源，请点按 **[!UICONTROL 编辑]** 图标，然后从可用数据源列表中选择。
   * 要删除现有数据源，请点按 **[!UICONTROL 删除]** 图标。 如果在表单数据模型中添加数据源中的数据模型对象，则会禁用“删除”图标。

      ![fdm-properties](assets/fdm-properties.png)

1. 点按 **[!UICONTROL 保存并关闭]** 以保存更新。

>[!NOTE]
>
>在表单数据模型中添加新数据源或更新现有数据源后，请确保在自适应Forms中（视情况而定）更新绑定引用<!--and interactive communications--> 使用更新的表单数据模型的报表包。

## 特定运行模式的上下文感知配置 {#runmode-specific-context-aware-config}

[!UICONTROL 表单数据模型] 利用 [Sling上下文感知配置](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/context-aware-configs.html) 支持不同的数据源参数以与不同 [!DNL Experience Manager] 运行模式。

When [!UICONTROL 表单数据模型] 使用云配置来存储参数，当通过源代码控制（Cloud-Manager GIT存储库）签入和部署该参数时，将为所有运行模式（开发、暂存和生产）使用相同的参数创建云配置。 但是，对于在测试和生产环境中需要使用不同数据集的用例，我们会将数据源参数（例如数据源URL）用于不同的 [!DNL Experience Manager] 运行模式。

要实现此目的，您需要创建一个包含数据源参数 — 值对的OSGi配置。 这会覆盖 [!UICONTROL 表单数据模型] 云配置。 由于OSGi配置默认支持这些运行模式，因此您可以根据运行模式将数据源参数覆盖为不同的值。

要在 [!UICONTROL 表单数据模型]:

1. 在本地开发实例上创建云配置。 有关详细步骤，请参阅 [如何配置数据源](/help/forms/configure-data-sources.md).

1. 将云配置存储到文件系统。
   1. 使用过滤器创建包 `/conf/{foldername}/settings/cloudconfigs/fdm`. 使用相同 `{foldername}` 在步骤1中。 和 `fdm` with `azurestorage` 用于Azure存储配置。
   1. 生成和下载包。 有关详细信息，请参阅 [包操作](/help/implementing/developing/tools/package-manager.md).

1. 在中集成云配置 [!DNL Experience Manager] 原型项目。
   1. 解压缩下载的包。
   1. 复制 `jcr_root` 文件夹，并将其放入 `ui.content` > `src` > `main` > `content`.
   1. 更新 `ui.content` > `src` > `main` > `content` > `META-INF` > `vault` > `filter.xml` 包含过滤器 `/conf/{foldername}/settings/cloudconfigs/fdm`. 有关详细信息，请参阅 [AEM项目原型的ui.content模块](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uicontent.html). 当通过CM管道部署此原型项目时，所有环境（或运行模式）上都会安装相同的云配置。 要根据环境更改云配置的字段（如URL）值，请使用以下步骤中讨论的OSGi配置。

1. 创建Apache Sling上下文感知配置。 要创建OSGi配置，请执行以下操作：
   1. **在 [!DNL Experience Manager] 原型项目。**
使用PID创建OSGi工厂配置文件 
`org.apache.sling.caconfig.impl.override.OsgiConfigurationOverrideProvider`. 在每个运行模式文件夹下创建同名文件，其中每个运行模式需要更改值。 有关详细信息，请参阅 [为配置OSGi [!DNL Adobe Experience Manager]](/help/implementing/deploying/configuring-osgi.md#creating-sogi-configurations).

   1. **设置OSGi配置json。** 要使用Apache Sling上下文感知配置覆盖提供程序，请执行以下操作：
      1. 关于本地开发实例 `/system/console/configMgr`，选择名为的工厂OSGi配置 **[!UICONTROL Apache Sling上下文感知配置覆盖提供程序：OSGi配置]**.
      1. 提供描述。
      1. 选择 **[!UICONTROL 已启用]**.
      1. 在覆盖下，提供sling覆盖语法中需要根据环境更改的字段。 有关详细信息，请参阅 [Apache Sling上下文感知配置 — 覆盖](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration-override.html#override-syntax). 例如， `cloudconfigs/fdm/{configName}/url="newURL"`.
通过选择 **[!UICONTROL +]**.
      1. 选择&#x200B;**[!UICONTROL 保存]**。
      1. 要获取OSGi配置JSON，请按照 [使用AEM SDK快速入门生成OSGi配置](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart).
      1. 将JSON放置到在上一步中创建的OSGi工厂配置文件中。
      1. 更改 `newURL` 基于环境（或运行模式）。
      1. 要根据运行模式更改密钥值，可使用 [cloud manager API](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) 稍后可在 [OSGi配置](/help/implementing/deploying/configuring-osgi.md#secret-configuration-values).
当通过CM管道部署此原型项目时，覆盖将在不同环境（或运行模式）中提供不同的值。

      >[!NOTE]
      >
      >[!DNL Adobe Managed Service] 用户可以使用加密支持加密密钥值(有关详细信息，请参阅 [对配置属性的加密支持](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/encryption-support-for-configuration-properties.html#enabling-encryption-support) 并将加密文本放在 [Service Pack 6.5.13.0中提供了上下文感知配置](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html#runmode-specific-context-aware-config).

1. 使用选项刷新数据源定义，以在 [表单数据模型编辑器](#data-sources) 要通过FDM UI刷新FDM缓存并获取最新配置，请执行以下操作：

## 下面的步骤 {#next-steps}

现在，您有一个表单数据模型，其中添加了数据源。 接下来，您可以编辑表单数据模型以添加和配置数据模型对象和服务、添加数据模型对象之间的关联、编辑属性、添加自定义数据模型对象和属性、生成示例数据等。

有关更多信息，请参阅 [使用表单数据模型](work-with-form-data-model.md).
