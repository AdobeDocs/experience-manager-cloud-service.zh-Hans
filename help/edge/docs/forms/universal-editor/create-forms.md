---
title: 使用Edge Delivery Services创建和发布自适应Forms
description: 关于使用AEM中的核心组件或Edge Delivery Services模板创建、创作和发布自适应Forms的分步说明，侧重于技术准确性和清晰度。
keywords: 自适应表单， edge delivery services，边缘交付服务，核心组件，通用编辑器，表单创建， AEM forms，模板选择，表单发布
feature: Edge Delivery Services
role: User, Developer
level: Beginner
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '1774'
ht-degree: 3%

---


# 使用Edge Delivery Services创建和发布自适应Forms

本文档提供了有关使用Edge Delivery Services在AEM中创建、配置和发布自适应Forms的说明。 其中涵盖核心组件和Edge Delivery Services模板。

在本指南结束时，您将学习如何：

- 为您的用例选择适当的模板类型
- 使用核心组件或Edge Delivery Services模板创建表单
- 使用正确的编辑器创作表单
- 配置表单并将其发布到Edge Delivery Services
- 访问已发布的表单并验证部署

## 模板选择

在开始之前，请确定哪种模板类型符合您的要求：

| 标准 | 核心组件模板 | Edge Delivery Services模板 |
|-------------------------|-----------------------------------------|-------------------------------------|
| 最适合 | 企业工作流，复杂的集成 | 高性能公共表单 |
| 编辑器 | 自适应表单编辑器 | 通用编辑器 |
| 发布 | AEM发布+ Edge Delivery Services | 仅限Edge Delivery Services |
| 复杂度 | 高级表单功能 | 简化、快速的表单 |
| 集成 | 完整的AEM生态系统 | 基于Git的开发 |
| 学习曲线 | AEM用户熟悉 | 现代、简化的方法 |

**决策指导：**

- 将&#x200B;**核心组件**&#x200B;用于复杂的工作流、深层AEM集成，或者利用现有AEM资源。
- 使用&#x200B;**Edge Delivery Services**&#x200B;实现高性能、简洁性和现代开发实践。

![模板选择决定](/help/edge/docs/forms/universal-editor/assets/template-selection-decision.svg)
*用于选择相应模板类型的决策流程图*

## 先决条件

在继续之前，请确保满足以下先决条件：

### 技术要求

- **AEM Forms as a Cloud Service**：具有Forms许可证的活动创作实例。
- **GitHub帐户**：用于存储库管理的个人或组织帐户。
- **存储库设置**：选择下列选项之一：
   - **新项目**： [创建具有自适应AEM块的新Forms项目](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)。 已为Edge Delivery Services预配置存储库。
   - **现有项目**： [将自适应Forms块添加到现有存储库](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)并更新配置。

### 环境配置

- **AEM-GitHub连接**： [在AEM实例和GitHub存储库之间建立连接](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)。
- **Edge Delivery Services**：确保存储库配置为自动部署。
- **权限**：验证您是否具有创建和发布表单所需的访问权限。

### 设置验证


1. 确认GitHub存储库包含自适应Forms块。
2. 测试AEM与GitHub存储库之间的连接。
3. 确保您可以将内容发布到Edge Delivery Services。



## 表单创建和发布工作流程

该过程包括三个主要阶段：

- **阶段1：**[模板选择和表单创建](#step-1-template-selection-and-form-creation)
- **阶段2：**[表单创作和设计](#step-2-form-authoring-and-design)
- **阶段3：** [配置和发布](#step-3-configuration-and-publishing)

每个阶段都包括验证步骤，以确认设置正确。

![三阶段工作流](/help/edge/docs/forms/universal-editor/assets/three-phase-workflow.svg)
*表单创建和发布的三个主要阶段概述*

### 步骤1：模板选择和表单创建

根据模板选择选择工作流：

>[!BEGINTABS]

>[!TAB Edge Delivery Services模板]

**用例：**&#x200B;高性能表单和现代开发工作流。

**功能：**&#x200B;通用编辑器创作和Edge Delivery Services发布。

#### 程序

1. **访问表单创建**
   - 登录到您的AEM Forms as a Cloud Service创作实例。
   - 导航到&#x200B;**Adobe Experience Manager** > **Forms** > **Forms和文档**。
   - 单击&#x200B;**创建** > **自适应Forms**。

1. **选择模板**
   - 在&#x200B;**Source**&#x200B;选项卡中，选择基于&#x200B;**Edge Delivery Services的模板**。
   - **创建**&#x200B;按钮变为启用状态。

     ![创建 EDS 表单](/help/edge/assets/create-eds-forms.png)

1. **配置选项（可选）**
   - **数据Source选项卡**：根据需要选择数据集成。
   - **提交选项卡**：选择提交操作（可以稍后配置）。
   - **传递选项卡**：设置发布/取消发布计划。

1. **完成表单设置**
   - 单击&#x200B;**创建**&#x200B;以打开表单创建向导。
   - 输入以下内容：
      - **名称**：内部标识符（无空格，使用连字符）。
      - **标题**：表单的显示名称。
      - **GitHub URL**：存储库URL （例如，`https://github.com/your-org/your-repo`）。

   ![创建表单向导](/help/edge/assets/create-form-wizard.png)

1. **验证**
   - 单击&#x200B;**创建**&#x200B;后，请验证：
      - 该表单将在通用编辑器中打开。
      - GitHub URL链接正确。
      - 组件面板可用。
      - 表单画布可见。

   ![通用编辑器界面](/help/edge/assets/author-form.png)

**结果：**&#x200B;表单已准备好在通用编辑器中创作。

>[!TAB 核心组件模板]

**用例：**&#x200B;企业工作流和复杂集成。

**功能：**&#x200B;自适应Forms编辑器创作、双重发布(AEM + Edge Delivery Services)、高级表单功能。

#### 程序

1. **访问表单创建**
   - 登录到您的AEM Forms as a Cloud Service创作实例。
   - 导航到&#x200B;**Adobe Experience Manager** > **Forms** > **Forms和文档**。
   - 单击&#x200B;**创建** > **自适应Forms**。

1. **选择模板和主题**
   - 在&#x200B;**Source**&#x200B;选项卡中，选择&#x200B;**基于核心组件的模板**。
   - 选择样式的&#x200B;**主题**。
   - **创建**&#x200B;按钮变为启用状态。

   ![核心组件模板选择](/help/forms/assets/core-component-based-template.png)

1. **配置选项（可选）**
   - **数据Source选项卡**：根据需要选择数据集成。
   - **提交选项卡**：选择提交操作（可以稍后配置）。
   - **传递选项卡**：设置发布/取消发布计划。

1. **完成表单设置**
   - 单击&#x200B;**创建**&#x200B;以打开表单创建向导。
   - 输入以下内容：
      - **名称**：内部标识符（无空格，使用连字符）。
      - **标题**：表单的显示名称。
      - **路径**： AEM存储库中的存储位置。

     ![创建表单向导](/help/forms/assets/create-cc-form.png)

1. **验证**
   - 单击&#x200B;**创建**&#x200B;后，请验证：
      - 该表单将在自适应Forms编辑器中打开。
      - 组件工具栏可用。
      - 属性面板可访问。
      - 应用主题样式。

     ![自适应表单编辑器](/help/forms/assets/af-editor-form.png)

**结果：**&#x200B;表单已准备好在自适应Forms编辑器中创作。

>[!ENDTABS]

### 第2步：表单创作和设计

创作体验因模板而异：

- **Edge Delivery Services模板**：通用编辑器
- **核心组件模板**：自适应Forms编辑器

![编辑器比较](/help/edge/docs/forms/universal-editor/assets/editor-comparison.svg)
*通用编辑器与自适应Forms编辑器功能的比较*

>[!BEGINTABS]

>[!TAB 通用编辑器(Edge Delivery Services)]

**界面：**&#x200B;针对性能进行了优化的现代简化编辑。

#### 添加表单组件

1. **访问组件库**
   - 在通用编辑器中打开内容浏览器。
   - 导航到内容树中的&#x200B;**自适应表单**&#x200B;组件。

   ![内容树导航](/help/edge/assets/content-tree.png)

1. **添加表单字段**
   - 单击&#x200B;**添加**&#x200B;图标以打开组件库。
   - 从&#x200B;**自适应表单组件**&#x200B;列表中选择组件。
   - 将组件拖放到表单画布上。

   ![添加组件](/help/edge/assets/add-component.png)

1. **设计表单**
   - 在属性面板中配置字段属性。
   - 设置验证规则和行为。
*s根据需要调整样式和布局。

   ![已填写注册表单](/help/edge/assets/contact-us.png)

#### 验证

- 所有必填字段都存在。
- 字段属性已正确配置。
- 布局响应灵敏且可访问。
- 验证规则按预期运行。

#### 后续步骤

- [配置提交操作](/help/edge/docs/forms/universal-editor/submit-action.md)以进行数据处理。
- 用于高级功能的[通用编辑器指南](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg)。

>[!TAB 自适应Forms编辑器（核心组件）]

**界面：**&#x200B;具有高级表单功能的全功能编辑。

#### 添加表单组件

1. **访问组件库**
   - 点击&#x200B;**将组件拖放至此**&#x200B;部分中的&#x200B;**插入组件**。

   ![组件插入区域](/help/forms/assets/drag-components-af-editor.png)

2. **添加表单字段**
   - 浏览&#x200B;**自适应表单组件**&#x200B;列表。
   - 将所需的组件拖到表单中。
   - 使用高级组件，例如面板、向导和数据集成。

   ![添加组件库](/help/forms/assets/add-component-af.png)

3. **设计表单**
   - 在属性面板中配置字段属性。
   - 设置复杂的验证规则和业务逻辑。
   - 应用主题和高级样式。

   ![已填写注册表单](/help/forms/assets/af-editor-form.png)

#### 验证

- 所有必填字段都存在。
- 配置复杂的验证规则。
- 应用主题样式。
- 数据集成按预期工作（如果适用）。

#### 后续步骤

- [为高级工作流配置提交操作](/help/forms/configure-submit-actions-core-components.md)。
- 用于企业功能的[核心组件指南](/help/forms/creating-adaptive-form-core-components.md)。

>[!ENDTABS]

### 步骤3：配置和发布

配置Edge Delivery Services并发布表单。 该流程因模板类型而异。

#### Edge Delivery Services配置

>[!BEGINTABS]
>[!TAB Edge Delivery Services模板（自动）]

**配置：**&#x200B;自动（无需手动设置）。

- GitHub存储库连接和Edge Delivery Services配置是在表单创建期间创建的。
- 发布端点会自动配置。

**验证：**

- 确认表单设置中显示配置。
- 确保GitHub URL链接正确。

![自动EDS配置](/help/edge/assets/aem-instance-eds-configuration.png)

>[!TAB 核心组件模板（手动）]

**配置：**&#x200B;需要手动安装。

#### 手动配置步骤

1. **访问配置工具**
   - 导航到&#x200B;**工具** > **云服务** > **Edge Delivery Services配置**。

   ![EDS配置访问权限](/help/edge/assets/select-eds-conf.png)

1. **创建配置**
   - 选择与表单名称匹配的文件夹（例如，`forms/enrollment-form`）。
   - 单击&#x200B;**创建** > **配置**。

   ![创建EDS配置](/help/forms/assets/create-eds-conf.png)

1. **配置属性**
   - 单击&#x200B;**Edge Delivery Services配置**。
   - 选择&#x200B;**属性**&#x200B;以打开配置对话框。

   ![配置属性](/help/forms/assets/eds-conf.png)

1. **设置参数**
   - **必需：**
      - **组织**： GitHub组织名称。
      - **站点名称**： GitHub存储库名称。
      - **分支**：分支名称（主名称留空）。
   - **可选：**
      - **Edge主机**：默认值（发布到.page和.live）。
      - **站点身份验证令牌**：用于安全身份验证（如果需要）。

1. **保存配置**
   - 单击&#x200B;**保存并关闭**。

#### 验证

- 配置创建成功。
- 正确指定GitHub组织和存储库。
- 分支设置与存储库结构匹配。
- 该表单将显示在配置文件夹中。

>[!ENDTABS]

#### 发布表单

>[!BEGINTABS]
>[!TAB 通用编辑器发布]

用于Edge Delivery Services模板的&#x200B;****

1. 在通用编辑器中，单击&#x200B;**发布**&#x200B;按钮（右上角）。
2. 在对话框中确认发布成功。
3. 请注意为暂存版本和实时版本生成的URL。

   ![通用编辑器发布](/help/edge/assets/publish-form.png)

- [发布指南](/help/edge/docs/forms/universal-editor/publish-forms.md)

>[!TAB 自适应Forms编辑器发布]

1. 在Experience Manager Forms控制台中，选择要发布的表单。
2. 单击工具栏中的&#x200B;**[!UICONTROL 发布]**。 查看要发布的参考资源。

![在自适应表单编辑器上发布表单](/help/forms/assets/publish-af-editor.png)

>[!NOTE]
>
> 有关详细信息，请参阅[在Experience Manager Forms中管理发布](/help/forms/manage-publication.md)。

>[!ENDTABS]

## 表单URL

可通过Edge Delivery Services URL访问发布的表单。

### URL结构

- **暂存（预览/测试）：**

  ```
  https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>
  ```

- **实时（生产）：**

  ```
  https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>
  ```

#### URL 参数

- `<branch>`： GitHub分支名称（例如，`main`，`develop`）
- `<repo>`： GitHub存储库名称（例如，`my-forms-project`）
- `<owner>`： GitHub组织或用户名（例如，`company-name`）
- `<form_name>`：在AEM中定义的表单标识符（例如，`contact-us`）

#### 示例

组织`contact-us`下的存储库`forms-project`中的表单`acme-corp`示例：

- **已暂存：** `https://main--forms-project--acme-corp.aem.page/content/forms/af/contact-us`
- **实时：**`https://main--forms-project--acme-corp.aem.live/content/forms/af/contact-us`

#### 环境差异

- **暂存(.page)：**&#x200B;测试的最新更改。
- **实时(.live)：**&#x200B;已发布用于生产的内容。

![URL结构](/help/edge/docs/forms/universal-editor/assets/url-structure.svg)
*Edge Delivery Services表单URL结构划分*

#### 可视化示例

**Edge Delivery Services模板：**

- 暂存： ![注册表单暂存版本](/help/forms/assets/registration-form-staged-version.png)
- 实时：![注册表实时版本](/help/forms/assets/registration-form-live-version.png)

**核心组件模板：**

- 暂存： ![注册表单暂存版本](/help/forms/assets/enrollment-form-staged-version.png)
- 实时：![注册表单实时版本](/help/forms/assets/enrollment-form-live-version.png)

## 疑难解答

以下是带有Edge Delivery Services的AEM Forms的常见问题和解决方案。

+++表单未加载

**问题：**&#x200B;表单URL返回404或空白页。

**分辨率：**

- 从URL中删除`.html`扩展名。
- 验证表单是否已发布。
- 查看GitHub存储库中的自适应Forms块。
- 确保表单名称与URL匹配（区分大小写）。

+++

+++配置问题

**问题：** Edge Delivery Services配置无法正常工作。

**分辨率：**

- 确保GitHub URL为`https://github.com/owner/repository`格式。
- 在配置中使用正确的分支名称。
- 验证存储库访问权限（公开或已验证）。
- 检查`fstab.yaml`以了解正确的GitHub详细信息。

+++

+++发布问题

**问题：**&#x200B;更改未出现在实时网站上。

**分辨率：**

- 等待2-3分钟以刷新CDN缓存。
- 确认发布工作流已完成。
- 首先在暂存(.page)环境中测试。
- 确保GitHub存储库已更新。

+++

+++通用编辑器问题

**问题：**&#x200B;无法编辑未加载的表单或组件。

**分辨率：**

- 使用支持的浏览器(Chrome、Firefox、Safari)。
- 清除浏览器缓存和Cookie。
- 检验网络连接。
- 确认作者权限。

+++

+++表单提交错误

**问题：**&#x200B;表单提交不起作用。

**分辨率：**

- 在表单属性中配置提交操作。
- 手动测试提交端点。
- 如果嵌入表单，请选中CORS设置。
- 验证是否已配置必填字段。

+++

+++性能问题

**问题：**&#x200B;表单加载缓慢或性能不佳。

**分辨率：**

- 优化图像。
- 删除不必要的组件。
- 利用Edge Delivery Services CDN。
- 最大程度地减少自定义JavaScript/CSS。

+++

+++获取帮助

如果问题仍然存在：

1. 检查Adobe Experience Cloud服务状态。
2. 查看[Edge Delivery Services文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/overview.html)。
3. 访问[Adobe Experience League社区](https://experienceleaguecommunities.adobe.com/)。
4. 联系Adobe客户关怀部门。

+++

## 后续步骤

完成表单创建和发布后，请考虑以下事项：

### 立即操作

- 使用本指南测试您的表单。
- 验证GitHub存储库和AEM连接。
- 查看示例表单。

### 高级主题

- [配置提交操作](/help/edge/docs/forms/universal-editor/submit-action.md)：设置数据处理和集成。
- [表单数据模型](/help/forms/create-form-data-models.md)：将表单连接到后端数据源。

### 性能优化

- [Edge Delivery Services最佳实践](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/overview.html)：最大化性能。
- [表单分析](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/analytics.html)：跟踪表单性能和用户行为。

