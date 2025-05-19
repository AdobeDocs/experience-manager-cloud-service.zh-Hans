---
title: 配置您的内容Source
description: 了解如何使用Helix 4中的fstab.yaml或Helix 5中的Edge Delivery Services UI（或配置服务API）配置Edge Delivery站点的内容源。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8696cf8a7e7cfc439450b34fa6fda10b38cd415e
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# 只需单击一下即可为Edge Delivery Services配置内容源 {#config-content-source}

Adobe Experience Manager (AEM) Edge Delivery Services允许使用全球分布式快速边缘网络从多个来源(如Google Drive、SharePoint或AEM本身)进行内容交付。

Helix 4和Helix 5的内容源配置在以下方面有所不同：

| 版本 | 内容源配置方法 |
| --- | --- |
| 螺旋4 | YAML文件(`fstab.yaml`) |
| 螺旋5 | 配置服务API （*否`fstab.yaml`*） |

本文提供了两个版本的全面配置步骤、示例和验证说明。

**开始之前**

如果您在Cloud Manager](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md##one-click-edge-delivery-site)中使用[单击Edge Delivery，则您的网站为带有单个存储库的Helix 5。 [按照Helix 5说明进行操作](#config-helix5)，然后使用提供的Helix 4 YAML版本说明作为后备。

**确定您的Helix版本**

* Helix 4 — 您的项目包括`fstab.yaml`文件。
* Helix 5 — 您的项目&#x200B;*不*&#x200B;使用`fstab.yaml`，是通过[Edge Delivery Services UI](#config-helix5)或API设置的。

通过存储库元数据确认，如果仍然不确定，请咨询管理员。

## 配置Helix 4的内容源

在Helix 4中， fstab.yaml文件定义站点的内容源。 此文件位于GitHub存储库的根目录下，将URL路径前缀（称为装载点）映射到外部内容源。 典型示例如下所示：

```yaml
mountpoints:
  /: https://drive.google.com/drive/folders/your-folder-id
```

此示例仅供说明之用。 实际URL应指向您的内容源，如Google驱动器文件夹、SharePoint目录或AEM路径。

**配置Helix 4的内容源：**

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

### 验证

* 使用AEM Sidekick Chrome扩展，单击&#x200B;**预览** > **发布** > **测试实时网站**。
* 验证URL： `https://main--<repo>--<org>.hlx.page/`

## 配置Helix 5的内容源 {#config-helix5}

Helix 5是重写的，不使用`fstab.yaml`，并且支持多个站点共享同一目录。 通过配置服务API或Edge Delivery Services UI管理配置。 配置是站点级别（而非存储库级别）。

概念上的区别如下：

| 长宽比 | 螺旋4 | 螺旋5 |
| --- | --- | --- |
| 配置 | 通过`fstab.yaml`完成 | 通过API或UI而不是YAML完成。 |
| 装入点 | 在`fstab.yaml`中定义。 | 非必需。 隐含地理解了根。 |

**配置Helix 5的内容源：**

1. 使用配置服务API，通过API密钥或访问令牌进行身份验证。
1. 进行以下`PUT` API调用：

   ```bash {.line-numbering}
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

### 验证

* 使用AEM Sidekick Chrome扩展，单击&#x200B;**预览** > **发布** > **测试实时网站**。
* 验证URL： `https://main--<repo>--<org>.aem.page/`
* （可选）通过以下`GET` API调用检查当前配置：

  ```bash
  GET /api/{program}/{programId}/site/{siteId}
  ```
