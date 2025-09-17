---
title: AEM Assets和Forms中的故障排除
description: 使用关键区域的文章链接，排查常见的AEM Assets和Forms问题，例如上传、元数据、搜索、投放、表单创建、提交和集成。
hidefromtoc: true
hide: true
source-git-commit: 5074e777c68c51955b9ad8f055e04067163b9596
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 1%

---


# AEM Assets和Forms问题疑难解答 {#troubleshoot-aem-assets-forms}

AEM as a Cloud Service通过AEM Assets为数字资产管理提供全面的解决方案，并通过AEM Forms提供强大的表单创建功能。 这两种服务都提供了云原生的PaaS解决方案，这些解决方案具有新一代智能功能，例如AI/ML，所有这些功能都在一个始终最新、始终可用和不断学习的系统中。

但是，复杂的企业环境可能会遇到跨不同领域的各种技术挑战。

本全面的故障排除指南为AEM Assets和Forms提供了系统化的诊断方法、分类的解决方案，以及分步式解决途径。 每个部分都包含快速参考指南、详细的故障排除方法和广泛的资源链接，以帮助您有效解决问题并优化AEM Cloud Service环境。

## AEM Assets疑难解答 {#aem-assets-troubleshooting}

AEM Assets简化了您跨体验管理、组织和交付数字资源的方式。 但是，可能会出现影响资源上传、元数据、集成或投放的问题。 本文提供了故障诊断步骤，以帮助您诊断和解决常见的AEM Assets问题。 通过遵循此处的指南，您可以高效地恢复工作流，并确保资产可跨渠道访问、准确且随时使用。

### 资产处理和演绎版 {#asset-processing-renditions-issues}

<table>
  <tbody>
  <tr>
    <td><strong>上传和处理</strong></td>
    <td><strong>演绎版</strong></td>
    <td><strong>PDF和文本提取</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26610">AEM as a Cloud Service中大型MP4文件的资源处理失败</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26639">DAM呈现与原始文件不匹配</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26785">AEM在10万个令牌之后截断从大型PDF提取的文本</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-23916">具有ZIP压缩上载的TIFF文件不生成演绎版</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26233">图像在AEM as a Cloud Service中未显示缩略图演绎版</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25518">AEM as a Cloud Service中大型PDF的文本提取限制</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-21865">将资源文件夹拖放到AEM Assets Web UI失败</a></td>
    <td></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26528">资产轮换问题使后续轮换不可见</a></td>
  </tr>
  <tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26450">提高Photoshop Firefly API集成的单部分资源上传限制</a></td>
  <td></td>
  <td></td>
  </tr>
  </tbody>
</table>

### Dynamic Media {#dynamic-media-issues}

<table>
  <tbody>
  <tr>
    <td><strong>视频</strong></td>
    <td><strong>旋转集和智能裁切</strong></td>
    <td><strong>交付和设置</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26533">修复了AEM中的视频上传、处理和渲染问题</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26715">旋转集卡在处理状态</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-17628">更改资产的Dynamic Media URL</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26677">Dynamic Media和DAM卡片视图之间的视频缩略图不匹配</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26873">AEM as a Cloud Service中未生成智能裁剪演绎版</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26367">AEM 6.5中的智能裁剪存在的图像中断问题</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26610">AEM Dynamic Media中的资源处理失败</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26637">TIFF演绎版的背景颜色问题</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25294">Dynamic Media常规设置页面未打开</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26197">使用Dynamic Media解决视频文件中的音频问题</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25885">Dynamic Media中的资产同步失败</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26461">解决不同环境中的资源名称差异</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26871">Dynamic Media视频播放器在较低环境中无法正常工作</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25471">Dynamic Media同步用户建议</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26902">使用API从Dynamic Media导出资源和元数据</a></td>
  </tr>
  </tbody>
</table>

### 元数据、标记和共享 {#metadata-tagging-sharing-issues}

<table>
  <tbody>
  <tr>
    <td><strong>元数据</strong></td>
    <td><strong>智能标记</strong></td>
    <td><strong>访问和共享</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25828">AEM Assets中的图像元数据差异</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25925">自动标记新上传的资产</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26928">尽管具有读取权限，但在Assets视图中仍受限制发表评论</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26655">解决非管理员用户的元数据架构可见性问题</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25889">将JWT迁移到OAuth后，智能标记不起作用</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25903">解决AEM Managed Services中的共享链接问题</a></td>
  </tr>

</tbody>
</table>

### 集成和访问 {#integrations-access}

<table>
  <tbody>
    <tr>
      <td><strong>Asset Link</strong></td>
      <td><strong>许可和定制</strong></td>
    </tr>
    <tr>
      <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26922">Adobe Asset Link使链接在InDesign中不可访问</a></td>
      <td>
        <a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26616">内容片段未包含在AEM Assets许可证中</a><br>
        </td>
    </tr>
    <tr>
      <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25562">解决InDesign中的AEM Asset Link连接问题</a></td>
      <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25525">解决AEM as a Cloud Service中的资源处理问题</a></td>
    </tr>
    <tr>
      <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25506">Adobe Asset Link插件网络错误：服务器不可访问</a></td>
      <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25829">正在更新AEM as a Cloud Service中视频资源的自定义缩略图</a>
      </td>
    </tr>
  </tbody>
</table>




## AEM Forms疑难解答 {#aem-forms-troubleshooting}

AEM Forms as a Cloud Service提供了强大的表单创建和管理功能。 但是，在安装、配置、表单创建或提交过程中可能会遇到问题。 此部分提供常见AEM Forms问题的全面故障排除指南。

### 安装和配置问题

<table>
  <tbody>
  <tr>
    <td><strong>设置和配置</strong></td>
    <td><strong>表单创建问题</strong></td>
    <td><strong>性能和缓存</strong></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-installation-and-configuration.md">Forms选项在导航中不可用</a></td>
    <td><a href="/help/forms/form-creation-failing.md">模板发布后表单创建失败</a></td>
    <td><a href="/help/forms/troubleshooting-caching-performance.md">自适应Forms缓存问题</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-installation-and-configuration.md#build-pipeline-fails">生成管道失败</a></td>
    <td><a href="/help/forms/form-creation-failing.md#cause-form-creation-fails">模板发布顺序问题</a></td>
    <td><a href="/help/forms/troubleshooting-caching-performance.md#images-videos-not-invalidated">Dispatcher缓存失效问题</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-installation-and-configuration.md#bundles-inactive-state">捆绑包激活问题</a></td>
    <td><a href="/help/forms/known-issues.md">已知的表单创建限制</a></td>
    <td><a href="/help/forms/troubleshooting-caching-performance.md#cdn-caching-stops-working-after-300-seconds">CDN缓存失败</a></td>
  </tr>
  </tbody>
</table>

### 表单提交和集成问题

<table>
  <tbody>
  <tr>
    <td><strong>Edge Delivery Services</strong></td>
    <td><strong>自定义提交操作</strong></td>
    <td><strong>集成问题</strong></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-403-forbidden-edge-delivery-form-submission.md">403表单提交中禁止出现错误</a></td>
    <td><a href="/help/forms/custom-submit-action-troubleshooting.md">自定义提交操作出现502错误</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-27434">DRM-SAML重定向失败</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-403-forbidden-edge-delivery-form-submission.md#cors-issues">CORS配置问题</a></td>
    <td><a href="/help/forms/custom-submit-action-troubleshooting.md#resolution">未处理的异常处理</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-27075">AEM Sites上禁用了“提交”按钮</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-403-forbidden-edge-delivery-form-submission.md#referrer-filter-issues">反向链接筛选条件配置</a></td>
    <td><a href="/help/forms/custom-submit-action-for-adaptive-forms-based-on-core-components.md">自定义操作的最佳实践</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26532">升级后的隐藏字段可见性</a></td>
  </tr>
  </tbody>
</table>

### Designer和开发问题

<table>
  <tbody>
  <tr>
    <td><strong>AEM Forms Designer</strong></td>
    <td><strong>开发环境</strong></td>
    <td><strong>版本和兼容性</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26558">Designer 6.5升级后未打开</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-27089">定位器无法以JDK 8/11开头</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26862">AEM Forms (AEMFD)包版本显示问题</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-21018">PDF Generator JPEG 2000错误</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-22689">JBoss日志路径配置</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26846">Windows中的版本号不正确</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-27406">PDF输出中缺少按钮</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-18084">Configuration Manager升级错误</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-17339">索引损坏解决方法</a></td>
  </tr>
  </tbody>
</table>



