---
title: 在自适应表单中创建和添加自定义函数
description: AEM Forms支持自定义函数，这些函数允许用户在规则编辑器中创建和使用自己的函数。
keywords: 添加自定义函数、使用自定义函数、创建自定义函数、在规则编辑器中使用自定义函数。
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: e7ab4233-2e91-45c6-9377-0c9204d03ee9
source-git-commit: 747203ccd3c7e428e2afe27c56e47c3ec18699f6
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 5%

---

# 为基于核心组件的自适应Form创建自定义函数

基于核心组件的自适应Forms通过根据用户输入调整内容和行为来提供动态用户体验。 自定义函数允许开发人员扩展功能，确保表单满足特定要求。 通过集成自定义函数，开发人员可以实施复杂的逻辑、自动化流程并引入符合特定业务需求或用户期望的独特交互。 它确保表单不仅适应不断变化的条件，而且为各种用例提供更加精确和有效的解决方案。
本文会指导您完成使用核心组件为自适应Forms创建自定义函数的步骤。

## 注意事项

* `parameter type`和`return type`不支持`None`。

* 自定义函数列表中不支持的函数包括：
   * 生成器函数
   * 异步/等待函数
   * 方法定义
   * 类方法
   * 默认参数
   * Rest参数

## 创建自定义函数的先决条件

在开始将自定义函数添加到自适应Forms之前，请确保您满足以下条件：

**软件：**

* **纯文本编辑器(IDE)**：虽然任何纯文本编辑器都可以工作，但诸如Microsoft Visual Studio Code之类的集成开发环境(IDE)可提供高级功能，以便于编辑。

* **Git：**&#x200B;管理代码更改需要此版本控制系统。 如果未安装，请从https://git-scm.com下载。


## 创建自定义功能 {#create-custom-function}

创建客户端库以在规则编辑器中调用自定义函数。 有关详细信息，请参阅[使用客户端库](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing)。

创建自定义函数的步骤包括：
1. [创建客户端库](#create-client-library)
1. [将客户端库添加到自适应表单](#use-custom-function)

### 创建客户端库 {#create-client-library}

您可以通过添加客户端库来添加自定义函数。 要创建客户端库，请执行以下步骤：

**克隆存储库**

克隆[AEM Formsas a Cloud Service存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git)：

1. 打开命令行或终端窗口。

1. 导航到要在计算机上存储存储库的所需位置。

1. 运行以下命令以克隆存储库：

   `git clone [Git Repository URL]`

此命令下载存储库并在计算机上创建克隆存储库的本地文件夹。 在本指南中，我们将此文件夹称为[AEMaaCS项目目录]。

**添加客户端库文件夹**

要将新的客户端库文件夹添加到[AEMaaCS项目目录]，请执行以下步骤：

1. 在编辑器中打开[AEMaaCS项目目录]。

   ![自定义函数文件夹结构](/help/forms/assets/custom-library-folder-structure.png)

1. 找到`ui.apps`。
1. 添加新文件夹。 例如，添加名为`experience-league`的文件夹。
1. 导航到`/experience-league/`文件夹并添加`ClientLibraryFolder`。 例如，创建一个名为`customclientlibs`的客户端库文件夹。

   `Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/`

**将文件和文件夹添加到客户端库文件夹**

将以下内容添加到添加的客户端库文件夹：

* .content.xml文件
* js.txt文件
* js文件夹

`Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/experience-league/customclientlibs/`

1. 在`.content.xml`中，添加以下代码行：

   ```javascript
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="cq:ClientLibraryFolder"
   categories="[customfunctionscategory]"/>
   ```

   >[!NOTE]
   >
   > 您可以为`client library folder`和`categories`属性选择任意名称。

1. 在`js.txt`中，添加以下代码行：

   ```javascript
         #base=js
       function.js
   ```
1. 在`js`文件夹中，将javascript文件添加为`function.js`，其中包含自定义函数：

   ```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */
   
    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();
   
    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();
   
    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }
   
    return age;
    }
   ```
1. 保存文件。

![自定义函数文件夹结构](/help/forms/assets/custom-function-added-files.png)

**在filter.xml中包含新文件夹**：

1. 导航到[AEMaaCS项目目录]中的`/ui.apps/src/main/content/META-INF/vault/filter.xml`文件。

1. 打开文件，并在末尾添加以下行：

   `<filter root="/apps/experience-league" />`
1. 保存文件。

![自定义函数筛选器xml](/help/forms/assets/custom-function-filterxml.png)

**将新创建的客户端库文件夹部署到您的AEM环境**

将AEM as a Cloud Service [AEMaaCS项目目录]部署到您的Cloud Service环境。 要部署到Cloud Service环境，请执行以下操作：

1. 提交更改

   1. 使用以下命令在存储库中添加、提交和推送更改：

   ```javascript
       git add .
       git commit -a -m "Adding custom functions"
       git push
   ```

1. 部署更新的代码：

   1. 通过现有的全栈管道触发代码部署。 这会自动构建和部署更新的代码。

如果尚未设置管道，请参阅[上的指南如何为AEM Formsas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline)设置管道。

成功执行管道后，客户端库中添加的自定义函数将在[自适应表单规则编辑器](/help/forms/rule-editor-core-components.md)中变得可用。

### 将客户端库添加到自适应表单{#use-custom-function}

将客户端库部署到Forms CS环境后，请在自适应表单中使用其功能。 在自适应表单中添加客户端库

1. 在编辑模式下打开表单。 要在编辑模式下打开表单，请选择一个表单，然后选择&#x200B;**[!UICONTROL 编辑]**。
1. 打开内容浏览器，然后选择自适应表单的&#x200B;**[!UICONTROL 指南容器]**&#x200B;组件。
1. 单击指南容器属性![指南属性](/help/forms/assets/configure-icon.svg)图标。这将打开“自适应表单容器”对话框。
1. 打开&#x200B;**[!UICONTROL 基本]**&#x200B;选项卡，并从下拉列表中选择&#x200B;**[!UICONTROL 客户端库类别]**&#x200B;的名称（在本例中，选择`customfunctionscategory`）。

   ![正在添加自定义函数客户端库](/help/forms/assets/clientlib-custom-function.png)

   >[!NOTE]
   >
   > 通过在&#x200B;**[!UICONTROL 客户端库类别]**&#x200B;字段中指定逗号分隔的列表，可以添加多个类别。

1. 单击&#x200B;**[!UICONTROL 完成]**。

您可以在自适应表单](/help/forms/rule-editor-core-components.md)的[规则编辑器中使用[JavaScript批注](##js-annotations)的自定义函数。

## 在自适应表单中使用自定义函数

在自适应表单中，您可以在规则编辑器](/help/forms/rule-editor-core-components.md)中使用[自定义函数。 让我们将以下代码添加到JavaScript文件（`Function.js`文件）中，以根据出生日期(YYYY-MM-DD)计算年龄。 创建自定义函数作为`calculateAge()`，它将出生日期作为输入并返回年龄：

```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */

    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();

    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();

    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }

    return age;
    }
```

在上例中，当用户以(YYYY-MM-DD)格式输入出生日期时，将调用自定义函数`calculateAge`并返回年龄。

![规则编辑器中的Calcualte Agae自定义函数](/help/forms/assets/custom-function-calculate-age.png)

让我们预览表单，观察自定义函数如何通过规则编辑器实现：

![在规则编辑器表单预览中计算Agae自定义函数](/help/forms/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> 您可以引用以下[自定义函数](/help/forms/assets//customfunctions.zip)文件夹。 使用[包管理器](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager)在AEM实例中下载并安装此文件夹。

## 自定义函数的功能

AEM Forms中的自定义函数为扩展和个性化表单的功能提供了可靠的解决方案。 您可以使用自定义函数来满足组织的特定需求。

这些函数支持各种功能，包括使用特定字段、使用全局字段和异步操作，以及合并缓存机制。 这种灵活性确保表单能够适应复杂的需求，并提供高效、量身定制的用户体验。 利用这些高级功能，您可以增强表单交互并优化性能，使AEM表单功能更强、响应更灵敏。

让我们深入了解一下自定义函数的功能。

### 自定义函数中的异步支持 {#support-of-async-functions}

您可以使用自定义函数在规则编辑器中实施异步函数。 有关如何执行此操作的指导，请参阅文章[在自适应表单中使用异步函数](/help/forms/using-async-funct-in-rule-editor.md)。

### 自定义函数支持的字段和全局范围对象 {#support-field-and-global-objects}

字段对象是指表单中的单个组件或元素，例如文本字段和复选框。 全局对象包含只读变量，例如表单实例、目标字段实例以及在自定义函数中修改表单的方法。

>[!NOTE]
>
> `param {scope} globals`必须是最后一个参数，它不会显示在自适应表单的规则编辑器中。

有关范围对象的详细信息，请参阅自定义函数中的[范围对象](/help/forms/custom-function-core-component-scope-function.md)一文。

### 自定义函数中的缓存支持

自适应Forms在规则编辑器中检索自定义函数列表时，为自定义函数实施缓存以增强响应时间。 `error.log`文件中显示一条消息，名称为`Fetched following custom functions list from cache`。

支持缓存的![自定义函数](/help/forms/assets/custom-function-cache-error.png)

如果修改了自定义函数，缓存将失效，并且会进行解析。

## 疑难解答

* 如果包含自定义函数代码的JavaScript文件出错，则自定义函数不会列在自适应表单的规则编辑器中。 要检查自定义函数列表，您可以导航到`error.log`文件以查找错误。 如果出现错误，自定义函数列表显示为空：

  ![错误日志文件](/help/forms/assets/custom-function-list-error-file.png)

  如果没有错误，则会获取自定义函数并显示在`error.log`文件中。 `error.log`文件中显示一条消息，名称为`Fetched following custom functions list`：

  使用正确的自定义函数![错误日志文件](/help/forms/assets/custom-function-list-fetched-in-error.png)

## 下一步

现在，让我们查看基于核心组件的自适应表单的各种[自定义函数示例](/help/forms/custom-function-core-components-use-cases.md)。

## 另请参阅

{{see-also-rule-editor}}
