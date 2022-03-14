---
title: 配置 Live Copy 同步
description: 了解可用的强大Live Copy同步选项，以及如何根据项目的需要配置和自定义这些选项。
feature: Multi Site Manager
role: Admin
exl-id: 0c97652c-edac-436e-9b5b-58000bccf534
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '2336'
ht-degree: 29%

---

# 配置 Live Copy 同步 {#configuring-live-copy-synchronization}

Adobe Experience Manager提供了大量现成的同步配置。 在使用Live Copy之前，您应考虑以下事项来定义Live Copy如何以及何时与其源内容同步。

1. 确定现有的转出配置是否符合您的要求
1. 如果现有的转出配置不支持，请决定您是否需要创建自己的转出配置。
1. 指定要用于Live Copy的转出配置。

## 已安装的自定义转出配置 {#installed-and-custom-rollout-configurations}

本部分提供有关已安装转出配置、其所使用的同步操作以及如何在需要时创建自定义配置的信息。

>[!CAUTION]
>
>正在更新或更改现成的转出配置 **not** 推荐。 如果需要自定义实时操作，则应在自定义转出配置中添加该操作。

### 转出触发器 {#rollout-triggers}

每个转出配置都使用一个可执行转出的转出触发器。转出配置可以使用以下触发器之一：

* **转出时**:的 **转出** 命令，或者 **同步** 命令。
* **修改**:源页面已修改。
* **激活**：激活源页面。
* **停用**：停用源页面。

>[!NOTE]
>
>使用 **修改** 触发器可能会影响性能。 请参阅 [MSM 最佳实践](best-practices.md#onmodify)以了解更多信息。

### 转出配置 {#rollout-configurations}

下表列出了随AEM一起提供的现成转出配置。 该表包含每个转出配置的触发器和同步操作。

<!--
If the installed rollout configuration actions do not meet your requirements, you can [create a new rollout configuration](#creating-a-rollout-configuration).
-->

| 名称 | 描述 | 触发器 | [同步操作](#synchronization-actions) |
|---|---|---|---|
| 标准转出配置 | 标准转出配置，允许在转出触发器上启动转出进程并运行操作：创建、更新、删除内容和排序子节点 | 转出 | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`productUpdate`<br>`orderChildren` |
| 在 Blueprint 激活时激活 | 在发布源时发布Live Copy | 激活 | `targetActivate` |
| 在 Blueprint 停用时停用 | 在停用源时停用Live Copy | 停用时 | `targetDeactivate` |
| 修改时推送 | 在修改源时将内容推送到Live Copy<br>当此转出配置使用On Modification触发器时，请谨慎使用此转出配置。 | 修改 | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`orderChildren` |
| 修改时推送（简略） | 在修改Blueprint页面时将内容推送到Live Copy，而不更新引用（例如，对于浅层副本）<br>当此转出配置使用On Modification触发器时，请谨慎使用此转出配置。 | 修改 | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`orderChildren` |
| 提升启动项 | 用于提升启动项页面的标准转出配置。 | 转出 | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`orderChildren`<br>`markLiveRelationship` |

### 同步操作 {#synchronization-actions}

下表列出了随AEM一起提供的现成同步操作。

<!--If the installed actions do not meet your requirements, you can [Create a New Synchronization Action](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action).-->

| 操作名称 | 描述 | 属性 |
|---|---|---|
| `contentCopy` | 如果源节点在Live Copy中不存在，则此操作会将节点复制到Live Copy。 [配置 **CQ MSM内容复制操作** 服务](#excluding-properties-and-node-types-from-synchronization) 指定要排除的节点类型、段落项和页面属性。 |  |
| `contentDelete` | 此操作会删除源上不存在的Live Copy节点。 [配置 **CQ MSM内容删除操作** 服务](#excluding-properties-and-node-types-from-synchronization) 指定要排除的节点类型、段落项和页面属性。 |  |
| `contentUpdate` | 此操作会使用源中的更改来更新Live Copy内容。 [配置 **CQ MSM内容更新操作** 服务](#excluding-properties-and-node-types-from-synchronization) 指定要排除的节点类型、段落项和页面属性。 |  |
| `editProperties` | 此操作将编辑Live Copy的属性。 的 `editMap` 属性确定要编辑的属性及其值。 的值 `editMap` 属性必须使用以下格式：<br>`[property_name_n]#[current_value]#[new_value]`<br>`current_value` 和 `new_value` 是正则表达式和 `n` 是递增的整数。<br>例如，请考虑以下值 `editMap`:<br>`sling:resourceType#/(contentpage`€`homepage)#/mobilecontentpage,cq:template#/contentpage#/mobilecontentpage`<br>此值编辑Live Copy节点的属性，如下所示：<br>的 `sling:resourceType` 属性设置为 `contentpage` 或 `homepage` 设置为 `mobilecontentpage`.<br>的 `cq:template` 设置为的属性 `contentpage` 设置为 `mobilecontentpage`. | `editMap: (String)` 标识属性、当前值和新值。 有关更多信息，请参阅描述。 |
| `notify` | 此操作会发送一个页面已被转出的页面事件。 要接收通知，首先需要订阅转出事件。 |  |
| `orderChildren` | 此操作会根据Blueprint上的顺序对子节点进行排序。 |  |
| `referencesUpdate` | 此同步操作会更新Live Copy上的引用。<br>它会在Live Copy页面中搜索指向Blueprint中资源的路径。 找到后，它会更新路径以指向Live Copy中的相关资源。 具有 Blueprint 外部目标的引用不会发生更改。<br>[配置 **CQ MSM引用更新操作** 服务](#excluding-properties-and-node-types-from-synchronization) 指定要排除的节点类型、段落项和页面属性。 |  |
| `targetVersion` | 此操作将创建Live Copy的版本。<br>此操作必须是转出配置中包含的唯一同步操作。 |  |
| `targetActivate` | 此操作可激活Live Copy。<br>此操作必须是转出配置中包含的唯一同步操作。 |  |
| `targetDeactivate` | 此操作将停用Live Copy。<br>此操作必须是转出配置中包含的唯一同步操作。 |  |
| `workflow` | 此操作将启动由target属性定义的工作流（仅限页面），并将Live Copy作为有效负载。<br>目标路径是模型节点的路径。 | `target: (String)` 是工作流模型的路径。 |
| `mandatory` | 此操作会将Live Copy页面上多个ACL的权限设置为特定用户组的只读权限。 配置了以下ACL:<br>`ActionSet.ACTION_NAME_REMOVE`<br>`ActionSet.ACTION_NAME_SET_PROPERTY`<br>`ActionSet.ACTION_NAME_ACL_MODIFY`<br>此操作仅用于页面。 | `target: (String)` 是要为其设置权限的组的ID。 |
| `mandatoryContent` | 此操作会将Live Copy页面上多个ACL的权限设置为特定用户组的只读权限。 配置了以下ACL:<br>`ActionSet.ACTION_NAME_SET_PROPERTY`<br>`ActionSet.ACTION_NAME_ACL_MODIFY`<br>此操作仅用于页面。 | `target: (String)` 是要为其设置权限的组的ID。 |
| `mandatoryStructure` | 此操作将设置 `ActionSet.ACTION_NAME_REMOVE` Live Copy页面上的ACL ，用于特定用户组的只读。<br>仅对页面使用此操作。 | `target: (String)` 是要为其设置权限的组的ID。 |
| `VersionCopyAction` | 如果Blueprint/源页面至少已发布一次，则此操作将使用已发布的版本创建Live Copy页面。 注意：此操作仅适用于基于已发布的源页面创建Live Copy页面，而不适用于更新现有Live Copy页面。 |  |
| `PageMoveAction` | 的 `PageMoveAction` 在Blueprint中移动页面时应用。<br>操作会复制（相关）Live Copy页面，而不是从移动之前的位置移动到之后的位置。<br>的 `PageMoveAction` 不会更改移动前所在位置的Live Copy页面。 因此，对于连续转出配置，它具有没有Blueprint的实时关系状态。<br>[****&#x200B;配置 CQ MSM 页面移动操作服务](#excluding-properties-and-node-types-from-synchronization)，以指定要排除的节点类型、段落项和页面属性。<br>此操作必须是转出配置中包含的唯一同步操作。 | 已设置 `prop_referenceUpdate: (Boolean)` 为true（默认）以更新引用。 |
| `markLiveRelationship` | 此操作表示启动项创建的内容存在实时关系。 |  |

<!--
### Creating a Rollout Configuration {#creating-a-rollout-configuration}

You can [create a rollout configuration](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration) when the installed rollout configurations do not meet your application requirements by performing the following steps.

1. [Create the rollout configuration](/help/sites-developing/extending-msm.md#create-the-rollout-configuration).
1. [Add synchronization actions to the rollout configuration](/help/sites-developing/extending-msm.md#add-synchronization-actions-to-the-rollout-configuration).

The new rollout configuration is then available to you when configuring rollout configurations on a blueprint or Live Copy page.
-->

### 从同步中排除属性和节点类型 {#excluding-properties-and-node-types-from-synchronization}

您可以配置多个支持相应同步操作的 OSGi 服务，以便它们不会影响特定的节点类型和属性。例如，与AEM内部功能相关的许多属性和子节点不应包含在Live Copy中。 只应复制与页面用户相关的内容。

使用AEM时，可通过多种方法来管理此类服务的配置设置。请参阅 [配置OSGi](/help/implementing/deploying/configuring-osgi.md) 以了解更多详细信息和建议的实践。

下表列出了可以为其指定要排除节点的同步操作。该表提供了要使用 Web 控制台进行配置的服务名称以及要使用存储库节点进行配置的 PID。

| 同步操作 | Web控制台中的服务名称 | 服务PID |
|---|---|---|
| `contentCopy` | CQ MSM内容复制操作 | `com.day.cq.wcm.msm.impl.actions.ContentCopyActionFactory` |
| `contentDelete` | CQ MSM内容删除操作 | `com.day.cq.wcm.msm.impl.actions.ContentDeleteActionFactory` |
| `contentUpdate` | CQ MSM内容更新操作 | `com.day.cq.wcm.msm.impl.actions.ContentUpdateActionFactory` |
| `PageMoveAction` | CQ MSM页面移动操作 | `com.day.cq.wcm.msm.impl.actions.PageMoveActionFactory` |
| `referencesUpdate` | CQ MSM引用更新操作 | `com.day.cq.wcm.msm.impl.actions.ReferencesUpdateActionFactory` |

下表描述了您可以配置的属性：

| Web控制台属性 | OSGi资产 | 描述 |
|---|---|---|
| 排除的节点类型 | `cq.wcm.msm.action.excludednodetypes` | 与要从同步操作中排除的节点类型匹配的正则表达式 |
| 排除的段落项目 | `cq.wcm.msm.action.excludedparagraphitems` | 与要从同步操作中排除的段落项目匹配的正则表达式 |
| 排除的页面属性 | `cq.wcm.msm.action.excludedprops` | 与要从同步操作中排除的页面属性匹配的正则表达式 |
| 忽略的Mixin NodeTypes | `cq.wcm.msm.action.ignoredMixin` | 与要从同步操作中排除的混合节点类型名称匹配的正则表达式(仅适用于 `contentUpdate` action) |

#### CQ MSM 内容更新操作 - 排除项 {#cq-msm-content-update-action-exclusions}

默认情况下，将排除多个属性和节点类型，这些属性和节点类型在 **CQ MSM 内容更新操作**&#x200B;的&#x200B;**排除的页面属性**&#x200B;下的 OSGi 配置中定义。

默认情况下，在转出时排除（即不更新）与以下正则表达式匹配的属性：

![Live Copy排除区](../assets/live-copy-exclude.png)

您可以根据需要更改定义排除列表的表达式。

例如，如果您希望将页面&#x200B;**标题**&#x200B;包含在考虑转出的更改中，请从排除项中删除 `jcr:title`。例如，使用正则表达式：

`jcr:(?!(title)$).*`

### 配置同步以更新引用 {#configuring-synchronization-for-updating-references}

您可以配置多个 OSGi 服务以支持与更新引用相关的对应同步操作。

使用AEM时，可通过多种方法来管理此类服务的配置设置。请参阅 [配置OSGi](/help/implementing/deploying/configuring-osgi.md) 以了解更多详细信息和建议的实践。

下表列出了可以为其指定引用更新的同步操作。该表提供了要使用 Web 控制台进行配置的服务名称以及要使用存储库节点进行配置的 PID。

| Web控制台属性 | OSGi资产 | 描述 |
|---|---|---|
| 更新嵌套LiveCopy中的引用 | `cq.wcm.msm.impl.action.referencesupdate.prop_updateNested` | 在Web控制台中选择此选项，或将此布尔属性设置为 `true` 使用存储库配置替换以最顶部Live Copy分支中的任何资源为目标的引用。 仅适用于 `referencesUpdate` 操作。 |
| 更新引用页面 | `cq.wcm.msm.impl.actions.pagemove.prop_referenceUpdate` | 在Web控制台中选择此选项，或将此布尔属性设置为 `true` 使用存储库配置来更新任何引用，以改为使用原始页面引用Live Copy页面。 仅适用于 `PageMoveAction`. |

## 指定要使用的转出配置 {#specifying-the-rollout-configurations-to-use}

MSM允许您指定通常使用的转出配置集，并在需要时可以为特定Live Copy覆盖它们。 MSM 提供了多个位置可指定要使用的转出配置。该位置可确定配置是否适用于特定的Live Copy。

以下位置列表可在其中指定要使用的转出配置，其中介绍了MSM如何确定要用于Live Copy的转出配置：

* **[Live Copy页面属性](live-copy-sync-config.md#setting-the-rollout-configurations-for-a-live-copy-page):** 将Live Copy页面配置为使用一个或多个转出配置后，MSM会使用这些转出配置。
* **[Blueprint页面属性](live-copy-sync-config.md#setting-the-rollout-configuration-for-a-blueprint-page):** 当Live Copy基于Blueprint，并且Live Copy页面未配置转出配置时，将使用与Blueprint源页面关联的转出配置。
* **Live Copy父页面属性：** 如果Live Copy页面和Blueprint源页面均未使用转出配置进行配置，则会使用适用于Live Copy页面父页面的转出配置。
* **[系统默认](live-copy-sync-config.md#setting-the-system-default-rollout-configuration):** 当无法确定Live Copy父页面的转出配置时，将使用系统默认转出配置。

例如，Blueprint使用 [WKND教程](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 站点作为源内容。 从该 Blueprint 创建一个网站。以下列表中的每个项都描述了有关使用转出配置的不同场景：

* 未将任何Blueprint页面或Live Copy页面配置为使用转出配置。 MSM对所有Live Copy页面使用系统默认转出配置。
* WKND站点的根页面配置了多个转出配置。 MSM对所有Live Copy页面都使用这些转出配置。
* WKND站点的根页面配置了多个转出配置，Live Copy站点的根页面配置了一组不同的转出配置。 MSM使用在Live Copy站点的根页面上配置的转出配置。

### 为 Live Copy 页面设置转出配置 {#setting-the-rollout-configurations-for-a-live-copy-page}

使用转出配置配置配置Live Copy页面，以便在转出源页面时使用。 子页面默认情况下会继承该配置。当您配置要使用的转出配置时，您正在覆盖Live Copy页面从其父页面继承的配置。

您还可以在您 [创建Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-page).

1. 使用 **站点** 控制台来选择Live Copy页面。
1. 从工具栏中选择&#x200B;**属性**。
1. 打开 **Live Copy** 选项卡。

   **配置**&#x200B;部分将显示页面继承的转出配置。

   ![父页面中的Live Copy继承](../assets/live-copy-inherit.png)

1. 如果需要，可调整 **Live Copy 继承**&#x200B;标记。如果选中，则Live Copy配置对所有子项都有效。

1. 清除&#x200B;**继承父项的转出配置**&#x200B;属性，然后从列表中选择一个或多个转出配置。

   选择的转出配置将显示在下拉列表下。

   ![覆盖Live Copy配置继承](../assets/live-copy-inherit-override.png)

1. 单击或点按 **保存并关闭**.

### 为 Blueprint 页面设置转出配置 {#setting-the-rollout-configuration-for-a-blueprint-page}

使用要在转出 Blueprint 页面时使用的转出配置对 Blueprint 页面进行配置。

请注意，Blueprint 页面的子页面将继承该配置。在配置要使用的转出配置时，可能会覆盖页面从其父页面继承的配置。

1. 使用&#x200B;**站点**&#x200B;控制台选择 Blueprint 的根页面。
1. 从工具栏中选择&#x200B;**属性**。
1. 打开 **Blueprint** 选项卡。
1. 使用下拉选择器选择一个或多个&#x200B;**转出配置**。
1. 使用&#x200B;**保存**&#x200B;持久存储您的更新。

### 设置系统默认转出配置 {#setting-the-system-default-rollout-configuration}

要指定要用作系统默认值的转出配置，请配置以下OSGi服务。

* **Day CQ WCM Live Relationship Manager** 与服务PID `com.day.cq.wcm.msm.impl.LiveRelationshipManagerImpl`

使用 [Web控制台](/help/implementing/deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 或 [存储库节点](/help/implementing/deploying/configuring-osgi.md#osgi-configuration-in-the-repository).

* 在Web控制台中，要配置的属性的名称为 **默认转出配置**.
* 使用存储库节点，要配置的属性的名称为 `liverelationshipmgr.relationsconfig.default`.

将此属性值设置为要用作系统默认值的转出配置的路径。默认值为 `/libs/msm/wcm/rolloutconfigs/default`，这是 **标准转出配置**.
