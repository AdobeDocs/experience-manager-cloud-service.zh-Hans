---
title: Adobe Experience Manager作为2020.4.0云服务发行说明
description: Experience Manager 2020.4.0发行说明
translation-type: tm+mt
source-git-commit: 49137535f4f6a6b62e697de6a7a9934f5b861bbc

---


# Release Notes for Adobe Experience Manager as a Cloud Service 2020.4.0 {#release-notes}

The following section outlines the general release notes for [!DNL Experience Manager] as a Cloud Service 2020.4.0.

## Release Date {#release-date}

作为云服务2020.4.0 [!DNL Experience Manager] 的发布日期为2020年4月9日。

## What&#39;s New in Assets {#assets}

了解当前版本和版本中的新增功 [!DNL Experience Manager Assets] 能、 [!DNL Dynamic Media] 增强和错误修复。

* [Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) 支持Experience Manager Assets的资产分发用例。 [!DNL Brand Portal] 可以将获得批准的品牌和产品资产安全地分发给外部代理、合作伙伴、内部团队和经销商进行下载，从而帮助组织满足其营销需求。
   * [!DNL Brand Portal] 配置通过控制台 [!DNL Adobe I/O] 完成。
   * Experience Manager作为云服 [!DNL Brand Portal] 务尚不支持 [!DNLE中的资产采购] 。

* [Adobe Asset Link](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html) v2.0可以作为云服 [!DNL Experience Manager] 务使用。 [!DNL Adobe Asset Link] 通过与桌面应用程序连接，以及通过应用程序内面板，简化 [!DNL Experience Manager Assets] 了创意人 [!DNL Creative Cloud] 员和营销人员在内 [!DNL Adobe Photoshop]容创建过程 [!DNL Adobe Illustrator]中的协 [!DNL Adobe InDesign][!DNL Asset Link] 作。
   * [!DNL Experience Manager] 为预配置，这 [!DNL Adobe Asset Link]样便于配 [置](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html) ，并可更快地向创意专业人士推广。
   * [!DNL Asset Link] 现在支持 [Experience Manager环境切换程序](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) ，该切换程序允许创意用户轻松连接到其他 [!DNL Experience Manager] 环境。 此功能非常有用的示例是，对于使用不同部署的多个客户端工作的代理设计 [!DNL Experience Manager Assets] 人员。

* 用户可以在 [文件夹属性用户界面中](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) ，将后处理工作流配置为自  动开始特定文件夹层次结构。
   * 文件夹“ [!UICONTROL 属性] ”用户界面得到简化，新的“资产处理”选项卡包含元数据用户档案、处理用户档案和新的自动开始工作流配置。
   * 资产重新处理对话框允许选择特定的处理用户档案并决定在子文件夹中重新处理。
   * [!DNL Dynamic Media]:添加了选择性发布配置，以便资产自动发布仅用于安全预览。 此外，资产可以显式发布到Experience Manager，而不发布到DMS7以在公共域中投放。

### 错误修复 {#assets-bug-fixes}

* 修复了资产处理问题。
* 对配置和 [!DNL Dynamic Media] 将资产发布到投放服务的 [!DNL Dynamic Media] 修复。

>[!MORELIKETHIS]
>
>* [关于Adobe Asset Link](https://www.adobe.com/creativecloud/business/enterprise/adobe-asset-link.html)
>* [配置Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html)
>* [将Experience Manager配置为使用资产链接](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html)
>* [在Experience Manager中使用资产微服务创建工作流](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html#post-processing-workflows)


## Cloud Manager的新增功能 {#whats-new-cloud-manager}

* 发布者URL现在可从云管理器UI的环境页面访问。
* 对导航进行更改，以允许用户从Cloud Manager概述页面编辑、切换或添加项目。
* 允许用户从Cloud Manager项目上的项目卡编辑登陆页的更改。
* 新管线状 **态管线运行** ，显示与其关联的环境。
* 改进了管道执行页面的可理解性。 这包括管道名称（仅限非生产管道）和类型的显示，以及指示管道状态是否为“进行中／已取消／失败”的标记。
* 用于改善用户体验并了解为何禁用“添加项目/环境”按钮的工具提示。
* 现在可通过UI和API删除失败的环境。
* 用于生成Git密码的过程对底层服务层中的问题具有更强的适应性。

### 错误修复 {#bug-fixes-cloud-manager}

* 管道执行详细信息页面上指向舞台环境的链接未始终导航到正确的位置。
* 环境创建进程中的各个步骤将比必要时提前超时，从而导致进程失败。
* 更新了构建容器中使用的Maven配置，以避免在下载对象元数据时出现死锁。
* 在某些情况下，构建映像步骤将无法成功下载客户包。
* 某些不常发生的情况会阻止环境被删除。
* Experience Cloud通知未得到一致接收。
