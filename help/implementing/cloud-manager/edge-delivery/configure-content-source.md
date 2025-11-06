---
title: 配置您的内容源
description: 了解如何为您的 Edge Delivery Site 配置内容源。在 Helix 4 架构中使用 `fstab.yaml`，或在 Helix 5 架构中使用 Cloud Manager 中的引导向导（或配置服务 API）。
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: f82eafc0-03d0-4c69-9b28-e769a012531b
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 100%

---

# 一键配置 Edge Delivery Services 的内容源 {#config-content-source}

>[!IMPORTANT]
>
>*Helix* 是支持 AEM Sites 基于文档创作的底层架构的内部名称。它不是一个功能或产品名称。在本文中，*Helix* 指的是您的 Edge Delivery Sites 所使用的架构版本。Helix 5 是底层架构的当前版本，Helix 4 是以前的版本。

Adobe Experience Manager (AEM) Edge Delivery Services 允许使用一个全球分布的快速边缘网络从多个来源（例如 Google Drive、SharePoint 或 AEM 本身）传递内容。

两个架构版本的内容源配置有以下不同：

| 版本 | 内容源配置方法 |
| --- | --- |
| Helix 4 | YAML 文件 (`fstab.yaml`) |
| Helix 5 | 配置服务 API（*否`fstab.yaml`*） |

这篇文章提供了两个版本的全面配置步骤、示例和验证说明。

**开始之前**

如果您使用 [Cloud Manager 中的一键边缘传递](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md##one-click-edge-delivery-site)，那么您的网站使用的是带有单个存储库的 Helix 5。[按照 Helix 5 说明进行操作](#config-helix5)，并使用说明中所提供的 Helix 4 YAML 版本作为应急后备。

**确定您的 Helix 版本**

* Helix 4 - 您的项目包含一个 `fstab.yaml` 文件。
* Helix 5——您的项目&#x200B;*未*&#x200B;使用 `fstab.yaml`，而是通过 [Cloud Manager 使用引导向导](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md)或 API 设置的。

如果您仍然不确定，请通过存储库元数据确认或者咨询您的管理员。

## 为 Helix 4 配置内容源

在 Helix 4 中，`fstab.yaml` 文件定义了网站的内容源。该文件位于 GitHub 存储库的根目录下，将 URL 路径前缀（称为“挂载点”）映射到外部内容源。典型示例如下所示：

```yaml
mountpoints:
  /: https://drive.google.com/drive/folders/your-folder-id
```

以上示例仅用于说明。实际 URL 应指向您的内容源，例如 Google Drive 文件夹、SharePoint 目录或 AEM 路径。

**如要为 Helix 4 配置内容源：**

步骤因您所使用的源系统而异。

* **Google Drive**

   1. 创建 Google Drive 文件夹。
   1. 与 `helix@adobe.com` 共享该文件夹。
   1. 获取可共享文件夹链接。
   1. 更新您的 `fstab.yaml`，如下所示：

      ```yaml
      mountpoints: 
          /: https://drive.google.com/drive/folders/<folder-id>
      ```

   1. 提交更改，并将其推送到 GitHub。

* **SharePoint**

   1. 创建 SharePoint 文件夹或文档库。
   1. 与 `helix@adobe.com` 共享访问权限。
   1. 获取文件夹 URL。
   1. 更新您的 `fstab.yaml`，如下所示：

      ```yaml
      mountpoints:
        /: https://<tenant>.sharepoint.com/sites/<site>/Shared%20Documents/<folder>
      ```

   1. 提交更改，并将其推送到 GitHub。

* **AEM**

   1. 识别您的 AEM 内容路径。
   1. 使用 AEM 内容导出 URL，如下所示：

      ```yaml
      mountpoints:
        /: https://author.<your-aem-instance>.com/bin/franklin.delivery/<org>/<repo>/main
      ```

   1. 提交更改，并将其推送到 GitHub。

### 验证

* 使用 AEM Sidekick Chrome 扩展，点击&#x200B;**预览** > **发布** > **测试实时网站**。
* 验证 URL：`https://main--<repo>--<org>.hlx.page/`

## 为 Helix 5 配置内容源 {#config-helix5}

Helix 5 为无重复，不使用 `fstab.yaml`，并且支持多个网站共享同一个目录。通过配置服务 API 或 Edge Delivery Sites 用户界面管理配置。配置是网站级别的（不是存储库级别的）。

从概念上看有如下区别：

| 方面 | Helix 4 | Helix 5 |
| --- | --- | --- |
| 配置 | 通过 `fstab.yaml` 完成 | 通过 API 或 UI 而不是 YAML 完成。 |
| 挂载点 | 在 `fstab.yaml` 中定义。 | 不必需。根为隐含了解。 |

**如要为 Helix 5 配置内容源：**

1. 使用配置服务 API，通过 API 密钥或访问令牌进行身份验证。
1. 执行以下 `PUT` API 调用：

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

1. 验证响应（预期：HTTP 200 OK）。

### 验证

* 使用 AEM Sidekick Chrome 扩展，点击&#x200B;**预览** > **发布** > **测试实时网站**。
* 验证 URL：`https://main--<repo>--<org>.aem.page/`
* （可选）通过以下 `GET` API 调用检查当前配置：

  ```bash
  GET /api/{program}/{programId}/site/{siteId}
  ```
