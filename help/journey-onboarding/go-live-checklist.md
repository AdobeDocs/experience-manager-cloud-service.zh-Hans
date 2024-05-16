---
title: 上线清单
description: 了解成功上线 AEM as a Cloud Service 所需具备的所有要素
exl-id: b424a9db-0f3b-4a8d-be84-365d68df46ca
source-git-commit: 581f075483280e4b33574bfd4cc1cb01b5601440
workflow-type: ht
source-wordcount: '575'
ht-degree: 100%

---

# 上线清单 {#Go-Live-Checklist}

查看此活动列表以确保您顺利且成功地执行 Go-Live。

* 运行具有功能和 UI 测试的端到端生产管道，以确保&#x200B;**总是最新的** AEM 产品体验。请参阅以下资源。
   * [AEM 版本更新](/help/implementing/deploying/aem-version-updates.md)
   * [自定义功能测试](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)
   * [UI 测试](/help/implementing/cloud-manager/ui-testing.md)
* 如果您要从 AEM 6.5 迁移，则应将内容迁移到生产环境，并确保在测试阶段有相关的子集可用。
   * AEM 的 DevOps 最佳实践意味着代码从开发环境移动到生产环境，而内容从生产环境向下移动。
* 设定代码和内容冻结期。
   * 另见 [迁移的代码和内容冻结时间线](#code-content-freeze)部分
* 执行最终内容增补。
* 验证 Dispatcher 配置
   * 使用有助于在本地配置、验证和模拟调度程序的本地调度程序验证器
      * [设置本地 Dispatcher 工具。](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html#prerequisites)
   * 仔细检查虚拟主机配置。
      * 最简单（和默认）的解决方案是在`/dispatcher/src/conf.d/available_vhostsfolder`中包括`ServerAlias *`你的虚拟主机文件。
         * 这将允许产品功能测试、调度程序缓存失效和克隆使用的主机别名发挥作用。
      * 然而，如果`ServerAlias *`是不可接受的，至少以下`ServerAlias`除了您的自定义域之外，还必须允许条目：
         * `localhost`
         * `*.local`
         * `publish*.adobeaemcloud.net`
         * `publish*.adobeaemcloud.com`
* 配置 CDN、SSL 和 DNS。
   * 如果您使用自己的 CDN，请输入支持票以配置适当的路由。
      * 见章节 [客户 CDN 指向 AEM 托管 CDN](/help/implementing/dispatcher/cdn.md#point-to-point-cdn)在 CDN 文档中了解详细信息。
      * 根据 CDN 供应商的文档配置 SSL 和 DNS。
   * 如果您不使用其他 CDN，请按照以下文档管理 SSL 和 DNS：
      * 管理 SSL 证书
         * [管理 SSL 证书简介](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
         * [管理 SSL 证书](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
      * 管理自定义域名（DNS）
         * 为确保 DNS 割接不会引入意外问题，最好在上线之前创建一个测试子域以连接您的生产实例并进行一轮 UAT 测试。因此，如果您的域是 example.com，您可以创建一个子域 test.example.com 并将其应用于生产。在域的 UAT 测试期间，您将需要寻找正确的链接重定向、缓存和调度程序配置等内容。
         * [自定义域名简介](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
         * [添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
         * [管理自定义域名](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)
   * 请记住验证为您的 DNS 记录设置的 TTL。
      * TTL 是 DNS 记录在请求服务器更新之前保留在缓存中的时间量。
      * 如果您的 TTL 非常高，则对 DNS 记录的更新将需要更长的时间才能传播。
* 运行满足您的业务需求和目标的性能和安全测试。
   * 对暂存环境进行测试。它的规模与生产环境相同。
   * 开发环境的规模与阶段和生产环境的规模不同。
* 切换并确保在没有任何新部署或内容更新的情况下执行实际上线。
* 创建 Admin Console 用户通知轮廓。参见 [通知轮廓](/help/journey-onboarding/notification-profiles.md)
* 考虑配置流量过滤规则来控制哪些流量不允许进入您的网站。
   * 速率限制流量过滤规则可以成为抵御 DDoS 攻击的有效工具。有一类特殊的流量过滤规则，称为 WAF 规则，需要单独的许可证。
   * 请参阅文档以了解一些 [建议的入门规则](/help/security/traffic-filter-rules-including-waf.md#recommended-starter-rules)。

如果您需要在上线期间重新调整任务，您可以随时参考该列表。
