---
title: 如何使用Forms Portal组件在Adobe Experience Manager Sites页面上列出表单？
description: 了解如何在AEM Sites页面上列出表单。
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: 58533d9a950fa4dc0e043ef8cb935d65fc68d233
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 1%

---


# 在站点页面上列出表单

想象一下，一位用户访问银行的网站搜索开户表格。 该银行使用Forms门户组件，通过输入特定关键词或按“新账户”或“个人银行”等类别进行过滤，帮助用户快速查找表单，并允许用户轻松找到所需表单，而无需滚动冗长的列表。

Forms Portal的&#x200B;**搜索和列表程序**&#x200B;组件允许您在Sites页面上显示和列出表单。 用户可以根据特定标准配置和提供全面的表单列表，以满足组织要求。 匿名用户可以访问Sites页面以查看和浏览可用表单。 使用位于屏幕右上角的&#x200B;**排序依据**&#x200B;下拉选项，可以按升序或降序对列出的表单进行排序。

![搜索和列表程序图标](assets/search-and-lister-component.png){width="250" align="center"}

## 先决条件

在探索Forms Portal组件的各种功能之前，请确保为您的环境启用了核心组件。 有关如何为您的环境启用核心组件的详细说明，请[单击此处](/help/forms/enable-adaptive-forms-core-components.md)。

<!--
## Enable Forms Portal components for your existing environment

To enable out-of-the-box Forms Portal components on existing AEM Forms as a Cloud Service, perform the following steps:

1. **Clone Cloud Manager Git repository on your local development instance:**  Your Cloud Manager Git repository contains a default AEM project. It is based on [AEM Archetype](https://github.com/adobe/aem-project-archetype/). Clone your Cloud Manager Git Repository using Self-Service Git Account Management from Cloud Manager UI to bring the project on your local development environment. For details on accessing the repository, see [Accessing Repositories](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/accessing-repos.html).  

1. **Create [!DNL Experience Manager Forms] as a [Cloud Service] project:** Create [!DNL Experience Manager Forms] as a [Cloud Service] project based on [AEM Archetype 50](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-50) or later. The archetype help developers easily start developing for [!DNL AEM Forms] as a Cloud Service. It also includes some sample themes and templates to help you started quickly.

    To create [!DNL Experience Manager Forms] as a Cloud Service project, open the command prompt and run the below command. To include [!DNL Forms] specific configurations, themes, and templates, set `includeForms=y`.  

    ```shell
    mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=30 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
    ```

    Also, change `appTitle`, `appId`, and `groupId`, in the above command to reflect your environment.

    After the project is ready, update the `<core.forms.components.version>x.y.z</core.forms.components.version>` property in the top-level `pom.xml` of the Archetype project to reflect the latest version of [core-forms-components](https://github.com/adobe/aem-core-forms-components) in your `AEM Archetype` project. 
 
1. **Deploy the project to your local development environment:** You can use the following command to deploy to your local development environment

    `mvn -PautoInstallPackage clean install`

    For the complete list of commands, see [Building and Installing](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#building-and-installing)

1. [Deploy the archetype to your [!DNL AEM Forms] as a Cloud Service environment](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html#embeddeds). -->

将最新的核心组件部署到环境后，即可在创作环境中访问Forms Portal组件。

## 在站点页面上列出表单

要将&#x200B;**Search &amp; Lister**&#x200B;门户组件添加到站点页面，请执行以下步骤：

1. 以&#x200B;**编辑**&#x200B;模式打开AEM Sites页面。
1. 转到&#x200B;**[!UICONTROL 页面信息]** > **[!UICONTROL 编辑模板]**
   ![编辑模板策略](/help/forms/assets/save-form-as-draft-edit-template.png){width="250" align="center"}

1. 单击&#x200B;**[!UICONTROL 策略]**&#x200B;并选择&#x200B;**[AEM原型项目名称] - Forms和通信门户**&#x200B;下的&#x200B;**[!UICONTROL 搜索和列表程序]**&#x200B;复选框。

   ![策略选择](/help/forms/assets/search-lister-enable-policy.png){width="250" align="center"}

1. 单击&#x200B;**[!UICONTROL 完成]**。
1. 现在，在创作模式下重新打开AEM Sites页面。
1. 在页面编辑器中找到用于添加Forms Portal组件的部分。

1. 单击&#x200B;**添加**&#x200B;图标。 图标是一个加号(+)，表示添加新组件的选项。

   单击&#x200B;**添加**&#x200B;图标会显示&#x200B;**插入新组件**&#x200B;对话框，其中显示了要插入的各种组件。

   >[!NOTE]
   >
   > 或者，您也可以拖放组件。

1. 浏览对话框中的可用组件，并从列表中选择所需的组件。 例如，从列表中选择&#x200B;**搜索和列表程序**&#x200B;组件以添加&#x200B;**搜索和列表程序** Forms门户组件。

   ![搜索和列表程序组件](/help/forms/assets/add-search-lister.png){width="250" align="center"}

现在，配置&#x200B;**Search and Lister**&#x200B;组件的属性。

## 了解“搜索和列表程序”组件的属性

您可以使用“配置”对话框轻松自定义&#x200B;**搜索和列表程序**&#x200B;组件属性，以获得无缝的用户体验。 要配置，请选择该组件，然后选择![配置图标](assets/configure_icon.png)。 **[!UICONTROL 搜索和列表程序]**&#x200B;对话框打开。

### “显示”选项卡

![显示选项卡](/help/forms/assets/search-and-lister-display-tab.png){width="250" align="center"}

1. 在&#x200B;**[!UICONTROL Title]**&#x200B;中，指定Search &amp; Lister组件的标题。 指示性标题使用户能够在表单列表中执行快速搜索。
1. 从&#x200B;**[!UICONTROL 布局]**&#x200B;列表中，选择以卡片或列表格式表示表单的布局。
1. 选择&#x200B;**[!UICONTROL 隐藏搜索]**&#x200B;和&#x200B;**[!UICONTROL 隐藏排序]**&#x200B;以隐藏搜索并按功能排序。
1. 在&#x200B;**[!UICONTROL 工具提示]**&#x200B;中，提供将鼠标悬停在该组件上时显示的工具提示。

### “资源”选项卡

![资产选项卡](/help/forms/assets/search-and-lister-asset-tab.png){width="250" align="center"}

1. 在&#x200B;**[!UICONTROL 资产文件夹]**&#x200B;选项卡中，指定从何处提取表单并将其列在页面上。
1. 使用&#x200B;**[!UICONTROL 添加其他位置]**，您可以配置多个文件夹位置。

### “结果”选项卡

![显示选项卡](/help/forms/assets/search-and-lister-result-tab.png){width="250" align="center"}

在&#x200B;**[!UICONTROL 结果]**&#x200B;选项卡中，配置每页显示的最大表单数。 默认设置是每页八个表单。

## 使用搜索和列表程序组件在“站点”页面上查看表单

要查看表单列表，请使用&#x200B;**Search &amp; Lister** Forms门户组件。 预览AEM Sites页面以查看屏幕上显示的&#x200B;**Assets**&#x200B;文件夹中的表单列表。 您还可以使用搜索栏搜索特定表单。

![搜索和列表程序图标](assets/search-and-lister-component.png){width="250" align="center"}

<!--
## Configure Azure Storage for Adaptive Forms {#configure-azure-storage-adaptive-forms}

[[!DNL Experience Manager Forms] Data Integration](data-integration.md) provides [!DNL Azure] storage configuration to integrate forms with [!DNL Azure] storage services. The Form Data Model (FDM) can be used to create Adaptive Forms that interact with [!DNL Azure] server to enable business workflows.

### Create Azure Storage Configuration {#create-azure-storage-configuration}

Before executing these steps, ensure that you have an Azure storage account and an access key to authorize access to the [!DNL Azure] storage account.

1. Navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Cloud Services]** &gt; **[!UICONTROL Azure Storage]**.
1. Select a folder to create the configuration and select **[!UICONTROL Create]**.
1. Specify a title for the configuration in the **[!UICONTROL Title]** field.
1. Specify the name of the [!DNL Azure] storage account in the **[!UICONTROL Azure Storage Account]** field.

### Configure Unified Storage Connector for Forms Portal {#configure-usc-forms-portal}

Perform the following steps to configure Unified Storage Connector for AEM Workflows:

1. Navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Forms]** &gt; **[!UICONTROL Unified Storage Connector]**.
1. In the **[!UICONTROL Forms Portal]** section, select **[!UICONTROL Azure]** from the **[!UICONTROL Storage]** drop-down list.
1. Specify the [configuration path for the Azure storage configuration](#create-azure-storage-configuration) in the **[!UICONTROL Storage Configuration Path]** field.
1. Select **[!UICONTROL Publish]** and then select **[!UICONTROL Save]** to save the configuration.

## Enable Forms Portal Components {#enable-forms-portal-components}

To use any core component (including the out-of-the-box portal components) in an Adobe Experience Manager (AEM) site, you must create a proxy component and enable it for your site. For creating a proxy component and enabling portal components, see [Using Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html?lang=en#create-proxy-components). 

Once a portal component is enabled, you can use it in the author instance of your sites page.

## Add and Configure Forms Portal Components {#configure-forms-portal-components}

You can create and customize Forms Portal on websites authored using AEM by adding and configuring the portal components. Ensure that the [components are enabled](#enable-forms-portal-components) before using them in the Forms Portal.

To add a component, either drag and drop the component from the Components pane to the layout container on the page, or select the add icon on the layout container and add the component from the [!UICONTROL Insert New Component] dialog.

### Configure Drafts & Submissions Component {#configure-drafts-submissions-component}

The Drafts & Submissions component displays forms that are saved as draft for completing later and submitted forms. To configure, select the component and then select the ![Configure icon](assets/configure_icon.png). In the [!UICONTROL Drafts and Submissions] dialog, specify the title to indicate the form listing as draft or submitted forms. Also select whether the component should list draft forms or submitted forms in card or list format.

![Drafts icon](assets/drafts-component.png)

![Submissions icon](assets/submission-listing.png)

### Configure Search & Lister Component {#configure-search-lister-component}

The Search & Lister component is used to list adaptive forms on a page and to implement search on the listed forms. 

![Search and Lister icon](assets/search-and-lister-component.png)

To configure, select the component and then select the ![Configure icon](assets/configure_icon.png). The [!UICONTROL Search and Lister] dialog opens.

1. In the [!UICONTROL Display] tab, configure the following:
    * In **[!UICONTROL Title]**, specify the title for the Search & Lister component. An indicative title enables the users perform quick search across the list of forms.
    * From the **[!UICONTROL Layout]** list, select the layout to represent the forms in card or list format.
    * Select **[!UICONTROL Hide Search]** and **[!UICONTROL Hide Sorting]** to hide the search and sort by features.
    * In **[!UICONTROL Tooltip]**, provide the tooltip that appears when you hover over the component. 
1. In the [!UICONTROL Asset Folder] tab, specify the location from where the forms are pulled and listed on the page. You can configure multiple folder locations.
1. In the [!UICONTROL Results] tab, configure the maximum number of forms to display per page. The default is eight forms per page.

### Configure Link Component {#configure-link-component}

The link component enables you to provide links to an adaptive form on the page. To configure, select the component and then select the ![Configure icon](assets/configure_icon.png). The [!UICONTROL Edit Link Component] dialog opens.

1. In the [!UICONTROL Display] tab, provide the link caption and tooltip to ease identification of the forms represented by the link.
1. In the [!UICONTROL Asset Info] tab, specify the repository path where the asset is stored. 
1. In the [!UICONTROL Query Params] tab, specify the additional parameters in the key-value pair format. When the link is clicked, these additional parameters and passed along with the form.

## Configure Asynchronous Form Submission Using Adobe Sign {#configure-asynchronous-form-submission-using-adobe-sign}

You can configure to submit an adaptive form only when all the recipients have completed the signing ceremony. Follow the steps below to configure the setting using Adobe Sign.

1. In the author instance, open an Adaptive Form in the edit mode.
1. From the left pane, select the Properties icon and expand the **[!UICONTROL ELECTRONIC SIGNTATURE]** option.
1. Select **[!UICONTROL Enable Adobe Sign]**. Various configuration options display. 
1. In the [!UICONTROL Submit the form] section, select the **[!UICONTROL after every recipient completes signing ceremony]** option to configure the Submit Form action, where the form is first sent to all the recipients for signing. Once all the recipients have signed the form, only then the form is submitted. 

## Save Adaptive Forms As Drafts {#save-adaptive-forms-as-drafts}

You can save forms as Drafts for completing them later. There are two ways in which a form is saved as a draft:

* Create a "Save Form" rule on a form component, for example, a button. On clicking the button, the rule triggers and the form are saved a draft.
* Enable Auto-Save feature, which saves the form as per the specified event or after a configured interval of time.

### Create Rules to Save an Adaptive Form as Draft {#rule-to-save-adaptive-form-as-draft}

To create a "Save Form" rule on a form component, for example, a button, follow the steps below:

1. In the author instance, open an Adaptive Form in edit mode.
1. From the left pane, select ![Components icon](assets/components_icon.png) and drag the [!UICONTROL Button] component to the form.
1. Select the [!UICONTROL Button] component and then select the ![Configure icon](assets/configure_icon.png). 
1. Select the [!UICONTROL Edit Rules] icon to open the Rule Editor. 
1. Select **[!UICONTROL Create]** to configure and create the rule.
1. In the [!UICONTROL When] section, select "is clicked" and in the [!UICONTROL Then] section, select the "Save Form" options.
1. Select **[!UICONTROL Done]** to save the rule.

### Enable Auto-save {#enable-auto-save}

You can configure the auto-save feature for an adaptive form as follows:

1. In the author instance, open an Adaptive Form in edit mode.
1. From the left pane, select the ![Properties icon](assets/configure_icon.png) and expand the [!UICONTROL AUTO-SAVE] option.
1. Select the **[!UICONTROL Enable]** check box to enable auto-save of the form. You can configure the following:
* By default, the [!UICONTROL Adaptive Form Event] is set to "true", which implies that the form is auto-saved after every event.
* In [!UICONTROL Trigger], configure to trigger auto-save based on the occurrence of an event or after a specific interval of time.
-->


## 后续步骤

在下一篇文章中，让我们了解如何将[表单另存为草稿，并使用Forms门户组件](/help/forms/save-core-component-based-form-as-draft.md)在站点页面上将其列出。

## 相关文章

{{forms-portal-see-also}}

## 另请参阅 {#see-also}

{{see-also}}