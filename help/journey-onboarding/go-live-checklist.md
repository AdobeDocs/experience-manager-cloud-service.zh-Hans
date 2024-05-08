---
title: 上线清单
description: 了解成功上线AEMas a Cloud Service所需具备的所有元素
source-git-commit: 4a03e2fe3519fd9e0d8d646526ea6c9cc6637f52
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 6%

---


# 上线清单 {#Go-Live-Checklist}

请查看此活动列表，确保您顺利成功地上线。

* 运行具有功能和UI测试的端到端生产管道，以确保 **始终最新** AEM产品体验。 请参阅以下资源。
   * [AEM 版本更新](/help/implementing/deploying/aem-version-updates.md)
   * [自定义功能测试](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)
   * [UI 测试](/help/implementing/cloud-manager/ui-testing.md)
* 如果您是从AEM 6.5迁移，则应将内容迁移到生产环境，并确保在暂存环境中有相关的子集可用于测试。
   * 适用于AEM的DevOps最佳实践意味着，当内容从生产环境向下移动时，代码会从开发环境向上移动到生产环境。
* 计划代码和内容冻结期。
   * 另请参阅部分 [用于迁移的代码和内容冻结时间线](#code-content-freeze)
* 执行最终内容增补。
* 验证Dispatcher配置。
   * 使用本地Dispatcher验证器，这有助于在本地配置、验证和模拟Dispatcher
      * [设置本地Dispatcher工具](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html#prerequisites)
   * 仔细查看虚拟主机配置。
      * 最简单（默认）的解决方案是包括 `ServerAlias *` 在虚拟主机文件中 `/dispatcher/src/conf.d/available_vhostsfolder`.
         * 这将允许产品功能测试、Dispatcher缓存失效和克隆使用的主机别名正常运行。
      * 但是，如果 `ServerAlias *` 不可接受，至少如下所示 `ServerAlias` 除了自定义域外，还必须允许以下条目：
         * `localhost`
         * `*.local`
         * `publish*.adobeaemcloud.net`
         * `publish*.adobeaemcloud.com`
* 配置CDN、SSL和DNS。
   * 如果您使用自己的CDN，请输入支持票证以配置相应的路由。
      * 请参阅部分 [客户CDN指向AEM托管的CDN](/help/implementing/dispatcher/cdn.md#point-to-point-cdn) 详细信息，请参阅CDN文档。
      * 根据CDN供应商的文档配置SSL和DNS。
   * 如果您没有使用其他CDN，请按照以下文档管理SSL和DNS：
      * 管理 SSL 证书
         * [管理 SSL 证书简介](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
         * [管理SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
      * 管理自定义域名(DNS)
         * 为了确保DNS直接转换不会引入意外问题，最好在正式启用并进行一轮UAT测试之前创建一个测试子域以将生产实例连接到该子域。 因此，如果您的域是example.com，则可以创建一个子域test.example.com并将其应用于生产环境。 在对域进行UAT测试期间，您需要查找适当的链接重定向、缓存和Dispatcher配置等。
         * [自定义域名简介](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
         * [添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
         * [管理自定义域名](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)
   * 请记住验证DNS记录的TTL集。
      * TTL是在请求服务器更新之前DNS记录保留在缓存中的时间。
      * 如果您的TTL非常高，则传播对DNS记录的更新将需要较长时间。
* 运行符合您的业务要求和目标的性能和安全性测试。
   * 在暂存环境中执行测试。  它的规模与生产环境相同。
   * 开发环境的大小与暂存和生产环境不同。
* 切换并确保不进行任何新部署或内容更新而执行实际上线。
* 创建Admin Console用户通知配置文件。 请参阅 [通知配置文件](/help/journey-onboarding/notification-profiles.md)
* 请考虑配置流量过滤器规则以控制网站上不允许的流量。
   * 速率限制流量过滤规则是防御DDoS攻击的有效工具。 一种称为WAF规则的特殊流量过滤器规则需要单独的许可证。
   * 请参阅文档以了解部分 [推荐的入门规则](/help/security/traffic-filter-rules-including-waf.md#recommended-starter-rules).

如果在上线期间需要重新校准任务，您随时可以引用列表。