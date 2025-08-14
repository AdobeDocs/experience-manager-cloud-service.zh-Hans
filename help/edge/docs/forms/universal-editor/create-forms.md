---
title: 使用Edge Delivery Services创建和发布自适应Forms
description: 关于使用AEM中的Edge Delivery Services模板创建、创作和发布自适应Forms的分步说明，侧重于技术准确性和清晰度。
keywords: 自适应表单， edge delivery services，通用编辑器，表单创建， AEM forms，表单发布
feature: Edge Delivery Services
role: User, Developer
level: Beginner
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: 07160248d5b5817d155a118475878ce04a687a32
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 1%

---


# 使用Edge Delivery Services创建和发布自适应Forms

本文档提供了使用AEM中的Edge Delivery Services模板创建、配置和发布自适应Forms的分步说明。 它涵盖了从表单创建到生产部署的完整工作流。

在本指南结束时，您将学习如何：

- 使用Edge Delivery Services模板创建表单
- 使用通用编辑器创作表单
- 配置表单并将其发布到Edge Delivery Services
- 访问已发布的表单并验证部署



## 先决条件

在继续之前，请确保满足以下先决条件：


- **AEM Forms as a Cloud Service**：具有Forms许可证的活动创作实例。
- **GitHub帐户**：用于存储库管理的个人或组织帐户。
- **存储库设置**：选择下列选项之一：
   - **新项目**： [创建具有自适应AEM块的新Forms项目](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)。 已为Edge Delivery Services预配置存储库。
   - **现有项目**： [将自适应Forms块添加到现有存储库](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)并更新配置。

- **AEM-GitHub连接**： [在AEM实例和GitHub存储库之间建立连接](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)。
- **Edge Delivery Services**：确保存储库配置为自动部署。
- **权限**：验证您是否具有创建和发布表单所需的访问权限。

- 确认GitHub存储库包含自适应Forms块。



## 表单创建和发布工作流程

该过程包括三个主要阶段：

- **阶段1：** [表单创建](#step-1-form-creation)
- **阶段2：**&#x200B;[表单创作和设计](#step-2-form-authoring-and-design)
- **阶段3：** [配置和发布](#step-3-configuration-and-publishing)

每个阶段都包括验证步骤，以确认设置正确。


### 步骤1：创建表单

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

### 第2步：表单创作和设计


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
   - 根据需要调整样式和布局。

   ![已填写注册表单](/help/edge/assets/contact-us.png)

#### 验证

- 所有必填字段都存在。
- 字段属性已正确配置。
- 布局响应灵敏且可访问。
- 验证规则按预期运行。

#### 后续步骤

- [配置提交操作](/help/edge/docs/forms/universal-editor/submit-action.md)以进行数据处理。
- 用于高级功能的[通用编辑器指南](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg)。

### 步骤3：配置和发布

配置Edge Delivery Services并发布表单。

**配置：**&#x200B;自动（无需手动设置）。

- GitHub存储库连接和Edge Delivery Services配置是在表单创建期间创建的。
- 发布端点会自动配置。

**验证：**

- 确认表单设置中显示配置。
- 确保GitHub URL链接正确。

![自动EDS配置](/help/edge/assets/aem-instance-eds-configuration.png)

#### 发布表单

1. 在通用编辑器中，单击&#x200B;**发布**&#x200B;按钮（右上角）。
2. 在对话框中确认发布成功。
3. 请注意为暂存版本和实时版本生成的URL。

   ![通用编辑器发布](/help/edge/assets/publish-form.png)

- [发布指南](/help/edge/docs/forms/universal-editor/publish-forms.md)

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

- [配置提交操作](/help/edge/docs/forms/universal-editor/submit-action.md)：设置数据处理和集成。
- [表单数据模型](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)：将表单连接到后端数据源。
- [Edge Delivery Services最佳实践](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/overview.html)：最大化性能。
- [表单分析](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/analytics.html)：跟踪表单性能和用户行为。

