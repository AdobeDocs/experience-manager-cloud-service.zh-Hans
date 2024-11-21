---
Title: How to configure Marketo Engage data for Adaptive Forms?
Description: Learn how to use Marketo Engage schema in Adaptive Forms.
Keywords: Use Marketo Engage data source in Adaptive Forms, How to connect a Marketo instance data source with form? , Connect a form to Marketo.
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
source-git-commit: 681c194f997ab66f93beedad4eea273614e6797d
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 6%

---


# 为现有的自适应Forms配置Marketo Engage数据源

<span class="preview">该功能在早期采用者计划下可用。 您可以使用官方电子邮件 ID 写信给 aem-forms-ea@adobe.com，加入早期采用者计划并申请使用该功能。</span>

![工作流](/help/forms/assets/workflow-marketo-2.png)

在创建云服务配置以将Marketo Engage与现有AEM Forms集成后，您可以为表单配置数据源。

通过配置数据集成，用户可连接到各种数据源或架构。 与Marketo Engage数据源集成并在不同表单中使用它有助于对该数据进行操作。 要探索自适应表单支持的现成数据源，请参阅[配置数据源](/help/forms/configure-data-sources.md)文章。

## 为表单配置Marketo Engage数据源的注意事项

为表单配置Marketo Engage数据源时的注意事项如下：

* 无法将Edge Delivery ServicesForms与Marketo Engage连接。

## 将Marketo Engage数据源用于表单的先决条件

将Marketo Engage数据源用于表单的先决条件：

* 创建[云服务配置以将Marketo Engage与表单](/help/forms/integrate-form-to-marketo-engage.md)集成。

## 如何为Marketo Engage数据源配置现有自适应表单？

要使用Marketo Engage数据源配置自适应表单，请执行以下步骤：
1. 登录到您的[!DNL Experience Manager Forms]创作实例。

1. 打开自适应表单进行编辑。
1. 打开内容树并选择&#x200B;**[!UICONTROL 指南容器]**。
1. 单击自适应表单容器属性![自适应表单容器属性](/help/forms/assets/configure-icon.svg)图标。 将打开用于配置数据源的自适应表单容器对话框。
1. 打开&#x200B;**[!UICONTROL 数据模型]**&#x200B;选项卡并选择表单模型作为&#x200B;**连接器**。
1. 从下拉列表中选择&#x200B;**[!UICONTROL 连接器]**。

1. 选择&#x200B;**[!UICONTROL 连接器]**&#x200B;后，您可以选择云配置。

   ![选择Marketo连接器](/help/forms/assets/select-marketo-connector.png)

   根据所选Marketo Engage配置，表单元素将显示在侧边栏中&#x200B;**[!UICONTROL 内容浏览器]**&#x200B;的&#x200B;**[!UICONTROL 数据模型对象]**&#x200B;选项卡中。 您可以拖放这些元素来构建自适应表单。

   ![Marketo Data Source](/help/forms/assets/marketo-engage-data-source.png)

1. 单击&#x200B;**[!UICONTROL 完成]**。

或者，您也可以编辑自适应表单属性以更改其关联配置。

自适应表单现在使用连接的Marketo Engage实例的数据源进行配置。 现在，将其配置为将数据发送到Adobe Marketo Engage。

## 常见问题解答(FAQ)

**问：更改表单的连接器时会出现什么情况？**\
**A：**&#x200B;如果更改表单的连接器，则现有绑定将无效。

**问：对于与Marketo Engage集成的表单，在规则编辑器的调用服务中可用的三项操作是什么？**\
**A：**&#x200B;在与Marketo Engage集成的&#x200B;**调用服务**&#x200B;中可用的三个现成操作是：
* 同步潜在客户
* 按ID获取潜在客户
* 按筛选器类型获取潜在客户

## 下一步

现在，您已为自适应Forms配置了Marketo Engage数据源。 接下来，您可以[配置自适应表单以将数据发送到Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)。

## 相关文章

{{af-submit-action}}

## 另请参阅

{{marketo-engage-see-also}}


