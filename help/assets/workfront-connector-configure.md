---
title: 配置 [!DNL Workfront for Experience Manager enhanced connector]
description: 配置 [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: d4e1247a-342c-4bc4-83bf-4e4902468fb3
source-git-commit: e2505c0fec1da8395930f131bfc55e1e2ce05881
workflow-type: tm+mt
source-wordcount: '1770'
ht-degree: 1%

---

# 配置 [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-configure.html) |
| AEM as a Cloud Service | 本文 |

在中具有管理员访问权限的用户 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 安装增强型连接器后对其进行配置。 有关安装说明，请参阅 [安装连接器](/help/assets/workfront-integrations.md).

>[!IMPORTANT]
>
> 自2022年6月起，Adobe发布了一个新的原生集成，用于将Workfront与Adobe Experience Manager Assetsas a Cloud Service连接。 这种集成已成为连接这两种解决方案的必需方法。 阻止将来Workfront与AEM Assetsas a Cloud Service连接的增强型连接器（1.9.8及更高版本）的任何新实施。

>[!IMPORTANT]
>
>* Adobe需要部署和配置 [!DNL Adobe Workfront for Experience Manager enhanced connector] 仅通过认证合作伙伴或 [!DNL Adobe Professional Services]. 如果部署与配置时没有认证合作伙伴或 [!DNL Adobe Professional Services]，Adobe不支持它。
>
>* Adobe可能会将更新发布到 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 使此连接器成为冗余连接器；如果发生这种情况，客户可能需要从使用此连接器过渡到使用此连接器。
>
>* Adobe支持增强型连接器版本1.7.4及更高版本。 不支持以前的预发行版和自定义版本。 要检查增强的连接器版本，请参阅的步骤5(a) [增强型连接器安装说明](workfront-connector-install.md).
>
>* 请参阅 [Workfront for Experience Manager Assets增强型连接器的合作伙伴认证考试](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). 有关考试的信息，请参见 [考试指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

## 配置事件订阅 {#event-subscriptions}

事件订阅用于通知AEM中发生的事件 [!DNL Adobe Workfront]. 有三个 [!DNL Workfront for Experience Manager enhanced connector] 需要事件订阅才能正常使用的功能包括：

* 自动创建项目链接文件夹。
* 将Workfront文档自定义表单值中的更改同步到AEM资源元数据。
* 项目完成后将资源自动发布到Brand Portal。

要使用这些功能，请启用事件订阅。

* 编辑 [!UICONTROL Workfront Tools] 您在步骤5中创建的Cloud Service配置，然后选择 [!UICONTROL 活动订阅] 选项卡。
* 选择 [!UICONTROL Workfront自定义集成] 您在第6节中创建了。
* 单击 [!UICONTROL 启用Workfront事件订阅].

  ![事件订阅](/help/assets/assets/event-subs.png)

## 配置链接的文件夹 {#linked-folders}

要订阅事件，请执行以下步骤：

1. 导航至 **[!UICONTROL 活动订阅]** 选项卡。
1. 选择在中创建的自定义集成 [!DNL Workfront].
1. 单击 **[!UICONTROL 启用Workfront事件订阅]**.

### 链接的文件夹结构配置 {#linked-folder-structure}

1. 转到云服务中的项目链接文件夹选项卡。
1. 链接文件夹父路径：选择DAM中要创建链接文件夹的文件夹。 如果留空，则默认为/content/dam。 确保Workfront工具元数据架构和Workfront链接文件夹元数据架构已应用于所选文件夹。
1. 链接的文件夹结构：输入逗号分隔的值。 每个值应 `DE:<some-project-custom-form-field>`、Portfolio、项目、年份、名称或某个“文本字符串值”（最后一个，带引号）。 它当前设置为Portfolio、项目、年、DE：项目类型、名称。
1. 如果Workfront中的文件夹标题应包括结构中的所有文件夹，则应选中使用文件夹结构名称在Workfront中构建链接的文件夹标题。 否则，它是最后一个文件夹的标题。
1. 子文件夹多字段允许您指定应创建为链接文件夹的子文件夹的文件夹列表。
1. 项目状态：选择要为其设置项目以创建链接文件夹的状态。
1. 在具有项目组合的项目中创建链接文件夹：项目必须属于的Portfolio列表，以便您可以创建链接文件夹。 将此列表留空可为所有项目组合创建链接文件夹。
1. 在具有自定义表单字段的项目中创建链接文件夹：自定义表单字段及其项目必须具有的相应值，以便您可以创建链接文件夹。 如果留空，将忽略此配置。 选择 `CUSTOM FORMS: Create DAM Linked Folder` 字段和输入 `Yes` 值。
1. 单击启用自动创建链接的文件夹。 如果您返回到“事件订阅”选项卡，现在可以看到有一个创建事件。

![链接的文件夹配置](/help/assets/assets/wf-linked-folder-config.png)

## 元数据架构映射 {#metadata-schema-mapping}

### 配置文件夹元数据映射 {#folder-metadata-mapping}

Workfront项目和AEM文件夹之间的元数据映射在AEM文件夹元数据架构中定义。 应像往常一样，在AEM中创建和配置文件夹元数据架构。 Workfront Tools将自动完成下拉列表添加到每个文件夹元数据架构表单字段的设置配置选项卡中。 此自动完成下拉菜单可让您指定每个AEM文件夹属性应映射到的Workfront字段。

要配置映射，请执行以下步骤：

1. 添加 `jcr:read` 权限 `/conf/global/settings/dam/adminui-extension/foldermetadataschema` 对象 `wf-workfront-users` 组。
1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 文件夹元数据架构]**.
1. 选择要编辑的文件夹元数据架构表单，然后单击编辑。
1. 选择要编辑的文件夹元数据架构表单字段，然后选择右侧面板上的设置选项卡。
1. 在 [!UICONTROL 从Workfront字段映射] 字段中，选择要映射到选定AEM文件夹属性的Workfront字段的名称。 可用选项包括：

   * 项目自定义表单字段
   * 项目概述字段(ID、名称、说明、参考编号、计划完成日期、项目所有者、项目发起人、Portfolio或项目群)

![元数据映射配置](/help/assets/assets/wf-metadata-mapping-config2.png)

### 配置资源元数据映射 {#asset-metadata-mapping}

Adobe Workfront文档与资源之间的元数据映射在AEM元数据架构中定义。 应像往常一样，在AEM中创建和配置元数据架构。 Workfront工具将配置选项添加到每个元数据架构表单字段的设置配置选项卡中。 利用这些选项，可指定每个AEM属性应映射到的Workfront字段。

要配置映射，请执行以下步骤：

1. 导航到 **工具** > **资产** > **元数据架构**.
1. 选择要编辑的元数据架构表单，然后单击 **编辑** 或从头开始创建元数据架构。
1. 选择要编辑的元数据架构表单字段，然后选择 **设置** 选项卡。
1. 在 [!DNL Workfront] 自定义表单字段选择 [!DNL Workfront] 要映射到选定AEM属性的字段。 可用选项包括：

   * 文档自定义表单字段
   * 项目自定义表单字段
   * 发布自定义表单字段
   * 任务自定义表单字段
   * 项目概述字段（ID、名称、描述或参考编号）

1. 如果 [!DNL Workfront] 字段已选择 [!UICONTROL Workfront自定义表单字段] 是Workfront User预输入字段，因此需要指定要映射的Workfront User字段。 为此，请选中从Workfront引用的对象字段中获取值，然后指定以下内容的名称： [!UICONTROL Workfront用户自定义表单字段] 以从中检索要映射的值。

   ![元数据映射配置](/help/assets/assets/wf-metadata-mapping-config1.png)

## 映射属性 {#map-property}

此工作流步骤允许用户将资产映射到 [!DNL Workfront] 项目、任务、问题或文档中的自定义表单。 此 [!DNL Workfront] 此步骤影响的工件使用有效负荷中的相对路径查找。 要映射的属性可通过步骤对话框配置进行控制。

**类型**：利用此字段，可选择属性应映射到的Workfront对象类型。

**ID属性**：利用此字段，可指定属性应映射到的Workfront对象ID的路径。 此字段中指定的路径应当相对于工作流有效负载。

**属性分配**：利用此多字段，可指定AEM属性与Workfront字段之间的映射。 多字段中的每一项将指定一个映射。 每个映射应具有格式 `<workfront-field>=<aem-mapped-property>`.

* 此 `workfront-field` 可以是

   * 由前缀标识的自定义表单字段 `DE:`.
   * 由其名称标识的可编辑字段。 字段名称可在 [[!DNL Workfront] API资源管理器](https://experience.workfront.com/s/api-explorer).

* 此 `aem-mapped-property` 可以是：

   * 文本值。 应使用引号将它们括起来。
   * AEM资产。 此引用应当相对于工作流有效负荷。
   * 命名值。 应使用括号括住。
   * 上述3个项目的拼接。 使用以下方式指定 `{+}`.
   * 通过将值围绕在上，对上述三个项目进行了更改 `{replace(<value>,"old-char","new-char")}`.

* 一些示例包括：

   * `status="INP"`
   * `DE:Asset Type=jcr:content/metadata/assetType`
   * `DE:Path={path}`
   * `URL="https://my-aem-author/assets.html"{+}{path}`

![用于映射属性的配置](/help/assets/assets/wf-map-property-config.png)

## 设置状态 {#set-status}

在工作流编辑器中，编辑的属性 **[!UICONTROL Workfront — 设置状态]** 在 **[!UICONTROL 参数]** 选项卡。

![编辑工作流以设置状态](/help/assets/assets/wf-set-status.png)

## 注释同步 {#comments-sync}

1. 在 [!DNL Experience Manager]，访问 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Workfront工具配置]**，选择配置，然后选择 **[!UICONTROL 属性]**.

   ![评论同步](/help/assets/assets/comments-sync1.png)

1. 选择 **[!UICONTROL 活动订阅]** 选项卡，单击 **[!UICONTROL 启用评论同步]** 日期 **[!UICONTROL 将Workfront中的注释发送到AEM]** 选项。

   ![已启用同步](/help/assets/assets/wf-comment-sync-enabled.png)

要测试从Workfront到AEM的注释同步，请执行以下步骤：

1. 导航到Workfront中的链接文档，并在更新选项卡中添加评论。

   ![在Workfront中发表评论](/help/assets/assets/comments-sync2.png)

1. 导航到AEM中的同一链接文档，选择该文档并打开 [!UICONTROL 时间线] 选项，然后选择 [!UICONTROL 评论]. 左侧边栏显示从中进行同步的评论 [!DNL Workfront].

## 资源版本 {#asset-versions}

要在AEM中维护资源的版本历史记录，请在AEM中配置资源版本控制。

1. 在Experience Manager中，访问 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Workfront工具配置]**，然后打开 **[!UICONTROL 高级]** 选项卡。

1. 选择选项 **[!UICONTROL 存储与现有资源版本同名的资源]**. 选中此选项后，可将与现有资产版本上传的同名资产存储到相同位置。 如果不选中此项，则使用不同的名称创建一个新资产(例如， `asset-name.pdf` 和 `asset-name-1.pdf`)。

1. 选择选项 **[!UICONTROL 创建新版本时更新资源元数据]**. 选中此选项后，会在创建新版本的资源时更新资源元数据。 如果未选中，则资源将保留其在创建新版本之前拥有的元数据。

![配置资源版本控制](/help/assets/assets/wf-config-versioning.png)

>[!NOTE]
>
>链接的文件夹不支持版本控制。 创建时 [!DNL Workfront] 文档位于链接的文件夹中的校对，资产早期版本上的注释和批注将被移除。

## 附加自定义表单 {#attach-custom-forms}

此工作流步骤允许用户将自定义表单附加到 [!DNL Workfront] 成品。 此工作流步骤可以添加到任何工作流模型中。 此 [!DNL Workfront] 此步骤影响的工件使用有效负荷中的相对路径查找。

在Experience Manager的工作流编辑器中，编辑 [!UICONTROL Workfront — 附加自定义表单] 工作流步骤。

![自定义表单](/help/assets/assets/wf-custom-forms.png).

## 自动发布资产 {#auto-publish-assets}

1. 在Experience Manager中，访问 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Workfront工具配置]**，然后打开 **[!UICONTROL 高级]** 选项卡。

1. 选择 **[!UICONTROL 从Workfront发送时自动发布资源]**. 当资产从Workfront发送到AEM时，此选项支持自动发布资产。 可以通过指定Workfront自定义表单字段及其应设置为的值，有条件地启用此功能。 无论何时将文档发送到AEM，如果它满足条件，则资源会自动发布。

1. 选择 **[!UICONTROL 项目完成后，将所有项目资源发布到Brand Portal]**. 此选项允许将资产自动发布到 [!DNL Brand Portal] 当他们所属的Workfront项目的状态更改为 `Complete`.

![配置自动发布](/help/assets/assets/wf-auto-publish-config.png)

## Workfront文档自定义表单更新 {#subscribe-workfront-doc-custom-form-updates}

要订阅中的更改，请执行以下操作 [!DNL Workfront] 要记录自定义表单，请在 **[!UICONTROL 高级]** 选项卡。 当您订阅这些更新时，它会更新您的映射 [!DNL Experience Manager] 当中的相应字段为元数据字段时 [!DNL Workfront] 文档自定义表单已更改。

![Workfront文档自定义表单更新中的配置 [!DNL Experience Manager]](/help/assets/assets/wf-custom-form-update.png)
