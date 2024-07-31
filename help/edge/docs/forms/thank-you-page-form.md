---
title: 提交表单后显示自定义感谢消息
description: 了解如何配置 Forms Block 的感谢页面和重定向，优化用户体验并简化用户历程。
feature: Edge Delivery Services
exl-id: e6c66b22-dc52-49e3-a920-059adb5be22f
role: Admin, Architect, Developer
source-git-commit: 4356fcc73a9c33a11365b1eb3f2ebee5c9de24f0
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 51%

---

# 提交表单后显示自定义感谢消息

在用户提交表单后，通过感谢消息提供无缝体验至关重要。 它不仅证实成功提交了申请，而且还提高了用户满意度，并指导他们进一步开展工作。

* **感谢信息**：感谢信息是用户体验的基石，可在增强品牌标识的同时提供保证和传达重要信息。 它是对用户行为的直接肯定，可培养用户的完成感和满足感。

* **重定向**：重定向在引导用户前往相关目标、优化参与度并最终提高转化率方面发挥着关键作用。通过无缝引导用户进入历程的下一步，重定向可确保流畅的导航体验。例如，在收集初始详细信息后，将用户重定向到支付页面。

Adaptive Forms Block 的默认行为是在提交时显示感谢信息。成功提交表单时，消息会显示在表单顶部。

![默认感谢信息](/help/edge/assets/thank-you-message.png)

但是，您可以灵活地定制此体验以满足您的特定需求。选项包括：

* 提交表单后显示自定义感谢消息
* 在提交后将用户重定向到另一个页面以供进一步操作

>[!NOTE]
>
> 您可以参考以下[查询电子表格](/help/edge/docs/forms/assets/enquiry.xlsx)，根据您的要求自定义感谢邮件。

## 配置自定义感谢消息

如果您希望在成功提交表单时显示个性化的感谢消息，则可以配置电子表格以显示该消息。

请按照以下步骤为您的 Adaptive Forms Block 配置自定义感谢消息：

1. 转到 Microsoft SharePoint 或 Google Workspace 上的 Edge Deliver 项目文件夹并打开电子表格。
1. 在电子表格中`submit`字段类型的`value`列中添加自定义的感谢消息。

   ![自定义感谢消息](/help/edge/docs/forms/assets/thankyou-custommessage.png)

   例如，在`submit`字段类型的`value`列中添加`Submission Successful!`消息。

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content)预览和发布工作表。

   ![自定义感谢消息](/help/edge/docs/forms/assets/customized-thank-you-message.png)

## 提交后将用户重定向到另一个页面

提交表单后将用户重定向到另一个页面，可以通过提供相关信息、确认操作并引导用户获得期望的结果来增强用户体验。例如，

* 用户填写购买表单后，他们将被重定向到支付页面以安全地完成交易。
* 提交活动或网络研讨会的注册表单后，用户将被重定向到显示活动详细信息（例如日期、时间和地点）的确认页面。

请按照以下步骤将用户重定向到其他页面：

1. 转到 Microsoft SharePoint 或 Google Workspace 上的 Edge Deliver 项目文件夹并打开电子表格。
1. 在电子表格中将`submit`字段类型的URL粘贴到`value`列中，以便在成功提交表单时重定向用户。
要将页面重定向到其他页面，请使用[Edge Delivery文档](https://www.aem.live/docs/)页面URL。

   ![感谢您重定向URL](/help/edge/docs/forms/assets/thankyou-redirecturl.png)

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content)预览和发布工作表。

   ![重定向感谢消息](/help/edge/docs/forms/assets/thankyou-redirectpage.gif)

您还可以创建新文档文件并在`submit`字段类型的`value`列中添加其预览URL。

在用户提交表单后，请务必提供清晰的感谢信息。 它确认提交成功，并提高了用户满意度。

## 另请参阅

{{see-more-forms-eds}}

<!--
## Configuring a custom thank you message

The default behavior of Adaptive Forms Block is to display the following thank you message on submission. The message is displayed on the top of the form. 

![default thank you message](/help/edge/assets/thank-you-message.png)


Follow the below steps to configure a custom thank you message for your Adaptive Forms Block:

1. Access your AEM Project on your local machine or GitHub repository.

2. Navigate to [AEM Project Folder]\blocks\form\submit.js file for editing.

3. Locate the following code 

    ```JavaScript

        thankYouMessage.innerHTML = payload?.body?.thankYouMessage || 'Thanks for your submission';

    ```

4. Replace the default message with your custom message. For example, 


    ```JavaScript

        thankYouMessage.innerHTML = payload?.body?.thankYouMessage || 'Your submission has been received and noted.';

    ```


1. Save the file. Commit the updated file to your GitHub Repository. Now, when you submit a form, the custom thank you message is displayed. For example,

![Custom thank you message](/help/edge/assets/custom-thank-you-message.png)

* **Thank you message**: A thank you message is a cornerstone of user experience, offering reassurance and conveying important information while reinforcing brand identity. It serves as a direct acknowledgment of the user's action, fostering a sense of completion and satisfaction.

* **Redirect**: A redirect plays a pivotal role in steering users towards relevant destinations, optimizing engagement, and ultimately boosting conversion rates. By seamlessly guiding users to the next step in their journey, a redirect ensures a smooth navigation experience. For example, redirecting user to payments page after collecting initial details. 

In the Adaptive Forms Block, the default behavior is to display a thank you message. However, you have the flexibility to tailor this experience to meet your specific needs. Options include:

* [Configuring a custom thank you message to align with your brand and communication goals](#configuring-the-thank-you-page-and-message) 
* [Redirecting users to another page post-submission for further action](#redirect-users-to-another-page-post-submission)

## Redirect users to another page post-submission

Redirecting a user to another page after form submission can enhance user experience by providing relevant information, confirming actions, and guiding users towards desired outcomes. For example, 

* after a user completes a purchase form, they are redirected to a payment page to complete the transaction securely. 
* upon submitting a registration form for an event or webinar, users are redirected to a confirmation page displaying event details, such as date, time, and location.

To redirect the "thankyou" page to a different page, use the [website redirects](https://www.aem.live/docs/redirects) spreadsheet. 





1. Access your AEM Edge Delivery project folder on Microsoft SharePoint or Google Workspace.
1. Create a Microsoft Word or Google Docs file named "thankyou" within your project directory.
1. Add your thank you message to the "thankyou" file. </br>
   
    ![Example thank you page](/help/edge/assets/sample-thankyou-page.png) 

1. Use AEM Sidekick to preview and publish the "thankyou" file.

 Your Adaptive Forms Block displays the "thankyou" page on form submission. 

## Redirect users to another page post-submission

By default, the Adaptive Forms Block redirects the users to the "thankyou" page. To redirect users to a page other than the default "thankyou" page, you have two options: 

* [Replace the "thankyou" page with a different page](#replace-the-existing-thankyou-page) 
* [Use website redirects for "thankyou" page redirection](#use-website-redirects-for-thankyou-page-redirection) 

### Replace the "thankyou" page

1. Open the "[EDS Project]/blocks/form/form.js" file for editing.
1. Change the `thankyou` page in the following line to page of your choice:

    ```JavaScript

    window.location.href = form.dataset?.redirect || 'thankyou';

    ```

    For example,

    ```JavaScript

    window.location.href = form.dataset?.redirect || 'payment';
        
    ```
    
    >[!NOTE]
    >
    > Ensure that a page with the same name exists in your Edge Delivery Services project folder on either Microsoft SharePoint or Google Workspace. If the page does not exist, proceed to create and publish it.  

1. Proceed to check in the updated 'form.js' folder and its underlying files to your Edge Delivery Services project on GitHub. This update ensures that the form now redirects to the updated page as specified.

1. Ensure that the page exists in your EDS project folder and publish it.


### Use website redirects for "thankyou" page redirection

Redirecting a user to another page after form submission can enhance user experience by providing relevant information, confirming actions, and guiding users towards desired outcomes. For example, 

* after a user completes a purchase form, they are redirected to a payment page to complete the transaction securely. 
* upon submitting a registration form for an event or webinar, users are redirected to a confirmation page displaying event details, such as date, time, and location.

To redirect the "thankyou" page to a different page, use the [website redirects](https://www.aem.live/docs/redirects) spreadsheet. 



## See also

{{see-more-forms-eds}}