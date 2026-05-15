---
title: AEM as a Cloud Service中的上下文实验
description: 了解如何使用试验边栏为您的站点添加试验功能。
feature: Administering
role: Admin
source-git-commit: c948abf5391e61f01912f769b17e1ac0bd81a745
workflow-type: tm+mt
source-wordcount: '1949'
ht-degree: 2%

---

# AEM as a Cloud Service中的上下文实验 {#contextual-experimentation}

试验是测试站点的设计、功能和代码的实践，旨在提高性能并使站点更加高效和简化。 这是通过改变内容或功能、将结果与以前的版本进行比较以及挑选具有可衡量效果的改进来实现的。

如果操作得当，这是一个提高转化率、参与度和访客体验的强大模式。 一般来说，在寻求采用这种做法时，需要避免以下几个问题：

* **太少**：大多数公司的试验不足，当他们进行试验时，他们试验的流量太少，无法获得有意义的结果。
* **速度太慢**：许多实验框架导致网站速度太慢，以致于潜在的新转化无法弥补由于渲染速度缓慢而导致的流量丢失和跳出次数。
* **太复杂**：如果设置新试验花费的时间过长，则运行的试验将减少。

对于在Adobe Experience Manager上运行的网站，开发人员可以选择为其网站添加新试验功能。 有三个因素使得此方法与其他实验框架不同：

* 使用作者已熟悉的工具可轻松设置测试，无需单独登录。
* 它深度集成到AEM交付系统中，不会减慢网站运行速度，并且可以灵活地应对代码和内容中的更改。
* 它允许测试简单的内容更改以及涵盖设计、功能和代码的实验。

## 试验边栏 {#experimentation-rail}

试验边栏是您设置试验的主要方式。 它可以在[Edge Delivery Services](/help/edge/overview.md)上下文或[通用编辑器](/help/implementing/universal-editor/introduction.md)中与您的项目一起使用。 因此，您将需要Github帐户、SharePoint或Google Drive等内容存储库，并且还需要[AEM Sidekick](https://www.aem.live/docs/sidekick)插件。 如果要使用通用编辑器，您还需要访问[AEM as a Cloud Service环境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)。 另请参阅[快速入门 — Universal Editor开发人员教程页面](https://www.aem.live/developer/tutorial)。

>[!WARNING]
>为了充分发挥试验能力，需要试验引擎。 在执行以下步骤之前，请确保已正确安装和更新引擎。 有关详细信息，请参阅以下[安装页面](https://github.com/adobe/aem-experimentation/tree/v2?tab=readme-ov-file#installation)。

### 在Edge Delivery Services中使用AEM Sidekick设置试验

要访问Edge Delivery Services项目中的试验边栏功能，您需要[AEM Sidekick](https://www.aem.live/docs/sidekick)插件。 要设置sidekick，请执行以下步骤：

1. 添加[AEM Sidekick扩展](https://chromewebstore.google.com/search/AEM%20Sidekick?hl=en-US&utm_source=ext_sidebar)并将其固定到您的浏览器中。
1. 在预览模式下打开项目页面。
1. 在AEM Sidekick栏上，单击设置图标![设置](/help/sites-cloud/administering/assets/settings-1.png)并选择&#x200B;**添加此项目**。
1. 单击试验选项卡以打开试验边栏。

### 在通用编辑器中设置试验

在设置实验之前，请记住，您需要使用AEM站点作为内容源，才能在通用编辑器中创作。 如果需要，您可以按照[将AEM设置为内容Source](https://www.aem.live/developer/ue-tutorial)页面中提供的教程将现有项目转换为作为内容源的AEM Sites站点。 准备在通用编辑器中设置试验时，请执行以下步骤：

1. 在通用编辑器中打开您的项目，并检查&#x200B;**A/B**图标扩展。 如果图标不可见，请确认您在扩展管理器中是否已启用该功能。 如果未启用，请启用它或请求访问权限。
   <!--1. Open your GitHub repository and check if the `plugins/experimention` folder exists. If not, you will need to set up the experimentation engine and MFE first (see the note above).-->
1. 将`fstab.yaml`配置指向项目配置，并将其链接到AEM创作实例。 另请参阅[将您的代码连接到内容](https://www.aem.live/developer/ue-tutorial#connect-your-code-to-your-content)
1. 打开AEM实例，如果项目已就绪，则直接在通用编辑器中打开该实例。
1. 打开要运行试验的项目和索引页，然后单击顶部栏上的&#x200B;**编辑**。
1. 单击A/B图标以打开试验扩展。

>[!NOTE]
>如果您在为项目设置试验时遇到问题，请联系`aem-contextual-experimentation@adobe.com`。

>[!NOTE]
>有关如何设置和配置试验引擎的更多详细信息，请参阅以下[存储库](https://github.com/adobe/aem-experimentation/tree/v2-ui)中的文档部分。

## 试验变量和常规工作流 {#experiment-variants-workflow}

在按照指南的其余部分配置您的第一个试验之前，您应该熟悉一些常用术语：

* **控制**：运行试验之前的体验。 所有实验都试图测试和证明比控制体验有所改进。
* **挑战者**：与控制体验不同的体验，并且已针对该体验或与其一起进行“测试”。
* **变体**：控件和挑战者是试验的所有变体。
* **统计显着性**：评估您的挑战者是否真的优于对照组。 计算统计显着性可以排除运气，专注于具有实际效果的结果。

一般而言，在设置试验时，您将使用预先存在的页面作为控制页面。 然后，通过使用试验边栏，创建一个挑战者页面，该页面最初是控制页面的副本。 在挑战者页面中，您可以测试各种内容，例如内容变体、各种页面布局、call-to-action (CTA)等。 还可通过在试验边栏中使用&#x200B;**生成变量**&#x200B;功能，使用AI生成的变量。

对于每个实验，流量最初在控制方和挑战方之间按50/50的分摊，但您可以根据需要配置流量的分摊方式。 激活试验后，您将通过操作遥测服务接收数据。

[可操作遥测服务](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)收集数据，例如，对照页中的访客数与挑战者页中的访客数。 然后，您可以使用此数据为您的网站选择所需的改进。 只要您遵循网站既定设计语言并使用现有功能，就应该能够设置试验变体，并在几分钟内将其发送到生产环境。

>[!NOTE]
>请记住，此插件不使用也不保留任何可能导致标识的最终用户数据。 在使用AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)中使用[操作遥测服务的默认配置时，不需要最终用户选择加入或Cookie同意。

<!--### Frequently used terms {#frequently-used-terms}

Before following the rest of the guide to set up your first experiment, there are a few frequently used terms that you should be familiar with:

* **Control**: the experience prior to running the experiment. All experiments try to test and demonstrate an improvement over the control experience.
* **Challenger**: an experience that is different from the control experience and is "tested" against it or alongside it.
* **Variants**: control and challenger are all variants of an experiment.
* **Statistical Significance**: Evaluating if your challenger is really better than the control. Calculating statistical significance allows you to rule out luck and concentrate on the results that have a real effect. -->

### 在通用编辑器中创建试验

要使用Universal Editor中的试验功能，您必须首先设置试验边栏（如上面各章所述），并确保使用AEM sites作为内容源。 完成所有设置后，请执行以下步骤。

### 在通用编辑器中开始编辑您的项目

打开AEM实例，如果项目已就绪，则直接在通用编辑器中打开该实例。 如果您没有项目就绪并且AEM站点未设置为内容源，请从提供的模板创建新的样板项目。 您可以链接您的存储库或我们的示例存储库来驱动它[https://github.com/sudo-buddy/ue-experimentation](https://github.com/sudo-buddy/ue-experimentation)。 另请参阅[设置AEM Sites as a Content Source](https://www.aem.live/developer/ue-tutorial)页面。 设置项目后，打开它以及要运行试验的索引页，然后单击顶部栏上的&#x200B;**编辑**。

### 启动A/B扩展

单击&#x200B;**A/B**&#x200B;图标以打开试验扩展。 首次使用时，界面将为空。 单击&#x200B;**新建**&#x200B;以开始新试验。

![a-b](/help/sites-cloud/administering/assets/a-b.png)

### 配置试验详细信息

一些试验值是预定义的，如下所示：

**试验类型**： A/B测试（当前仅支持此类型）
**针对**&#x200B;进行优化：转换（当前仅支持此类型）

您还可以将试验重命名为更具描述性的某些项目，例如，`homepage-head-experiment`。

![试验详细信息](/help/sites-cloud/administering/assets/exp-values.png)

### 添加和编辑变体

在继续之前，请确保您了解上述挑战者和变体的概念。 单击&#x200B;**新增**&#x200B;以创建挑战者变体：

* 您将转到同一选项卡中的挑战者页面 — 它最初只是您的控制项的副本。
* 直接在上下文中编辑页面或单击&#x200B;**生成变量**&#x200B;以使用AI帮助。
* 进行更改后，请返回扩展以继续。

![Control-variant](/help/sites-cloud/administering/assets/control-variant.png)

### 定义其他属性并另存为草稿

在试验边栏中，您可以设置开始日期和结束日期（均可选）。 如果未提供开始日期，则测试将在发布后开始。 如果未提供结束日期，则测试将无限期运行。 您也可以调整流量拆分，我们建议从偶数50/50拆分开始。

完成后，单击&#x200B;**保存** — 这会将您的试验另存为草稿。 请注意，试验尚未处于活动状态。 您可以通过单击&#x200B;**返回实验**&#x200B;返回概述，也可以停留在“编辑”界面以激活实验。

![草稿](/help/sites-cloud/administering/assets/draft-save.png)

### 激活试验

准备就绪后，单击&#x200B;**激活**&#x200B;以启动试验并发布试验页面。 测试将开始收集操作遥测(RUM)数据（请参阅以下章节中的更多详细信息）。

![激活](/help/sites-cloud/administering/assets/activate.png)

### Monitor and Promote

在试验达到统计显着性后，单击&#x200B;**提升**&#x200B;以将所需的变体设置为新对照。 请记住，您可以在激活后的任何时间提升试验变体，即使它没有达到统计意义。

### 在Edge Delivery Services中对AEM Sidekick使用试验

如果您安装了AEM Sidekick，则可以直接在Edge Delivery服务中将试验边栏与您的项目一起使用，而无需使用通用编辑器。 该功能与上述A/B测试基本相同，请记住，您需要&#x200B;**预览**&#x200B;模式才能编辑和配置该测试。 完成测试配置后，单击&#x200B;**激活**&#x200B;以启用控件和挑战者变体并开始收集遥测数据。

<!-- ### Experiment Identifier {#experiment-identifier}

Before you start, every experiment should have its own identifier for tracking and analytics purposes. A good starting point is to come up with a good, unique identifier for your experiment which will be the “Experiment ID”. Experiments are often numbered linearly or correlated to their Issue ID in an issue tracker or management system. Experiment IDs often use a prefix for the project, for example: `OPT-0134`, `EXP0004` or `CCX0076`.

### Create your Challenger Page {#create-challenger-page}

By convention, it is recommended to create a folder with a lowercase experiment ID in your `/experiments/ folder` (for example /experiments/ccx0076/). All the pages for the challenger variants are located in this folder. You create this folder in your local repository, for example, Sharepoint or Goggle Drive.

Your experiments folder should look something like this:

![experiments-folder](/help/sites-cloud/administering/assets/experiments-folder.png)

Once the folder is created, put a copy of your control page into that folder, and apply the changes on the page that you would like to test as part of your experiment variant (see video above). As an example let’s assume we have the following page on the website that we want to run an experiment on:

![control-page](/help/sites-cloud/administering/assets/control-page.png)

Your copy of the challenger placed in the experiments/experiment-id folder might look like this:

![challenger-page](/help/sites-cloud/administering/assets/challenger-page.png)

Preview and publish the challenger page using the sidekick and when you are done authoring the challenger page. The URL of the published challenger will be used in the next section - configuring the experiment.

### Configuring the experiment {#configure-experiment}

As soon as the challenger pages are ready to go, you need to go back to the control page and add metadata indicating that the page(s) are now part of the test.

There are two metadata rows that need to be added for an experiment variant.

* **Experiment**: containing your experiment ID.

* **Experiment Variants**: containing URLs for all the challengers of this page, separated by line breaks if you have more than one challenger.

See the example below:

![metadata-page](/help/sites-cloud/administering/assets/metadata-page.png)

For each experiment, the traffic is split between all the variants (control and challengers) and is automatically set to an even distribution. As such, if you have one challenger, there will automatically be an even 50/50 split between control and the challenger. If you have two challengers, you will automatically see a third of the traffic allocated to control and each challenger and so on.

You can override the traffic split by configuring the metadata. For more information on how you can customize the metadata used in your experiments, see the following [page](https://github.com/adobe/aem-experience-decisioning/wiki/Experiments#authoring).

### Preview and Stage your Experiment Variants {#preview-stage-experiment}

As soon as you are ready to preview and stage your experiment, click Preview from the side-kick in the upper left side. Whenever you are previewing a page that has a running experiment, you will see the experimentation overlay in your `.aem.page` preview environment. The experimentation overlay lets you switch between the experiment variants and also provides traffic data.

<!--- ![experimentation-overlay](/help/sites-cloud/administering/assets/experimentation-overlay.png)

By using the experimentation overlay, authors can get quick insights on the performance of experiments being run on the production site. These insights are helpful in making a decision about the duration of the experiment, but also about which variant is best suited for production.-->

<!--- The data collection to measure the effectiveness of each variant is based on the [Operational Telemetry service in AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md). -->

<!--- ### Send your Experiment Variant to Production {#production-experiment}

Select the experiment pages and click Publish from the side-kick to push both the control and the challenger variant(s) live.

### Use Case Examples {#use-case-examples}

Presented below are several use case examples for experiment variants. Generally speaking, the basic worklflow will be similar to the one described above, with particular changes for each use case (like the number of challenger pages or metadata changes).

#### Full Page Experiment {#full-page}

You use a full page experiment to test between two variants of the same page. This is a full page variant of an a/b test where you have a control and a challenger page. You will replace the whole content of the "original" control page in the challenger variant with a different type of content. Keep in mind that by default the customer traffic is split evenly (50/50), but you can create custom splits if you like. -->

<!--The metadata on the control page should look like this:

METADATA SETUP

#### Sections of the page Experiment {#sections-of-the-page}

This is experiment is similar to the full page one presented above but now the a/b test will contain changes to a section of the page instead of the whole content. For example, you can modify and test a carousel element, the call to action element and so on. As such, you will have a control and a challenger page, with the challenger page containing the modified elements. The metadata on the control page should look like this:

METADATA SETUP

#### Multi-path Experiment {#multi-path}

By leveraging the experimentation plug-in, you can set up a/b tests on several pages of your website at once. For example, on all product pages, photo galleries, all blog posts and so on.

The configuration logic is the same as above - you will create a control page and one or more challenger variants of that page. What changes in the multi-page use-case, is the following:

• You will create multiple control pages each with one or more variants.
• The control pages must have the same experiment ID in metadata field.

For example: We have 5 different production pages for which we need to set up an a/b test. We create 5 control pages (as detailed in the chapters above) and 5 (or more) challenger variants.

We then create an experiment ID, let’s say `prod-exp` and add this ID in the experiment metadata field for each control page. This basically means that all pages with the same ID are now “grouped”. We then assign the challenger variants for each control page, taking care to sequence them properly in case we have more than one variant for each control.

The metadata on the control page should look like this:

METADATA SETUP

#### Code-level experiments {#code-level}

Note that the examples above assume you have different content variants to serve, but if you want to run a pure code-based a/b test, this is achievable via:

Metadata

Experiment    Hero Test
Experiment Variants    2

This will create just two variants, without touching the content, and you'll be able to target those based on the `experiment-hero-test` and `variant-control/variant-challenger-1/variant-challenger-`2 CSS classes that will be set on the `<body>` element.

#### Browser based audience experiment {#browser-based}

You can create browser based experiments, where you deliver separate challenger pages depending on the browser used. You can, for example, serve a different challenger page to a Firefox user as opposed to a Chrome user. This is achieved by leveraging the audience parameter.

Once you configure the experiment, the target audience will be evaluated based on the context of the browser (client side) and limited to the browser APIs available. As such, you do not need to use server side third-party systems or customer profile data for your experiment.

Before you start authoring this experiment variant, the audience parameter needs to be defined in the project codebase. For more details, see ee the following [page](https://github.com/adobe/aem-experience-decisioning/wiki/Experiments#authoring).

Once the audiences have been defined you are ready to author the experiment. As stated previously, let’s say you want to create a Firefox versus Chrome experiment where you will serve different pages depending on the browser.

You need two different challenger pages, so set up the experiment as follows:

1.Duplicate the Control page by right-clicking and copying it to the experiment folder. You need to copies, one for Firefox and one for Chrome.
2.Rename the copies. Give them specific names like “page-for-firefox”.
3.Change the content of the pages depending on what you need to serve on Firefox versus Chrome.
4.Change the metadata as explained in the section below.
5.Click Preview from the side-kick in the upper left side, to preview the changes.

The most important part when authoring this experiment is to change the metadata in the control page. Let’s say you defined the browser audiences in the codebase as: Audience: Firefox and Audience: Chrome. You need to edit the control page and add these audiences and point to the appropriate challenge page you set up previously. It should look similar to this:

Metadata
Title Control Page
Description This is the control page.
Experiment ExpBrowser
Experiment Variants `https://{ref}--{repo}--{org}.hlx.page/my-page-for-firefox https://{ref}--{repo}--{org}.hlx.page/my-page-for-chrome`
Audience: Firefox `https://{ref}--{repo}--{org}.hlx.page/page-for-firefox`
Audience: Chrome `https://{ref}--{repo}--{org}.hlx.page/page-for-chrome`

After this configuration, the users will be triaged based on the browser they connect with and the appropriate challenger page will be served.

Please keep in mind that the names above are only for illustration purposes. You can define the Audiences parameter and the challenger pages according to your needs, for example: Audience (Firefox) or Audience Firefox.-->

## 其他注意事项 {#other-considerations}

下面显示了使用上下文试验时应考虑的几个方面。

### 转化 {#conversion}

设置试验以解决转化问题（跟踪页面上的可点击元素）。 目前，我们支持页面级实验，每页一个实验。

<!--### Make sure experiment Variants are not indexed {#experiment-not-indexed}

When running experiments, it is usually best practice to exclude the variants from the sitemap and ensure they are not indexed by search engines. This is because the variant page could be seen as duplicate content and negatively impact SEO.

You can do this by using either of the following two methods:

* If you centralize all experiments in a dedicated folder, like `/experiments`: make sure your bulk `metadata.xlsx` sheet contains a row with `/experiments/**` as path, and a robots column with the values `noindex`, `nofollow`.
* If you keep the experiment control and variants with the regular content: add a robots entry in the page metadata for each variant, with the value `noindex`, `nofollow`.-->

## 开发人员和技术资源 {#dev-resources}

Adobe Experience Manager 使用[运营遥测](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)功能收集运营数据，仅用于发现并解决基于 Adobe Experience Manager 构建的网站中的功能与性能问题。 操作遥测数据可用于诊断性能问题。 操作遥测通过取样保护访客的隐私（仅监视所有页面查看的一小部分）。

### 隐私 {#privacy-experimentation}

AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)中的[操作遥测服务旨在保留访客隐私并最大限度地减少数据收集。 作为访客，这意味着Adobe不会尝试收集您的个人信息或可以跟踪回您的信息。 作为站点操作员，请查看下面收集的数据项以了解它们是否需要同意。
AEM Operational Telemetry不使用任何客户端状态或ID（如Cookie或`localStorage`、`sessionStorage`或类似项）来收集使用情况度量。 数据是通过`Navigator.sendBeacon`调用透明提交的，而不是通过像素或类似技术提交的。 不存在通过设备或个人的IP地址、用户代理字符串或任何其他数据来捕获采样数据的“指纹”。

不得将个人数据添加到操作遥测数据收集中，也不得将操作遥测数据用于超出严格必要范围的用例。
