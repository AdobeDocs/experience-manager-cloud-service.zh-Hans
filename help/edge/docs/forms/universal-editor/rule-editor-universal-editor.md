---
title: 通用编辑器中的动态表单规则编辑器
description: 使用通用编辑器中的规则编辑器创建动态、智能的表单。无需编码即可添加条件逻辑、计算和交互式行为。
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
exl-id: 846f56e1-3a98-4a69-b4f7-40ec99ceb348
source-git-commit: 03e46bb43e684a6b7057045cf298f40f9f1fe622
workflow-type: tm+mt
source-wordcount: '2781'
ht-degree: 4%

---


# 通用编辑器中的动态表单规则编辑器

规则编辑器允许作者将静态表单转换为响应式智能体验，而无需编写代码。 您可以有条件地显示字段、执行计算、验证数据、引导用户完成流以及集成根据人员类型调整的业务逻辑。

## 您将学习的内容

在本指南结束时，您将能够：

- 了解规则如何起作用以及在什么情况下需要使用不同的规则类型
- 能够在通用编辑器中启用并访问规则编辑器
- 创建条件逻辑以动态显示或隐藏字段
- 能够实施自动计算和数据验证
- 能够为复杂的业务规则构建自定义函数
- 将最佳实践应用于性能、可维护性和UX

## 为何使用规则编辑器？

- **条件逻辑**：仅在需要减少噪音和认知负载时显示相关字段。
- **动态计算**：根据用户类型自动计算值（总计、费率、税）。
- **数据验证**：通过实时检查并清除消息来提前避免错误。
- **引导式体验**：引导用户完成逻辑步骤（向导、分支）。
- **无代码创作**：通过可视化界面配置强大的行为。

常见方案包括税计算器、贷款和保费估算器、资格流程、多步骤应用程序以及带条件问题的调查。

## 规则的工作方式

规则定义在满足条件时应发生的情况。 从概念上讲，规则分为两部分：

- **条件**：计算为true或false的语句。
   - 示例：“收入> 50,000”、“覆盖范围= &#39;是&#39;”、“字段为空”
- **操作**：当条件为true时（也可以选择当条件为false时）发生的情况。
   - 示例：显示/隐藏字段、设置/清除值、验证输入、启用/禁用按钮

+++ 规则逻辑模式

- **条件→操作(When/Then)**

  ```text
  WHEN Gross Salary > 50000
  THEN Show "Additional Deduction"
  ```

  最适合有条件的可见性和渐进式披露。

- **Action ←条件（设置If/Only If）**

  ```text
  SET Taxable Income = Gross Salary - Deductions
  IF Deductions are applicable
  ```

  最适合计算和数据转换。

- **If → Then → Else （备用操作）**

  ```text
  IF Income > 50000
  THEN Show "High Income" fields
  ELSE Show "Standard Income" fields
  ```

  最适合分支逻辑和互斥流。

+++

+++ 现实世界示例

- **条件**：“总收入超过 50,000 美元”
- **主要操作**：显示“附加扣款”
- **备用操作**：隐藏“附加扣款”
- **结果**：用户只能看到适用于他们的字段

+++

## 先决条件


+++ 访问要求

**基本权限和设置**：

- **AEM as a Cloud Service**：具有表单编辑权限的创作访问权限
- **通用编辑器**：在您的环境中安装和配置
- **规则编辑器扩展**：已通过[Extension Manager](/help/implementing/developing/extending/extension-manager.md)启用
- **表单编辑权限**：能够在通用编辑器中创建和修改表单组件

**验证步骤**：

1. 确认您可以从AEM Sites控制台访问通用编辑器
2. 验证您是否能够创建和编辑表单组件
3. 选择表单组件时，请检查是否显示规则编辑器图标![edit-rules](/help/forms/assets/edit-rules-icon.svg)

+++

+++ 技术要求

**所需的知识和技能**：

- **通用编辑器熟练程度**：体验使用文本输入、下拉列表和基本字段属性创建表单
- **业务逻辑了解**：能够为特定用例定义条件要求和验证规则
- **表单组件熟悉度**：字段类型（文本、数字、下拉列表）、属性（必需、可见、只读）和表单结构的知识

**高级用法可选**：

- **JavaScript基础知识**：仅在创建自定义函数（数据类型、函数、基本语法）时需要
- **JSON了解**：有助于复杂的数据操作和API集成

**评估问题**：

- 能否在通用编辑器中创建一个包含文本输入和提交按钮的基本表单？
- 您是否了解在您的业务环境中，何时字段是必填字段还是可选字段？
- 能否确定哪些表单元素需要在用例中进行条件可视性？

+++

+++ 启用规则编辑器扩展

**重要信息**：默认情况下，在通用编辑器环境中未启用规则编辑器扩展。

**激活步骤**：

1. 导航到AEM环境中的[Extension Manager](/help/implementing/developing/extending/extension-manager.md)
2. 在可用扩展列表中，找到“规则编辑器”扩展
3. 单击&#x200B;**启用**&#x200B;并确认激活
4. 等待系统刷新（可能需要1-2分钟）

**验证**：

- 启用后，当您选择表单组件![edit-rules](/help/forms/assets/edit-rules-icon.svg)时，将显示规则编辑器图标

![通用编辑器规则编辑器](/help/edge/docs/forms/assets/universal-editor-rule-editor.png)
图：选择表单组件时将显示规则编辑器图标

要打开规则编辑器，请执行以下操作：

1. 在通用编辑器中选择表单组件。
2. 单击规则编辑器图标。
3. 规则编辑器将在侧面板中打开。

![规则编辑器用户界面](/help/edge/docs/forms/assets/rule-editor-for-field.png)
图：用于编辑组件规则的规则编辑器界面

>[!NOTE]
>
> 在本文中，“表单组件”和“表单对象”是指相同的元素（例如，输入、按钮、面板）。

## 规则编辑器界面概述

![规则编辑器用户界面](/help/edge/docs/forms/assets/rule-editor-interface.png)
图：带编号组件的完整规则编辑器界面

- **组件标题和规则类型**：确认所选的组件和活动的规则类型。
- **表单对象和函数面板**：
   - 表单对象：规则中用于引用的字段和容器的分层视图
   - 函数：内置的数学、字符串、日期和验证帮助程序
- **面板切换**：显示/隐藏对象和函数面板以增加工作区
- **可视化规则生成器**：拖放、下拉驱动规则编辑器
- **控件**：完成（保存），取消（放弃）。 保存前始终测试规则。

+++

+++ 管理现有规则

当组件已有规则时，您可以：

- **视图**：查看规则摘要和逻辑
- **编辑**：修改条件和操作
- **重新排序**：更改执行顺序（从上到下）
- **启用/禁用**：切换测试规则
- **删除**：安全地删除规则

>[!TIP]
>
> 将特定规则放在常规规则之前。 执行是自上而下的。

+++

## 可用规则类型

选择最符合您意图的规则类型。

+++ 条件逻辑

- **When**：复杂条件行为的主规则(条件→操作± Else)
- **隐藏/显示**：根据条件控制可见性（渐进式公开）
- **启用/禁用**：控制字段是否为交互字段（例如，禁用提交直到必填字段有效）

+++

+++ 数据操作

- **设置值**：自动填充值（例如，日期、总计、副本）
- **清除值**：条件更改时删除数据
- **格式**：转换显示格式（货币、电话、日期），而不更改存储值

+++

+++ 验证

- **验证**：自定义验证逻辑，包括跨字段检查和业务规则

+++

+++ 计算

- **数学表达式**：实时计算值（总计、税额、比率）

+++

+++ 用户界面

- **设置焦点**：将焦点移动到特定字段（谨慎使用）
- **设置属性**：动态修改组件属性（占位符、选项等）

+++

+++ 表单控件

- **提交表单**：以编程方式提交表单（仅在通过验证之后）
- **重置表单**：清除并重置为初始状态（使用前确认）
- **保存表单**：另存为草稿供以后使用（长表单，多会话）

+++

+++ 高级

- **调用服务**：调用外部API/服务（句柄加载和错误）
- **添加/删除实例**：管理可重复的部分（例如，依赖项、地址）
- **导航到**：路由到其他表单/页面（导航之前保留数据）
- **在面板之间导航**：控制向导步骤导航并跳过
- **调度事件**：触发集成或分析的自定义事件

+++

## 分步教程：构建智能税务计算器

+++ 教程概述

此示例演示了条件可视性和自动计算。

![显示创建条件规则的规则编辑器界面屏幕截图，该条件规则具有表单字段可见性的When-Then逻辑](/help/edge/docs/forms/assets/rule-editor-1.png)
图：具有智能条件字段的计税表单

您将构建一个表单，该表单：

1. 通过显示相关字段适应用户输入
2. 实时计算值
3. 验证数据以提高准确性

+++

+++ 窗体结构

| 字段名称 | 类型 | 用途 | 行为 |
|-------------------------|---------------|--------------------------------|-----------------------------------------|
| 薪金毛额 | 数字输入 | 用户的年收入 | 触发条件逻辑 |
| 附加扣款 | 数字输入 | 附加扣减额（如果适用） | 仅在薪金> $50,000时可见 |
| 应课税收入 | 数字输入 | 计算值 | 只读，更改时更新 |
| 应付税项 | 数字输入 | 计算值 | 只读，以统一速率计算 |

+++

+++ 业务逻辑

- **规则1：条件显示**

  ```text
  WHEN Gross Salary > 50,000
  THEN Show "Additional Deduction"
  ELSE Hide "Additional Deduction"
  ```

- **规则2：应纳税收入计算**

  ```text
  SET Taxable Income = Gross Salary - Additional Deduction
  (Only when Additional Deduction applies)
  ```

- **规则3：应付税计算**

  ```text
  SET Tax Payable = Taxable Income × 10%
  (Simplified flat rate)
  ```

+++

+++ 第1步：创建基础表单

**目标**：使用所有字段和初始设置构建基本表单。

1. **打开通用编辑器**：
   - 导航到AEM Sites控制台，选择您的页面，单击&#x200B;**编辑**
   - 确保已正确配置[通用编辑器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction.html?lang=zh-Hans)

2. **按此顺序添加表单组件**：
   - 标题(H2)：“计税表单”
   - 数字输入：“薪金毛额”（必需：是，占位符：“输入年薪”）
   - 编号输入：“附加扣款”（必需：否，占位符：“输入附加扣款”）
   - 数字输入：“应纳税收入”（只读：是）
   - 编号输入：“应付税”（只读：是）
   - “提交”按钮：“计税”

3. **配置初始字段属性**：
   - 隐藏“额外扣除”（在“属性”面板中设置为“可见：否”）
   - 将“应纳税收入”和“应付税款”设置为只读：是

![含总薪金、婚姻状况和受抚养子女输入字段的税务计算表单屏幕截图，显示应用规则之前的表单结构](/help/edge/docs/forms/assets/rule-editor2.png)
图：配置了基本组件的初始表单结构

**检查点**：您应该有一个表单，其中包含“Additional Deduction”为隐藏且计算字段为只读的所有必填字段。

+++

+++ 步骤2：添加条件可见性规则

**目标**：仅在总薪金超过$50,000时显示“额外扣减”字段。

1. **选择Gross Salary字段**&#x200B;并单击规则编辑器图标![edit-rules](/help/forms/assets/edit-rules-icon.svg)
2. **创建新规则**：
   - 单击&#x200B;**创建**
   - 将规则类型从“设置值”更改为&#x200B;**“时间”**
3. **配置条件**：
   - 从下拉列表中选择&#x200B;**&quot;大于&quot;**
   - 在数字字段中输入`50000`
4. **设置Then操作**：
   - 从选择操作下拉列表中选择&#x200B;**“显示”**
   - 从表单对象拖动或选择&#x200B;**“附加扣款”**&#x200B;字段
5. **添加Else操作**：
   - 单击&#x200B;**“添加Else部分”**
   - 从选择操作下拉列表中选择&#x200B;**“隐藏”**
   - 选择&#x200B;**“附加扣款”**&#x200B;字段
6. **保存规则**：单击&#x200B;**完成**

>[!NOTE]
>
> 替代方法：通过直接在“Additional Deduction”字段上创建“显示/隐藏”规则，而不是在“Gross Salary”字段上创建“When”规则，可以获得相同的结果。

+++

+++ 第3步：添加计算规则

**目标**：根据用户输入自动计算“应纳税所得”和“应付税款”。

**配置应纳税收入计算**：

1. **选择“应纳税收入”字段**&#x200B;并打开规则编辑器
2. **创建数学表达式**：
   - 单击&#x200B;**创建**→选择&#x200B;**“数学表达式”**
   - 生成表达式：**薪金总额−附加扣减额**
   - 将“薪金总额”拖到第一个字段
   - 选择&#x200B;**&quot;减号&quot;**&#x200B;运算符
   - 将“Additional Deduction”拖到第二个字段
3. **保存**：单击&#x200B;**完成**

**配置应付税计算**：

1. **选择“应付税”字段**&#x200B;并打开规则编辑器
2. **创建数学表达式**：
   - 单击&#x200B;**创建**→选择&#x200B;**“数学表达式”**
   - 生成表达式：**应纳税所得× 10 ÷ 100**
   - 将“应纳税收入”拖到第一个字段
   - 选择&#x200B;**“乘以”**&#x200B;运算符
   - 输入`10`作为数字
   - 单击&#x200B;**“扩展表达式”**
   - 选择&#x200B;**除以“**”运算符
   - 输入`100`作为数字
3. **保存**：单击&#x200B;**完成**

+++

+++ 第4步：测试表单

**通过测试完整流程来验证您的实施**：

1. **预览表单**：在通用编辑器中单击预览模式
2. **测试条件逻辑**：
   - 输入薪金总额= `30000` →“附加扣减额”应保持隐藏
   - 输入薪金总额= `60000`，→应显示“附加扣减额”
3. **测试计算**：
   - 如果薪金总额= `60000`，请输入附加扣减额= `5000`
   - 验证应纳税所得= `55000` (60000 - 5000)
   - 验证应付税= `5500` (55000 × 10%)

![预览表单](/help/edge/docs/forms/assets/rule-editor-form.png)
图：带条件字段和自动计算的已完成税计算器

**成功标准**：表单应动态显示/隐藏字段，并根据用户类型实时计算值。


+++

## 高级：自定义函数

对于内置功能以外的复杂业务逻辑，您可以创建自定义JavaScript功能，以便与规则编辑器无缝集成。

+++ 何时使用自定义函数

**自定义函数的理想方案**：

- **复杂计算**：数学表达式规则中不易表示多步计算
- **特定于业务的验证**：特定于您的组织或行业的自定义验证逻辑
- **数据转换**：格式转换、字符串操作或数据解析
- **外部集成**：调用内部API或第三方服务（具有限制）

**自定义函数的好处**：

- **可重用性**：一次写入，跨多个表单和规则使用
- **可维护性**：易于更新和调试的集中式逻辑
- **性能**：与复杂的规则链相比，优化了JavaScript执行
- **灵活性**：处理标准规则未解决的边缘案例和复杂方案

+++

+++ 创建和实施自定义函数

**文件位置**：必须在Edge Delivery Services项目的`/blocks/form/functions.js`中定义所有自定义函数。

**开发工作流**：

1. **函数设计**
   - 使用描述性、面向操作的函数名称
   - 定义清除参数类型和返回值
   - 谨慎处理边缘用例和无效输入

2. **实施**
   - 写下简洁明了、评论有条的JavaScript
   - 包括输入验证和错误处理
   - 在集成之前独立测试功能

3. **文档**
   - 添加全面的JSDoc注释
   - 包括用法示例和参数描述
   - 记录任何限制或依赖关系

4. **部署**
   - 使用指定的导出导出导出功能导出函数
   - 部署到您的项目存储库
   - 测试之前验证构建已完成

**示例实施**：

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
图：将自定义函数添加到functions.js文件

+++

+++ 在规则编辑器中使用自定义函数

**集成步骤**：

1. **将函数添加到项目**
   - 在您的项目中创建或编辑`/blocks/form/functions.js`
   - 在导出语句中包含您的函数

2. **部署和生成**
   - 将更改提交到存储库
   - 确保构建过程成功完成
   - 允许CDN缓存更新的时间

3. 在规则编辑器中&#x200B;**访问**
   - 打开任何表单组件的规则编辑器
   - 在&#x200B;**选择操作**&#x200B;下拉列表中选择&#x200B;**“函数输出”**
   - 从可用函数列表中选择自定义函数
   - 使用表单字段或静态值配置函数参数

4. **全面测试**
   - 预览表单以验证函数行为
   - 使用包括边缘用例的各种输入组合进行测试
   - 验证对表单加载和交互的性能影响

规则编辑器中的![自定义函数](/help/edge/docs/forms/assets/custom-function-rule-editor.png)
图：在规则编辑器界面中选择并配置自定义函数


**函数使用的最佳实践**：

- **错误处理**：始终包含函数失败的回退行为
- **性能**：配置文件函数具有真实的数据卷
- **安全**：验证所有输入以防止安全漏洞
- **测试**：创建涵盖正常和边缘案例的测试案例

+++


### 自定义函数的静态导入

通用编辑器的规则编辑器支持静态导入，使您能够跨多个文件和表单组织可重用的逻辑。 您可以从其他模块导入函数，而不是将所有自定义函数保存在单个文件(/blocks/form/functions.js)中。
例如：从外部文件导入函数
请考虑以下文件夹结构：

```
      form
      ┣ commonLib
      ┃ ┗ functions.js
      ┣ rules
      ┃ ┗ _form.json
      ┣ form.js
      ┗ functions.js
```

您可以将函数从`commonLib/functions.js`导入主`functions.js`文件，如下所示：

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

### 组织不同Forms中的自定义函数

您可以在单独的文件或文件夹中创建不同的功能集，并根据需要导出它们：

- 如果您希望某些函数仅在特定表单中可用，则可以在表单配置中提供函数文件的路径。

- 如果路径的文本框留空，则规则编辑器默认为从`/blocks/form/functions.js`加载函数

UE![中的](/help/forms/assets/custom-function-in-ue.png){width=50%}自定义函数

在上面的屏幕快照中，自定义函数的路径已添加到自定义函数路径文本框中。 此表单的自定义函数是从指定的文件(`cc_function.js`)加载的。

这样就可以灵活地跨多个表单共享功能或按表单将其隔离。

## 规则开发的最佳实践


+++ 性能优化

- 最大限度地降低规则复杂性；将大型逻辑拆分为小型、重点突出的规则
- 按频率对规则排序（最常见的是第一个）
- 使每个组件的规则集可管理
- 与复制逻辑相比，更喜欢可重用的自定义函数

+++

+++ 用户体验

- 提供明确的验证和内联反馈
- 避免出现不一致的视觉变化；仔细使用显示/隐藏
- 跨设备和布局进行测试

+++

+++ 开发卫生

- 使用边缘用例和已知值进行测试
- 跨浏览器验证
- 在复杂规则背后记录意图，而不仅仅是机制
- 维护大型表单的规则库存
- 对组件和规则使用一致的命名
- 在非生产环境中版本自定义函数和测试

+++

## 常见问题排查


+++ 未触发规则

- 验证组件名称和引用
- 检查执行顺序（从上到下）
- 使用已知值验证条件
- 检查浏览器控制台是否存在阻止错误

+++

+++ 错误行为

- 查看运算符和分组（和/或）
- 单独测试表达式片段
- 确认数据类型（数字与字符串）

+++

+++ 性能问题

- 简化深度嵌套条件
- 配置文件自定义函数
- 将规则内的外部调用最小化
- 使用特定的选择器和引用

+++

+++ 自定义函数问题

- 确认文件路径： `/blocks/form/functions.js`
- 确保命名的导出正确
- 确认内部版本包含您的更改
- 部署后清除浏览器缓存
- 验证参数类型和错误处理

+++

+++ 通用编辑器集成

- 确认已启用规则编辑器扩展
- 选择支持的组件
- 使用支持的浏览器(Chrome、Firefox、Safari)
- 验证您是否具有所需的权限

## 重要限制

>[!IMPORTANT]
>
> 自定义函数约束：
>
> - 不支持静态/动态导入
> - 所有逻辑都必须位于`/blocks/form/functions.js`中
> - 函数必须为同步（无异步/等待或Promise）
> - 浏览器API访问受限

>[!WARNING]
>
> 生产注意事项：
>
> - 在暂存环境中进行全面测试
> - 在部署后监视性能
> - 制定规则问题的回滚计划
> - 考虑慢速网络和低规格设备

## 摘要

通用编辑器中的规则编辑器将静态表单转换为实时适应用户输入的智能、响应式体验。 通过利用条件逻辑、自动计算和自定义业务规则，您可以创建复杂的表单工作流，而无需编写应用程序代码。

**您已学到的关键功能**：

- **条件逻辑**：根据用户输入显示和隐藏字段，以创建集中、相关的体验
- **动态计算**：在用户与表单交互时，自动计算值（税、合计、费率）
- **数据验证**：通过清晰、可操作的反馈消息实施实时验证
- **自定义函数**：使用JavaScript扩展功能以实现复杂的业务逻辑和集成
- **性能优化**：应用最佳实践以进行可维护的高效规则开发

**值已传递**：

- **增强的用户体验**：通过渐进式公开和智能表单流减少认知负担
- **减少了错误**：通过实时验证和引导式输入防止无效提交
- **提高了效率**：自动计算和数据输入以最大限度地减少用户工作量
- **可维护的解决方案**：创建可在您的组织中扩展的可重复使用、有良好记录的规则

**业务影响**：

Forms成为用于数据收集、潜在客户资格鉴定和用户参与的强大工具。 使用规则编辑器，非技术作者可以实施复杂的业务逻辑，在降低开发成本的同时提高表单完成率和数据质量。

+++

## 后续步骤

**推荐的学习路径**：

1. **从基础知识开始**：创建简单的显示/隐藏规则以了解核心概念
2. **教程实践**：使用税务计算器示例作为您自己表单的基础
3. **逐步展开**：随着置信度的增长，添加数学表达式和验证规则
4. **实施自定义函数**：针对专门的业务需求开发JavaScript函数
5. **优化和扩展**：应用性能最佳实践并维护规则文档

**其他资源**：

- [通用编辑器文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction.html?lang=zh-Hans)，了解更广泛的上下文
- 用于启用其他功能的[Extension Manager指南](/help/implementing/developing/extending/extension-manager.md)
- [Edge Delivery Services表单](/help/edge/docs/forms/overview.md)以了解全面的表单开发指导

