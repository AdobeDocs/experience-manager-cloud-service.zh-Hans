---
title: 使用 Edge Delivery Services 创建和发布自适应表单
description: 关于在 AEM 中使用 Edge Delivery Services 模板创建、创作和发布自适应表单的分步说明，重点关注技术准确性和清晰度。
keywords: 自适应表单，Edge Delivery Services，通用编辑器，表单创建，AEM 表单，表单发布
feature: Edge Delivery Services
role: User, Developer
level: Beginner
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: 07160248d5b5817d155a118475878ce04a687a32
workflow-type: ht
source-wordcount: '1005'
ht-degree: 100%

---


# 使用 Edge Delivery Services 创建和发布自适应表单

此文档分步详细介绍了如何使用 Edge Delivery Services 模板在 AEM 中创建、配置和发布自适应表单。它涵盖了从表单创建到生产部署的完整工作流。

本指南结束时，您将了解如何：

- 使用 Edge Delivery Services 模板创建表单
- 使用通用编辑器创作表单
- 配置表单并将其发布到 Edge Delivery Services
- 访问已发布的表单并验证部署



## 先决条件

在继续之前，请先确保满足以下先决条件：


- **AEM Forms as a Cloud Service**：具有 Forms 许可证的活跃的作者实例。
- **GitHub 帐户**：用于存储库管理的个人或组织帐户。
- **存储库设置**：选择以下方法之一：
   - **新项目**：[创建包含自适应表单块的新 AEM 项目](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)。存储库已为 Edge Delivery Services 预配置。
   - **现有项目**：[将自适应表单块添加到一个现有存储库](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)，然后更新配置。

- **AEM-GitHub 连接**：[连接](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)您的 AEM 实例与 GitHub 存储库。
- **Edge Delivery Services**：确保存储库已配置为自动部署。
- **权限**：验证您是否具有创建和发布表单所需的访问权限。

- 确认 GitHub 存储库包含自适应表单块。



## 表单创建和发布工作流

此过程包括三个主要阶段：

- **阶段 1：** [创建表单](#step-1-form-creation)
- **阶段 2：**[创作和设计表单](#step-2-form-authoring-and-design)
- **阶段 3：**[配置和发布](#step-3-configuration-and-publishing)

每个阶段都包括验证步骤，以确认设置正确。


### 步骤 1：创建表单

1. **访问表单创建**
   - 登录您的 AEM Forms as a Cloud Service 作者实例。
   - 导航至 **Adobe Experience Manager** > **表单** > **表单和文档**。
   - 点击&#x200B;**创建** > **自适应表单**。

1. **选择模板**
   - 在&#x200B;**源**&#x200B;选项卡中选择一个&#x200B;**基于 Edge Delivery Services 的模板**。
   - **创建**&#x200B;按钮变为启用状态。

     ![创建 EDS 表单](/help/edge/assets/create-eds-forms.png)

1. **配置选项（可选）**
   - **数据源选项卡**：需要时选择数据集成。
   - **提交选项卡**：选择一个提交操作（可稍后配置）。
   - **投放选项卡**：设置发布/取消发布的时间计划。

1. **完成表单设置**
   - 点击&#x200B;**创建**，打开表单创建向导。
   - 输入以下内容：
      - **名称**：内部标识符（无空格，使用连字符）。
      - **标题**：表单的显示名称。
      - **GitHub 存储库**：存储库 URL（例如 `https://github.com/your-org/your-repo`）。

   ![创建表单向导](/help/edge/assets/create-form-wizard.png)

1. **验证**
   - 点击&#x200B;**创建**&#x200B;后，验证：
      - 表单在通用编辑器中打开。
      - GitHub URL 已正确链接。
      - 组件面板可用。
      - 表单画布可见。

   ![通用编辑器用户界面](/help/edge/assets/author-form.png)

**结果：**&#x200B;表单已准备就绪，可在通用编辑器中进行创作。

### 步骤 2：创作和设计表单


1. **访问组件库**
   - 在通用编辑器中打开内容浏览器。
   - 导航到内容树中的&#x200B;**自适应表单**&#x200B;组件。

   ![内容树导航](/help/edge/assets/content-tree.png)

1. **添加表单字段**
   - 点击&#x200B;**添加**&#x200B;图标，打开组件库。
   - 从&#x200B;**自适应表单组件**&#x200B;列表中添加组件。
   - 将组件拖放到表单画布上。

   ![添加组件](/help/edge/assets/add-component.png)

1. **设计表单**
   - 在属性面板中配置字段属性。
   - 设置验证规则和行为。

   - 根据需要调整样式和布局。

   ![完成的注册表](/help/edge/assets/contact-us.png)

#### 验证

- 所有必填字段都显示出来。
- 正确配置了字段属性。
- 布局是响应式的，且可访问。
- 验证规则按预期运行。

#### 后续步骤

- 为数据处理[配置提交操作](/help/edge/docs/forms/universal-editor/submit-action.md)。
- [通用编辑器指南](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg)提供高级功能。

### 步骤 3：配置和发布

配置 Edge Delivery Services 并发布表单。

**配置：**&#x200B;自动（无需手动设置）。

- GitHub 存储库连接和 Edge Delivery Services 配置在表单创建过程中创建。
- 发布端点自动配置。

**验证：**

- 确认配置显示在表单的设置中。
- 确保 GitHub URL 正确链接。

![自动 EDS 配置](/help/edge/assets/aem-instance-eds-configuration.png)

#### 发布表单

1. 在通用编辑器中点击&#x200B;**发布**&#x200B;按钮（右上角）。
2. 在对话框中确认发布成功。
3. 请注意为暂存版本和上线版本生成的 URL。

   ![通用编辑器发布](/help/edge/assets/publish-form.png)

- [发布指南](/help/edge/docs/forms/universal-editor/publish-forms.md)

## 表单 URL

已发布的表单可通过 Edge Delivery Services URL 访问。

### URL 结构

- **暂存（预览/测试）：**

  ```
  https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>
  ```

- **上线（生产）：**

  ```
  https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>
  ```

#### URL 参数

- `<branch>`：GitHub 分支名称（例如 `main`，`develop`）
- `<repo>`：GitHub 存储库名称（例如 `my-forms-project`）
- `<owner>`：GitHub 组织或用户名（例如 `company-name`）
- `<form_name>`：AEM 中定义的表单标识符（例如 `contact-us`）

#### 示例

在组织 `acme-corp` 的存储库 `forms-project` 中的 `contact-us` 表单示例：

- **暂存：** `https://main--forms-project--acme-corp.aem.page/content/forms/af/contact-us`
- **上线：** `https://main--forms-project--acme-corp.aem.live/content/forms/af/contact-us`

#### 环境差异

- **暂存 (.page)：**&#x200B;用于测试的最新更改。
- **上线 (.live)：**&#x200B;用于生产的已发布内容。

![URL 结构](/help/edge/docs/forms/universal-editor/assets/url-structure.svg)
*Edge Delivery Services 表单 URL 结构细分*

#### 视觉示例

**Edge Delivery Services 模板：**

- 暂存：![注册表单暂存版本](/help/forms/assets/registration-form-staged-version.png)
- 上线：![注册表单上线版本](/help/forms/assets/registration-form-live-version.png)

## 疑难解答

以下是 AEM Forms 与 Edge Delivery Services 的常见问题和解决方法。

+++表单未加载

**问题：**&#x200B;表单 URL 返回 404 或空白页。

**解决方法：**

- 从 URL 中移除 `.html` 扩展名。
- 验证表单已发布。
- 检查 GitHub 存储库中的自适应表单块。
- 确保表单名称与 URL 匹配（区分大小写）。

+++

+++配置问题

**问题：** Edge Delivery Services 配置不起作用。

**解决方法：**

- 确保 GitHub URL 使用 `https://github.com/owner/repository` 格式。
- 在配置中使用正确的分支名称。
- 验证存储库访问权限（公共或经过身份验证）。
- 查看 `fstab.yaml`，获取正确的 GitHub 详细信息。

+++

+++发布问题

**问题：**&#x200B;上线网站上未显示更改。

**解决方法：**

- 等待 2-3 分钟，刷新 CDN 缓存。
- 确认发布工作流已完成。
- 首先在暂存（.page）环境中进行测试。
- 确保 GitHub 存储库已更新。

+++

+++通用编辑器问题

**问题：**&#x200B;无法编辑表单或组件未加载。

**解决方法：**

- 使用受支持的浏览器（Chrome、Firefox、Safari）。
- 清除浏览器缓存和 cookie。
- 验证网络连接。
- 确认作者权限。

+++

+++表单提交错误

**问题：**&#x200B;表单提交不起作用。

**解决方法：**

- 在表单属性中配置提交操作。
- 手动测试提交端点。
- 如果是嵌入表单，请检查 CORS 设置。
- 验证是否已配置必填字段。

+++

+++性能问题

**问题：**&#x200B;表单加载缓慢或性能低。

**解决方法：**

- 优化图像。
- 移除不必要的组件。
- 使用 Edge Delivery Services CDN。
- 将自定义 JavaScript/CSS 最小化。

+++

+++获取帮助 

如果问题仍然存在：

1. 检查 Adobe Experience Cloud 服务状态。
2. 查看 [Edge Delivery Services 文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/overview.html?lang=zh-Hans)。
3. 访问 [Adobe Experience League 社区](https://experienceleaguecommunities.adobe.com/)。
4. 联系 Adobe 客户关怀部门。

+++

## 后续步骤

完成表单创建和发布后，请考虑以下事项：

- [配置提交操作](/help/edge/docs/forms/universal-editor/submit-action.md)：设置数据处理和集成。
- [表单数据模型](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)：将表单与后端数据源连接。
- [Edge Delivery Services 最佳实践](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/overview.html?lang=zh-Hans)：最大限度提高性能。
- [表单分析](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/analytics.html)：跟踪表单性能和用户行为。

