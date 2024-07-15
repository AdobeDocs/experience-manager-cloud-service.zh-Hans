---
title: 配置 [!DNL Workfront for Experience Manager enhanced connector]
description: 配置 [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Workfront Integrations and Apps
exl-id: d4e1247a-342c-4bc4-83bf-4e4902468fb3
source-git-commit: 257930bc2633a0d31ad3bd28305b8159597befa5
workflow-type: tm+mt
source-wordcount: '1767'
ht-degree: 1%

---

# 配置 [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-configure.html) |
| AEM as a Cloud Service | 本文 |

在[!DNL Adobe Experience Manager]中具有[!DNL Cloud Service]管理员访问权限的用户在安装增强型连接器后对其进行配置。 有关安装说明，请参阅[安装连接器](/help/assets/workfront-integrations.md)。

>[!IMPORTANT]
>
> 自2022年6月起，Adobe发布了一个新的原生集成，用于将Workfront与Adobe Experience Manager Assetsas a Cloud Service连接。 这种集成已成为连接这两种解决方案的必需方法。 阻止将来as a Cloud Service与WorkfrontAEM Assets连接的增强型连接器（1.9.8及更高版本）的任何新实施。

>[!IMPORTANT]
>
>* Adobe仅需要通过认证合作伙伴或[!DNL Adobe Professional Services]来部署和配置[!DNL Adobe Workfront for Experience Manager enhanced connector]。 如果未使用认证合作伙伴或[!DNL Adobe Professional Services]进行部署和配置，则Adobe不支持该功能。
>
>* Adobe可能会发布使此连接器冗余的[!DNL Adobe Workfront]和[!DNL Adobe Experience Manager]更新；如果发生这种情况，客户可能需要从使用此连接器过渡。
>
>* Adobe支持增强型连接器版本1.7.4及更高版本。 不支持以前的预发行版和自定义版本。 要检查增强型连接器版本，请参阅[增强型连接器安装说明](workfront-connector-install.md)的步骤5(a)。
>
>* 查看Experience Manager Assets增强型连接器的[Workfront合作伙伴认证考试](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html)。 有关考试的信息，请参阅[考试指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/)。

## 配置事件订阅 {#event-subscriptions}

事件订阅用于通知AEM [!DNL Adobe Workfront]中发生的事件。 有三个[!DNL Workfront for Experience Manager enhanced connector]功能需要事件订阅才能正常工作，它们是：

* 自动创建项目链接文件夹。
* 将Workfront文档自定义表单值中的更改同步到AEM资源元数据。
* 项目完成后将资源自动发布到Brand Portal。

要使用这些功能，请启用事件订阅。

* 编辑您在步骤5中创建的[!UICONTROL Workfront Tools]Cloud Service配置，然后选择[!UICONTROL 事件订阅]选项卡。
* 选择您在第6节中创建的[!UICONTROL Workfront自定义集成]。
* 单击[!UICONTROL 启用Workfront活动订阅]。

  ![事件订阅](/help/assets/assets/event-subs.png)

## 配置链接的文件夹 {#linked-folders}

要订阅事件，请执行以下步骤：

1. 导航到云服务中的&#x200B;**[!UICONTROL 事件订阅]**&#x200B;选项卡。
1. 选择在[!DNL Workfront]中创建的自定义集成。
1. 单击&#x200B;**[!UICONTROL 启用Workfront活动订阅]**。

### 链接的文件夹结构配置 {#linked-folder-structure}

1. 转到云服务中的项目链接文件夹选项卡。
1. 链接的文件夹父路径：在DAM中选择一个文件夹，您要在该文件夹中创建链接的文件夹。 如果留空，则默认为/content/dam。 确保Workfront工具元数据架构和Workfront链接文件夹元数据架构已应用于所选文件夹。
1. 链接的文件夹结构：输入逗号分隔的值。 每个值应为`DE:<some-project-custom-form-field>`、Portfolio、项目、年份、名称或某个“文本字符串值”（最后一个值带有引号）。 它当前设置为Portfolio、项目、年、DE：项目类型、名称。
1. 配置权限：将`jcr:all permissions`权限添加到`wf-workfront-users`组的`/conf/workfront-tools/settings/cloudconfigs`。
1. 如果Workfront中的文件夹标题应包括结构中的所有文件夹，则应选中使用文件夹结构名称在Workfront中构建链接的文件夹标题。 否则，它是最后一个文件夹的标题。
1. 子文件夹多字段允许您指定应创建为链接文件夹的子文件夹的文件夹列表。
1. 项目状态：选择要为其设置项目以创建链接文件夹的状态。
1. 在具有项目组合的项目中创建链接文件夹：项目必须属于的Portfolio列表，以便您可以创建链接文件夹。 将此列表留空可为所有项目组合创建链接文件夹。
1. 在具有自定义表单字段的项目中创建链接文件夹：自定义表单字段及其项目必须具有的相应值，以便您可以创建链接文件夹。 如果留空，将忽略此配置。 为字段选择`CUSTOM FORMS: Create DAM Linked Folder`，为值输入`Yes`。
1. 配置权限：为`wf-workfront-users group`配置这些权限`jcr:all permissions for /conf/workfront-tools/settings/cloudconfigs`。
1. 单击启用自动创建链接的文件夹。 如果您返回到“事件订阅”选项卡，现在可以看到有一个创建事件。

![链接的文件夹配置](/help/assets/assets/wf-linked-folder-config.png)

## 元数据架构映射 {#metadata-schema-mapping}

### 配置文件夹元数据映射 {#folder-metadata-mapping}

Workfront项目和AEM文件夹之间的元数据映射在AEM文件夹元数据架构中定义。 应像往常一样，在AEM中创建和配置文件夹元数据架构。 Workfront Tools会为每个文件夹元数据架构表单字段的设置配置选项卡添加一个自动完成下拉列表。 此自动完成下拉菜单可让您指定每个AEM文件夹属性应映射到的Workfront字段。

要配置映射，请执行以下步骤：

1. 为`wf-workfront-users`组添加`jcr:read`权限到`/conf/global/settings/dam/adminui-extension/foldermetadataschema`。
1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 文件夹元数据架构]**。
1. 选择要编辑的文件夹元数据架构表单，然后单击编辑。
1. 选择要编辑的文件夹元数据架构表单字段，然后选择右侧面板上的设置选项卡。
1. 在[!UICONTROL 从Workfront字段映射]字段中，选择要映射到选定AEM文件夹属性的Workfront字段的名称。 可用选项包括：

   * 项目自定义表单字段
   * 项目概述字段(ID、名称、说明、参考编号、计划完成日期、项目所有者、项目发起人、Portfolio或项目群)

![元数据映射配置](/help/assets/assets/wf-metadata-mapping-config2.png)

### 配置资源元数据映射 {#asset-metadata-mapping}

Adobe Workfront文档与Assets之间的元数据映射在AEM元数据架构中定义。 应像往常一样，在AEM中创建和配置元数据架构。 Workfront工具将配置选项添加到每个元数据架构表单字段的设置配置选项卡中。 利用这些选项，可指定每个AEM属性应映射到的Workfront字段。

要配置映射，请执行以下步骤：

1. 导航到&#x200B;**工具** > **Assets** > **元数据架构**。
1. 选择要编辑的元数据架构表单，然后单击&#x200B;**编辑**&#x200B;或从头开始创建元数据架构。
1. 选择要编辑的元数据架构表单字段，然后选择右侧面板上的&#x200B;**设置**&#x200B;选项卡。
1. 在[!DNL Workfront]自定义表单字段中，选择要映射到选定AEM属性的[!DNL Workfront]字段的名称。 可用选项包括：

   * 文档自定义表单字段
   * 项目自定义表单字段
   * 发布自定义表单字段
   * 任务自定义表单字段
   * 项目概述字段（ID、名称、描述或参考编号）

1. 如果在[!UICONTROL Workfront自定义表单字段]中选择的[!DNL Workfront]字段是Workfront用户预输入字段，则需要指定要映射的Workfront用户字段。 为此，请选中“从Workfront引用对象字段获取值”，然后指定要从中检索要映射的值的[!UICONTROL Workfront用户自定义表单字段]的名称。

   ![元数据映射配置](/help/assets/assets/wf-metadata-mapping-config1.png)

## 映射属性 {#map-property}

此工作流步骤允许用户将属性映射到项目、任务、问题或文档上的[!DNL Workfront]自定义表单。 此步骤影响的[!DNL Workfront]工件将使用有效负载中的相对路径进行查找。 要映射的属性可通过步骤对话框配置进行控制。

**类型**：此字段允许您选择属性应映射到的Workfront对象类型。

**ID属性**：此字段允许您指定属性应映射到的Workfront对象ID的路径。 此字段中指定的路径应当相对于工作流有效负载。

**属性分配**：此多字段允许您指定AEM属性与Workfront字段之间的映射。 多字段中的每一项将指定一个映射。 每个映射的格式应为`<workfront-field>=<aem-mapped-property>`。

* `workfront-field`可以是

   * 由前缀`DE:`标识的自定义表单字段。
   * 由其名称标识的可编辑字段。 在[[!DNL Workfront] API Explorer](https://experience.workfront.com/s/api-explorer)中找到字段名称。

* `aem-mapped-property`可以是：

   * 文本值。 应使用引号将它们括起来。
   * AEM资产。 此引用应当相对于工作流有效负荷。
   * 命名值。 应使用括号括住。
   * 上述3个项目的拼接。 使用`{+}`指定它。
   * 通过`{replace(<value>,"old-char","new-char")}`包围值对以上3个项目所做的更改。

* 一些示例包括：

   * `status="INP"`
   * `DE:Asset Type=jcr:content/metadata/assetType`
   * `DE:Path={path}`
   * `URL="https://my-aem-author/assets.html"{+}{path}`

![映射属性的配置](/help/assets/assets/wf-map-property-config.png)

## 设置状态 {#set-status}

在工作流编辑器中，在&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡中编辑&#x200B;**[!UICONTROL Workfront — 设置状态]**&#x200B;的属性。

![编辑工作流以设置状态](/help/assets/assets/wf-set-status.png)

## 注释同步 {#comments-sync}

1. 在[!DNL Experience Manager]中，访问&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Workfront工具配置]**，选择配置，然后选择&#x200B;**[!UICONTROL 属性]**。

   ![评论同步](/help/assets/assets/comments-sync1.png)

1. 选择&#x200B;**[!UICONTROL 事件订阅]**&#x200B;选项卡，单击&#x200B;**[!UICONTROL 将Workfront中的评论发送到AEM]**&#x200B;选项上的&#x200B;**[!UICONTROL 启用评论同步]**。

   ![同步已启用](/help/assets/assets/wf-comment-sync-enabled.png)

要测试从Workfront到AEM的注释同步，请执行以下步骤：

1. 导航到Workfront中的链接文档，并在更新选项卡中添加评论。

   ![在Workfront中留下评论](/help/assets/assets/comments-sync2.png)

1. 导航到AEM中的同一链接文档，选择该文档并在左侧导航中打开[!UICONTROL 时间轴]选项，然后选择[!UICONTROL 注释]。 左侧边栏显示与[!DNL Workfront]同步的评论。

## 资源版本 {#asset-versions}

要在AEM中维护资源的版本历史记录，请在AEM中配置资源版本控制。

1. 在Experience Manager中，访问&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Workfront工具配置]**，然后打开&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡。

1. 选择选项&#x200B;**[!UICONTROL 存储与现有资源版本同名的资源]**。 选中此选项后，可将与现有资产版本上传的同名资产存储到相同位置。 如果未选中，则使用不同的名称（例如，`asset-name.pdf`和`asset-name-1.pdf`）创建新资产。

1. 选择选项&#x200B;**[!UICONTROL 创建新版本]**&#x200B;时更新资源元数据。 选中此选项后，会在创建新版本的资源时更新资源元数据。 如果未选中，则资源将保留其在创建新版本之前拥有的元数据。

![配置资源版本控制](/help/assets/assets/wf-config-versioning.png)

>[!NOTE]
>
>链接的文件夹不支持版本控制。 在链接的文件夹中创建带文档的[!DNL Workfront]验证时，将删除资产早期版本上的注释和批注。

## 附加自定义表单 {#attach-custom-forms}

此工作流步骤允许用户将自定义表单附加到[!DNL Workfront]项目。 此工作流步骤可以添加到任何工作流模型中。 此步骤影响的[!DNL Workfront]工件将使用有效负载中的相对路径进行查找。

在Experience Manager的工作流编辑器中，编辑[!UICONTROL Workfront — 附加自定义表单]工作流步骤的属性。

![自定义表单](/help/assets/assets/wf-custom-forms.png)。

## 自动发布资产 {#auto-publish-assets}

1. 在Experience Manager中，访问&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Workfront工具配置]**，然后打开&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡。

1. 选择&#x200B;**[!UICONTROL 从Workfront]**&#x200B;发送时自动发布资源。 当资产从Workfront发送到AEM时，此选项支持自动发布资产。 可以通过指定Workfront自定义表单字段及其应设置为的值，有条件地启用此功能。 无论何时将文档发送到AEM，如果它满足条件，则资源会自动发布。

1. 选择&#x200B;**[!UICONTROL 项目完成后，将所有项目资源Publish到Brand Portal]**。 此选项允许当资产所属的Workfront项目的状态更改为`Complete`时，将资产自动发布到[!DNL Brand Portal]。

![配置自动发布](/help/assets/assets/wf-auto-publish-config.png)

## Workfront文档自定义表单更新 {#subscribe-workfront-doc-custom-form-updates}

要订阅[!DNL Workfront]文档自定义表单中的更改，请在&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡中选择相关选项。 当您订阅这些更新时，它会在[!DNL Workfront]文档自定义表单中的相应字段更改时更新映射的[!DNL Experience Manager]元数据字段。

![Workfront在[!DNL Experience Manager]](/help/assets/assets/wf-custom-form-update.png)中记录自定义表单更新配置
