---
title: AEM as a Cloud Service中的上下文实验
description: 了解如何使用试验插件向您的站点添加试验功能。
feature: Administering
role: Admin
badgeSaas: label="AEM Sites" type="Positive" tooltip="适用于AEM Sites)。"
exl-id: 420f8d5e-27f9-4081-b174-b2d7752779f7
source-git-commit: eed3a4866e3018b2ff6bc6e5c201523ab271c35f
workflow-type: tm+mt
source-wordcount: '1805'
ht-degree: 0%

---

# AEM as a Cloud Service中的上下文实验 {#contextual-experimentation}

>[!NOTE]
>目前，情景实验功能仅通过Beta版计划提供。 请联系Adobe支持人员或您的客户经理，以获取测试版计划的访问权限。

试验是测试站点的设计、功能和代码的实践，旨在提高性能并使站点更加高效和简化。 这是通过改变内容或功能、将结果与以前的版本进行比较以及挑选具有可衡量效果的改进来实现的。

如果操作得当，这是一个提高转化率、参与度和访客体验的强大模式。 一般来说，在寻求采用这种做法时，需要避免以下几个问题：

* **太少**：大多数公司的试验不足，当他们进行试验时，他们试验的流量太少，无法获得有意义的结果。
* **速度太慢**：许多实验框架导致网站速度太慢，以致于潜在的新转化无法弥补由于渲染速度缓慢而导致的流量丢失和跳出次数。
* **太复杂**：如果设置新试验花费的时间过长，则运行的试验将减少。

对于在Adobe Experience Manager上运行的网站，有一个“开箱即用”的&#x200B;**试验插件**，它允许开发人员向其网站添加试验功能。 有三个因素使得此方法与其他实验框架不同：

* 使用作者已熟悉的工具可轻松设置测试，无需单独登录。
* 它深度集成到AEM交付系统中，不会减慢网站运行速度，并且可以灵活地应对代码和内容中的更改。
* 它允许测试简单的内容更改以及涵盖设计、功能和代码的实验。

## 开始之前 {#before-start}

试验插件在[Edge Delivery Services](/help/edge/overview.md)的上下文中使用，因此您需要Github帐户、SharePoint或Google Drive等内容存储库，还需要[AEM Sidekick](https://www.aem.live/docs/sidekick)。 另请参阅[快速入门 — Universal Editor开发人员教程页面](https://www.aem.live/developer/tutorial)和[快速入门 — 开发人员教程](https://www.aem.live/developer/tutorial)。

完成所有设置后，**请观看此标题为**&#x200B;即时试验[的视频](https://business.adobe.com/cn/products/experience-manager/sites/testing-optimization.html)，简短演示试验插件的工作原理。

## 常用术语 {#frequently-used-terms}

在按照指南的其余部分设置您的第一个试验之前，您应该熟悉一些常用术语：

* **控制**：运行试验之前的体验。 所有实验都试图测试和证明比控制体验有所改进。
* **挑战者**：与控制体验不同的体验，该体验将针对该体验或与之一起“测试”。
* **变体**：控件和挑战者是试验的所有变体。
* **统计显着性**：评估您的挑战者是否真的优于对照组。 计算统计显着性可以排除运气，专注于具有实际效果的结果。

## 试验变量和常规工作流 {#experiment-variants-workflow}

一般而言，在设置试验时，您将使用预先存在的页面作为控制页面。 然后，您将创建一个挑战者页面，以替换一些访客的控制页面。 在挑战者页面中，您可以测试各种内容，例如内容变体、各种页面布局、call-to-action (CTA)等。 您可以通过在“控制”页面中添加元数据参数来配置这些试验变体（请参阅下文）。

然后，[操作遥测服务](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)收集数据，例如，对照页中的访客数与挑战者页中的访客数。 然后，您可以使用此数据为您的网站选择所需的改进。 只要您遵循网站既定设计语言并使用现有的块功能，就应该能够设置试验变体，并在几分钟内将其发送到生产环境。

>[!NOTE]
>请记住，此插件不使用也不保留任何可能导致标识的最终用户数据。 在使用AEM as a Cloud Service[中使用](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)操作遥测服务的默认配置时，无需最终用户选择加入或Cookie同意。

### 试验标识符 {#experiment-identifier}

在开始之前，每个试验都应该有自己的标识符用于跟踪和分析。 一个好的起点，是为您的试验提出一个好的、唯一的标识符，即“试验ID”。 试验通常按线性方式编号，或将其与问题跟踪器或管理系统中的问题ID相关联。 试验ID通常使用项目的前缀，例如： `OPT-0134`、`EXP0004`或`CCX0076`。

### 创建挑战者页面 {#create-challenger-page}

按照惯例，建议在`/experiments/ folder`中创建试验ID为小写的文件夹（例如/experiments/ccx0076/）。 挑战者变体的所有页面都位于此文件夹中。 您可以在本地存储库中创建此文件夹，例如Sharepoint或Goggle Drive。

试验文件夹应当如下所示：

![experiments-folder](/help/sites-cloud/administering/assets/experiments-folder.png)

创建文件夹后，将控制页面副本放入该文件夹，并在该页面上应用要作为试验变体的一部分测试的更改（请参阅上面的视频）。 例如，假设我们要在网站上运行试验的网页如下所示：

![control-page](/help/sites-cloud/administering/assets/control-page.png)

您放置在`experiments/<experiment-id>`文件夹中的挑战者副本可能如下所示：

![挑战者页面](/help/sites-cloud/administering/assets/challenger-page.png)

使用sidekick以及完成挑战者页面创作后预览和发布挑战者页面。 已发布挑战者的URL将在下一部分 — 配置试验中使用。

### 配置试验 {#configure-experiment}

一旦挑战者页面已准备就绪，您需要返回控制页面并添加元数据，以指示该页面现在是测试的一部分。

为试验变体需要添加两个元数据行。

* **试验**：包含您的试验ID。

* **试验变体**：包含此页面的所有挑战者的URL，如果您有多个挑战者，则用换行符分隔。

请参阅以下示例：

![metadata-page](/help/sites-cloud/administering/assets/metadata-page.png)

对于每个实验，流量会在所有变体（控制体验和挑战体验）之间拆分，并自动设置为均匀分布。 因此，如果你有一个挑战者，那么控制权与挑战者之间就会自动平分秋色。 如果您有两个挑战者，您将自动看到分配给控制的流量以及每个挑战者的流量中的三分之一，以此类推。

您可以通过配置元数据来覆盖流量分摊。 有关如何自定义实验中使用的元数据的详细信息，请参阅以下[页](https://github.com/adobe/aem-experience-decisioning/wiki/Experiments#authoring)。

### 预览和暂存试验变体 {#preview-stage-experiment}

准备好预览和暂存试验后，从左上角的侧踢中单击预览。 每当您预览包含正在运行的试验的页面时，您都会在`.aem.page`预览环境中看到试验叠加。 试验覆盖允许您在试验变体之间切换，并提供流量数据。

<!--- ![experimentation-overlay](/help/sites-cloud/administering/assets/experimentation-overlay.png)

By using the experimentation overlay, authors can get quick insights on the performance of experiments being run on the production site. These insights are helpful in making a decision about the duration of the experiment, but also about which variant is best suited for production.-->

用于衡量每个变体有效性的数据收集基于AEM as a Cloud Service[中的](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)操作遥测服务。

### 将试验变体发送到生产环境 {#production-experiment}

选择试验页面，然后单击侧踢中的发布，将控件和挑战者变体推送到实时状态。

### 用例示例 {#use-case-examples}

下面提供了试验变体的几个用例示例。 一般而言，基本工作流将与上面描述的工作流类似，对每个用例进行特定的更改（例如挑战者页面数量或元数据更改）。

#### 全页试验 {#full-page}

可使用全页试验在同一个页面的两个变体之间进行测试。 这是a/b测试的全页变体，您具有控件和挑战者页面。 您将使用不同类型的内容替换挑战者变体中“原始”控制页面的整个内容。 请记住，默认情况下，客户流量是平均拆分(50/50)，但如果您愿意，可以创建自定义拆分。

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

下面显示了使用上下文试验时应考虑的其他几个方面。

### 转化 {#conversion}

设置试验以解决转化问题（跟踪页面上的可点击元素）。 必须针对以下各项定义所有试验：

* 试验类型
* 试验将应用于哪个体验块
* 试验将包含多少个变体
* 每个变体的构成是什么

### 确保试验变体未编制索引 {#experiment-not-indexed}

运行实验时，通常最佳实践是从站点地图中排除变体，并确保搜索引擎不为这些变体编制索引。 这是因为变量页面可能会被视为重复的内容并对SEO产生负面影响。

可以使用以下两种方法之一完成此操作：

* 如果将所有实验集中到一个专用文件夹（如`/experiments`）中：请确保您的批量`metadata.xlsx`工作表包含一行，其中路径为`/experiments/**`，并且包含值为`noindex`、`nofollow`的robots列。
* 如果保留具有常规内容的试验控件和变体：请在每个变体的页面元数据中添加一个robots条目，其值为`noindex`，`nofollow`。

## 开发人员和技术资源 {#dev-resources}

Adobe Experience Manager使用[操作遥测]&#x200B;(/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)

)，以收集在发现和修复由Adobe Experience Manager提供支持的站点上的功能和性能问题所必需的操作数据。 操作遥测数据可用于诊断性能问题。 操作遥测通过取样保护访客的隐私（仅监视所有页面查看的一小部分）。

### 隐私 {#privacy-experimentation}

AEM as a Cloud Service[中的](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)操作遥测服务旨在保留访客隐私并最大限度地减少数据收集。 作为访客，这意味着Adobe不会尝试收集您的个人信息或可以跟踪回您的信息。 作为站点操作员，请查看下面收集的数据项以了解它们是否需要同意。
AEM Operational Telemetry不使用任何客户端状态或ID（如Cookie或`localStorage`、`sessionStorage`或类似项）来收集使用情况度量。 数据是通过`Navigator.sendBeacon`调用透明提交的，而不是通过像素或类似技术提交的。 不存在通过设备或个人的IP地址、用户代理字符串或任何其他数据来捕获采样数据的“指纹”。

不得将个人数据添加到操作遥测数据收集中，也不得将操作遥测数据用于超出严格必要范围的用例。

### 常见问题解答 {#faq}

下面列出了常见问题：

问：我能否调整我的试验变体之间的分割比率，例如对照组为10%，挑战者为90%？

可以，可通过[元数据](#configure-experiment)配置拆分比率。

问：我能否对文本和图像都进行实验？

可以，该变体可以是一个完全不同的页面，因此您甚至可以测试布局更改。
