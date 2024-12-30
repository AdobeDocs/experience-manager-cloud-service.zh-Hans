---
title: AEM as a Cloud Service 团队和产品配置文件
description: 了解 AEM as a Cloud Service 团队和产品配置文件可怎样准许和限制访问您已许可的 Adobe 解决方案。
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
feature: Onboarding
role: Admin, User, Developer
source-git-commit: c8534ddf84998377ee63575403417165ccec2dbd
workflow-type: ht
source-wordcount: '2059'
ht-degree: 100%

---


# AEM as a Cloud Service 团队和产品配置文件 {#product-profiles}

了解 AEM as a Cloud Service 团队和产品配置文件可怎样准许和限制访问您已许可的 Adobe 解决方案。

## 产品配置文件 {#profiles}

授予用户访问特定 Adobe 解决方案的权限时，您不一定要授予他们完全访问权限。 产品配置文件使每个解决方案都有自己的用户权限集。 可以通过 [Admin Console](/help/journey-onboarding/admin-console.md) 访问这些内容。

Adobe Admin Console 具有由产品、产品实例和产品配置文件组成的结构化层次结构，其中可以为组织的内部用户分配成员资格，从而使他们能够访问已获得已授予许可的解决方案和功能。

<!-- Alexandru: Drafting for now 

Your AEM as a Cloud Service team members are added and assigned to one or more of the following product profiles via the Admin Console during onboarding.

* **AEM Administrators**: An AEM administrator is typically assigned to developers, in particular developers who need access to, for example, the development environments. The AEM administrator's product profile is used to grant administrator privileges in the associated AEM instance.

* **AEM Users**: AEM users are the users in your organization who use AEM as a Cloud Service generally to create content. These users need to access AEM to do their tasks. The AEM users product profile is typically assigned to an AEM content author who creates and reviews the content. This content can be of many types such as pages, assets, publications, and so on. The AEM users product profile shown below is assigned to these members.

![Product profiles](/help/onboarding/assets/admin-console-profiles.png) -->

## AEM as a Cloud Service 产品配置文件 {#aem-product-profiles}

AEM as a Cloud Service 是一种全云本地服务，将 AEM 作为服务提供。 它以云端原生的方式提供 AEM，具有新的属性，如始终打开、始终最新、始终安全和始终保持规模。 同时，它保留了 AEM 作为可定制平台向客户提供的主要价值主张，并允许企业级团队整合到其开发和传递过程中。 请参阅 [Adobe Experience Manager as a Cloud Service 简介](/help/overview/introduction.md)，了解有关 AEM as a Cloud Service 的更多信息。

### 组织级别产品实例 {#org-level-product-instances}

>[!NOTE]
>
> 本文介绍的某些产品实例和产品配置文件可能仅出现在新创建的环境中。未来的机制将允许现有环境也进行更新。

当 Adobe 首次处理 AEM 解决方案的许可时，两个产品实例将出现在 Adobe Experience Manager as a Cloud Service 产品下的 Adobe Admin Console 中：

* **AEM 组织级别**：包含一个或多个产品配置文件，这些配置文件表示对所有 AEM 环境范围内的功能的访问，而不仅仅是单个环境
* **Cloud Manager**：包含与对 Cloud Manager 功能的不同访问级别相对应的产品配置文件。

<!--
>[!NOTE]
>
>For existing programs, the AEM Org-Level Product Instance is created upon selecting the **Update product** profiles action for a given environment.
-->

![组织级别产品实例](/help/onboarding/assets/orglevel.png)

AEM 组织级产品实例内部有一个名为 AEM 组织级报告器的产品配置文件，目前尚未使用，但将来可能会用于表示检索有关 AEM 产品许可证信息的权限。

当 Forms 通信解决方案获得许可时，相应的产品配置文件也将出现在 AEM 组织级产品实例下。

![报告器产品配置文件](/help/onboarding/assets/org-level-reporters.png)

### 环境和层级产品实例 {#environment-and-tier-level-product-instances}

在使用一个或多个 AEM 环境配置新程序时，每个环境将出现两个产品实例，分别包含用于创作和发布的产品配置文件。

![环境产品实例](/help/onboarding/assets/env-productinstances.png)

对于已在包含 AEM Sites 的程序中配置环境的组织，以下是作者产品实例中的产品配置文件：

![Sites 产品实例](/help/onboarding/assets/sites-product-instances.png)

下表描述了特定于环境层的产品实例下可能的产品配置文件列表。

<table style="table-layout:auto">
    <tr>
        <th>产品实例</th>
        <th>命名惯例</th>
        <th>默认服务器</th>
        <th>描述</th>
    </tr>
    <tr>
        <td>AEM 作者</td>
        <td>AEM Sites 内容管理员 - 作者 - 程序 <code>id</code> - 环境 <code>id</code></td>
        <td>AEM Sites 内容管理员</td>
        <td>
            <ul>
                <li>旨在控制对此环境中 AEM Sites 作者功能的访问。此产品配置文件中的用户将是 AEM Sites 内容作者 AEM 组的成员，该组会在 AEM 中自动创建。AEM 组权限应在 AEM 中配置为所需的访问级别。</li><br>
                <li>如果仍选择默认服务
                    <ul>
                        <li>此产品配置文件中的用户也将成为“AEM Sites 内容管理员 - 服务”AEM 组的成员。</li>
                      <!--  <li>users in this product profile will have access to AEM Sites Content Management API.</li>
                        <li>an Adobe Developer Console API OAuth S2S project containing AEM Sites Content Management API can optionally be scoped to this environment.</li>-->
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM 管理员 - 作者 - 程序 <code>id</code> - 环境 <code>id</code></td>
        <td>AEM 管理员</td>
        <td>
            <ul>
                <li>旨在不受限制地访问 AEM 作者和发布环境功能。此产品配置文件中的用户将成为 AEM 中自动创建的 AEM 管理员作者 AEM 组的成员。</li><br>
                <li>如果仍选择默认服务
                    <ul>
                        <li>此产品配置文件中的用户也将成为“AEM 管理员 - 服务”AEM 组的成员</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM 用户 - 作者 - 程序 <code>id</code> - 环境 <code>id</code></td>
        <td>AEM 用户</td>
        <td>
            <ul>
                <li>旨在对 AEM 作者环境功能进行非常有限的访问。此产品配置文件中的用户将成为 AEM 中自动创建的“投稿人”AEM 组的成员</li><br>
                <li>如果仍选择默认服务
                    <ul>
                        <li>此产品配置文件中的用户也将成为“AEM 用户 - 服务”AEM 组的成员</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM 报告器 - 作者 - 程序 <code>id</code> - 环境 <code>id</code></td>
        <td>AEM 报告器</td>
        <td>
            <ul>
                <li>目前未使用，但将来可能会提供对此环境的作者层的报告信息的访问权限。</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Assets 协作者 - 作者 - 程序 <code>id</code> - 环境 <code>id</code></td>
        <td>AEM Assets 协作者用户</td>
        <td>
        <ul>
                <li>用于对 DAM 进行只读访问。此产品配置文件中的用户将成为 AEM 中自动创建的“投稿人”AEM 组的成员。
                </li>
                <li>
                此外，它还提供 Adobe Express 权限，以创建资产变体。
                </li>
          <ul>
    </tr>
    <tr>
        <td></td>
        <td>AEM Assets 高级用户 - 作者 - 程序 <code>id</code> - 环境 <code>id</code></td>
        <td>AEM Assets 高级用户</td>
<td>
        <ul>
                <li>用于对 DAM 进行只读访问。此产品配置文件中的用户将成为 AEM 中自动创建的“投稿人”AEM 组的成员。
                </li>
                <li>
                此外，它还提供 Adobe Express 权限，以创建资产变体。
                </li>
          <ul>
</td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Forms 内容管理员 - 作者 - 程序 <code>id</code> - 环境 <code>id</code></td>
        <td>AEM Forms 内容管理员</td>
        <td>
            <ul>
                <li>旨在控制对此环境中 AEM Forms 作者功能的访问。此产品配置文件中的用户将成为 AEM Forms 表单用户 AEM 组的成员，该组在 AEM 中自动创建。</li><br>
                <li>如果仍选择默认服务
                    <ul>
                        <li>此产品配置文件中的用户也将成为“AEM Forms 内容管理员 - 服务”AEM 组的成员。</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Forms 开发人员 - 作者 - 程序 <code>id</code>  - 环境 <code>id</code></td>
        <td>AEM Forms 开发人员</td>
        <td>
            <ul>
                <li>旨在控制对此环境中 AEM Forms 作者功能的访问。此产品配置文件中的用户将成为 AEM Forms 表单高级用户 AEM 组的成员，该组在 AEM 中自动创建。除了正常的表单创作任务外，这些用户还有权上传 XDP 和作者表单数据模型。</li><br>
                <li>如果仍选择默认服务
                    <ul>
                        <li>此产品配置文件中的用户也将成为“AEM Forms 开发人员 - 服务”AEM 组的成员。</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Forms 通信服务用户 - 作者 - 程序 <code>id</code>  - 环境 <code>id</code></td>
        <td>AEM Forms 通信服务用户</td>
        <td>
            <ul>
                <li>旨在控制对此环境中的 AEM Forms 通信服务功能的访问。此产品配置文件中的用户将成为 AEM Forms 表单用户 AEM 组的成员，该组在 AEM 中自动创建。</li><br>
                <li>如果仍选择默认服务
                    <ul>
                        <li>此产品配置文件中的用户也将成为“AEM Forms 通信服务用户 - 服务”AEM 组的成员。</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>AEM 发布</td>
        <td>AEM 用户 - 发布 - 程序 <code>id</code>  - 环境 <code>id</code></td>
        <td>AEM 用户</td>
        <td>
            <ul>
                <li>旨在对 AEM 作者环境功能进行非常有限的访问。此产品配置文件中的用户将成为 AEM 中自动创建的“投稿人”AEM 组的成员</li><br>
                <li>如果仍选择默认服务
                    <ul>
                        <li>此产品配置文件中的用户也将成为“AEM 用户 - 服务”AEM 组的成员</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM 报告器 - 发布 - 程序 <code>id</code>  - 环境 <code>id</code></td>
        <td>AEM 报告器</td>
        <td>
            <ul>
                <li>目前未使用，但将来可能会提供对此环境的发布层的报告信息的访问权限。</li>
            </ul>
        </td>
    </tr>
   <tr>
        <td></td>
        <td>AEM Forms 通信服务用户 - 发布 - 程序 <code>id</code> - 环境 <code>id</code></td>
        <td>AEM Forms 通信服务用户</td>
        <td>
            <ul>
                <li>旨在控制对此环境中的 AEM Forms 通信服务功能的访问。此产品配置文件中的用户将成为 AEM Forms 表单用户 AEM 组的成员，该组在 AEM 中自动创建。</li><br>
                <li>如果仍选择默认服务
                    <ul>
                        <li>此产品配置文件中的用户也将成为“AEM Forms 通信服务用户 - 服务”AEM 组的成员。</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
</table>

请注意，每个产品配置文件都默认启用关联的产品配置文件服务。除非您有复杂的访问要求，否则建议仅选择默认服务。系统会在 AEM 中创建一个相应的 AEM 组，命名惯例为 `<Product Profile Prefix> - Service` （例如，**AEM Sites 内容管理员 - 服务**），并且上层产品配置文件中的用户将自动成为该相应 AEM 组的成员。

AEM 中与该服务关联的 AEM 组将拥有该环境层组合中该服务的所有关联产品配置文件中存在的用户聚合集。

![服务](/help/onboarding/assets/services.png)

以下图像表示反映 AEM Sites 内容管理器作者层产品配置文件和服务的 AEM 组。

![AEM 组到服务映射](/help/onboarding/assets/profile-to-service-mapping.png)

>[!NOTE]
>
>每个分配给 AEM as a Cloud Service 产品配置文件的用户都只能通过 **Cloud Manager 用户**&#x200B;角色以只读方式访问 Cloud Manager。
>
>仅有 **Cloud Manager 用户**&#x200B;角色的用户可登录到 Cloud Manager 并使用&#x200B;**项目**&#x200B;菜单选项导航到 AEM 作者环境（如果存在这些环境）。**Cloud Manager 用户**&#x200B;角色不足以访问项目详细信息。如果需要此类访问，则必须由系统管理员为用户授予其他角色。

>[!WARNING]
>
>不得更改 **AEM 管理员**&#x200B;产品配置文件名称。更改 **AEM 管理员**&#x200B;产品配置文件的名称将让所有分配给该配置文件的用户失去管理员权限。

>[!TIP]
>
>* 要详细了解 AEM 产品配置文件，请参阅[分配 AEM 产品配置文件](/help/journey-onboarding/assign-profiles-aem.md)。
>* 有关上线过程的详细信息，请参阅[上线历程](/help/journey-onboarding/overview.md)。

### 为现有环境添加产品轮廓 {#adding-product-profiles-for-existing-environments}

2024 年 11 月初之前创建的环境可能会缺少上述部分描述的组织级产品实例以及某些产品轮廓。现有的产品轮廓也会缺少服务切换功能。建议更新这些产品轮廓，这是访问某些未来 API 的前提条件。

如果程序中的一个或多个环境需要更新其产品轮廓，则 Cloud Manager 将会显示下面的通知。请注意，环境必须处于最新的 AEM 版本，然后才能更新其产品轮廓。

![实现产品轮廓现代化](/help/onboarding/assets/modernize-product-profiles.png)

点击&#x200B;**添加产品轮廓**&#x200B;按钮将会打开一个菜单，其中会显示将新产品轮廓添加到该程序中所有可用环境或个体环境的选项。

![替换环境](/help/onboarding/assets/choose-env-r.png)

点击&#x200B;**所有环境**&#x200B;将新的产品轮廓添加到该程序中的所有环境。或者，单击&#x200B;**个体环境**&#x200B;将新产品轮廓添加到选定的环境；这会将用户导航到“环境”列表页面，在该页面可以从&#x200B;**更多选项**&#x200B;图标中选择&#x200B;**添加产品轮廓**&#x200B;操作。

![个体环境](/help/onboarding/assets/individual-environments.png)

您还可以通过导航到“程序概述”页面的“环境”部分，单击与环境相对应的“更多选项”图标，然后选择“添加产品轮廓”，将产品轮廓添加到选定的环境。

在添加新的产品轮廓时，环境状态会显示“正在添加产品轮廓”，随后在该过程完成后会显示“正在运行”。


## Cloud Manager 产品配置文件 {#cloud-manager-product-profiles}

Cloud Manager 具有预配置的产品配置文件，可以将其视为基于角色的权限。 您的系统管理员负责通过将 Cloud Manager 团队分配给这些产品配置文件来进行设置。

>[!TIP]
>
>有关更多详细信息，请参阅 [Cloud Manager 中基于角色的权限。](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)

每个产品配置文件都具有与其关联的特定权限。

* **业务负责人**
   * 在此角色中，您有权添加新项目或编辑项目、添加或更新环境、将代码部署到 AEM 环境或执行代码质量检查。
   * 此用户负责定义 KPI、审批生产部署，如有必要，还负责忽略重大的 3 层故障。
* **部署管理员**
   * 在此角色中，您有权添加或更新环境、运行任何管道以及将代码部署到 AEM 环境或执行代码质量检查。
   * 此用户管理部署操作并使用 Cloud Manager 执行暂存/生产部署、编辑 CI/CD 管道、在必要时批准重大的 3 层故障，并可访问 Git 存储库。
* **开发人员**
   * 在此角色中，您有权生成个人访问令牌以访问 git。
   * 此用户开发并测试自定义应用程序代码并主要使用 Cloud Manager 查看部署状态，并可访问 Git 存储库以提交代码。
* **项目管理员**
   * 在此角色中，您有权安排管道、忽略 3 层质量关卡并提供生产批准。
   * 此用户使用 Cloud Manager 执行团队设置、审查状态、查看 KPI，并可在必要时审批重大的 3 层故障。

一个用户可以分配给多个产品配置文件。 例如，将&#x200B;**业务负责人**&#x200B;和&#x200B;**部署管理员**&#x200B;角色分配给用户，可以为他们提供所有这些权限。

您的 Cloud Manager 团队至少包括：

* 一位&#x200B;**业务负责人**，通常也是系统管理员，必须是第一个登录和访问 Cloud Manager 的人
* 一位&#x200B;**部署管理员**
* 一位&#x200B;**开发人员**

>[!NOTE]
>
>要被授予 AEM as a Cloud Service 访问权限，用户必须属于以下两种产品配置文件之一：`AEM Users` 或 `AEM Administrators`。 管理 Cloud Manager 的权限不够。

>[!TIP]
>
>* 要详细了解 Cloud Manager 产品配置文件，请参阅[将团队成员分配到 Cloud Manager 产品配置文件](/help/journey-onboarding/assign-profiles-cloud-manager.md)。
>* 有关上线过程的详细信息，请参阅[上线历程](/help/journey-onboarding/overview.md)。
