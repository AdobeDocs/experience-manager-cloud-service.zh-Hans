---
title: AEM as a Cloud Service 团队和产品配置文件
description: 了解 AEM as a Cloud Service 团队和产品配置文件可怎样准许和限制访问您已许可的 Adobe 解决方案。
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 5f630c8a618502907e4be50844e07184e38e1b1e
workflow-type: tm+mt
source-wordcount: '1821'
ht-degree: 39%

---


# AEM as a Cloud Service 团队和产品配置文件 {#product-profiles}

了解 AEM as a Cloud Service 团队和产品配置文件可怎样准许和限制访问您已许可的 Adobe 解决方案。

## 产品配置文件 {#profiles}

授予用户访问特定 Adobe 解决方案的权限时，您不一定要授予他们完全访问权限。 产品配置文件使每个解决方案都有自己的用户权限集。 可以通过 [Admin Console](/help/journey-onboarding/admin-console.md) 访问这些内容。

Adobe Admin Console具有产品、产品实例和产品配置文件的结构化层次结构，可以为该组织的内部用户分配成员资格，使他们有权访问已许可的解决方案和功能。

<!-- Alexandru: Drafting for now 

Your AEM as a Cloud Service team members are added and assigned to one or more of the following product profiles via the Admin Console during onboarding.

* **AEM Administrators**: An AEM administrator is typically assigned to developers, in particular developers who need access to, for example, the development environments. The AEM administrator's product profile is used to grant administrator privileges in the associated AEM instance.

* **AEM Users**: AEM users are the users in your organization who use AEM as a Cloud Service generally to create content. These users need to access AEM to do their tasks. The AEM users product profile is typically assigned to an AEM content author who creates and reviews the content. This content can be of many types such as pages, assets, publications, and so on. The AEM users product profile shown below is assigned to these members.

![Product profiles](/help/onboarding/assets/admin-console-profiles.png) -->

## AEM as a Cloud Service 产品配置文件 {#aem-product-profiles}

AEM as a Cloud Service 是一种全云本地服务，将 AEM 作为服务提供。 它以云端原生的方式提供 AEM，具有新的属性，如始终打开、始终最新、始终安全和始终保持规模。 同时，它保留了 AEM 作为可定制平台向客户提供的主要价值主张，并允许企业级团队整合到其开发和交付过程中。 请参阅 [Adobe Experience Manager as a Cloud Service 简介](/help/overview/introduction.md)，了解有关 AEM as a Cloud Service 的更多信息。

### 组织级别的产品实例 {#org-level-product-instances}

>[!NOTE]
>
> 本文中介绍的某些产品实例和产品配置文件可能只显示给新创建的环境。 未来的机制还将允许更新现有环境。

当Adobe首次处理AEM解决方案的许可时，Adobe Admin Console中的Adobe Experience Manager as a Cloud Service产品下将显示两个产品实例：

* **AEM组织级别** — 包含一个或多个产品配置文件，这些配置文件表示对适用于所有AEM环境的功能的访问权限，而不只是对单个功能的访问权限
* **Cloud Manager** — 包含与对Cloud Manager功能的不同访问级别对应的产品配置文件。

<!--
>[!NOTE]
>
>For existing programs, the AEM Org-Level Product Instance is created upon selecting the **Update product** profiles action for a given environment.
-->

![组织级别的产品实例](/help/onboarding/assets/orglevel.png)

AEM组织级产品实例内有一个名为AEM组织级报告者的产品配置文件，它目前不使用，但将来可能会用于表示对检索有关AEM产品许可证信息的访问权限。

在许可Forms通信解决方案后，AEM组织级别的产品实例下也会显示相应的产品配置文件。

![Reporters产品配置文件](/help/onboarding/assets/org-level-reporters.png)

### 环境和层级产品实例 {#environment-and-tier-level-product-instances}

在使用一个或多个AEM环境配置新程序时，每个环境将显示两个产品实例，分别包含用于创作和发布的产品配置文件。

![环境产品实例](/help/onboarding/assets/env-productinstances.png)

以下是创作产品实例中的产品配置文件，适用于在包含AEM Sites的项目中设置环境的组织：

![站点产品实例](/help/onboarding/assets/sites-product-instances.png)

下表介绍了特定于环境层的产品实例下的可能产品配置文件列表。

<table style="table-layout:auto">
    <tr>
        <th>产品实例</th>
        <th>命名约定</th>
        <th>默认服务</th>
        <th>描述</th>
    </tr>
    <tr>
        <td>AEM Author</td>
        <td>AEM Sites Content Managers — 作者 — 项目<code>id</code> — 环境 <code>id</code></td>
        <td>AEM Sites Content Managers</td>
        <td>
            <ul>
                <li>旨在控制对此环境中的AEM Sites创作功能的访问。 此产品配置文件中的用户将成为AEM Sites内容创作AEM组的成员，该组是在AEM中自动创建的。 应在AEM中使用所需的访问级别配置AEM组权限。</li><br>
                <li>如果默认服务保持选中状态
                    <ul>
                        <li>此产品配置文件中的用户也将成为“AEM Sites内容管理器 — 服务”AEM组的成员。</li>
                      <!--  <li>users in this product profile will have access to AEM Sites Content Management API.</li>
                        <li>an Adobe Developer Console API OAuth S2S project containing AEM Sites Content Management API can optionally be scoped to this environment.</li>-->
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM管理员 — 作者 — 项目<code>id</code> — 环境 <code>id</code></td>
        <td>AEM管理员</td>
        <td>
            <ul>
                <li>旨在实现对AEM创作和发布环境功能的无限制访问。 此产品配置文件中的用户将成为在AEM中自动创建的AEM Administrators创作AEM组的成员。</li><br>
                <li>如果默认服务保持选中状态
                    <ul>
                        <li>此产品配置文件中的用户也将成为“AEM管理员 — 服务”AEM组的成员</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM用户 — 作者 — 项目<code>id</code> — 环境 <code>id</code></td>
        <td>AEM 用户</td>
        <td>
            <ul>
                <li>旨在提供对极其有限的AEM创作环境功能的访问。 此产品配置文件中的用户将成为在AEM中自动创建的“参与者”AEM组的成员</li><br>
                <li>如果默认服务保持选中状态
                    <ul>
                        <li>此产品配置文件中的用户也将成为“AEM用户 — 服务”AEM组的成员</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Reporters — 作者 — 项目<code>id</code> — 环境 <code>id</code></td>
        <td>AEM记者</td>
        <td>
            <ul>
                <li>当前未使用，但将来可能会提供对此环境的创作层的相关报表信息的访问权限。</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Assets Collaborator — 作者 — 项目<code>id</code> — 环境 <code>id</code></td>
        <td>AEM Assets协作者用户</td>
        <td>
        <ul>
                <li>旨在提供对DAM的只读访问权限。 此产品配置文件中的用户将成为在AEM中自动创建的“参与者”AEM组的成员。
                </li>
                <li>
                此外，它还提供创建Adobe Express变体的资源权限。
                </li>
          <ul>
    </tr>
    <tr>
        <td></td>
        <td>AEM Assets超级用户 — 作者 — 项目<code>id</code> — 环境 <code>id</code></td>
        <td>AEM Assets Power Users</td>
<td>
        <ul>
                <li>旨在提供对DAM的只读访问权限。 此产品配置文件中的用户将成为在AEM中自动创建的“参与者”AEM组的成员。
                </li>
                <li>
                此外，它还提供创建Adobe Express变体的资源权限。
                </li>
          <ul>
</td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Forms Content Managers — 作者 — 项目<code>id</code> — 环境 <code>id</code></td>
        <td>AEM Forms Content Managers</td>
        <td>
            <ul>
                <li>旨在控制对此环境中的AEM Forms创作功能的访问。 此产品配置文件中的用户将成为AEM Forms forms-users AEM组的成员，该组是在AEM中自动创建的。</li><br>
                <li>如果默认服务保持选中状态
                    <ul>
                        <li>此产品配置文件中的用户也将成为“AEM Forms内容管理器 — 服务”AEM组的成员。</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Forms开发人员 — 作者 — 计划<code>id</code> — 环境 <code>id</code></td>
        <td>AEM Forms开发人员</td>
        <td>
            <ul>
                <li>旨在控制对此环境中的AEM Forms创作功能的访问。 此产品配置文件中的用户将成为AEM Forms forms-power-users AEM组的成员，该组是在AEM中自动创建的。 除了正常的表单创作任务外，这些用户还有权上传XDP和创作表单数据模型。</li><br>
                <li>如果默认服务保持选中状态
                    <ul>
                        <li>此产品配置文件中的用户还将是“AEM Forms开发人员 — 服务”AEM组的成员。</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Forms Communications Service用户 — 作者 — 项目<code>id</code> — 环境 <code>id</code></td>
        <td>AEM Forms Communications Service用户</td>
        <td>
            <ul>
                <li>旨在控制对此环境中的AEM Forms Communications Services功能的访问。 此产品配置文件中的用户将成为AEM Forms forms-users AEM组的成员，该组是在AEM中自动创建的。</li><br>
                <li>如果默认服务保持选中状态
                    <ul>
                        <li>此产品配置文件中的用户也将成为“AEM Forms Communications Service用户 — 服务”AEM组的成员。</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>AEM 发布</td>
        <td>AEM用户 — 发布 — 项目<code>id</code> — 环境 <code>id</code></td>
        <td>AEM 用户</td>
        <td>
            <ul>
                <li>旨在提供对极其有限的AEM创作环境功能的访问。 此产品配置文件中的用户将成为在AEM中自动创建的“contrib”AEM组的成员</li><br>
                <li>如果默认服务保持选中状态
                    <ul>
                        <li>此产品配置文件中的用户也将成为“AEM用户 — 服务”AEM组的成员。</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM记者 — 发布 — 项目<code>id</code> — 环境 <code>id</code></td>
        <td>AEM记者</td>
        <td>
            <ul>
                <li>当前未使用，但将来可能会提供对此环境的发布层的相关报表信息的访问权限。</li>
            </ul>
        </td>
    </tr>
   <tr>
        <td></td>
        <td>AEM Forms Communications Service用户 — 发布 — 项目<code>id</code> — 环境 <code>id</code></td>
        <td>AEM Forms Communications Service用户</td>
        <td>
            <ul>
                <li>旨在控制对此环境中的AEM Forms Communications Services功能的访问。 此产品配置文件中的用户将成为AEM Forms forms-users AEM组的成员，该组是在AEM中自动创建的。</li><br>
                <li>如果默认服务保持选中状态
                    <ul>
                        <li>此产品配置文件中的用户也将成为“AEM Forms Communications Service用户 — 服务”AEM组的成员。</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
</table>

请注意，默认情况下，每个产品配置文件都启用了一个关联的产品配置文件服务。 除非您有复杂的访问要求，否则建议仅选择默认服务。 将在AEM中使用命名约定`<Product Profile Prefix> - Service`创建相应的AEM组(例如，**AEM Sites Content Managers - Service**)，父产品配置文件中的用户将自动成为该相应AEM组的成员。

与该服务相关联的AEM中的AEM组将具有一组聚合的用户，这些用户存在于该服务的所有关联产品配置文件中，以用于该环境层组合。

![服务](/help/onboarding/assets/services.png)

下图显示了反映AEM Sites Content Manager创作层产品配置文件和服务的AEM组。

![AEM组到服务的映射](/help/onboarding/assets/profile-to-service-mapping.png)

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
