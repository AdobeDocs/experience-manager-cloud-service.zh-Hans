---
title: 如何创建表单数据模型(FDM)？
description: 了解如何创建表单数据模型(FDM)，以及使用自适应表单或AEM Workflow向数据源发送或检索数据。
feature: Adaptive Forms, Form Data Model
role: User, Developer
level: Beginner, Intermediate
exl-id: b17b7441-912c-44c7-a835-809f014a8c86
source-git-commit: 7b31a2ea016567979288c7a8e55ed5bf8dfc181d
workflow-type: tm+mt
source-wordcount: '1543'
ht-degree: 1%

---

# 创建表单数据模型(FDM) {#create-form-data-model}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html) |
| AEM as a Cloud Service | 本文 |


![数据集成](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms]数据集成提供了一个直观的用户界面，用于创建和使用表单数据模型。 表单数据模型(FDM)依赖于数据源进行数据交换；但是，您可以创建具有或不具有数据源的表单数据模型(FDM)。 根据您是否配置了数据源，可使用两种方法从数据模型创建：

* **使用预配置的数据源**：如果您已按照[配置数据源](configure-data-sources.md)中的说明配置数据源，则可以在创建表单数据模型(FDM)时选择它们。 它提供选定数据源中的所有数据模型对象、属性和服务，可用于表单数据模型(FDM)。

* **没有数据源**：如果尚未为表单数据模型(FDM)配置数据源，则仍可以创建它而不使用数据源。 您可以使用表单数据模型(FDM)创作自适应Forms <!--and interactive communication-->并使用示例数据测试它们。 在数据源可用时，您可以将表单数据模型(FDM)与数据源绑定，数据源会自动反映在关联的自适应Forms<!--and interactive communications-->中。

>[!NOTE]
>
>您必须是&#x200B;**fdm-author**&#x200B;和&#x200B;**forms-user**&#x200B;组的成员才能创建和使用表单数据模型(FDM)。 请与您的[!DNL Experience Manager]管理员联系以成为组的成员。

## 创建表单数据模型(FDM) {#data-sources}

请确保已配置要在表单数据模型(FDM)中使用的数据源，如[配置数据源](configure-data-sources.md)中所述。 执行以下操作以基于配置的数据源创建表单数据模型(FDM)：

1. 在[!DNL Experience Manager]创作实例中，导航到&#x200B;**[!UICONTROL Forms >数据集成]**。
1. 选择&#x200B;**[!UICONTROL 创建>表单数据模型]**。
1. 在创建表单数据模型对话框中：

   * 指定表单数据模型(FDM)的名称。
   * （**可选**）为表单数据模型(FDM)指定标题、描述和标记。
   * （**可选，并且仅在配置了数据源时适用**）选择&#x200B;**[!UICONTROL 数据Source配置]**&#x200B;字段旁边的勾号图标，然后选择您要使用的数据源的云服务所在的配置节点。 它将在下一页上可供选择的数据源列表限制为所选配置节点中的可用数据源列表。 但是，默认情况下会列出所有[!DNL Experience Manager]用户配置文件数据源。 如果不选择配置节点，则会列出所有配置节点的数据源。

1. 选择&#x200B;**[!UICONTROL 下一步]**。

1. （**仅当配置了数据源时才适用**）**[!UICONTROL 选择数据源]**&#x200B;屏幕列出了可用的数据源（如果有）。 选择要在表单数据模型中使用的数据源。
1. 选择&#x200B;**[!UICONTROL 创建]**，然后在确认对话框中，选择&#x200B;**[!UICONTROL 打开]**&#x200B;以打开表单数据模型编辑器。

   让我们查看表单数据模型编辑器UI的不同组件。

   ![具有三个数据源的表单数据模型 — RESTful服务、[!DNL Experience Manager]用户配置文件和RDBMS](assets/fdm-ui.png)

   A. **[!UICONTROL 数据源]**&#x200B;列出表单数据模型中的数据源。 展开数据源以查看其数据模型对象和服务。

   B. **[!UICONTROL 刷新数据Source定义]**&#x200B;从配置的数据源中获取数据源定义中的任何更改，并在表单数据模型编辑器的“数据源”选项卡中更新它们。

   C. **[!UICONTROL 模型]**&#x200B;显示添加的数据模型对象的内容区域。

   D. **[!UICONTROL 服务]**&#x200B;显示添加的数据源操作或服务的内容区域。

   E. **[!UICONTROL 工具栏]**&#x200B;用于表单数据模型(FDM)的工具。 工具栏根据表单数据模型(FDM)中的选定对象显示更多选项。

   F. **[!UICONTROL 添加选定项]**&#x200B;将选定数据模型对象和服务添加到表单数据模型。

有关表单数据模型编辑器以及如何使用它来编辑和配置表单数据模型(FDM)的详细信息，请参阅[使用表单数据模型](work-with-form-data-model.md)。

## 更新数据源 {#update}

执行以下操作以将数据源添加或更新到现有表单数据模型(FDM)。

1. 转到&#x200B;**[!UICONTROL Forms >数据集成]**，选择要添加或更新数据源的表单数据模型(FDM)，然后选择&#x200B;**[!UICONTROL 属性]**。
1. 在“表单数据模型”属性中，转到&#x200B;**[!UICONTROL 更新Source]**&#x200B;选项卡。

   在&#x200B;**[!UICONTROL 更新Source]**&#x200B;选项卡中：

   * 在&#x200B;**[!UICONTROL 上下文感知配置]**&#x200B;字段中选择浏览图标，然后选择要添加的数据源的云配置驻留的配置节点。 如果不选择节点，则在选择&#x200B;**[!UICONTROL 添加源]**&#x200B;时，将列出仅驻留在`global`节点中的云配置。

   * 要添加新数据源，请选择&#x200B;**[!UICONTROL 添加源]**，然后选择要添加到表单数据模型(FDM)的数据源。 将显示在`global`中配置的所有数据源和选定的配置节点（如果有）。

   * 要将现有数据源替换为相同类型的另一个数据源，请选择该数据源的&#x200B;**[!UICONTROL 编辑]**&#x200B;图标，然后从可用数据源列表中选择。
   * 要删除现有数据源，请选择数据源的&#x200B;**[!UICONTROL 删除]**&#x200B;图标。 如果在表单数据模型(FDM)中添加了数据源中的数据模型对象，则“删除”图标将被禁用。

     ![fdm-properties](assets/fdm-properties.png)

1. 选择&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;以保存更新。

>[!NOTE]
>
>在表单数据模型(FDM)中添加新数据源或更新现有数据源后，请确保在使用更新的表单数据模型(FDM)的自适应Forms<!--and interactive communications-->中更新相应的绑定引用。

## 特定运行模式的上下文感知配置 {#runmode-specific-context-aware-config}

[!UICONTROL 表单数据模型(FDM)]利用[Sling上下文感知配置](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/context-aware-configs.html)支持不同的数据源参数以连接不同[!DNL Experience Manager]运行模式的数据源。

当[!UICONTROL 表单数据模型(FDM)]使用云配置存储参数时，这些参数在签入并通过源代码管理（Cloud-Manager GIT存储库）部署时会为所有运行模式（开发、暂存和生产）创建具有相同参数的云配置。 但是，对于测试和生产环境需要拥有不同数据集的用例，我们为不同的[!DNL Experience Manager]运行模式使用数据源参数（例如，数据源URL）。

要实现此目的，您需要创建包含数据源参数 — 值对的OSGi配置。 此操作在运行时覆盖[!UICONTROL 表单数据模型(FDM)]云配置中的相同对。 由于OSGi配置默认支持这些运行模式，因此您可以根据运行模式将数据源参数覆盖为不同的值。

要在[!UICONTROL 表单数据模型(FDM)]中启用特定于部署的云配置，请执行以下操作：

1. 在本地开发实例上创建云配置。 有关详细步骤，请参阅[如何配置数据源](/help/forms/configure-data-sources.md)。

1. 将云配置存储到文件系统。
   1. 使用筛选器`/conf/{foldername}/settings/cloudconfigs/fdm`创建包。 使用与步骤1中相同的`{foldername}`。 并将`fdm`替换为Azure存储配置的`azurestorage`。
   1. 生成并下载包。 有关详细信息，请参阅[包操作](/help/implementing/developing/tools/package-manager.md)。

1. 在[!DNL Experience Manager]原型项目中集成云配置。
   1. 解压缩下载的包。
   1. 复制`jcr_root`文件夹并将其放入您的`ui.content` > `src` > `main` > `content`。
   1. 更新`ui.content` > `src` > `main` > `content` > `META-INF` > `vault` > `filter.xml`以包含筛选器`/conf/{foldername}/settings/cloudconfigs/fdm`。 有关详细信息，请参阅AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uicontent.html)的[ui.content模块。 当通过CM管道部署此原型项目时，将在所有环境（或运行模式）上安装相同的云配置。 要根据环境更改云配置的字段（如URL）值，请使用以下步骤中讨论的OSGi配置。

1. 创建Apache Sling上下文感知配置。 要创建OSGi配置，请执行以下操作：
   1. **在[!DNL Experience Manager]原型项目中设置OSGi配置文件。**
创建PID为`org.apache.sling.caconfig.impl.override.OsgiConfigurationOverrideProvider`的OSGi工厂配置文件。 在每个运行模式文件夹下创建同名文件，其中每个运行模式需要更改值。 有关详细信息，请参阅[为 [!DNL Adobe Experience Manager]](/help/implementing/deploying/configuring-osgi.md#creating-sogi-configurations)配置OSGi。

   1. **设置OSGI配置json。**&#x200B;要使用Apache Sling上下文感知配置覆盖提供程序：
      1. 在本地开发实例`/system/console/configMgr`上，选择名为&#x200B;**[!UICONTROL Apache Sling上下文感知配置覆盖提供程序]**&#x200B;的工厂OSGi配置。
      1. 提供描述。
      1. 选择&#x200B;**[!UICONTROL 已启用]**。
      1. 在覆盖下，根据sling覆盖语法中的环境，提供需要更改的字段。 有关详细信息，请参阅[Apache Sling上下文感知配置 — 覆盖](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration-override.html#override-syntax)。 例如，`cloudconfigs/fdm/{configName}/url="newURL"`。
通过选择**[!UICONTROL +]**，可以添加多个覆盖。
      1. 选择&#x200B;**[!UICONTROL 保存]**。
      1. 要获取OSGi配置JSON，请按照[使用AEM SDK快速入门](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart)生成OSGi配置中的步骤操作。
      1. 将JSON放置在上一步中创建的OSGi工厂配置文件中。
      1. 根据环境（或运行模式）更改`newURL`的值。
      1. 要基于运行模式更改密码值，可使用[Cloud Manager API](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties)创建密码变量，以后可在[OSGi配置](/help/implementing/deploying/configuring-osgi.md#secret-configuration-values)中引用。
当通过CM管道部署此原型项目时，覆盖将在不同的环境（或运行模式）中提供不同的值。
      >[!NOTE]
      >
      >[!DNL Adobe Managed Service]用户可以使用加密支持来加密密钥值(有关详细信息，请参阅对配置属性的[加密支持](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/encryption-support-for-configuration-properties.html#enabling-encryption-support)，并将加密文本置于[上下文感知配置在service pack 6.5.13.0](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html#runmode-specific-context-aware-config)中可用后的值中。

1. 使用[表单数据模型编辑器](#data-sources)中刷新数据源定义的选项刷新数据源定义，以通过FDM UI刷新FDM缓存并获取最新配置。

## 后续步骤 {#next-steps}

现在，您拥有一个添加了数据源的表单数据模型(FDM)。 接下来，可以编辑表单数据模型(FDM)以添加和配置数据模型对象和服务，添加数据模型对象之间的关联，编辑属性，添加自定义数据模型对象和属性，生成示例数据，等等。

有关详细信息，请参阅[使用表单数据模型](work-with-form-data-model.md)。


>[!MORELIKETHIS]
>
>* [使用表单数据模型(FDM)](/help/forms/using-form-data-model.md)