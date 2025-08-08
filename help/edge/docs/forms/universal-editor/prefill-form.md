---
title: 如何预填自适应表单字段
description: 使用现有数据预填自适应表单的字段。 用户可通过使用其社交个人资料登录在表单中预填基本信息。
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
level: Beginner, Intermediate
time: 45-60 minutes
keywords: 预填自适应表单、自适应表单边缘交付服务、自适应表单自动填写
source-git-commit: f843a7c91c3d47610580a3787a96e7e3bd49ba09
workflow-type: tm+mt
source-wordcount: '1829'
ht-degree: 3%

---

# 使用Edge Delivery Services在自适应Forms中配置预填充服务

表单预填充是在用户打开表单后立即使用外部源的相关数据自动填充表单字段的过程。 利用来自用户配置文件、数据库、保存的草稿或其他后端系统的信息，预填充可简化表单填充体验 — 减少手动输入，最大程度地减少错误，并加快完成过程。 这不仅会提高用户满意度，还会增加成功提交表单的可能性。

## 表单预填的好处

| 收益 | 描述 |
|---------|-------------|
| 更快地完成&#x200B;**&#x200B;** | 减少手动数据输入，帮助用户快速完成表单 |
| **已改进的用户体验** | Forms更加个性化和方便，对于回头用户来说更是如此 |
| **更高的转化率** | 通过最大程度地减少所需的用户工作量来减少表单放弃 |
| **减少输入错误** | 来自可靠来源的数据可减少拼写错误和不正确条目 |
| **更好的数据质量** | 确保后端系统的结构化、准确和一致的数据 |

## 预填充的工作方式

下图说明了用户打开自适应表单时发生的自动预填充过程：

![表单预填流程](/help/edge/docs/forms/universal-editor/assets/prefill-process-flow.svg)

预填充过程包括四个关键步骤：

1. **用户打开表单**：用户通过URL或导航访问自适应表单
1. **识别数据Source**：预填充服务确定配置的数据源（表单数据模型或草稿服务）
1. **检索数据**：系统根据上下文、参数或用户标识获取相关用户数据
1. **映射和显示**：数据使用`bindRef`属性映射到表单字段，并且已填充的表单向用户显示

此自动化流程可确保用户看到一个已预填充了其相关信息的表单，从而显着改善用户体验和表单完成率。

## 预填充的数据结构

自适应Forms支持两种类型的字段：

- **绑定字段**：字段连接到具有非空`bindRef`属性的数据源
- **未绑定的字段**：具有空`bindRef`值的独立字段

预填充数据结构包括：

- **afBoundData**：包含绑定字段和面板的数据
- **afUnBoundData**：包含未绑定字段的数据

数据格式必须与您的表单模型匹配：

- **XFA表单**：与XFA模板架构兼容的XML
- **XML架构表单**：与架构结构匹配的XML
- **JSON架构表单**： JSON与架构兼容
- **表单数据模型(FDM)表单**： JSON匹配FDM结构
- **无架构表单**：所有字段都未绑定并使用未绑定的XML

## 先决条件

在配置预填充服务之前，请确保您具有：

### 必需的设置

- [为Edge Delivery Services配置的GitHub存储库](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)
- [已将自适应Forms块添加到您的项目](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)
- [已配置数据源](/help/forms/configure-data-sources.md)
- [表单数据模型(FDM)已创建](/help/forms/create-form-data-models.md)

### 访问要求

- 访问AEM Forms as a Cloud Service
- 创建和编辑表单的权限
- 启用了所需扩展的通用编辑器访问

>[!TIP]
>
> 您还可以编辑表单以在通用编辑器中集成表单数据模型(FDM)，以从各种后端源获取数据。 有关详细信息，请参阅通用编辑器中的[将表单与表单数据模型集成](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)一文。

## 预填充服务选项

Universal Editor提供两种预填充服务选项：

| 服务类型 | 用途 | 数据源 | 最适合 |
|--------------|---------|-------------|----------|
| **表单门户草稿预填** | 恢复部分完成的表单 | Forms Portal中已保存草稿 | 继续未完成的应用程序 |
| **表单数据模型预填充** | 填充来自外部系统的字段 | 通过FDM的后端数据库 | 自动填写用户配置文件数据 |

### 详细比较

| 功能 | 草稿预填充服务 | FDM预填充服务 |
|---------|----------------------|---------------------|
| **身份验证** | 草稿访问权限需要用户登录 | 基于数据源可配置 |
| **设置复杂性** | 最低配置 | 需要FDM设置和映射 |
| **数据类型** | 静态保存的数据 | 实时动态数据 |
| **用例** | 恢复保存的应用程序 | 从用户配置文件或数据库预填充 |


## 配置表单的预填充服务

+++第1阶段：设置表单数据模型

### 步骤1：创建表单数据模型

1. 登录到您的AEM Forms as a Cloud Service实例
1. 导航到&#x200B;**Adobe Experience Manager** > **Forms** > **数据集成**
1. 选择&#x200B;**创建** > **表单数据模型**
1. 选择您的&#x200B;**数据Source配置**&#x200B;并选择配置的&#x200B;**数据Source**

   ![已创建表单数据模型](/help/edge/docs/forms/universal-editor/assets/create-fdm.png)

   >[!TIP]
   >
   >有关创建表单数据模型的详细说明，请参阅[创建表单数据模型](/help/forms/create-form-data-models.md)。

### 步骤2：配置FDM服务

1. 转到&#x200B;**Adobe Experience Manager** > **Forms** > **数据集成**
1. 在编辑模式下打开表单数据模型
1. 选择数据模型对象并单击&#x200B;**编辑属性**
1. 为所选数据模型对象配置&#x200B;**读取**&#x200B;和&#x200B;**写入**&#x200B;服务

   ![配置读写服务](/help/edge/docs/forms/universal-editor/assets/configure-reda-write-service.png)

1. 配置服务参数：

   - 单击读取服务参数的编辑图标
   - 将参数绑定到&#x200B;**用户配置文件属性**、**请求属性**&#x200B;或&#x200B;**文字值**
   - 指定绑定值（例如，`petid`用于pet注册表）

   ![配置pet id参数](/help/edge/docs/forms/universal-editor/assets/pet-id-arguments.png)

1. 单击&#x200B;**完成**&#x200B;保存参数，单击&#x200B;**保存**&#x200B;保存FDM

   >[!NOTE]
   >
   > 了解有关在[使用表单数据模型(FDM)](/help/forms/work-with-form-data-model.md)中配置FDM服务的更多信息。

+++

+++第2阶段：创建和配置自适应表单

### 第3步：创建自适应表单

1. 导航到&#x200B;**Adobe Experience Manager** > **Forms** > **Forms和文档**
1. 选择&#x200B;**创建** > **自适应Forms**
1. 在&#x200B;**Source**&#x200B;选项卡中，选择一个Edge Delivery Services模板：

   ![选择 Edge Delivery Services 模板](/help/edge/assets/create-eds-forms.png)

1. 单击&#x200B;**创建**&#x200B;以打开&#x200B;**创建表单**&#x200B;向导
1. 指定表单详细信息：

   - **名称**：为您的表单输入描述性名称
   - **标题**：提供用户友好的标题
   - **GitHub URL**：输入您的存储库URL（例如，`https://github.com/wkndforms/edsforms`）

1. 单击&#x200B;**创建**

   ![创建基于架构的表单](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form1.png)

表单在通用编辑器中打开以进行创作。

### 步骤4：配置表单数据Source

1. 选择您的表单并单击&#x200B;**属性**

   ![选择表单属性](/help/edge/docs/forms/universal-editor/assets/select-form-properties1.png)

2. 打开&#x200B;**表单模型**&#x200B;选项卡
3. 从&#x200B;**选择自**&#x200B;下拉列表中，选择&#x200B;**表单数据模型(FDM)**
4. 从下拉列表中选择您创建的表单数据模型（例如PetFDM）

   ![选择表单模型选项卡](/help/edge/docs/forms/universal-editor/assets/select-form-model1.png)

5. 单击&#x200B;**保存并关闭**
6. 打开表单以在通用编辑器中编辑

FDM中的表单元素显示在&#x200B;**内容浏览器**&#x200B;的&#x200B;**数据源**&#x200B;选项卡中。

### 步骤5：将数据绑定添加到表单字段

1. 从&#x200B;**数据源**&#x200B;选项卡中选择数据元素
2. 单击&#x200B;**添加**&#x200B;或拖放元素以构建表单

   ![显示基于架构的表单的通用编辑器屏幕截图](/help/edge/docs/forms/universal-editor/assets/ue-form.png)

3. 将数据绑定添加到表单字段：

   - 选择表单字段
   - 在&#x200B;**属性**&#x200B;面板中，找到&#x200B;**绑定引用**&#x200B;属性
   - 选择适当的数据绑定引用

     ![数据绑定](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding1.png)

+++

+++第3阶段：配置预填充服务

### 步骤6：启用所需的扩展

确保在通用编辑器中启用这些扩展：

1. **AEM表单属性扩展**

   - 在通用编辑器中打开&#x200B;**Extension Manager**
   - 启用&#x200B;**AEM表单属性**&#x200B;扩展

   ![表单属性图标](/help/edge/docs/forms/universal-editor/assets/form-edit-properties.png)

1. **Data Source扩展**

   - 如果您没有看到&#x200B;**数据源**&#x200B;图标，请启用&#x200B;**数据源**&#x200B;扩展

   ![通用编辑器Extension Manager屏幕截图](/help/edge/docs/forms/universal-editor/assets/extension-manager.png)

   >[!TIP]
   >
   > 有关管理扩展的详细说明，请参阅[Extension Manager功能亮点](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)。

### 步骤7：配置预填充服务

1. 在通用编辑器中打开自适应表单
2. 单击&#x200B;**AEM表单属性**&#x200B;扩展图标

   ![选择表单属性图标](/help/edge/docs/forms/universal-editor/assets/select-fdm-properties-icon.png)

3. 单击&#x200B;**预填充**&#x200B;选项卡
4. 选择&#x200B;**表单数据模型预填充服务**

   ![选择预填充服务](/help/edge/docs/forms/universal-editor/assets/select-fdm-prefill.png)

5. 单击&#x200B;**保存并关闭**

+++

+++第4阶段：测试预填充配置

### 步骤8：预览和测试

1. 转到&#x200B;**Forms** > **Forms和文档**
2. 选择您的自适应表单
3. 选择&#x200B;**预览为HTML**
4. 通过将参数附加到URL来测试预填充：

   https://your-preview-url.com?&lt;bindreferencefield>=&lt;value>

   **示例：**

   https://your-preview-url.com?petid=12345

   ![预填表单](/help/edge/docs/forms/universal-editor/assets/prefill-form.png)

表单应基于提供的参数自动填充数据。

+++

## 示例

### 预填充数据结构示例

基于FDM的表单的&#x200B;**JSON示例：**

    “
    
    &lbrace;
    ”afBoundData“： &lbrace;
    ”user“： &lbrace;
    ”firstName“： &lbrace;”John“，
    ”lastName“： ”Doe“，
    ”email“： ”john.doe@example.com“，
    ”phone“：“+1-555-0123”
    &rbrace;
    &rbrace;，
    ”afUnBoundData“： &lbrace;
    ”additionalInfo“： ”用户首选项已加载“
    &rbrace;
    &rbrace;
    
    ”“
”
基于XFA的表单的&#x200B;**XML示例：**

    “
    
    &lt;？xml version=&quot;1.0&quot; encoding=&quot;UTF-8&quot;？>
    &lt;afData>
    &lt;afBoundData>
    &lt;user>
    &lt;firstName>John&lt;/firstName>
    &lt;lastName>Doe&lt;/lastName>
    &lt;email>john.doe@example.com&lt;/email>
    &lt;/user>
    &lt;/afBoundData>
    &lt;/afData>
    
    &quot;&#39;

### 预填充URL示例

以下URL仅供说明之用，无法按原样工作。 在测试预填充功能时，将主机和参数替换为与您自己的环境相关的主机和参数。

**基本预填充测试：**

`https://preview.example.com/form.html?userId=12345`

**多个参数测试：**

`https://preview.example.com/form.html?userId=12345&category=premium`


## 疑难解答

+++常见问题和解决方案

| 问题 | 可能的原因 | 解决方案 |
|-------|----------------|----------|
| **表单字段未预填** | 不正确的`bindRef`值 | 验证`bindRef`是否与FDM字段名称完全匹配 |
| **数据格式错误** | 数据结构不匹配 | 确保预填充数据与表单模型架构匹配 |
| 找不到&#x200B;**服务** | FDM配置问题 | 检查是否已正确配置和保存FDM服务 |
| **身份验证错误** | 数据源连接 | 验证数据源凭据和连接 |
| **正在加载部分数据** | 缺少字段映射 | 确保所有必填字段具有正确的数据绑定 |

+++

+++调试步骤

1. **验证FDM配置：**

   - 检查服务是否正确配置
   - 独立测试FDM服务
   - 验证数据源连接

2. **检查表单配置：**

   - 确认表单与正确的FDM相关联
   - 验证字段`bindRef`值
   - 先测试不含预填充的表单

3. **测试数据流：**

   - 使用浏览器开发人员工具检查网络请求
   - 检查JavaScript错误的控制台
   - 验证响应数据格式

4. **常见错误消息：**

   - “未找到预填充服务”：检查服务配置
   - “数据绑定失败”：验证`bindRef`准确性
   - “数据格式无效”：确保数据与架构匹配

+++

## 最佳实践

+++配置最佳实践

- **使用描述性命名**：清楚地命名您的FDM和服务
- **验证数据架构**：确保数据结构与表单要求匹配
- **增量测试**：一次配置并测试一个字段
- **文档映射**：跟踪字段到数据的映射

+++

+++性能优化

- **最小化数据量**：仅预填必要的字段
- **使用缓存**：为经常访问的数据配置适当的缓存
- **优化查询**：确保数据库查询有效
- **监测性能**：在启用预填充的情况下跟踪表单加载时间

+++

+++安全注意事项

- **验证输入参数**：始终验证URL参数
- **清理数据**：在预填充表单之前清理数据
- **实施访问控制**：确保用户只能访问自己的数据
- **使用HTTPS**：始终使用安全连接进行数据传输

+++

+++用户体验准则

- **提供反馈**：在数据提取期间显示加载指示器
- **正常处理错误**：显示有用的错误消息
- **允许覆盖**：允许用户修改预填充的数据
- **保持一致性**：跨表单使用一致的预填充行为

+++

## 常见问题解答

+++如何测试预填充是否正常工作？

预览表单并使用以下格式将预填充参数附加到URL： `?<bindreferencefield>=<value>`。 确保字段具有与您的数据结构匹配的有效`bindRef`。 使用浏览器开发人员工具检查网络请求，并验证是否正确获取了数据。

+++

+++预填充自适应Forms支持哪些数据格式？

自适应Forms支持多种格式，具体取决于您的表单模型：

- **XFA表单**：与XFA架构匹配的XML
- **JSON架构表单**： JSON数据与架构兼容
- **FDM表单**：映射到数据模型结构的JSON
- **XML架构表单**：与架构结构匹配的XML

+++

+++我可以预填已绑定和未绑定的字段吗？

可以，您可以预填充这两种类型的字段。 绑定字段使用`afBoundData`部分，并且必须与您的表单模型架构匹配。 未绑定字段使用`afUnBoundData`部分，可包含任何其他数据。

+++

+++如果只有一些字段正在预填，我应该怎么做？

检查所有字段是否具有完全匹配您的FDM的正确`bindRef`值。 验证数据源是否包含所有必填字段，以及数据结构是否与表单模型架构匹配。

+++

+++如何处理预填充服务的身份验证？

身份验证取决于您的数据源配置。 对于基于FDM的预填充，请在数据源设置中配置身份验证。 对于草稿预填，用户通常需要登录才能访问其保存的草稿。

+++

+++我是否可以在一个表单中使用多个预填充服务？

您可以为每个表单配置一个主预填充服务。 但是，您可以在单个表单数据模型中组合不同的数据源，以实现相似的功能。

+++

## 相关主题

- [在通用编辑器中将表单与表单数据模型集成](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)
- [创建表单数据模型](/help/forms/create-form-data-models.md)
- [使用表单数据模型(FDM)](/help/forms/work-with-form-data-model.md)
- [配置数据源](/help/forms/configure-data-sources.md)
- [Edge Delivery ServicesAEM Forms入门](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
