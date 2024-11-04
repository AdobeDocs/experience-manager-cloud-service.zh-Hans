---
title: 如何基于核心组件创建自适应表单的自定义提交操作？
description: 了解如何为自适应Forms创建自定义提交操作，以便在使用自定义提交操作提交数据之前处理数据。
feature: Adaptive Forms, Core Components
role: User, Developer
level: Intermediate
source-git-commit: b1d5e210d84ad1443b30e4b166f52da51a182b09
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 4%

---


# 创建自适应Forms（核心组件）的自定义提交操作

提交操作允许用户为从表单捕获的数据选择目标，并定义要在表单提交上执行的附加功能。 AEM表单支持多个[现成提交操作(OOTB)](/help/forms/configure-submit-actions-core-components.md)，例如发送电子邮件或将数据保存到SharePoint或OneDrive。

您还可以创建自定义提交操作以添加[现成选项](/help/forms/configure-submit-actions-core-components.md#select-and-configure-a-submit-action-for-an-adaptive-form-select-and-configure-submit-action)中未包含的功能。 例如，将表单数据与第三方应用程序集成或根据用户输入触发个性化短信通知。

<!-- ![Custom Submit Image](/help/forms/assets/custom-submit-action-hero-image.png)
-->

## 先决条件

在开始为自适应Forms创建第一个自定义提交操作之前，请确保您满足以下条件：

* **纯文本编辑器(IDE)**：虽然任何纯文本编辑器都可以工作，但诸如Microsoft Visual Studio Code之类的集成开发环境(IDE)可提供高级功能，以便于编辑。

* **Git**：管理代码更改需要此版本控制系统。 如果未安装，请从https://git-scm.com下载。

## 为表单创建您的第一个自定义提交操作

下图描述了为自适应表单创建自定义提交操作的步骤：

![自定义提交操作工作流](/help/forms/assets/custom-submit-action-workflow.png){width=50%， height-50%}

### 克隆AEM as a Cloud Service Git存储库。

1. 打开命令行并选择要存储AEM as a Cloud Service存储库的目录，如`/cloud-service-repository/`。

1. 运行以下命令以克隆存储库：

   ```
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<app-id>/
   ```
   **在何处查找此信息？**

   有关查找这些详细信息的逐步说明，请参阅Adobe Experience League文章“[访问Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git)”。

   **您的项目已准备就绪！**

   当命令成功完成时，您会看到在本地目录中创建了一个新文件夹。 此文件夹以您的应用程序（例如，app-id）命名。 此文件夹包含从AEM as a Cloud Service Git存储库下载的所有文件和代码。 您可以在`archetype.properties`文件中找到AEM项目的`<appid>`。

   ![原型属性](/help/forms/assets/custom-submit-action-archetype-app-id.png)

   在本指南中，我们将此文件夹称为`[AEMaaCS project directory]`。

## 添加新提交操作

1. 在编辑器中打开存储库文件夹。

   ![克隆的存储库](/help/forms/assets/custom-submit-action-clone-repo.png)

1. 导航到`[AEMaaCS project directory]`中的以下目录：

   ```
   /ui.apps/src/main/content/jcr_root/apps/<app-id>/
   ```
   **重要信息**：将`<app-id>`替换为您的实际应用程序ID。

1. 为自定义提交操作创建新文件夹，并为它指定您选择的名称。 例如，将文件夹命名为`customsubmitaction`。

   ![创建自定义提交操作文件夹](/help/forms/assets/custom-submit-action-create-folder.png)

1. 导航到添加的自定义提交操作目录。

   在您的`[AEMaaCS project directory]`中，导航到以下路径：

   `/ui.apps/src/main/content/jcr_root/apps/<app-id>/customsubmitaction/`

   `Important`：替换 <app-id> 以及实际的应用程序ID。

1. 创建新的配置文件。
在`customsubmitaction`文件夹中，创建一个名为`.content.xml`的新文件。

   ![创建配置文件](/help/forms/assets/custom-submit-action-create-config-folder.png)

1. 打开此文件并粘贴以下内容，将`[customsubmitaction]`替换为提交操作的名称

   ```
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
   jcr:description="[customsubmitaction]"
   jcr:primaryType="sling:Folder"
   
   guideComponentType="fd/af/components/guidesubmittype"
   guideDataModel="basic,xfa,xsd"
   submitService="[customsubmitaction]"/>
   ```

   例如，将`[customsubmitaction]`替换为您自定义的提交操作名称`Custom Submit Action`。

   ![创建自定义提交操作配置文件](/help/forms/assets/custom-submit-action-config-file.png)

   >[!NOTE]
   >
   > 记住[customsubmitaction]的名称，因为在创作表单时，`Submit action`下拉列表中会显示相同的名称。


**在`filter.xml`**&#x200B;中包含新文件夹

1. 导航到[AEMaaCS项目目录]中的`/ui.apps/src/main/content/META-INF/vault/filter.xml`文件。

1. 打开文件，并在末尾添加以下行：

   ```
   <filter root="/apps/<app-id>/[customsubmitaction-folder]"/>
   ```
   例如，添加以下代码行以在`filter.xml`文件中添加`customsubmitaction`文件夹：

   ```
   <filter root="/apps/wknd/customsubmitaction"/>
   ```

   ![在filter.xml中添加已创建的文件夹](/help/forms/assets/custom-submit-action-filter-xml.png)

1. 保存更改。

### 为添加的提交操作实施服务。

1. 导航到`[AEMaaCS project directory]`中的以下目录：
   `/core/src/main/java/com/<app-id>/core/service/`
   `Important`：替换 <app-id> 以及实际的应用程序ID。
1. 创建新的Java文件以便为添加的提交操作实施服务。 例如，添加新的Java文件作为`CustomSubmitService.java`。

   ![自定义提交操作文件夹](/help/forms/assets/custom-submit-action-custom-submit-folder.png)

1. 打开此文件并添加用于自定义提交操作实施的代码。

   例如，以下Java代码是一个OSGi服务，它通过记录提交的数据来处理表单提交并返回状态`OK`。 在`CustomSubmitService.java`文件中添加以下代码：

   ```
   package com.wknd.core.service;
   
   import com.adobe.aemds.guide.model.FormSubmitInfo;
   import com.adobe.aemds.guide.service.FormSubmitActionService;
   import java.util.HashMap;
   import java.util.Map;
   import org.osgi.service.component.annotations.Component;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   
       @Component(
       service = FormSubmitActionService.class,
       immediate = true
           )
       public class CustomSubmitService implements FormSubmitActionService {
   
       private static final String serviceName = "Custom Submit Action";
   
       private static Logger log = LoggerFactory.getLogger(CustomSubmitService.class);
   
       @Override
       public String getServiceName() {
       return serviceName;
       }
   
       @Override
       public Map<String, Object> submit(FormSubmitInfo formSubmitInfo) {
       String data = formSubmitInfo.getData();
       log.info("Using custom submit action service, [data] --> " + data);
       Map<String, Object> result = new HashMap<>();
       result.put("status", "OK");
       return result;
        }
       }
   ```

   ![自定义提交操作服务](/help/forms/assets/custom-submit-action-service.png)

1. 保存更改。

### 部署代码。

**为本地开发环境部署代码**

* 将AEM as a Cloud Service `[AEMaaCS project directory]`部署到本地开发环境，以尝试在本地计算机上执行新的提交操作。 要部署到本地开发环境，请执行以下操作：

   1. 确保您的本地开发环境已启动并正在运行。 如果尚未设置本地开发环境，请参阅[为AEM Forms设置本地开发环境](/help/forms/setup-local-development-environment.md)指南。

   1. 打开终端窗口或命令提示符。

   1. 导航到`[AEMaaCS project directory]`。

   1. 运行以下命令：

      ```
      mvn -PautoInstallPackage clean install
      ```
      ![本地部署](/help/forms/assets/custom-submit-action-local-deployment.png)

**部署Cloud Service环境的代码**

* 将AEM as a Cloud Service `[AEMaaCS project directory]`部署到您的Cloud Service环境。 要部署到Cloud Service环境，请执行以下操作：

   1. 提交更改：

      添加新的自定义提交操作配置后，使用清除的Git消息提交更改。 （例如，“添加了新自定义提交操作”）。

   1. 部署更新的代码：

      通过[现有的全栈管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline)触发代码部署。 它通过新的自定义提交操作支持自动构建和部署更新的代码。

      如果尚未设置管道，请参阅[上的指南如何为AEM Formsas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline)设置管道。

      ![云部署](/help/forms/assets/custom-submit-action-cloud-deployment.png)

      **如何确认安装？**

      成功构建项目后，在创作表单时，自定义提交操作将显示在`Submit action`下拉列表中。

      ![自定义提交操作下拉列表](/help/forms/assets/custom-submit-action-drop-down-list.png)

  现在，您的环境已准备好在创作表单时使用添加的自定义提交操作。

### 使用新添加的提交操作预览自适应表单

1. 登录到您的AEM Formsas a Cloud Service实例。
1. 转到&#x200B;**Forms** > **Forms和文档**。

   ![Forms和文档](/help/forms/assets/custom-submit-action-fnd.png)

1. 选择自适应表单并单击&#x200B;**编辑**。 表单将在编辑模式下打开。

   ![编辑表单](/help/forms/assets/custom-submit-action-edit-af.png)

1. 打开内容浏览器，然后选择自适应表单的&#x200B;**[!UICONTROL 指南容器]**&#x200B;组件。
1. 单击指南容器属性![指南属性](/help/forms/assets/configure-icon.svg)图标。这将打开“自适应表单容器”对话框。
1. 单击&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡。
1. 从&#x200B;**[!UICONTROL 提交操作]**&#x200B;下拉列表中选择提交操作。 例如，选择提交操作作为`Custom Submit Action`。

   ![自定义提交表单](/help/forms/assets/custom-submit-action-select-submit-action.png)

1. 填写并提交表单。

   ![提交表单](/help/forms/assets/custom-submit-action-submit-form.png)

   ![感谢消息](/help/forms/assets/custom-submit-action-thankyou-msg.png)

   成功提交表单后，您可以检查&#x200B;**Adobe Experience Manager Web控制台配置**&#x200B;以验证本地开发环境中自定义提交操作的操作。
1. 转到 `http://<host>:<port>/system/console/configMgr`.

1. 导航到`http://<host>:<port>/system/console/slinglog`上的&#x200B;**Adobe Experience Manager Web控制台日志支持**。

   ![ConfigMgr](/help/forms/assets/custom-submit-action-sling-log.png)

1. 单击`logs/error.log`选项。
   ![打开error.log文件](/help/forms/assets/custom-submit-action-error-log.png)

1. 打开`error.log`文件以查看数据是否已附加到该文件。

   ![错误。日志文件](/help/forms/assets/custom-submit-action-form-data-display.png)

   >[!NOTE]
   >
   > 要查看AEM as a Cloud Service环境中的错误日志，您可以使用Splunk。

<!--
## Best practices

 * It is recommended to use the OSGi service approach for creating a custom submit action, as it is faster than the AEM servlet approach. 

## Next steps
-->

## 相关文章

{{af-submit-action}}


<!-- The [Adaptive Forms Core Components](https://github.com/adobe/aem-core-forms-components) repository includes a sample folder, `customsubmission/logsubmit`, to simplify the process of adding new custom submit actions. It also provides the Java service implementation for the `logsubmit` custom submit action, named `CustomAFSubmitService`.java. These resources are available on GitHub. -->