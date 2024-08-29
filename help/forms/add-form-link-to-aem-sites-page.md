---
title: 如何使用链接Forms Portal组件在AEM Sites页面上添加表单链接？
description: 了解如何将表单链接添加到AEM Sites页面。
feature: Adaptive Forms, Core Components
role: User, Developer, Admin
source-git-commit: 58533d9a950fa4dc0e043ef8cb935d65fc68d233
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 1%

---


# 将表单链接添加到站点页面

在银行网站方案中，**链接** Forms Portal组件通过引导用户访问网站各个部分的特定表单来增强导航。 它在整个网站中战略性地直接引用各种表单，如贷款申请、开户表单或反馈调查。 **Link**&#x200B;组件插入的链接可将用户指引到站点页面中的特定自适应Forms。 例如，在银行的网站上，匿名用户可以访问一般查询表单，而登录用户可以直接访问更安全的表单，如贷款申请或交易授权表单。

![链接图标](/help/forms/assets/link-forms.png){width="250" align="center"}

## 先决条件

在探索Forms Portal组件的各种功能之前，请确保为您的环境启用了核心组件。 有关如何为您的环境启用核心组件的详细说明，请[单击此处](/help/forms/enable-adaptive-forms-core-components.md)。

将最新的核心组件部署到环境后，即可在创作环境中访问Forms Portal组件。

## 将链接组件添加到您的站点页面

要将&#x200B;**Link**&#x200B;门户组件添加到您的站点页面，请执行以下步骤：

1. 以&#x200B;**编辑**&#x200B;模式打开AEM Sites页面。
1. 转到&#x200B;**[!UICONTROL 页面信息]** > **[!UICONTROL 编辑模板]**
   ![编辑模板策略](/help/forms/assets/save-form-as-draft-edit-template.png){width="250" align="center"}

1. 单击&#x200B;**[!UICONTROL 策略]**&#x200B;并选择&#x200B;**[AEM原型项目名称] - Forms和通信门户**&#x200B;下的&#x200B;**[!UICONTROL 链接]**&#x200B;复选框。

   ![策略选择](/help/forms/assets/add-link.png){width="250" align="center"}

1. 单击&#x200B;**[!UICONTROL 完成]**。
1. 现在，在创作模式下重新打开AEM Sites页面。
1. 在页面编辑器中找到用于添加Forms Portal组件的部分。

1. 单击&#x200B;**添加**&#x200B;图标。 图标是一个加号(+)，表示添加新组件的选项。

   单击&#x200B;**添加**&#x200B;图标会显示&#x200B;**插入新组件**&#x200B;对话框，其中显示了要插入的各种组件。

   >[!NOTE]
   >
   > 或者，您也可以拖放组件。

1. 浏览对话框中的可用组件，并从列表中选择所需的组件。 例如，从列表中选择&#x200B;**Link**&#x200B;组件以添加&#x200B;**Link** Forms门户组件。

   ![链接组件](/help/forms/assets/add-link-in-sites.png){width="250" align="center"}

现在，配置&#x200B;**Link**&#x200B;组件的属性。

## 了解链接组件的属性

您可以使用“配置”对话框轻松自定义&#x200B;**链接**&#x200B;组件属性，以获得无缝的用户体验。 要配置，请选择该组件，然后选择![配置图标](assets/configure_icon.png)。 **[!UICONTROL 链接]**&#x200B;对话框打开。

### “显示”选项卡

![显示选项卡](/help/forms/assets/link-asset-tab.png){width="250" align="center"}

在&#x200B;**[!UICONTROL 显示]**&#x200B;选项卡中，提供链接标题和工具提示，以便于识别链接所表示的表单。

### 资源信息选项卡

![Assets信息选项卡](/help/forms/assets/link-asset-info.png){width="250" align="center"}

在&#x200B;**[!UICONTROL 资源信息]**&#x200B;选项卡中，指定存储资源的存储库路径。

### “查询参数”选项卡

![查询参数选项卡](/help/forms/assets/link-query-tab.png){width="250" align="center"}

在&#x200B;**[!UICONTROL 查询参数]**&#x200B;选项卡中，以键值对格式指定其他参数。 单击链接时，这些附加参数将与表单一起传递。

## 使用链接组件在“站点”页面上查看表单链接

预览“站点”页面以查看指向自适应表单的链接，该表单在&#x200B;**Link**&#x200B;组件的&#x200B;**Assets信息**&#x200B;属性选项卡中指定。 单击该链接会在屏幕上向用户显示表单，用户随后可以根据权限访问该表单。

![查询参数选项卡](/help/forms/assets/link-forms.png){width="250" align="center"}

## 相关文章

{{forms-portal-see-also}}

## 另请参阅 {#see-also}

{{see-also}}
