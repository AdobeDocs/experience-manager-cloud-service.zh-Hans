---
title: Adobe Experience Manager as a Cloud Service 2020.4.0 发行说明
description: Experience Manager 2020.4.0 发行说明
exl-id: d98a3862-76fa-4b5b-b81a-333f5f532b67
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 95%

---

# Adobe Experience Manager as a Cloud Service 2020.4.0 发行说明{#release-notes}

本页面概述了 [!DNL Experience Manager] as a Cloud Service 2020.4.0 版的常规发行说明。

## 发布日期 {#release-date}

[!DNL Experience Manager] as a Cloud Service 2020.4.0 的发布日期是 2020 年 4 月 9 日。

## Assets 的新增功能 {#assets}

了解当前版本中 [!DNL Experience Manager Assets] 和 [!DNL Dynamic Media] 的新增功能、增强功能和错误修复。

* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 支持 Experience Manager Assets 的资产分发用例。[!DNL Brand Portal] 可以将获得批准的品牌和产品资产安全地分发给外部代理、合作伙伴、内部团队和经销商进行下载，从而帮助组织满足其营销需求。
   * [!DNL Brand Portal] 配置可通过 [!DNL Adobe I/O] 控制台完成。请参阅[配置 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html)。
   * [!DNL Experience Manager] as a Cloud Service 尚不支持 [!DNL Brand Portal] 中的资产采购。

* [Adobe Asset Link](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html) v2.0 可与 [!DNL Experience Manager] as a Cloud Service 搭配使用。[!DNL Adobe Asset Link] 可通过应用程序内 [!DNL Asset Link] 面板将 [!DNL Experience Manager Assets] 与 [!DNL Creative Cloud] 桌面应用程序 [!DNL Adobe Photoshop]、[!DNL Adobe Illustrator] 和 [!DNL Adobe InDesign] 连接，从而简化内容创建过程中创意专业人士与营销人员之间的协作。
   * 已为 [!DNL Adobe Asset Link] 预配置了 [!DNL Experience Manager]，这样可以[轻松配置](https://helpx.adobe.com/cn/enterprise/using/configure-aem-assets-for-asset-link.html)并更快速地向创意专业人士推广。
   * 现在，[!DNL Asset Link] 支持 [Experience Manager 环境切换器](https://helpx.adobe.com/cn/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink)，该切换器让创意用户能够轻松连接到其他 [!DNL Experience Manager] 环境。例如，对于使用不同 [!DNL Experience Manager Assets] 部署来与多个客户开展合作的广告公司设计师而言，这项功能非常有用。

* 用户可以将[后处理工作流](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)配置为在特定文件夹层次结构的文件夹[!UICONTROL 属性]用户界面中自动启动。
   * 文件夹[!UICONTROL 属性]用户界面得到简化，新的[!UICONTROL 资产处理]选项卡包含元数据配置文件、处理配置文件以及新的自动启动工作流配置。

      ![处理配置文件可以轻松应用于文件夹，并且上传到文件夹的所有资产都可以使用这些配置文件进行处理](/help/assets/assets/asset-processing-folder-properties.png)

   * 资产重新处理选项允许选择特定的处理配置文件来重新处理子文件夹中用户选择的资产。

      ![使用特定处理配置文件重新处理选定的资产](/help/assets/assets/fpo-existing-asset-reprocess.gif)

   * [!DNL Dynamic Media]：添加了选择性发布配置，以便仅出于安全预览目的自动发布资产。此外，还可以将资产明确发布到 Experience Manager（不发布到 DMS7）以便在公共域中交付。

### 错误修复 {#assets-bug-fixes}

* 修复了资产处理问题。
* 修复了 [!DNL Dynamic Media] 配置，并将资产发布到 [!DNL Dynamic Media] 交付服务。

>[!MORELIKETHIS]
>
>* [关于 Adobe Asset Link](https://www.adobe.com/cn/creativecloud/business/enterprise/adobe-asset-link.html)
>* [配置 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html)
>* [配置 Experience Manager 以搭配使用 Asset Link](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html)
>* [使用资产微服务在 Experience Manager 中创建工作流](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html#post-processing-workflows)


## Cloud Manager 的新增功能 {#whats-new-cloud-manager}

* 现在，可以从 Cloud Manager UI 的环境页面访问发布者 URL。
* 导航更改让用户能够从 Cloud Manager 概述页面编辑、切换或添加项目。
* 更改让用户能够从 Cloud Manager 登陆页面上的项目卡片编辑项目。
* 根据与管道关联的环境，会显示新的管道状态&#x200B;**管道正在运行**。
* 改进了管道执行页面的可理解性。这包括显示管道名称（仅限非生产管道）和类型，以及指示管道状态是否为“进行中/已取消/失败”的徽章。
* 添加了用于改善用户体验和增进了解为何禁用“添加项目/环境”按钮的工具提示。
* 现在，可以通过 UI 和 API 删除失败的环境。
* 提高了用于生成 Git 密码的进程弹性，以应对基础服务层中的问题。

### 错误修复 {#bug-fixes-cloud-manager}

* 管道执行详细信息页面上指向暂存环境的链接不是总能导航到正确的位置。
* 环境创建进程中的各个步骤超时时间提前，从而导致进程失败。
* 更新了生成容器中使用的 Maven 配置，以避免下载伪像元数据时出现死锁。
* 在某些情况下，生成图像步骤可能无法成功下载客户包。
* 某些偶然发生的情况可能会阻止删除环境。
* 不能终如收到 Experience Cloud 通知。
