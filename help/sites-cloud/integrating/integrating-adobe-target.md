---
title: 与 Adobe Target 集成
description: '与 Adobe Target 集成 '
feature: 管理
role: 管理员
translation-type: tm+mt
source-git-commit: 69c865dbc87ca021443e53b61440faca8fa3c4d4
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 2%

---


# 与 Adobe Target 集成{#integrating-with-adobe-target}

作为Adobe Marketing Cloud的一部分，Adobe Target允许您通过在所有渠道中进行定位和衡量来提高内容相关性。 将Adobe Target和AEM作为Cloud Service集成需要：

* 使用触屏UI在AEM中创建目标配置作为Cloud Service（需要IMS配置）。
* 在[Adobe启动](https://docs.adobe.com/content/help/en/launch/using/intro/get-started/quick-start.html)中添加并配置Adobe Target作为扩展。

Adobe启动是管理AEM页面（JS库/标记）中Analytics和目标的客户端属性所必需的。 尽管如此，“体验定位”需要与Launch集成。 对于导出到目标的体验片段，您只需要Adobe Target配置和IMS。

>[!NOTE]
>
>Adobe Experience Manager作为没有现有目标帐户的Cloud Service客户，可以请求访问目标 Foundation Pack for Experience Cloud。 Foundation Pack提供对目标的批量限制使用。

## 创建Adobe Target配置{#create-configuration}

1. 导航到&#x200B;**工具** → **Cloud Services**。
   ![导](assets/cloudservice1.png "航")
2. 选择&#x200B;**Adobe Target**。
3. 选择&#x200B;**创建**按钮。
   ![创](assets/tenant1.png "建")
4. 填写详细信息（请参阅下文），然后选择&#x200B;**Connect**。
   ![ConnectConnect](assets/open_screen1.png "")

### IMS 配置 {#ims-configuration}

要将目标与AEM和Launch正确集成，必须同时为Launch和目标配置IMS。 虽然在AEM中将Launch的IMS配置预配置为Cloud Service，但必须创建目标IMS配置(配置目标后)。 请参阅[此视频](https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html)和[本页](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/integration-ims-adobe-io.html)，了解如何创建目标IMS配置。

### Adobe Target租户ID和Adobe Target客户端代码{#tenant-client}

配置Adobe Target租户ID和Adobe Target客户端代码字段时，请注意以下事项：

1. 对于大多数客户，租户ID和客户端代码是相同的。 这意味着这两个字段包含相同的信息并且相同。 请确保在这两个字段中输入租户ID。
2. 出于旧版目的，您还可以在租户ID和客户端代码字段中输入不同的值。

在这两种情况下，请注意：

* 默认情况下，客户端代码（如果是先添加的）也会自动复制到租户ID字段中。
* 您可以选择更改默认的租户ID集。
* 因此，对目标的后端调用将基于租户ID，而对目标的客户端调用将基于客户端代码。

如前所述，AEM作为Cloud Service最常使用第一种情况。 无论采用哪种方式，请确保&#x200B;**和**&#x200B;字段都包含正确的信息，具体取决于您的要求。

>[!NOTE]
>
> 如果要更改现有目标配置：
>
> 1. 重新输入租户ID。
> 2. 重新连接到目标。
> 3. 保存配置。


### 编辑目标配置{#edit-target-configuration}

要编辑目标配置，请执行以下步骤：

1. 选择现有配置，然后单击&#x200B;**属性**。
2. 编辑属性。
3. 选择&#x200B;**重新连接到Adobe Target**。
4. 选择&#x200B;**保存并关闭**。

### 将配置添加到站点{#add-configuration}

要将触屏UI配置应用到站点，请转至：**站点** → **选择任何站点页面** → **属性** → **高级** → **配置** →选择配置租户。

## 使用Adobe Launch {#integrate-target-launch}在AEM站点上集成Adobe Target

AEM优惠与Experience Platform Launch的开箱即用集成。 通过将Adobe Target扩展添加到Experience Platform Launch，您可以在AEM网页上使用Adobe Target的功能。 目标库只能通过使用Launch呈现。

>[!NOTE]
>
>现有（旧版）框架仍然有效，但无法在触屏用户界面中进行配置。 建议在启动项中重新生成变量映射配置。

作为一般概述，集成步骤包括：

1. 创建启动项属性
2. 添加所需的扩展
3. 创建数据元素（用于捕获Context Hub参数）
4. 创建页面规则
5. 构建和发布

### 创建启动项属性{#create-property}

属性是一个容器，其中填充了扩展、规则和数据元素。

1. 选择&#x200B;**新建属性**&#x200B;按钮。
2. 为您的属性提供名称。
3. 作为域，输入要加载启动库的IP/主机。
4. 选择&#x200B;**保存**按钮。
   ![LaunchpropertyLaunchproperty](assets/properties_newproperty1.png "")

### 添加所需的扩展{#add-extension}

**扩** 展管理核心库设置的容器。Adobe Target扩展通过使用目标 JavaScript SDK用于现代Web、at.js，支持客户端实现。 必须添加&#x200B;**Adobe Target**&#x200B;和&#x200B;**Adobe ContextHub**&#x200B;扩展。

1. 选择“扩展目录”选项，并在筛选器中搜索目标。
2. 选择&#x200B;**Adobe Target** at.js并单击“Install（安装）”选项。
   ![目标](assets/search_ext1.png "搜索目标搜索")
3. 选择&#x200B;**配置**&#x200B;按钮。 请注意导入了目标帐户凭据的配置窗口以及此扩展的at.js版本。
4. 选择&#x200B;**保存**&#x200B;以将目标扩展添加到Launch属性。 您应能看到&#x200B;**已安装的扩展**列表下列出的目标扩展。
   ![保存扩](assets/configure_extension1.png "展保存扩展")
5. 重复上述步骤以搜索&#x200B;**Adobe ContextHub**&#x200B;扩展并安装它（这是与contexthub参数集成时所需的，将根据其进行定位）。

### 创建数据元素{#data-element}

**数** 据元素是可以将Context Hub参数映射到的占位符。

1. 选择&#x200B;**数据元素**。
2. 选择&#x200B;**添加数据元素**。
3. 提供数据元素的名称并将其映射到Context Hub参数。
4. 选择&#x200B;**保存**。
   ![数据](assets/data_elem1.png "元素数据元素")

### 创建页面规则{#page-rule}

在&#x200B;**规则**&#x200B;中，我们定义并排序一系列在现场执行的操作，以实现定位。

1. 添加一组操作，如屏幕截图所示。
   ![操](assets/rules1.png "作")
2. 在添加参数至所有Mbox中，将之前配置的数据元素（请参阅上面的数据元素）添加到将在mbox调用中发送的参数。
   ![Mbox](assets/map_data1.png "Actions")

### 生成和发布{#build-publish}

要了解如何构建和发布，请参阅此[页面](https://docs.adobe.com/content/help/en/experience-manager-learn/aem-target-tutorial/aem-target-implementation/using-launch-adobe-io.html)。

## 经典UI和触屏UI配置之间内容结构的更改{#changes-content-structure}

| **更改** | **经典UI配置** | **触屏UI配置** | **后果** |
|---|---|---|---|
| 目标配置的位置。 | /etc/cloudservices/testandtarget/ | /conf/tenant/settings/cloudservices/目标 | 以前在/etc/cloudservices/testandtarget下存在多个配置，但现在在租户下存在单个配置。 |

>[!NOTE]
>
>现有客户仍支持旧版配置（没有编辑或创建新配置的选项）。 旧版配置是使用VSTS的客户上传的内容包的一部分。
