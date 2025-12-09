---
title: 交互式通信(IC)编辑器入门
description: 交互式通信允许组织设计和提供个性化、数据驱动的通信。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: d24e88b545a17e50c1e80e1aedbb1d0adf55f609
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 11%

---


# 交互式通信(IC)编辑器入门

>[!NOTE]
>
> 交互式通信功能在早期采用者计划下提供。 请从您的工作地址发送电子邮件至 `aem-forms-ea@adobe.com`，以申请访问权限。

>[!IMPORTANT]
>
> **文档可能会发生变化**：此提示词库目前正在针对产品进行测试，因此可能会进行更新和修订。随着 Forms Experience Builder 在早期采用者计划期间不断改进，提示词、示例和最佳实践可能会发生变化。

Adobe Experience Manager (AEM) Forms中的&#x200B;**交互式通信(IC)编辑器**&#x200B;允许组织跨数字和打印渠道设计和提供个性化的数据驱动通信，例如报表、发票和信件。 本指南概述了如何入门 — 从入门到导航IC编辑器界面。


## 登录和访问

### 满足访问权限要求

要使用交互式通信，请确保您的AEM Forms as a Cloud Service环境包含&#x200B;**AEM Forms加载项**，并且您的帐户具有适当的权限。

### 验证浏览器

要了解受支持的浏览器和客户端平台，请按照链接文章[受支持的客户端平台](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/overview/supported-platforms)进行操作

>[!NOTE]
>
> **支持发布周期较快的浏览器：**
> Firefox、Chrome 和 Edge 定期发布更新。Adobe 致力于对这些浏览器即将推出的版本保持上述支持级别。

### 配置用户角色和权限

对IC编辑器功能的访问由AEM[中的](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions)用户角色控制。 以下是创建和管理交互式通信时涉及的关键角色：

| **角色** | **描述** | **密钥权限** |
| --------------------- | ---------------------------------------------------------- | -------------------------------------------- |
| **表单作者** | 创建和编辑交互式通信。 | 创建、编辑、预览和发布集成电路。 |
| **模板作者** | 为交互式通信设计可重用模板。 | 创建和锁定模板，定义布局。 |
| **管理员** | 管理用户访问、权限和配置。 | 分配角色、管理模板和发布IC。 |
| **FDM作者** | [创建和管理表单数据模型(FDM)](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/create-form-data-models)以进行数据集成。 | 创建、编辑和配置数据源和模型。 |

>[!NOTE]
>
> 确保用户属于相应的AEM组（例如，`forms-user`、`fdm-author`、`template-authors`）以访问相应的功能。

## 访问集成电路编辑器

1. 登录到您的&#x200B;**AEM Forms as a Cloud Service**&#x200B;实例。
2. 导航到&#x200B;**Forms >交互式通信**。
3. 单击&#x200B;**创建** → **交互式通信**。
4. 选择&#x200B;**模板**，配置数据源，然后单击&#x200B;**创建**&#x200B;以打开&#x200B;**交互式通信编辑器**。

该编辑器提供了一个统一的环境，用于设计、预览和管理通信的打印版本和Web版本。

## 导航界面

**交互式通信编辑器**&#x200B;界面旨在让作者直观地访问所有设计工具和配置选项。

![查找IC文档](/help/forms/interactive-communication/assets/navigate-the-interface.png)

### 1.顶部工具栏

![查找IC文档](/help/forms/interactive-communication/assets/tool-bar.png)

**位置：**&#x200B;最顶部部分

**用途：**&#x200B;提供环境访问和全局操作。

**包括：**

显示&#x200B;**Adobe Experience Cloud环境**（例如，暂存），以及用于管理用户设置和环境访问权限的&#x200B;**项目标题**、**Beta反馈**、**通知**&#x200B;和&#x200B;**配置文件控件**。

### 2.选项卡栏（设计/主选项卡和文件控件）

![查找IC文档](/help/forms/interactive-communication/assets/tab-bar.png)

**位置：**&#x200B;在顶部标题下

**目的：**&#x200B;管理视图和通信文件。

**包括：**

**选项卡：**&#x200B;在&#x200B;**设计视图**&#x200B;和&#x200B;**母版页视图**&#x200B;之间切换以进行布局和可重用的元素设计

**文件名：**&#x200B;显示当前通信的标题（如ic-11）

**查看控件：**&#x200B;选项，如规则、创建、缩放(85%)、撤消/重做、删除、PDF预览和保存

### 3.左侧面板（导航和组件工具）

![查找IC文档](/help/forms/interactive-communication/assets/left-panel.png)

**位置：**&#x200B;界面的左侧

**用途：**&#x200B;访问项目结构、可重用资源和数据绑定。

**包括：**

* **主页：**&#x200B;将用户转到交互式通信(IC)主屏幕，您可以在其中查看和管理现有IC和文件夹。

* **菜单面板：**&#x200B;显示与视图相关的选项，如“标尺”、“对象边界”、“对齐网格”、“对齐功能对象”和“导入XDP功能”。

* **层次结构视图：**&#x200B;显示通信的组件结构，显示页面、面板和子表单的组织。

* **组件库：**&#x200B;包含可以拖到画布上的设计元素，如文本、图像、子表单和条形码。

* **片段：**&#x200B;允许在多个通信中重复使用预定义的设计和内容块。

* **数据模型：**&#x200B;将通信连接到基础表单数据模型(FDM)以绑定动态数据。

### 4.中Workspace（设计画布）

![查找IC文档](/help/forms/interactive-communication/assets/canvas.png)

**位置：**&#x200B;接口中心

**目的：**&#x200B;用于设计交互式通信的主工作区。

**功能：**

* 从库中拖放组件

* 排列可视布局并设置其格式

* 添加或编辑页面、子表单和字段

* 使用左下角的控件在页面之间导航（例如“1/1”）

* 发布前预览最终布局

### 5.右侧面板（“属性”面板）

![查找IC文档](/help/forms/interactive-communication/assets/right-panel.png)

**位置：**&#x200B;屏幕右侧

**用途：**&#x200B;自定义组件行为和样式。

**包括：**

* 常规设置（名称、类型、流动/定位）

* 布局和外观选项

* 分页、位置、存在和数据绑定控件