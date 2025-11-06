---
title: Edge Delivery Services 表单规则编辑器
description: 使用通用编辑器中的规则编辑器创建动态、智能的表单。无需编码即可添加条件逻辑、计算和交互式行为。
feature: Edge Delivery Services
role: Admin, Developer
level: Intermediate
exl-id: 846f56e1-3a98-4a69-b4f7-40ec99ceb348
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2824'
ht-degree: 100%

---


# Edge Delivery Services 表单规则编辑器

规则编辑器使作者无需编写代码即可将静态表单转化为响应式、智能化的体验。您可以有条件地显示字段、执行计算、验证数据、引导用户完成流程、集成随输入而调整的业务逻辑。

## 您将了解的内容

本指南结束时，您将能够：

- 了解规则如何起作用以及在什么情况下需要使用不同的规则类型
- 能够在通用编辑器中启用并访问规则编辑器
- 创建条件逻辑，动态地显示或隐藏字段
- 能够实施自动计算和数据验证
- 能够为复杂的业务规则构建自定义函数
- 应用性能、可维护性和用户体验方面的最佳做法

## 为什么要使用规则编辑器？

- **条件逻辑**：仅在需要时显示相关字段，以减少干扰和认知负荷。
- **动态计算**：根据用户的输入自动计算数值（总数、费率、税额）
- **数据验证**：通过实时检查和清晰的信息尽早预防错误。
- **引导式体验**：引导用户完成逻辑步骤（向导、分支）。
- **无代码创作**：通过一个可视化界面配置有效的行为方式。

常见场景包括税费计算器、贷款和保费估算器、资格流程、多步骤申请以及包含有条件问题的意见调查。

## 规则如何起作用

规则定义了当满足某个条件时应该发生什么。从概念上讲，规则包括两个部分：

- **条件**：一个语句，评估的结果为“真”或“假”。
   - 示例：“收入 > 50,000”，“覆盖范围 =‘是’”，“字段为空”
- **操作**：当条件为真时发生的事情（可以选择添加在条件为假的情况下发生的事情）。
   - 示例：显示/隐藏字段，设置/清除值，验证输入，启用/禁用按钮

+++ 规则逻辑模式

- **条件 → 操作 (When/Then)**

  ```text
  WHEN Gross Salary > 50000
  THEN Show "Additional Deduction"
  ```

  最适合用于有条件的可见性和渐进方式披露信息。

- **操作 ← 条件 (Set If/Only if)**

  ```text
  SET Taxable Income = Gross Salary - Deductions
  IF Deductions are applicable
  ```

  最适合用于计算和数据转换。

- **If → Then → Else（替代操作）**

  ```text
  IF Income > 50000
  THEN Show "High Income" fields
  ELSE Show "Standard Income" fields
  ```

  最适合用于分支逻辑和互斥选项流程。

+++

+++ 真实世界示例

- **条件**：“总收入超过 50,000 美元”
- **主要操作**：显示“附加扣除”
- **替代操作**：隐藏“附加扣除”
- **结果**：用户只看到适用于他们的字段

+++

## 先决条件


+++ 满足访问权限要求

**基本权限和设置**：

- **AEM as a Cloud Service**：有表单编辑权限的创作访问权限
- **通用编辑器**：已在您的环境中安装并配置
- **规则编辑器扩展**：已通过[扩展管理器](/help/implementing/developing/extending/extension-manager.md)启用
- **表单编辑权限**：能够在通用编辑器中创建和更改表单组件

**验证步骤**：

1. 确认您可以从 AEM Sites 控制台访问通用编辑器
2. 验证您可以创建和编辑表单组件
3. 检查在选择表单组件后是否显示规则编辑器图标 ![edit-rules](/help/forms/assets/edit-rules-icon.svg)

+++

+++ 技术要求

**必需的知识和技能**：

- **熟悉通用编辑器**：具备创建表单并在其中包含文本输入、下拉菜单和基本字段属性的经验
- **理解业务逻辑**：能够针对您的特定用例定义条件要求和验证规则
- **熟悉表单组件**：了解字段类型（文本、数字、下拉菜单）、属性（必需、可见、只读）和表单结构

**在高级使用中的可选技能**：

- **JavaScript 基础知识**：只有在创建自定义函数时需要（数据类型、函数、基本语法）
- **理解 JSON**：对复杂的数据操作和 API 集成有帮助

**评估问题**：

- 您可以在通用编辑器中创建包含文本输入和提交按钮的基本表单吗？
- 您是否了解在您的业务环境中哪些情况下字段是必需的，哪些情况下字段是可选的？
- 您能否确定在您的用例中哪些表单元素需要根据条件决定可见性？

+++

+++ 启用规则编辑器扩展

**重要**：默认情况下，通用编辑器环境中未启用规则编辑器扩展。

**激活步骤**：

1. 导航到 AEM 环境中的[扩展管理器](/help/implementing/developing/extending/extension-manager.md)
2. 在可用扩展列表中找到“规则编辑器”扩展
3. 点击&#x200B;**启用**，然后确认激活
4. 等待系统刷新（可能需要 1-2 分钟）

**验证**：

- 启用之后，您选择表单组件后就会出现规则编辑器图标：![edit-rules](/help/forms/assets/edit-rules-icon.svg)

![通用编辑器规则编辑器](/help/edge/docs/forms/assets/universal-editor-rule-editor.png)
图：选择表单组件后会显示规则编辑器图标

要打开规则编辑器：

1. 在通用编辑器中选择一个表单组件。
2. 点击规则编辑器图标。
3. 规则编辑器将在侧边面板中打开。

![规则编辑器用户界面](/help/edge/docs/forms/assets/rule-editor-for-field.png)
图：用于编辑组件规则的规则编辑器界面

>[!NOTE]
>
> 在本文中，“表单组件”和“表单对象”指的是相同的元素（例如输入、按钮、面板等）。

## 规则编辑器界面概述

![规则编辑器用户界面](/help/edge/docs/forms/assets/rule-editor-interface.png)
图：完整的规则编辑器界面和带编号的组件

1. **组件标题和规则类型**：确认所选组件和活跃规则类型。
2. **表单对象和函数面板**：

   - 表单对象：可以在规则中引用的字段和容器的层级视图
   - 函数：内置的数学、字符串、日期和验证助手

3. **面板切换**：显示/隐藏对象和函数面板，增加工作区
4. **可视化规则生成器**：拖放式、下拉驱动的规则编写器
5. **控件**：完成（保存）、取消（放弃）。保存之前务必测试规则。

+++

+++ 管理现有规则

当组件已有规则时，您可以：

- **查看**：查看规则汇总和逻辑
- **编辑**：更改条件和操作
- **重新排序**：改变执行顺序（从上到下）
- **启用/禁用**：为测试切换规则
- **删除**：安全删除规则

>[!TIP]
>
> 将特定规则放在一般规则的前面。执行顺序从上到下。

+++

## 可用规则类型

选择最符合您目的的规则类型。

+++ 条件逻辑

- **如果**：有条件的复杂行为的主要规则（条件 → 操作 ± 否则）
- **隐藏/显示**：根据条件控制可见性（渐进展示）
- **启用/禁用**：控制字段是否可交互（例如禁用提交，直到必需字段有效）

+++

+++ 数据操作

- **设置值**：自动填充值（例如日期、总计、副本）
- **清除值**：当条件改变时移除数据
- **格式**：转换显示格式（货币、电话、日期），而不改变存储的值

+++

+++ 验证

- **验证**：自定义验证逻辑，包括跨字段检查和业务规则

+++

+++ 计算

- **数学表达式**：实时计算数值（总计、税额、比率）

+++

+++ 用户界面

- **设置焦点**：将焦点移至特定字段（谨慎使用）
- **设置属性**：动态更改组件属性（占位符、选项等）

+++

+++ 表单控制

- **提交表单**：以编程方式提交表单（仅在验证通过后）
- **重置表单**：清除并重置为初始状态（使用前确认）
- **保存表单**：保存为草稿，以后继续使用（长表单、多会话）

+++

+++ 高级

- **调用服务**：调用外部 API/服务（处理加载和错误）
- **添加/删除实例**：管理可重复分区（例如依赖项、地址）
- **导航到**：路由到其他表单/页面（导航前保留数据）
- **在面板之间导航**：控制向导步骤导航和跳过
- **分派事件**：触发集成或分析的自定义事件

+++

## 分步教程：构建智能税费计算器

+++ 教程概述

此示例演示了有条件的可见性和自动计算。

![规则编辑器界面的屏幕快照，展示了使用 When-Then 逻辑创建表单字段可见性的条件规则](/help/edge/docs/forms/assets/rule-editor-1.png)
图：包含智能条件字段的税费计算表

您将构建这样一个表单：

1. 根据用户输入显示相关字段
2. 实时计算数值
3. 验证数据，以提高准确性

+++

+++ 表单结构

| 字段名称 | 类型 | 用途 | 行为 |
|-------------------------|---------------|--------------------------------|-----------------------------------------|
| 总收入 | 数字输入 | 用户的年收入 | 触发条件逻辑 |
| 附加扣除 | 数字输入 | 额外扣除项（符合条件的情况下） | 只有在收入 > $50,000 的情况下可见 |
| 应税收入 | 数字输入 | 计算值 | 只读，更改时更新 |
| 应缴税费 | 数字输入 | 计算值 | 只读，按固定费率计算 |

+++

+++ 业务逻辑

- **规则 1：根据条件显示**

  ```text
  WHEN Gross Salary > 50,000
  THEN Show "Additional Deduction"
  ELSE Hide "Additional Deduction"
  ```

- **规则 2：计算应税收入**

  ```text
  SET Taxable Income = Gross Salary - Additional Deduction
  (Only when Additional Deduction applies)
  ```

- **规则 3：计算应缴税费**

  ```text
  SET Tax Payable = Taxable Income × 10%
  (Simplified flat rate)
  ```

+++

+++ 步骤 1：创建表单

**目标**：构建包含所有字段和初始设置的基本表单。

1. **打开通用编辑器**：
   - 导航到 AEM Sites 控制台，选择您的页面，点击&#x200B;**编辑**
   - 确保您已正确配置了[通用编辑器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction.html?lang=zh-Hans)

2. **按以下顺序添加表单组件**：
   - 标题 (H2)：“税费计算表”
   - 数字输入：“总收入”（必填：是，占位符：“输入年薪”）
   - 数字输入：“附加扣除”（必填：否，占位符：“输入附加扣除”）
   - 数字输入：“应税收入”（只读：是）
   - 数字输入：“应缴税费”（只读：是）
   - 提交按钮：“计算税费”

3. **配置初始字段属性**：
   - 隐藏“附加扣除”（在属性面板中设置可见性：否）
   - 将“应税收入”和“应缴税费”设置为只读：是

![税费计算表屏幕快照，包含总收入、婚姻状况和受抚养子女的输入字段，这是应用规则之前的表单结构](/help/edge/docs/forms/assets/rule-editor2.png)
图：配置了基本组件的初始表单结构

**检查点**：您现在有一个包含所有必填字段的表单，其中“附加扣除”是隐藏的，计算得到的字段为只读。

+++

+++ 步骤 2：添加条件可见性规则

**目标**：只有在总收入超过 50,000 美元的情况下才显示“附加扣除”字段。

1. **选择总收入字段**，然后点击规则编辑器图标 ![edit-rules](/help/forms/assets/edit-rules-icon.svg)
2. **创建新规则**：
   - 单击&#x200B;**创建**
   - 将规则类型从“设置值”更改为&#x200B;**“如果”**
3. **配置条件**：
   - 从下拉菜单中选择&#x200B;**“大于”**
   - 在数字字段中输入 `50000`
4. **设置 Then 操作**：
   - 从选择操作下拉菜单中选择&#x200B;**“显示”**
   - 从表单对象中拖动或选择&#x200B;**“附加扣除”**&#x200B;字段
5. **添加 Else 操作**：
   - 点击&#x200B;**“添加 Else 操作”**
   - 从选择操作下拉菜单中选择&#x200B;**“显示”**
   - 选择&#x200B;**“附加扣除”**&#x200B;字段
6. **保存规则**：点击&#x200B;**完成**

>[!NOTE]
>
> 替代方法：您可以直接在“附加扣除”字段上创建显示/隐藏规则，而不是在“总收入”上创建“如果”规则，可以获得相同的结果。

+++

+++ 步骤 3：添加计算规则

**目标**：根据用户输入自动计算“应税收入”和“应缴税费”。

**配置应税收入的计算**：

1. **选择“应税收入”字段**，打开规则编辑器
2. **创建数学表达式**：
   - 点击&#x200B;**创建** → 选择 **“数学表达式”**
   - 构建表达式：**总收入 - 附加扣除**
   - 将“总收入”拖到第一个字段
   - 选择&#x200B;**“减”**&#x200B;运算符
   - 将“附加扣除”拖到第二个字段
3. **保存**：点击&#x200B;**完成**

**配置应缴税费计算**：

1. **选择“应缴税费”字段**，打开规则编辑器
2. **创建数学表达式**：
   - 点击&#x200B;**创建** → 选择 **“数学表达式”**
   - 构建表达式：**应税收入 × 10 ÷ 100**
   - 将“应税收入”拖到第一个字段
   - 选择&#x200B;**“乘以”**&#x200B;运算符
   - 输入数字 `10`
   - 点击&#x200B;**“扩展表达式”**
   - 选择&#x200B;**“除以”**&#x200B;运算符
   - 输入数字 `100`
3. **保存**：点击&#x200B;**完成**

+++

+++ 步骤 4：测试表单

**测试完整流程，验证您的实施**：

1. **预览表单**：点击通用编辑器中的预览模式
2. **测试条件逻辑**：
   - 输入总收入 = `30000` → 应隐藏“附加扣除”
   - 输入总收入 = `60000` → 应显示“附加扣除”
3. **测试计算**：
   - 总收入 = `60000` 的情况下，输入附加扣除 = `5000`
   - 验证应税收入 = `55000` (60000 - 5000)
   - 验证应缴税费 = `5500` (55000 × 10%)

![预览表单](/help/edge/docs/forms/assets/rule-editor-form.png)
图：已完成的包含条件字段和自动计算的税费计算器

**成功标准**：表单应在用户输入时动态显示/隐藏字段并实时计算数值。


+++

## 高级：自定义函数

对于超出内置功能的复杂业务逻辑，您可以创建与规则编辑器无缝集成的自定义 JavaScript 函数。

+++ 何时使用自定义函数

**自定义函数的理想场景**：

- **复杂计算**：难以用数学表达式规则表达的多步骤计算
- **业务特有的验证**：您的组织或行业特有的自定义验证逻辑
- **数据转换**：格式转换、字符串操作或数据解析
- **外部集成**：调用内部 API 或第三方服务（受限）

**自定义函数的好处**：

- **可重复使用**：只需编写一次，就可用于各种表单和规则
- **可维护**：集中逻辑，易于更新和调试
- **性能**：与复杂规则链相比，优化了 JavaScript 执行
- **灵活**：能够处理边缘情况和标准规则无法应对的复杂场景

+++

+++ 创建和实施自定义函数

**文件位置**：您的 Edge Delivery Services 项目中的所有自定义函数都必须定义在 `/blocks/form/functions.js` 中。

**开发工作流**：

1. **函数设计**
   - 使用以操作为导向的描述性函数名称
   - 定义明确的参数类型和返回值
   - 妥善处理边缘情况和无效输入

2. **实施**
   - 编写整齐简洁、有良好注释的 JavaScript
   - 包含输入验证和错误处理
   - 集成之前独立测试函数

3. **文档**
   - 添加全面的 JSDoc 注释
   - 包含使用示例和参数说明
   - 记录任何限制或依赖关系

4. **部署**
   - 函数导出时将其命名
   - 部署到您的项目存储库
   - 测试之前验证函数已完成构建

**实施示例**：

```javascript
/**
 * Concatenates first and last name with proper formatting
 * @name getFullName
 * @description Combines first and last name, handles edge cases like missing values
 * @param {string} firstName - The person's first name
 * @param {string} lastName - The person's last name  
 * @returns {string} Formatted full name or empty string if both inputs are invalid
 */
function getFullName(firstName, lastName) {
  // Handle null, undefined, or empty string inputs
  const first = (firstName || '').toString().trim();
  const last = (lastName || '').toString().trim();
  
  return `${first} ${last}`.trim();
}

/**
 * Calculates the number of days between two dates
 * @name days
 * @description Computes absolute difference in days, handles various date input formats
 * @param {Date|string} endDate - End date (Date object or ISO string)
 * @param {Date|string} startDate - Start date (Date object or ISO string)
 * @returns {number} Number of days between dates, 0 if inputs are invalid
 */
function days(endDate, startDate) {
  // Convert string inputs to Date objects
  const start = typeof startDate === 'string' ? new Date(startDate) : startDate;
  const end = typeof endDate === 'string' ? new Date(endDate) : endDate;

  // Validate date objects
  if (Number.isNaN(start.getTime()) || Number.isNaN(end.getTime())) {
    return 0;
  }

  // Calculate absolute difference in milliseconds, then convert to days
  const diffInMs = Math.abs(end.getTime() - start.getTime());
  return Math.floor(diffInMs / (1000 * 60 * 60 * 24));
}

// Export functions for use in Rule Editor
export { getFullName, days };
```

![添加自定义函数](/help/edge/docs/forms/assets/create-custom-function.png)
图：在 functions.js 文件中添加自定义函数

+++

+++ 在规则编辑器中使用自定义函数

**集成步骤**：

1. **将函数添加到项目中**
   - 在您的项目中创建或编辑 `/blocks/form/functions.js`
   - 在导出语句中包含您的函数

2. **部署和构建**
   - 提交对存储库的更改
   - 确保构建过程成功完成
   - 留出 CDN 缓存更新的时间

3. **在规则编辑器中访问**
   - 为任何表单组件打开规则编辑器
   - 在&#x200B;**选择操作**&#x200B;下拉菜单中选择&#x200B;**“函数输出”**
   - 从可用函数列表中选择您的自定义函数
   - 使用表单字段或静态值配置函数参数

4. **彻底测试**
   - 预览表单，验证函数行为
   - 使用各种输入组合（包括边缘情况）进行测试
   - 验证对表单加载和交互性能的影响

![规则编辑器中的自定义函数](/help/edge/docs/forms/assets/custom-function-rule-editor.png)
图：在规则编辑器界面中选择和配置自定义函数

>[!NOTE]
>
> 规则编辑器的增强功能（包括自定义事件驱动规则、对动态变量的支持以及 API 集成）同样适用于 Edge Delivery Services 表单。要详细了解这些增强功能及其使用方法，请参阅[规则编辑器增强功能与使用案例](/help/forms/rule-editor-enhancements-use-cases.md)文章。

**函数使用的最佳做法**：

- **错误处理**：始终包含函数失败情况下的应变行为
- **性能**：用实际数据量分析函数的执行情况
- **安全性**：验证所有输入，防止安全漏洞
- **测试**：创建涵盖正常情况和边缘情况的测试案例

+++


### 自定义函数的静态导入

通用编辑器的规则编辑器支持静态导入，使您能够在各种文件和表单中组织可重复使用的逻辑。您可以从其他模块导入函数，而不必将所有自定义函数保存在一个文件 (/blocks/form/functions.js) 中。
例如：从外部文件导入函数
考虑以下文件夹结构：

```
      form
      ┣ commonLib
      ┃ ┗ functions.js
      ┣ rules
      ┃ ┗ _form.json
      ┣ form.js
      ┗ functions.js
```

您可以从 `commonLib/functions.js` 将函数导入您的 `functions.js` 主文件中，如下所示：

```
`import {days} from './commonLib/functions';
/**
 * Get Full Name
 * @name getFullName Concats first name and last name
 * @param {string} firstname in String format
 * @param {string} lastname in String format
 * @return {string}
 */
function getFullName(firstname, lastname) {
  return `${firstname} ${lastname}`.trim();
}

// Export multiple functions for use in Rule Editor
export { getFullName, days};
```

### 在不同的表单中组织自定义函数

您可以在单独的文件或文件夹中创建不同的函数集，然后根据需要导出它们：

- 如果您希望某些函数仅供特定表单使用，可以在表单配置中提供相关函数文件的路径。

- 如果此路径的文本框为空白，规则编辑器就默认从 `/blocks/form/functions.js` 加载函数

![UE 中的自定义函数](/help/forms/assets/custom-function-in-ue.png){width=50%}

在上面的屏幕快照中，“自定义函数路径”文本框中添加了自定义函数的路径。此表单的自定义函数就从指定文件 (`cc_function.js`) 加载。

这样就可以在各种表单中共享函数，也可以将函数在每个表单中分开使用，为用户提供了灵活性。

## 规则开发的最佳做法


+++ 性能优化

- 最大程度减少规则的复杂性；将大逻辑分解成突出重点的小规则
- 按频率对规则排序（最常用规则优先）
- 保持每个组件的规则集易于管理
- 优先采用可重复使用的自定义函数，而不是重复逻辑

+++

+++ 用户体验

- 提供清晰的验证和内联反馈
- 避免不和谐的视觉变化；谨慎使用显示/隐藏
- 测试各种不同的设备和布局

+++

+++ 开发卫生

- 使用边缘情况和已知值测试
- 验证各种不同的浏览器
- 记录复杂规则背后的目的，而不仅仅记录机制
- 为大表单维护规则库存
- 为组件和规则使用一致的命名惯例
- 为自定义函数制定版本，并在非生产环境中测试

+++

## 常见问题排查


+++ 规则未触发

- 验证组件名称和引用
- 检查执行顺序（从上到下）
- 使用已知值验证条件
- 检查浏览器控制台是否显示阻止错误

+++

+++ 错误的行为

- 检查运算符和分组（AND/OR）
- 单独测试表达式片段
- 确认数据类型（数字与字符串对比）

+++

+++ 性能问题

- 简化深度嵌套的条件
- 分析自定义函数的执行情况
- 尽量减少规则中的外部调用
- 使用特定的选择器和引用

+++

+++ 自定义函数问题

- 确认文件路径：`/blocks/form/functions.js`
- 确保所命名的导出正确
- 确认构建中包含了您的更改
- 部署后清除浏览器缓存
- 验证参数类型和错误处理

+++

+++ 通用编辑器集成

- 确认规则编辑器扩展已启用
- 选择受支持的组件
- 使用受支持的浏览器（Chrome、Firefox、Safari）
- 验证您具有必需的权限

## 重要限制

>[!IMPORTANT]
>
> 自定义函数约束：
>
> - 不支持静态/动态导入
> - 所有逻辑都必须位于 `/blocks/form/functions.js`
> - 函数必须同步（没有 async/await 或 Promises）
> - 浏览器 API 访问受限

>[!WARNING]
>
> 生产考虑事项：
>
> - 在暂存阶段进行彻底测试
> - 监控部署后的性能
> - 为规则问题制定一个回滚计划
> - 考虑慢网速和低规格设备

## 摘要

通用编辑器中的规则编辑器将静态表单转换为智能的响应式体验，可根据用户输入实时调整。通过条件逻辑、自动计算和自定义业务规则，您无需编写应用程序代码就可以创建复杂的表单工作流。

**您已了解的关键功能**：

- **条件逻辑**：根据用户输入显示和隐藏字段，以创建有针对性的相关体验
- **动态计算**：用户与表单交互时，能自动计算数值（税额、总计、费率）
- **数据验证**：通过清晰、可操作的反馈信息实施实时验证
- **自定义函数**：使用 JavaScript 扩展功能实现复杂的业务逻辑和集成
- **性能优化**：应用最佳做法，实现可维护、高效的规则开发

**传递的价值**：

- **增强用户体验**：通过渐进展开的方式和智能表单流程减少认知负荷
- **减少错误**：通过实时验证和引导式输入防止无效提交
- **提高效率**：通过自动计算和数据输入最大限度地减少用户工作量
- **可维护的解决方案**：创建可重复使用、记录良好、可在整个组织内扩展的规则

**业务影响**：

表单成为数据收集、潜在客户鉴定和用户参与的有力工具。规则编辑器使非技术作者能够实施复杂的业务逻辑，降低开发成本，同时提高表单完成率和数据质量。

+++

## 后续步骤

**推荐的学习路径**：

1. **从基础开始**：创建简单的显示/隐藏规则，理解核心概念
2. **使用教程练习**：使用税费计算器示例作为基础，创建您自己的表单
3. **逐渐扩展**：随着您的信心增强，添加数学表达式和验证规则
4. **实施自定义函数**：针对特定业务需求开发 JavaScript 函数
5. **优化和规模扩展**：应用性能最佳做法，维护规则文档

**其他资源**：

- [通用编辑器文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction.html?lang=zh-Hans)：用于更广泛的上下文
- [扩展管理器指南](/help/implementing/developing/extending/extension-manager.md)：用于启用附加功能
- [Edge Delivery Services 表单](/help/edge/docs/forms/overview.md)：提供全面的表单开发指导

