---
title: Cloud Manager 2025.5.0 版的发行说明
description: 了解 Adobe Experience Manager as a Cloud Service 中的 Cloud Manager 2025.5.0 版本。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: effa19a98d59993e330e925fb933a436ff9d20d7
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 18%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.5.0 的发行说明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中的 Cloud Manager 2025.5.0 版本。

另请参阅 [Adobe Experience Manager as a Cloud Service 的当前发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 发行日期 {#release-date}

AEM as a Cloud Service中Cloud Manager 2025.5.0的发布日期是2025年5月8日星期四。

下一个计划发布于2025年6月5日星期四。

## 新增功能 {#what-is-new}

### 如何通过一次单击更改Edge Delivery Services的内容源

Adobe Experience Manager (AEM) Edge Delivery Services允许使用全球分布式快速边缘网络从多个来源(如Google Drive、SharePoint或AEM本身)进行内容交付。

Helix 4和Helix 5的内容源配置在以下方面有所不同：

| 版本 | 配置方法 |
| --- | --- |
| 螺旋4 | YAML文件(`fstab.yaml`) |
| 螺旋5 | 配置服务API （*否`fstab.yaml`*） |

本文提供了两个版本的全面配置步骤、示例和验证说明。

B **在您开始之前**

如果您在Cloud Manager[&#128279;](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md##one-click-edge-delivery-site)中使用单击Edge Delivery，则您的网站为带有单个存储库的Helix 5。 按照Helix 5说明进行操作，并使用提供的Helix 4 YAML版本作为后备。

**确定您的Helix版本**

* Helix 4 — 您的项目包括`fstab.yaml`文件。
* Helix 5 — 您的项目&#x200B;*不*&#x200B;使用`fstab.yaml`，是通过Edge Delivery Services UI或API设置的。

通过存储库元数据确认，如果仍然不确定，请咨询管理员。

#### 配置内容源(Helix 4)

在Helix 4中，内容源在位于GitHub存储库根目录的名为`fstab.yaml`的YAML配置文件中定义。

##### YAML文件格式

`fstab.yaml`文件定义了与以下示例类似的装载点（映射到内容源URL的URL路径前缀）（仅供说明之用）：

```yaml
mountpoints:
  /: https://drive.google.com/drive/folders/your-folder-id
```

##### 更改内容源

步骤因您使用的源系统而异。

* **Google驱动器**

   1. 创建Google驱动器文件夹。
   1. 与`helix@adobe.com`共享文件夹。
   1. 获取可共享文件夹链接。
   1. 更新您的`fstab.yaml`，如下所示：

      ```yaml
      mountpoints: 
          /: https://drive.google.com/drive/folders/<folder-id>
      ```

   1. 提交更改并将其推送到GitHub。

* **SharePoint**

   1. 创建SharePoint文件夹或文档库。
   1. 与`helix@adobe.com`共享访问权限。
   1. 获取文件夹URL。
   1. 更新您的`fstab.yaml`，如下所示：

      ```yaml
      mountpoints:
        /: https://<tenant>.sharepoint.com/sites/<site>/Shared%20Documents/<folder>
      ```

   1. 提交更改并将其推送到GitHub。

* **AEM**

   1. 识别您的AEM内容路径。
   1. 使用AEM内容导出URL，如下所示：

      ```yaml
      mountpoints:
        /: https://author.<your-aem-instance>.com/bin/franklin.delivery/<org>/<repo>/main
      ```

   1. 提交更改并将其推送到GitHub。

##### 验证

* 使用AEM Sidekick Chrome扩展，单击&#x200B;**预览** > **发布** > **测试实时网站**。
* 验证URL： `https://main--<repo>--<org>.hlx.page/`

#### 配置内容源(Helix 5)

Helix 5是重写的，不使用`fstab.yaml`，并且支持多个站点共享同一目录。 通过配置服务API或Edge Delivery Services UI管理配置。 配置是站点级别（而非存储库级别）。

##### 概念差异

| 长宽比 | 螺旋4 | 螺旋5 |
| --- | --- | --- |
| 配置文件 | `fstab.yaml` | API或用户界面配置 |
| 装入点 | YAML定义的 | 非必需（隐式根） |

##### 更改内容源

使用配置服务API。

1. 通过API密钥或访问令牌进行身份验证。
1. 进行以下`PUT` API调用：

   ```bash
   PUT /api/{program}/{programId}/site/{siteId}
   Content-Type: application/json
   
   {
     "sitename": "my-site",
     "branchName": "main",
     "version": "v5",
     "repo": "my-content-repo-link"
   }
   ```

1. 验证响应（预期： HTTP 200 OK）。

##### 验证

* 使用AEM Sidekick Chrome扩展，单击&#x200B;**预览** > **发布** > **测试实时网站**。
* 验证URL： `https://main--<repo>--<org>.aem.page/`
* （可选）通过以下`GET` API调用检查当前配置：

  ```bash
  GET /api/{program}/{programId}/site/{siteId}
  ```

<!--
* **AI-powered build summaries now available for internal use**

    Internal users can now use AI-powered build summaries to simplify build log analysis. The feature provides actionable recommendations and helps identify the root causes of build failures.

    ![Build Summary dialog box](/help/implementing/cloud-manager/release-notes/assets/build-summary.png)
-->


## 早期采用者计划 {#early-adoption}

参与Cloud Manager的早期采用者计划，在即将发布的功能正式发布之前获得对这些功能的独家访问权。

目前提供以下早期采用商机：

### 添加 Edge Delivery 管道 {#add-eds-pipeline}

使用Edge Delivery Services构建的站点现在支持&#x200B;**管道**，此功能不仅限于Cloud Service环境。 在适用的情况下，您可以使用&#x200B;**管道**&#x200B;管理流量过滤规则和Web应用程序防火墙(WAF)配置等设置。 请参阅[支持的配置](/help/operations/config-pipeline.md#configurations)。

<!-- ![Add Edge Delivery pipeline in Add Pipeline drop-down list](/help/implementing/cloud-manager/release-notes/assets/add-edge-delivery-pipeline.png) -->

如果您有兴趣测试这项新功能并分享您的反馈，请从与Adobe ID关联的电子邮件地址向[grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com)发送电子邮件。

### 自带Git — 现在支持Azure DevOps {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

客户现在可以将其Azure DevOps Git存储库载入到Cloud Manager中，并支持现代Azure DevOps和旧版VSTS (Visual Studio Team Services)存储库。

* 对于Edge Delivery Services用户，已载入的存储库可用于同步和部署网站代码。
* 对于AEM as a Cloud Service和Adobe Managed Services (AMS)用户，存储库可以同时链接到全栈管道和前端管道。

即将支持其他管道类型以及通过代码质量管道进行拉取请求验证。

请参阅[在 Cloud Manager 中添加外部存储库](/help/implementing/cloud-manager/managing-code/external-repositories.md)。

![添加“存储库”对话框](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

如果您有兴趣测试此新功能并分享您的反馈，请从与您的 Adobe ID 关联的电子邮件地址发送电子邮件至 [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com)。请务必注明您想要使用的 Git 平台以及您是处于专用/公共还是企业存储库结构中。

<!--
## Bug fixes

* Issue

* Issue

* Issue
-->

<!-- ## Known issues {#known-issues} -->

