---
title: 如何在可视规则编辑器中使用异步函数调用？
description: 可视规则编辑器中的异步函数调用
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
source-git-commit: f6e1de0c2cc2c056b3bfcea6ce5d7aaed041f6f8
workflow-type: tm+mt
source-wordcount: '1437'
ht-degree: 1%

---


# 在基于核心组件的自适应表单中使用异步函数

自适应Forms](/help/forms/rule-editor-core-components.md)中的[规则编辑器支持异步功能，允许您集成和管理需要等待外部进程或数据检索的操作，而不会中断用户与表单的交互。

## 哪些因素决定了使用异步或同步功能？

有效管理用户交互对于创建流畅的体验至关重要。 处理操作的两种常用方法是同步和异步函数。

**同步功能**&#x200B;逐个执行任务，导致应用程序等待每个操作完成后再继续。 这可能会导致延迟和用户体验减少，尤其是在任务需要等待外部资源（如文件上传或数据获取）时。

例如，考虑用户上传图像的情况，整个表单暂停，等待上传完成。 此暂停使用户无法与其他字段交互，从而导致挫折感和延迟。 在等待图像处理时，如果输入的信息离开或失去耐心，则可能会丢失这些信息，从而使体验变得繁琐和低效。

另一方面，**异步函数**&#x200B;允许同时运行任务。 这意味着，在执行后台进程时，用户可以继续与应用程序交互。 异步操作增强了响应能力，使用户能够立即收到反馈并保持参与而不出现中断。

相反，通过异步方法，用户可以在后台上传图像，同时继续无缝填写表单的其余部分。 该界面保持响应式，允许实时更新并在上传过程中提供即时反馈。 它增强了用户参与度，确保畅通无阻的体验。

![异步和同步函数](/help/forms/assets/sync-async.png){align=center}

## 为自适应Forms实施异步函数

您可以在规则编辑器中使用以下规则类型为自适应Forms实施异步函数：

* [异步函数调用](#using-asynchronous-function-calls-in-the-visual-rule-editor)
* [函数输出](#how-to-use-function-output-rule-type)

## 如何使用异步函数调用规则类型？

<span class="preview">这是一项预发布功能，可通过我们的[预发布渠道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features)访问。</span>

您可以为异步操作编写[自定义函数](/help/forms/custom-function-core-component-create-function.md)，并在规则编辑器中使用&#x200B;**[!UICONTROL 异步函数调用]**&#x200B;规则类型配置异步函数。

### 通过用例探索异步函数调用规则类型

考虑用户输入一次性密码(OTP)的网站上的注册表。 只有在输入正确的OTP后，才会显示用于添加用户详细信息的面板。 如果OTP不正确，面板将保持隐藏状态，屏幕上将显示一条错误消息。

![登录表单](/help/forms/assets/rule-editor-login-form.png) {width-50%}

在注册表单中，当用户单击&#x200B;**Confirm**&#x200B;按钮时，将异步调用`matchOTP()`函数以验证输入的OTP。 `matchOTP()`函数是作为[自定义函数](/help/forms/custom-function-core-component-create-function.md)实现的。 使用规则编辑器中的&#x200B;**[!UICONTROL 异步函数调用]**&#x200B;规则类型，您可以在自适应表单的规则编辑器中配置`matchOTP()`函数。 您还可以在规则编辑器中实施成功和失败回调。

下图说明了使用&#x200B;**[!UICONTROL 异步函数调用]**&#x200B;规则类型为自适应Forms调用异步函数的步骤：

![用于添加异步函数的工作流](/help/forms/assets/workflow-to-add-async-func.png){width=50%， align=center}

### 1.在JS文件中为异步操作编写自定义函数

>[!NOTE]
>
> * 当您选择&#x200B;**异步函数调用**&#x200B;规则类型时，表单的规则编辑器仅显示返回类型为`Promise`的函数。
> * 要了解如何创建自定义函数，请参阅标题为[基于核心组件的自适应表单的自定义函数](/help/forms/custom-function-core-component-create-function.md)的文章。

`matchOTP()`函数作为自定义函数实现。 以下代码会添加到自定义函数的JS文件中：

```JavaScript
/**
 * generates the otp for success use case
 * @param {string} otp
 * @return {PROMISE}
 */
function matchOTP(otp) {
     return new Promise((resolve, reject) => {
        // Perform some asynchronous operation here
         asyncOperationForOTPMatch(otp, (error, result) => {
            if (error) {
                // On failure, call reject(error)
                reject(error);
            } else {
                // On success, call resolve(result)
                resolve(result);
            }
        });
    });
}

/**
 * generates the otp
 */
function asyncOperationForOTPMatch(otp, callback) {
    setTimeout(() => {
        if(otp === '111') {
            callback( null, {'valid':'true'});    
        } else {
            callback( {'valid':'false'}, null);
        }
    }, 1000);
}
```

代码定义一个函数`matchOTP()`，该函数生成用于异步验证一次性密码(OTP)的promise。 它使用函数`asyncOperationForOTPMatch()`来模拟OTP匹配过程。 该函数检查提供的OTP是否等于`111`。 如果输入的OTP正确，它将使用null为错误调用回调，并使用一个对象指示OTP有效`({'valid':'true'})`。如果OTP无效，它将使用错误对象`({'valid':'false'})`为结果调用null。

### 2.在规则编辑器中配置异步函数

执行以下步骤以在规则编辑器中配置异步函数：

1. [创建规则以使用Async Function调用规则类型使用异步函数](#21-create-a-rule-to-use-asynchronous-function-using-the-async-function-call-rule-type)
1. [实施异步函数的回调](#22-implement-the-callbacks-for-asynchronous-function)

#### 2.1创建规则以使用Async Function调用规则类型来使用异步函数

要创建规则以使用异步操作，请使用&#x200B;**[!UICONTROL 异步函数调用]**&#x200B;规则类型，请执行以下步骤：

1. 在创作模式下打开自适应表单，选择一个表单组件，然后选择&#x200B;**[!UICONTROL 规则编辑器]**&#x200B;以打开规则编辑器。
1. 选择&#x200B;**[!UICONTROL 创建]**。
1. 在规则的&#x200B;**When**&#x200B;部分中为单击按钮创建条件。 例如，单击&#x200B;**When[Confirm]**。
1. 在&#x200B;**Then**&#x200B;部分中，从&#x200B;**选择操作**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 异步函数调用]**。
当您选择**[!UICONTROL 异步函数调用]**，并且返回类型为`Promise`的函数出现时。
1. 从列表中选择异步函数。 例如，选择`matchOTP()`函数，其回调将显示为`Add success callback`和`add failure callback`。
1. 现在，选择&#x200B;**[!UICONTROL Input]**&#x200B;绑定。 例如，选择&#x200B;**[!UICONTROL 输入]**&#x200B;作为`Form Object`并将其与`OTP`字段进行比较。

下面的屏幕截图显示了规则：

![规则类型](/help/forms/assets/asyn-function-rule-type.png)

现在，您可以继续为`matchOTP`函数实施回调： `Success`和`Failure`。

#### 2.2实施异步函数的回调

使用可视规则编辑器对异步函数实施成功和失败回调方法。

**为`Add Success callback`方法创建规则**

如果OTP与值`111`匹配，让我们创建一个规则以显示`userdetails`面板。

1. 单击&#x200B;**[!UICONTROL 添加成功回调]**。
1. 单击&#x200B;**[!UICONTROL 添加语句]**&#x200B;以创建规则。
1. 在规则的&#x200B;**When**&#x200B;部分中创建条件。
1. 选择&#x200B;**[!UICONTROL 函数输出]** > **[!UICONTROL 获取事件有效负载]**。

   >[!NOTE]
   >
   > **[!UICONTROL 获取事件有效负载]**&#x200B;函数检索与特定事件关联的数据以动态管理用户交互。

1. 从&#x200B;**Input**&#x200B;部分中选择其相应的绑定。 例如，选择&#x200B;**[!UICONTROL 字符串]**&#x200B;并输入`valid`。 将输入的字符串与`true`进行比较。
1. 在&#x200B;**Then**&#x200B;部分中，从&#x200B;**选择操作**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 显示]**。 例如，显示`userdetails`面板。
1. 单击&#x200B;**[!UICONTROL 添加语句]**。
1. 从&#x200B;**选择操作**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 隐藏]** 例如，隐藏`error message`文本框。
1. 单击&#x200B;**[!UICONTROL 完成]**。

![成功调用](/help/forms/assets/rule-editor-success-callback.png){width=50%， height=50%}

请参阅下面的屏幕截图，其中用户以`111`身份进入OTP，单击`Confirm`按钮时将显示`User Details`面板。

![成功](/help/forms/assets/success.gif)

**为`Add Failure callback`方法创建规则**

让我们创建一个规则，以在OTP与值`111`不匹配时显示失败消息。

1. 单击&#x200B;**[!UICONTROL 添加失败回调]**。

1. 单击&#x200B;**[!UICONTROL 添加语句]**&#x200B;以创建规则。
1. 在规则的&#x200B;**When**&#x200B;部分中创建条件。
1. 选择&#x200B;**[!UICONTROL 函数输出]** > **[!UICONTROL 获取事件有效负载]**。
1. 从&#x200B;**Input**&#x200B;部分中选择其相应的绑定。 例如，选择&#x200B;**[!UICONTROL 字符串]**&#x200B;并输入`valid`。 将输入的字符串与`false`进行比较。
1. 在&#x200B;**Then**&#x200B;部分中，从&#x200B;**选择操作**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 显示]**。 例如，显示`error message`文本框。
1. 单击&#x200B;**[!UICONTROL 添加语句]**。
1. 从&#x200B;**选择操作**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 隐藏]** 例如，隐藏`userdetails`面板。
1. 单击&#x200B;**[!UICONTROL 完成]**。

![失败回调方法](/help/forms/assets/rule-editor-failure-callback.png){width=50%， height=50%}

请参阅下面的屏幕截图，其中用户以`123`身份进入OTP，单击`Confirm`按钮时将显示错误消息。

![失败](/help/forms/assets/failure.gif)

下面的屏幕快照显示了使用&#x200B;**[!UICONTROL 异步函数调用]**&#x200B;实现异步函数的完整规则：

用于异步函数调用的![规则](/help/forms/assets/rule-editor-async-callbacks.png)

您还可以通过单击&#x200B;**[!UICONTROL 编辑成功回调]**&#x200B;和&#x200B;**[!UICONTROL 编辑失败回调]**&#x200B;来编辑回调。

## 如何使用函数输出规则类型？

您还可以使用同步函数间接调用异步函数。 在自适应表单的规则编辑器中使用&#x200B;**[!UICONTROL 函数输出]**&#x200B;规则类型执行同步函数。

查看以下代码，了解如何使用&#x200B;**[!UICONTROL 函数输出]**&#x200B;规则类型调用异步函数：

```javascript
    
    async function asyncFunction() {
    const response = await fetch('https://petstore.swagger.io/v2/store/inventory');
    const data = await response.json();
    return data;
    }

    /**
    * callAsyncFunction
    * @name callAsyncFunction callAsyncFunction
    */
    function callAsyncFunction() {
    asyncFunction()
        .then(responseData => {
        console.log('Response data:', responseData);
        })
        .catch(error => {
         console.error('Error:', error);
    });
}
```

在上述示例中，asyncFunction函数是`asynchronous function`。 它通过向`https://petstore.swagger.io/v2/store/inventory`发出`GET`请求来执行异步操作。 它使用`await`等待响应，使用`response.json()`将响应正文解析为JSON，然后返回数据。 `callAsyncFunction`函数是一个同步自定义函数，它调用`asyncFunction`函数并在控制台中显示响应数据。 虽然`callAsyncFunction`函数是同步的，但它调用异步asyncFunction函数并使用`then`和`catch`语句处理其结果。

要查看其是否有效，让我们添加一个按钮，并为单击按钮时调用异步函数的按钮创建规则。

![为异步函数创建规则](/help/forms/assets/rule-for-async-funct.png){width=50%}

请参阅下面控制台窗口的屏幕截图，以演示当用户单击`Fetch`按钮时，将调用自定义函数`callAsyncFunction`，进而调用异步函数`asyncFunction`。 在控制台窗口中Inspect以查看对单击按钮的响应：

![控制台窗口](/help/forms/assets/async-custom-funct-console.png)

## 另请参阅

{{see-also-rule-editor}}