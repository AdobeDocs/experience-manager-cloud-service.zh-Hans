---
title: 如何启用Adobe Analytics以进行自适应表单的快速跟踪分析？
description: Experience Cloud设置自动化帮助Adobe Analytics连接到自适应表单，以便快速跟踪关于访客交互和参与的分析见解。
keywords: 使用Experience Cloud设置自动化为自适应表单启用Adobe Analytics，在Forms中启用Adobe Analytics，在自适应Forms中启用Adobe Analytics，Forms Analytics集成、Forms和Adobe Analytics
feature: Adaptive Forms
role: Admin, User
exl-id: 0e1aa040-08b4-4c1a-b247-ad6fff410187
source-git-commit: a23576b5dc6d78a29fe19cd23f3c4788f2bee23e
workflow-type: tm+mt
source-wordcount: '1588'
ht-degree: 2%

---

# 使用Experience Cloud设置自动为自适应表单启用Adobe Analytics {#integrate-adobe-analytics-to-aem-forms-with-experience-cloud-setup-automation}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | 本文 |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/configure-analytics-forms-documents.html) |

“Experience Cloud设置自动化”有助于将Adobe Analytics连接到Adaptive Forms，后者有助于快速跟踪分析用户与您的表单的交互，并提供有关访客交互和参与情况的洞察。 Experience Cloud设置自动化还有助于监控表单性能，其中涉及评估完成时间和流失点等指标。 此分析有助于优化表单以获得更好的用户体验，同时根据登录状态（例如，匿名用户）区分用户行为以确定一般趋势和模式。

## 将Adobe Analytics与自适应Forms集成的优势 {#advantages-of-integrating-adobe-analytics-with-aem-forms}

* **最终用户行为分析**： Adobe Analytics有助于了解最终用户行为，揭示用户操作、流失和完成率，从而更深入地了解个人如何与表单互动。
* **使非技术性业务用户能够获得见解**：Adobe Analytics通过其易于使用的界面使非技术性用户也能够访问和解释表单使用数据，从而促进数据驱动型决策以增强注册体验。
* **根据使用情况优化数据捕获体验**：组织可以轻松地识别数据捕获中的棘手问题，从而带来有针对性的改进，提高表单可用性并增加成功提交次数。

## 自适应Forms使用量度的范围 {#scope-of-adaptive-forms-usage-metrics}

Adobe Analytics提供了一系列全面的自适应Forms性能指标，旨在提供有关表单使用情况的宝贵见解，并提供快速跟踪分析。 这些指标包括：

* **表单呈现、表单提交、验证错误和独特访客**，允许您评估表单的使用情况和有效性。

* **访客洞察**，其中包含访问和提交频率以及独特访客计数，可全面了解表单受众。

* **设备类型**&#x200B;数据，它通知您用户使用哪些设备来访问您的表单。

* **地理细分**&#x200B;将显示表单用户的区域分布。

* **流量源**&#x200B;和&#x200B;**常用表单**&#x200B;量度（由顶级反向链接域和最常访问的表单组成）可帮助您了解流量的来源以及最常用的表单。

* **热门表单上的用户活动**&#x200B;提供了有关字段访问、表单呈现、验证错误、放弃的表单和表单提交的见解，允许您分析用户行为。

* **表单逗留时间的时间线**，它提供了基于时间线的用户参与表单视图。

* **需要访客协助的区域**&#x200B;量度，包括帮助视图、验证错误实例和字段访问频率，突出显示用户在填写表单时需要协助的位置。

![分析报告](assets/analytics-report.png){width="100%"}


有关每个量度的详细信息，请访问[查看和了解AEM Forms Analytics报表](/help/forms/view-understand-aem-forms-analytics-reports.md)

## 先决条件 {#prerequisites}

<!--
Analytics, Data Collection (Formerly Adobe Launch), and Experience Manager (experience.adobe.com)
-->

Experience Cloud设置自动化需要&#x200B;**Adobe Analytics许可证**、**数据收集(以前为AdobeLaunch)**&#x200B;来管理跟踪脚本，以及&#x200B;**Experience Manager Forms许可证**&#x200B;来简化数据聚合和洞察生成。

如果您拥有&#x200B;**Adobe Analytics**&#x200B;和&#x200B;**Experience Manager Forms**&#x200B;的有效许可证，并且与&#x200B;**数据收集(以前为AdobeLaunch)**&#x200B;集成，则应在开发人员控制台中验证其可用性。

要验证上述内容是否可用于您的Formsas a Cloud Service环境，请访问[开发人员控制台](https://developer.adobe.com/console/projects)，导航到项目并使用项目ID — 环境ID搜索您的项目，例如，对于URL为`https://author-p45913-e175111-cmstg.adobeaemcloud.com/index.html`、项目ID — 环境ID为`p45913-e175111`的环境。 确保列出了Experience Cloud设置自动化、Adobe Analytics和Experience Platform LaunchAPI。 如果列出了这些参数，则可启用Adobe Analytics以进行自适应Forms的快速跟踪分析。

![预先Forms Analytics集成](assets/analytics-aem.png){width="100%"}

<!-- 
>[!NOTE]
> If you have an active licenses for Experience Cloud Setup Automation, Adobe Analytics, and Experience Platform Launch API, you should verify their availability within your developer console.
-->

<!-- For more information about your available integrations, see [troubleshooting Adaptive Forms with Analytics Integration](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/view-understand-aem-forms-analytics-reports.html)
-->

## 配置Adobe Analytics {#configure-adobe-analytics}

执行以下列出的步骤来启用和配置Adobe Analytics，以便快速跟踪您的自适应Forms分析：

* [为基于基础组件的自适应Forms启用Adobe Analytics](#integrate-adobe-analytics-with-aem-forms-for-foundation-component)
* [基于核心组件为自适应Forms启用Adobe Analytics](#integrate-adobe-analytics-with-aem-forms-for-core-components)

>[!VIDEO](https://video.tv.adobe.com/v/3424577/enable-adobe-analytics/?quality=12&learn=on)


<!--
>[!NOTE]
>
> This is the demo video for **Foundation Component**. In **Core Component** you are required to perform similar steps but the container is not chosen for forms.
-->

### 通过自适应Forms for Foundation组件启用Adobe Analytics {#integrate-adobe-analytics-with-aem-forms-for-foundation-component}

1. 为云服务创建配置容器：
   1. 转到&#x200B;**[!UICONTROL 工具>常规>配置浏览器]**。
   1. 选择或创建配置容器，并启用&#x200B;**[!UICONTROL 云配置]**&#x200B;的文件夹。
   1. 选择&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;以保存配置并退出对话框。
1. 在您的AEM实例上，转到&#x200B;**[Forms]** >> **[Forms和文档]**。
1. 选择您的&#x200B;**[!UICONTROL 表单]** >> **[!UICONTROL 属性]**，在&#x200B;**[!UICONTROL 配置容器]**&#x200B;中，选择您在步骤1中的&#x200B;**[!UICONTROL 配置浏览器]**&#x200B;中创建或选择的配置容器。
1. 选择左边栏上的“任务”面板，然后单击&#x200B;**设置Analytics**&#x200B;和&#x200B;**激活Adobe Analytics**。
1. 提供您喜欢的报表包名称，单击&#x200B;**[!UICONTROL 下一步]**&#x200B;和&#x200B;**[!UICONTROL 保存]**。
1. 保存项目后，安装程序将运行一段时间，直到Adobe Analytics与您的自适应表单集成，您还可以检查&#x200B;**集成状态**。

   >[!NOTE]
   >
   >如果您的设置超过15分钟，请重试为表单启用分析。

1. 在您的AEM实例上，转到&#x200B;**[!UICONTROL Forms]** >> **[Forms和文档]**&#x200B;并选择您的&#x200B;**[!UICONTROL 表单]**，您会看到Adobe Analytics已集成到您的表单中，如下图所示。
1. 现在您可以查看[自适应表单Adobe Analytics报表](#view-adobe-analytics-report)。

![集成的AEM Analytics](assets/analytics-aem-integrated.png){width="100%"}


### 为核心组件启用具有自适应Forms的Adobe Analytics {#integrate-adobe-analytics-with-aem-forms-for-core-components}

1. 在您的AEM实例上，转到&#x200B;**[!UICONTROL Forms]** >> **[!UICONTROL Forms和文档]**&#x200B;并选择您的&#x200B;**[!UICONTROL 表单]**。
1. 选择左侧的任务面板，然后单击&#x200B;**设置Analytics**&#x200B;和&#x200B;**激活Adobe Analytics**。
1. 提供您喜欢的报表包名称，单击&#x200B;**[!UICONTROL 下一步]**&#x200B;和&#x200B;**[!UICONTROL 保存]**。
1. 保存项目后，安装程序将运行一段时间，直到Adobe Analytics与您的自适应表单集成，您还可以检查&#x200B;**集成状态**。

   >[!NOTE]
   >
   >如果您的设置超过15分钟，请重试为表单启用分析。

1. 在您的AEM实例上，转到&#x200B;**[!UICONTROL Forms]** >> **[!UICONTROL Forms和文档]**&#x200B;并选择您的&#x200B;**[!UICONTROL 表单]**，您会看到Adobe Analytics已集成到您的表单中。
1. 现在您可以查看[自适应表单Adobe Analytics报表](#view-adobe-analytics-report)。

## 查看自适应Forms Adobe Analytics报表 {#view-adobe-analytics-report}

1. 在您的AEM实例上，转到&#x200B;**[!UICONTROL Forms]** >> **[!UICONTROL Forms和文档]**。
1. 选择您的表单，您会看到Adobe Analytics已集成（如左图所示）到为Adobe Analytics激活的Forms。

   ![查看报告](assets/activ-aa.png){width="100%"}

1. 单击&#x200B;**Adobe Analytics**&#x200B;查看您的报告并分析性能数据。

要使用手动方法将自适应表单与Adobe Analytics连接，请访问[将AEM Forms与Adobe Analytics集成](/help/forms/integrate-aem-forms-with-adobe-analytics.md)。

## 在站点中启用Analytics到自适应Forms {#Connect-Analytics-to-Adaptive-Forms-in-Sites}

在AEM Sites中为自适应表单配置Fast Track Analytics有助于跟踪用户交互和表单在Sites页面中的表单提交。 通过在您的站点Forms中无缝集成Analytics，您可以获得关于用户行为、转化率和表单中需要改进的领域的宝贵见解。

### 先决条件 {#Prerequisites-to-connect-forms-analytics-to-sites}

要在Adaptive Forms for AEM Sites中连接并启用Analytics，您必须确保AEM Sites具有活动的Adobe Analytics。

### 在站点中连接自适应Forms以启用Analytics {#Connect-analytics-to-adaptive-forms}

要在AEM Sites页面中连接自适应表单以启用Analytics以进行快速跟踪分析，请使用AEM Archetype/Git存储库和部署管道将`customfooterlibs`客户端库包含到AEM Sites页面。

1. 在文本编辑器中打开[AEM Forms原型或克隆的Git存储库](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)项目。 例如，Visual Studio Code。

1. 导航到您的自适应表单所在的站点页面，例如，在此演示项目中，我们有`ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`。

1. 复制`sling:resourceSuperType`的值。 例如，值为`core/wcm/components/page/v3/page`。

   ![Sling 资源](/help/forms/assets/slingresource.png){width="100%"}

1. 在与`core/wcm/components/page/v3/page`相同的位置`ui.apps/src/main/content/jcr_root/apps`处创建类似的结构。

   ![覆盖结构](/help/forms/assets/overlaystructure.png){width="100%"}

1. 添加`customfooterlibs.html`文件。

   ```
   // customheaderlibs.html
   <sly data-sly-use.page="com.adobe.cq.wcm.core.components.models.Page">
   <sly data-sly-test="${page.data && page.dataLayerClientlibIncluded}" data-sly-call="${clientlib.js @ categories='core.forms.components.commons.v1.datalayer', async=true}"></sly>
   </sly>
   ```

   `customfooterlibs.html`用于JavaScript。

1. [运行管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html)以部署更改。

### 在站点中启用Forms的Form Analytics规则 {#bind-forms-analytics-rules-to-forms-in-sites}

1. 访问&#x200B;**Adobe Experience Platform数据收集**。
1. 单击左侧的&#x200B;**标记**。
1. 使用下图所示的程序ID搜索项目，例如，对于URL为`https://author-p45921-e175111-cmstg.adobeaemcloud.com/index.html`的环境，程序ID为`45921`。

   ![Search-your-form-in-data-collection](/help/forms/assets/aep-data-collection.png){width="100%"}

1. 为&#x200B;**表单规则**&#x200B;和&#x200B;**数据元素**&#x200B;添加配置，如下所示：

#### 添加表单规则 {#form-rules}

1. 选择您的表单并添加位于右上角的&#x200B;**新属性**，或单击您的表单。
1. 在属性页面上，单击&#x200B;**规则**&#x200B;并为您的表单选择事件。在下面的示例图像中，它是&#x200B;**表单事件**。

   ![Search-your-form-in-data-collection](/help/forms/assets/aep-form-event-properties.png){width="100%"}

1. 选择表单的所有事件和位于右上栏的&#x200B;**复制**。
1. 复制后，将显示&#x200B;**复制规则**&#x200B;弹出窗口，可在其中搜索具有项目ID的站点页面以粘贴表单规则。

   ![复制表单规则](/help/forms/assets/copy-form-rules.png){width="100%"}

1. 单击&#x200B;**复制**&#x200B;以将表单规则粘贴到站点页面。

#### 添加数据元素 {#data-elements}

1. 选择您的表单并添加位于右上角的&#x200B;**新属性**，或单击您的表单。
1. 在属性页面上，单击&#x200B;**数据元素**&#x200B;并为您的表单选择事件。
1. 选择表单的所有事件和位于右上栏的&#x200B;**复制**。
1. 复制后，将显示&#x200B;**复制规则**&#x200B;弹出窗口，可在其中搜索具有项目ID的站点页面以粘贴表单规则。
1. 单击&#x200B;**复制**&#x200B;以将表单规则粘贴到站点页面。

   ![表单数据元素](/help/forms/assets/form-data-elements.png){width="100%"}

通过上述步骤绑定表单和Sites规则后，执行以下步骤以在Sites页面中启用Analytics到自适应表单：

1. 单击左侧的&#x200B;**发布流**。
1. 单击&#x200B;**添加库**&#x200B;并输入您喜欢的名称。
1. 在右侧的&#x200B;**环境**&#x200B;下拉列表中，选择&#x200B;**开发**。
1. 单击&#x200B;**添加所有更改的资源**。
1. 单击&#x200B;**保存并生成到开发**。

![发布到开发](/help/forms/assets/publish-to-dev.png){width="100%"}


<!--

## Best Practices

1.    Verify that Adobe Analytics is enabled on all the forms activated for Adobe Analytics.

1.    Check the Adobe Analytics report periodically to gain insights into user behavior and form performance. For instance, you may set the cadence to 15 days or the period you prefer to choose for report analysis. This enables you to improve the forms enrollment experience.

1.    Enable Analytics for all or most of your forms for tracking and analyzing user interaction with your forms and to gain insights into visitor interactions and engagement.

1. Check your forms performance after you update your form fields or components.

1.    Share Analytics report with your peer groups for review, you can schedule your report for a later time.

-->

## 另请参阅 {#see-also}

* [查看并了解自适应Forms分析报表](/help/forms/view-understand-aem-forms-analytics-reports.md)
* [将自适应表单添加到 AEM Sites 页面或体验片段](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [将AEM Forms与Adobe Analytics集成](/help/forms/integrate-aem-forms-with-adobe-analytics.md)
