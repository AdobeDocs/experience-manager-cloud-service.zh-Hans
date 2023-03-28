---
title: 使用核心组件和 Headless 构建具有吸引力的表单
seo-title: Build Engaging Forms Using Core Components and Headless
description: 使用核心组件和 Headless 构建具有吸引力的表单
seo-description: Build Engaging Forms Using Core Components and Headless
topic-tags: develop
hide: true
hidefromtoc: true
source-git-commit: f65c5241e1e61e5a0bd9981778939caa313de76a
workflow-type: ht
source-wordcount: '3412'
ht-degree: 100%

---


# 使用核心组件和 Headless 构建具有吸引力的表单

## 实验室概述

在此动手实验室中，您将学习：

如何使用 AEM Forms 通过与 AEM Sites 一致的最新核心组件轻松创建自适应表单，通过将自适应表单作为 Headless 表单交付到 Web、移动设备和聊天来实现全渠道数据捕获体验。您还将了解有关样式化、自定义项和前端开发的最佳实践。

## 要点

* **业务敏捷性**：作为商业用户，我可以轻松地为多个渠道创作表单体验。

* **前端开发人员的力量**：作为前端开发人员，我可以使用 Headless 表单来控制最终用户体验。

* **开发人员速度**：作为开发人员，我可以轻松且一致地自定义 Sites 和 Forms 组件。

## 前提条件


+++AEM Forms as Cloud Service 沙盒



<table>
        <thead>
            <tr><th>实验室 ID</th><th>创作实例 URL</th><th>发布实例 URL</th></tr>           
        </thead>
        <tbody>
            <tr><td>L716001</td><td>https://author-p105303-e986623.adobeaemcloud.com</td><td>https://publish-p105303-e986623.adobeaemcloud.com</td></tr><tr><td>L716002</td><td>https://author-p106405-e993047.adobeaemcloud.com</td><td>https://publish-p106405-e993047.adobeaemcloud.com</td></tr><tr><td>L716003</td><td>https://author-p106406-e993049.adobeaemcloud.com</td><td>https://publish-p106406-e993049.adobeaemcloud.com</td></tr><tr><td>L716004</td><td>https://author-p106398-e993114.adobeaemcloud.com</td><td>https://publish-p106398-e993114.adobeaemcloud.com</td></tr><tr><td>L716005</td><td>https://author-p106407-e993048.adobeaemcloud.com</td><td>https://publish-p106407-e993048.adobeaemcloud.com</td></tr><tr><td>L716006</td><td>https://author-p106408-e993155.adobeaemcloud.com</td><td>https://publish-p106408-e993155.adobeaemcloud.com</td></tr><tr><td>L716007</td><td>https://author-p106343-e993067.adobeaemcloud.com</td><td>https://publish-p106343-e993067.adobeaemcloud.com</td></tr><tr><td>L716008</td><td>https://author-p106399-e993108.adobeaemcloud.com</td><td>https://publish-p106399-e993108.adobeaemcloud.com</td></tr><tr><td>L716009</td><td>https://author-p106344-e993064.adobeaemcloud.com</td><td>https://publish-p106344-e993064.adobeaemcloud.com</td></tr><tr><td>L716010</td><td>https://author-p106409-e993051.adobeaemcloud.com</td><td>https://publish-p106409-e993051.adobeaemcloud.com</td></tr><tr><td>L716011</td><td>https://author-p106345-e993060.adobeaemcloud.com</td><td>https://publish-p106345-e993060.adobeaemcloud.com</td></tr><tr><td>L716012</td><td>https://author-p106346-e993061.adobeaemcloud.com</td><td>https://publish-p106346-e993061.adobeaemcloud.com</td></tr><tr><td>L716013</td><td>https://author-p106410-e993153.adobeaemcloud.com</td><td>https://publish-p106410-e993153.adobeaemcloud.com</td></tr><tr><td>L716014</td><td>https://author-p106502-e993073.adobeaemcloud.com</td><td>https://publish-p106502-e993073.adobeaemcloud.com</td></tr><tr><td>L716015</td><td>https://author-p106401-e993112.adobeaemcloud.com</td><td>https://publish-p106401-e993112.adobeaemcloud.com</td></tr><tr><td>L716016</td><td>https://author-p106452-e993115.adobeaemcloud.com</td><td>https://publish-p106452-e993115.adobeaemcloud.com</td></tr><tr><td>L716017</td><td>https://author-p106453-e993113.adobeaemcloud.com</td><td>https://publish-p106453-e993113.adobeaemcloud.com</td></tr><tr><td>L716018</td><td>https://author-p106411-e993050.adobeaemcloud.com</td><td>https://publish-p106411-e993050.adobeaemcloud.com</td></tr><tr><td>L716019</td><td>https://author-p106454-e993116.adobeaemcloud.com</td><td>https://publish-p106454-e993116.adobeaemcloud.com</td></tr><tr><td>L716020</td><td>https://author-p106347-e993063.adobeaemcloud.com</td><td>https://publish-p106347-e993063.adobeaemcloud.com</td></tr><tr><td>L716021</td><td>https://author-p106455-e993109.adobeaemcloud.com</td><td>https://publish-p106455-e993109.adobeaemcloud.com</td></tr><tr><td>L716022</td><td>https://author-p106456-e993110.adobeaemcloud.com</td><td>https://publish-p106456-e993110.adobeaemcloud.com</td></tr><tr><td>L716023</td><td>https://author-p106466-e993291.adobeaemcloud.com</td><td>https://publish-p106466-e993291.adobeaemcloud.com</td></tr><tr><td>L716024</td><td>https://author-p106413-e993156.adobeaemcloud.com</td><td>https://publish-p106413-e993156.adobeaemcloud.com</td></tr><tr><td>L716025</td><td>https://author-p106348-e993066.adobeaemcloud.com</td><td>https://publish-p106348-e993066.adobeaemcloud.com</td></tr><tr><td>L716026</td><td>https://author-p106414-e993154.adobeaemcloud.com</td><td>https://publish-p106414-e993154.adobeaemcloud.com</td></tr><tr><td>L716027</td><td>https://author-p106349-e993065.adobeaemcloud.com</td><td>https://publish-p106349-e993065.adobeaemcloud.com</td></tr><tr><td>L716028</td><td>https://author-p106415-e993152.adobeaemcloud.com</td><td>https://publish-p106415-e993152.adobeaemcloud.com</td></tr><tr><td>L716029</td><td>https://author-p106350-e993068.adobeaemcloud.com</td><td>https://publish-p106350-e993068.adobeaemcloud.com</td></tr><tr><td>L716030</td><td>https://author-p106351-e993062.adobeaemcloud.com</td><td>https://publish-p106351-e993062.adobeaemcloud.com</td></tr><tr><td>L716031</td><td>https://author-p106417-e993158.adobeaemcloud.com</td><td>https://publish-p106417-e993158.adobeaemcloud.com</td></tr><tr><td>L716032</td><td>https://author-p106418-e993159.adobeaemcloud.com</td><td>https://publish-p106418-e993159.adobeaemcloud.com</td></tr><tr><td>L716033</td><td>https://author-p106503-e993080.adobeaemcloud.com</td><td>https://publish-p106503-e993080.adobeaemcloud.com</td></tr><tr><td>L716034</td><td>https://author-p106457-e993125.adobeaemcloud.com</td><td>https://publish-p106457-e993125.adobeaemcloud.com</td></tr><tr><td>L716035</td><td>https://author-p106504-e993081.adobeaemcloud.com</td><td>https://publish-p106504-e993081.adobeaemcloud.com</td></tr><tr><td>L716036</td><td>https://author-p106458-e993120.adobeaemcloud.com</td><td>https://publish-p106458-e993120.adobeaemcloud.com</td></tr><tr><td>L716037</td><td>https://author-p106419-e993160.adobeaemcloud.com</td><td>https://publish-p106419-e993160.adobeaemcloud.com</td></tr><tr><td>L716038</td><td>https://author-p106420-e993162.adobeaemcloud.com</td><td>https://publish-p106420-e993162.adobeaemcloud.com</td></tr><tr><td>L716039</td><td>https://author-p106517-e993235.adobeaemcloud.com</td><td>https://publish-p106517-e993235.adobeaemcloud.com</td></tr><tr><td>L716040</td><td>https://author-p106506-e993079.adobeaemcloud.com</td><td>https://publish-p106506-e993079.adobeaemcloud.com</td></tr><tr><td>L716041</td><td>https://author-p106507-e993074.adobeaemcloud.com</td><td>https://publish-p106507-e993074.adobeaemcloud.com</td></tr><tr><td>L716042</td><td>https://author-p106508-e993075.adobeaemcloud.com</td><td>https://publish-p106508-e993075.adobeaemcloud.com</td></tr><tr><td>L716043</td><td>https://author-p106421-e993163.adobeaemcloud.com</td><td>https://publish-p106421-e993163.adobeaemcloud.com</td></tr><tr><td>L716044</td><td>https://author-p106459-e993121.adobeaemcloud.com</td><td>https://publish-p106459-e993121.adobeaemcloud.com</td></tr><tr><td>L716045</td><td>https://author-p106467-e993292.adobeaemcloud.com</td><td>https://publish-p106467-e993292.adobeaemcloud.com</td></tr><tr><td>L716046</td><td>https://author-p106518-e993234.adobeaemcloud.com</td><td>https://publish-p106518-e993234.adobeaemcloud.com</td></tr><tr><td>L716047</td><td>https://author-p106511-e993076.adobeaemcloud.com</td><td>https://publish-p106511-e993076.adobeaemcloud.com</td></tr><tr><td>L716048</td><td>https://author-p106512-e993077.adobeaemcloud.com</td><td>https://publish-p106512-e993077.adobeaemcloud.com</td></tr><tr><td>L716049</td><td>https://author-p106460-e993124.adobeaemcloud.com</td><td>https://publish-p106460-e993124.adobeaemcloud.com</td></tr><tr><td>L716050</td><td>https://author-p106519-e993237.adobeaemcloud.com</td><td>https://publish-p106519-e993237.adobeaemcloud.com</td></tr><tr><td>L716051</td><td>https://author-p106513-e993084.adobeaemcloud.com</td><td>https://publish-p106513-e993084.adobeaemcloud.com</td></tr><tr><td>L716052</td><td>https://author-p106461-e993122.adobeaemcloud.com</td><td>https://publish-p106461-e993122.adobeaemcloud.com</td></tr><tr><td>L716053</td><td>https://author-p106514-e993082.adobeaemcloud.com</td><td>https://publish-p106514-e993082.adobeaemcloud.com</td></tr><tr><td>L716054</td><td>https://author-p106462-e993123.adobeaemcloud.com</td><td>https://publish-p106462-e993123.adobeaemcloud.com</td></tr><tr><td>L716055</td><td>https://author-p106463-e993127.adobeaemcloud.com</td><td>https://publish-p106463-e993127.adobeaemcloud.com</td></tr><tr><td>L716056</td><td>https://author-p106515-e993083.adobeaemcloud.com</td><td>https://publish-p106515-e993083.adobeaemcloud.com</td></tr><tr><td>L716057</td><td>https://author-p106464-e993126.adobeaemcloud.com</td><td>https://publish-p106464-e993126.adobeaemcloud.com</td></tr><tr><td>L716058</td><td>https://author-p106520-e993236.adobeaemcloud.com</td><td>https://publish-p106520-e993236.adobeaemcloud.com</td></tr><tr><td>L716059</td><td>https://author-p106423-e993161.adobeaemcloud.com</td><td>https://publish-p106423-e993161.adobeaemcloud.com</td></tr><tr><td>L716060</td><td>https://author-p106516-e993078.adobeaemcloud.com</td><td>https://publish-p106516-e993078.adobeaemcloud.com</td></tr><tr><td>L716061</td><td>https://author-p106521-e993240.adobeaemcloud.com</td><td>https://publish-p106521-e993240.adobeaemcloud.com</td></tr><tr><td>L716062</td><td>https://author-p106424-e993308.adobeaemcloud.com</td><td>https://publish-p106424-e993308.adobeaemcloud.com</td></tr><tr><td>L716063</td><td>https://author-p106468-e993295.adobeaemcloud.com</td><td>https://publish-p106468-e993295.adobeaemcloud.com</td></tr><tr><td>L716064</td><td>https://author-p106425-e993309.adobeaemcloud.com</td><td>https://publish-p106425-e993309.adobeaemcloud.com</td></tr><tr><td>L716065</td><td>https://author-p106426-e993314.adobeaemcloud.com</td><td>https://publish-p106426-e993314.adobeaemcloud.com</td></tr><tr><td>L716066</td><td>https://author-p106469-e993293.adobeaemcloud.com</td><td>https://publish-p106469-e993293.adobeaemcloud.com</td></tr><tr><td>L716067</td><td>https://author-p106522-e993238.adobeaemcloud.com</td><td>https://publish-p106522-e993238.adobeaemcloud.com</td></tr><tr><td>L716068</td><td>https://author-p106470-e993299.adobeaemcloud.com</td><td>https://publish-p106470-e993299.adobeaemcloud.com</td></tr><tr><td>L716069</td><td>https://author-p106427-e993311.adobeaemcloud.com</td><td>https://publish-p106427-e993311.adobeaemcloud.com</td></tr><tr><td>L716070</td><td>https://author-p106428-e993310.adobeaemcloud.com</td><td>https://publish-p106428-e993310.adobeaemcloud.com</td></tr><tr><td>L716071</td><td>https://author-p106471-e993298.adobeaemcloud.com</td><td>https://publish-p106471-e993298.adobeaemcloud.com</td></tr><tr><td>L716072</td><td>https://author-p106429-e993315.adobeaemcloud.com</td><td>https://publish-p106429-e993315.adobeaemcloud.com</td></tr><tr><td>L716073</td><td>https://author-p106523-e993239.adobeaemcloud.com</td><td>https://publish-p106523-e993239.adobeaemcloud.com</td></tr><tr><td>L716074</td><td>https://author-p106472-e993300.adobeaemcloud.com</td><td>https://publish-p106472-e993300.adobeaemcloud.com</td></tr><tr><td>L716075</td><td>https://author-p106430-e993312.adobeaemcloud.com</td><td>https://publish-p106430-e993312.adobeaemcloud.com</td></tr><tr><td>L716076</td><td>https://author-p106524-e993241.adobeaemcloud.com</td><td>https://publish-p106524-e993241.adobeaemcloud.com</td></tr><tr><td>L716077</td><td>https://author-p106431-e993313.adobeaemcloud.com</td><td>https://publish-p106431-e993313.adobeaemcloud.com</td></tr><tr><td>L716078</td><td>https://author-p106473-e993294.adobeaemcloud.com</td><td>https://publish-p106473-e993294.adobeaemcloud.com</td></tr><tr><td>L716079</td><td>https://author-p106474-e993297.adobeaemcloud.com</td><td>https://publish-p106474-e993297.adobeaemcloud.com</td></tr><tr><td>L716080</td><td>https://author-p106475-e993296.adobeaemcloud.com</td><td>https://publish-p106475-e993296.adobeaemcloud.com</td></tr><tr><td>L716081</td><td>https://author-p106476-e993353.adobeaemcloud.com</td><td>https://publish-p106476-e993353.adobeaemcloud.com</td></tr><tr><td>L716082</td><td>https://author-p106525-e993247.adobeaemcloud.com</td><td>https://publish-p106525-e993247.adobeaemcloud.com</td></tr><tr><td>L716083</td><td>https://author-p106526-e993244.adobeaemcloud.com</td><td>https://publish-p106526-e993244.adobeaemcloud.com</td></tr><tr><td>L716084</td><td>https://author-p106527-e993243.adobeaemcloud.com</td><td>https://publish-p106527-e993243.adobeaemcloud.com</td></tr><tr><td>L716085</td><td>https://author-p106477-e993356.adobeaemcloud.com</td><td>https://publish-p106477-e993356.adobeaemcloud.com</td></tr><tr><td>L716086</td><td>https://author-p106478-e993355.adobeaemcloud.com</td><td>https://publish-p106478-e993355.adobeaemcloud.com</td></tr><tr><td>L716087</td><td>https://author-p106528-e993245.adobeaemcloud.com</td><td>https://publish-p106528-e993245.adobeaemcloud.com</td></tr><tr><td>L716088</td><td>https://author-p106432-e993316.adobeaemcloud.com</td><td>https://publish-p106432-e993316.adobeaemcloud.com</td></tr><tr><td>L716089</td><td>https://author-p106529-e993242.adobeaemcloud.com</td><td>https://publish-p106529-e993242.adobeaemcloud.com</td></tr><tr><td>L716090</td><td>https://author-p106436-e993320.adobeaemcloud.com</td><td>https://publish-p106436-e993320.adobeaemcloud.com</td></tr><tr><td>L716091</td><td>https://author-p106480-e993301.adobeaemcloud.com</td><td>https://publish-p106480-e993301.adobeaemcloud.com</td></tr><tr><td>L716092</td><td>https://author-p106530-e993246.adobeaemcloud.com</td><td>https://publish-p106530-e993246.adobeaemcloud.com</td></tr><tr><td>L716093</td><td>https://author-p106481-e993352.adobeaemcloud.com</td><td>https://publish-p106481-e993352.adobeaemcloud.com</td></tr><tr><td>L716094</td><td>https://author-p106482-e993354.adobeaemcloud.com</td><td>https://publish-p106482-e993354.adobeaemcloud.com</td></tr><tr><td>L716095</td><td>https://author-p106531-e993248.adobeaemcloud.com</td><td>https://publish-p106531-e993248.adobeaemcloud.com</td></tr><tr><td>L716096</td><td>https://author-p106483-e993357.adobeaemcloud.com</td><td>https://publish-p106483-e993357.adobeaemcloud.com</td></tr><tr><td>L716097</td><td>https://author-p106433-e993318.adobeaemcloud.com</td><td>https://publish-p106433-e993318.adobeaemcloud.com</td></tr><tr><td>L716098</td><td>https://author-p106532-e993249.adobeaemcloud.com</td><td>https://publish-p106532-e993249.adobeaemcloud.com</td></tr><tr><td>L716099</td><td>https://author-p106434-e993317.adobeaemcloud.com</td><td>https://publish-p106434-e993317.adobeaemcloud.com</td></tr><tr><td>L716100</td><td>https://author-p106435-e993319.adobeaemcloud.com</td><td>https://publish-p106435-e993319.adobeaemcloud.com</td></tr>
        </tbody>
</table>

+++

## 第 1 课

### 目标

自行熟悉 AEM Forms as a Cloud Service 环境。

### 课程背景

在本课中，您将通过导航用户界面来自行熟悉 AEM Forms as a Cloud Service 环境。

### 练习

1. 打开浏览器并输入 Cloud Service 创作环境的 URL。例如：
   [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/start.html](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/start.html)

1. 登录到 Cloud Service 创作环境。您的创作环境的登录凭据将在实验室期间与您共享。

1. 登录后，导航至 AEM Forms UI。单击&#x200B;**表单**。

   ![](/help/forms/assets/screenshot2028113829.png)

1. 单击&#x200B;**表单和文档**。关闭任何与偏好设置或信息相关的弹出窗口。

   ![](/help/forms/assets/screenshot2028113929.png)

   将显示所有可用的表单。

   ![](/help/forms/assets/screenshot2028114029.png)

## 第 2 课

### 目标

使用最新的核心组件创作自适应表单，然后配置并提交表单。

### 课程背景

在本课中，作为商业用户，您将使用自适应表单创作功能和用于数据捕获的标准化 OOTB 核心组件，为 Web、移动设备和聊天等多个渠道创作自适应表单。

### 练习

1. 为表单创建提交端点：

   1. 在新的浏览器标签页中打开 <https://requestbin.com/>。
      ![](/help/forms/assets/screenshot2028114329.png)

   1. 单击&#x200B;**创建公共 bin** 并复制端点 URL。
      ![](/help/forms/assets/screenshot202023-03-0120at206.10.0020pm.png)

1. 使用“向导”界面创作自适应表单：

   1. 在第 1 课中使用的浏览器标签页中，导航至 AEM Forms as Cloud Service Web 界面，然后导航至“表单和文档”。
      ![](/help/forms/assets/screenshot2028114029.png)

   1. 单击&#x200B;**创建**并选择“自适应表单”。
      ![](/help/forms/assets/screenshot2028114629.png)

   1. 从模板选择屏幕中选择&#x200B;**空白（核心组件）**模板，如下所示：
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.1520pm.png)

   1. 单击&#x200B;**样式**&#x200B;选项卡，选择 **wknd-theme** 主题，如下所示：
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.2320pm.png)

   1. 单击&#x200B;**提交**&#x200B;选项卡，并选择&#x200B;**提交到 REST 端点**信息卡，并在
      **POST 请求的 URL** 字段中指定公共 bin，如下所示：
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.5320pm.png)

   1. 单击&#x200B;**创建**。为表单指定名称和标题。例如，**contactus**。单击&#x200B;**创建**。
      ![](/help/forms/assets/screenshot2028123329.png)

   1. 这将打开自适应表单编辑器。关闭偏好设置或信息的任何弹出窗口或对话框。单击左边栏上的组件浏览器并将&#x200B;**页脚**组件添加到空白表单的底部。
      ![](/help/forms/assets/screenshot2028121929.png)

   1. 页眉是自适应表单模板的一部分。利用它，可轻松地在所有自适应表单中提供一致的页眉/页脚。或者，您也可以选择使其在表单中保持可编辑状态，如下一步中的页脚组件所示。

   1. 在表单中间添加一个&#x200B;**标题**组件。
      ![](/help/forms/assets/screenshot2028122129.png)

   1. 在标题组件的后面添加一个&#x200B;**文本输入**组件。
      ![](/help/forms/assets/screenshot2028122329.png)

   1. 添加一个&#x200B;**数值输入**组件。
      ![](/help/forms/assets/screenshot2028122429.png)

   1. 将&#x200B;**提交按钮**组件添加到表单。
      ![](/help/forms/assets/screenshot2028122529.png)

   1. 单击&#x200B;**标题**&#x200B;组件，以便显示&#x200B;**弹出菜单**。单击菜单中的&#x200B;**编辑图标**以编辑标签。
      ![](/help/forms/assets/screenshot2028122629.png)

   1. 输入 `Contact Us` 作为标题文本。
      ![](/help/forms/assets/screenshot2028122829.png)

   1. 单击&#x200B;**文本输入**&#x200B;组件，以便显示弹出菜单。单击菜单中的&#x200B;**编辑图标**以编辑标签。
      ![](/help/forms/assets/screenshot2028122929.png)

   1. 输入&#x200B;**全名**作为字段标签。
      ![](/help/forms/assets/screenshot2028123029.png)

   1. 单击&#x200B;**数值输入**&#x200B;组件，以便显示弹出菜单。单击菜单中的&#x200B;**编辑图标**以编辑标签。
      ![](/help/forms/assets/screenshot2028123129.png)

   1. 输入&#x200B;**电话号码**作为字段标签。
      ![](/help/forms/assets/screenshot2028123829.png)


1. 向表单添加验证：

   1. 单击&#x200B;**电话号码**&#x200B;组件，以便显示弹出菜单。单击菜单中的&#x200B;**“扳手”图标**以配置字段。
      ![](/help/forms/assets/screenshot2028123429.png)

   1. 打开&#x200B;**验证选项卡**，将字段标记为&#x200B;**必填**，然后单击&#x200B;**完成**。这将显示成功消息。
      ![](/help/forms/assets/screenshot2028123529.png)

      ![](/help/forms/assets/screenshot2028123629.png)

   1. 单击&#x200B;**预览**以从最终用户的角度预览表单。
      ![](/help/forms/assets/screenshot2028125529.png)

   1. 用虚拟数据填写表单
      ![](/help/forms/assets/screenshot2028125629.png)

   1. 提交表单
      ![](/help/forms/assets/screenshot2028125729.png)

   1. 在“请求 bin”选项卡中，检查提交的数据。
      ![](/help/forms/assets/screenshot2028125829.png)

现在，为了完成剩余练习，请使用预先创建的注册表单。

1. 打开 AEM Forms 管理界面（例如 `https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments`），选择注册表单。

   ![](/help/forms/assets/screenshot2028115529.png)

1. 单击&#x200B;**发布**。

   ![](/help/forms/assets/screenshot2028115629.png)

   这将显示成功消息。

   ![](/help/forms/assets/screenshot2028115729.png)

   表单的发布 URL 类似于 `https://publish-p105303-e986623.adobeaemcloud.com/content/forms/af/registration.html`。

1. 要查看已发布的表单，请将上述 URL 中的程序 ID (pXXXXXX) 和环境 ID (eXXXXXX) 替换为您的环境 ID。

## 第 3 课

### 目标

使用前端开发最佳实践更新样式。

### 课程背景

在本课中，作为前端开发人员，您将了解如何轻松地更新先前创建的自适应表单的样式。

### 练习

设置主题的本地存储库：

1. 使用管理员权限打开命令提示符或 shell：

   ![](/help/forms/assets/screenshot2028115829.png)

1. 在命令提示符下，使用以下命令导航到 **c:\git** 文件夹

   ```Shell
   cd c:\git
   ```

1. 使用以下命令克隆主题前端代码：

   ```Shell
   git clone -b WKND https://github.com/adobe/aem-forms-theme-canvas
   ```


1. 按照列出的顺序使用以下命令导航到 **aem-forms-theme-canvas** 目录并打开 Visual Studio Code。

   ```Shell
   cd aem-forms-theme-canvas
   code .
   ```

   ![](/help/forms/assets/screenshot2028126029.png)

1. 选择&#x200B;**信任父文件夹中所有文件的作者**，并单击&#x200B;**是的，我信任作者**。

   ![](/help/forms/assets/screenshot2028116229.png)

1. 要呈现在云服务发布环境中托管的表单，请重命名 `env_template` 文件。要重命名此文件，请右键单击 **env_template** 文件并选择&#x200B;**重命名**&#x200B;选项。

   ![](/help/forms/assets/screenshot2028116429.png)

   </br>

   ![](/help/forms/assets/screenshot2028116529.png)

1. 为 .env 文件中的变量设置以下值并保存文件：

   * **AEM_URL**：指定您的云服务发布环境。例如，`https://publish-p105303-e986623.adobeaemcloud.com/`

   * **AEM_ADAPTIVE_FORM**：指定表单的路径。例如，如果表单路径为 `/content/forms/af/registration`，则此变量的值将为 `registration`。

   ![](/help/forms/assets/screenshot2028116429.png)


1. 在命令提示符窗口中，运行以下命令：

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028117029.png)

   >[!NOTE]
   >
   > * 如果您收到一条消息，要求您通过 `npm notice Run npm nstall -g npm@9.6.0` 命令更新 npm，请忽略此消息。
   > * 除非工作簿中指示您运行其他 npm 命令，否则不要这样做。


1. 现在，运行以下命令来预览表单。

   ```Shell
   npm run live
   ```

   ![](/help/forms/assets/screenshot2028117229.png)

   执行上述命令后，等待 `webpack compiled` 消息。表单将显示在浏览器标签页中。

   >[!NOTE]
   >
   >如果在执行 `npm run live` 命令超过 3-4 分钟后，浏览器出现黑屏，请将浏览器 URL 中的 `localhost` 更改为 127.0.0.1，并点按 **Enter**。


   ![](/help/forms/assets/screenshot2028115129.png)


1. 在 Visual Studio Code 中，打开 `PROJECT\src\site\_variables.scss` 文件。请注意，`$error` 颜色是红色阴影。

   ![](/help/forms/assets/screenshot2028120729.png)

1. 在浏览器中，提交表单以在&#x200B;**名字**&#x200B;字段中看到红色。

   ![](/help/forms/assets/screenshot2028120829.png)

1. 将 **$error** 颜色设置为 **#5736eb** 并保存文件。

   ![](/help/forms/assets/screenshot2028120729.png)

1. 刷新浏览器并提交表单。请注意，“名字”字段上的错误颜色已相应地发生变化。

   ![](/help/forms/assets/screenshot2028121129.png)

1. 在命令提示符中，按 **Ctrl+C**，输入 **Y**，然后按 **Enter** 键以终止 npm 进程。请务必停止 npm 服务器，以避免与下一组练习发生冲突。
1. 关闭 Visual Studio Code 和命令提示符窗口。

## 第 4 课

### 目标

将表单作为 Headless 表单呈现到 Web/移动设备和其他界面。

### 课程背景

在本课中，作为前端开发人员，您将了解如何使用 React 图谱设计框架将之前创建的自适应表单呈现为 Headless 表单。

### 练习

使用 React 初学者项目设置本地存储库：

1. 使用管理员权限打开命令提示符。

   ![](/help/forms/assets/screenshot2028115829.png)

1. 在命令提示符下，使用以下命令导航到 **c:\git** 文件夹

   ```Shell
   cd c:\git
   ```

1. 使用以下命令克隆自适应表单 React 初学者项目：

   ```Shell
   git clone https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028117329.png)

1. 按照列出的顺序使用以下命令导航到 **react-starter-kit-aem-headless-forms** 目录并打开 Visual Studio Code。

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028117529.png)


   这将打开 Visual Studio Code 窗口。

   ![](/help/forms/assets/screenshot2028117429.png)

要呈现在云服务发布环境中托管的表单，请执行以下操作：

1. 将 env_template 文件重命名为 .env 文件。要重命名，请右键单击 **env_template** 文件并选择&#x200B;**重命名**&#x200B;选项。

   ![](/help/forms/assets/screenshot2028117629.png)

   ![](/help/forms/assets/screenshot2028117729.png)

1. 为 .env 文件中的变量设置以下值。更新变量后，保存文件。

   * **AEM_URL**：指定云服务发布环境的 URL。例如，`https://publish-p105303-e986623.adobeaemcloud.com`

   * **AEM_FORM_PATH**：指定上一节课中创建的自适应表单的路径。例如，`/content/forms/af/registration/`

      ![](/help/forms/assets/screenshot202023-03-0820at202.49.1820pm.png)

1. 打开命令窗口，确保您位于 react-starter-kit-aem-headless-forms 目录中，然后运行以下命令：

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028118029.png)


1. 在命令提示符窗口中，运行以下命令：

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028118129.png)

   上面的命令将启动一个本地开发服务器，该服务器将使用 react-spectrum 前端库以 Headless 方式呈现从 AEM 获取的表单定义。

   >[!NOTE]
   >
   > 
   > 如果在执行 `npm start` 命令超过 3-4 分钟后，浏览器出现黑屏，请将浏览器 URL 中的 `localhost` 更改为 127.0.0.1，并点按 **Enter**。

   ![](/help/forms/assets/screenshot2028118229.png)

让我们检查此 Headless 表单中的规则执行情况：

1. 选择&#x200B;**选中框以接收 5% 的折扣**&#x200B;选项。用于申请信用卡的后续选项已被禁用。

   ![](/help/forms/assets/screenshot2028126229.png)

1. 取消选择&#x200B;**选中框以接收 5% 的折扣**，启用信用卡选项。

   ![](/help/forms/assets/screenshot2028126329.png)

让我们以商业用户的身份对服务器上的表单进行更改，并自动查看 Headless 表单中反映的更改。

1. 在浏览器中打开 AEM Forms 管理界面。例如，[https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/forms.html/content/dam/formsanddocuments](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments)。

1. 选择&#x200B;**注册**&#x200B;表单并点击&#x200B;**编辑。**&#x200B;这将在自适应表单编辑器中打开表单。

   ![](/help/forms/assets/screenshot2028118529.png)

1. 选择&#x200B;**电话号码**&#x200B;字段并单击工具栏中的&#x200B;**编辑图标（铅笔图标）**。如果您看不到弹出工具栏，请单击右上角的&#x200B;**编辑**&#x200B;按钮（**预览**&#x200B;按钮左侧）以切换到编辑模式。

   ![](/help/forms/assets/screenshot2028119629.png)

1. 将标签更改为手机号码。单击表单中的任意空白区域，这将保存对表单所做的更改。

   ![](/help/forms/assets/screenshot2028119729.png)

让我们发布更新后的表单以将更改传播到发布环境。

1. 在 AEM Forms 管理界面选项卡中，选择注册表单，然后单击&#x200B;**取消发布**。如果您没有看到&#x200B;**取消发布**&#x200B;按钮，请跳至步骤 3 以直接发布更改。

   ![](/help/forms/assets/screenshot2028119829.png)

1. 单击&#x200B;**取消发布**。在相应的对话框中单击&#x200B;**关闭**。

   ![](/help/forms/assets/screenshot2028119929.png)

   ![](/help/forms/assets/screenshot2028120029.png)


1. 在浏览器刷新后，选择注册表单，然后单击&#x200B;**发布**。

   ![](/help/forms/assets/screenshot2028120129.png)


1. 单击&#x200B;**发布**。在相应的对话框中，单击&#x200B;**关闭**。

   ![](/help/forms/assets/screenshot2028120329.png)

   ![](/help/forms/assets/screenshot2028120429.png)

1. 刷新显示了 Headless 表单的浏览器标签页。请注意，电话号码标签已更改为手机号码。

   ![](/help/forms/assets/screenshot2028120529.png)

1. 打开用于启动 **react-starter-kit-aem-headless-forms** 项目的命令提示符窗口，按 **Ctrl+C**，然后输入 **Y** 并按 Enter 键以终止 npm 进程。请务必停止 npm 服务器，以避免与下一组练习发生冲突。

1. 关闭 Visual Studio Code 和命令提示符窗口。


## 第 5 课

### 目标

使用 Google Material UI 将表单呈现为 Headless 表单

### 课程背景

在本课中，作为前端开发人员，您将了解如何使用 Google Material UI 将之前创建的自适应表单呈现为 Headless 表单。

### 练习

使用 Material UI 初学者项目设置本地存储库：

1. 使用管理员权限打开命令提示符。

   ![](/help/forms/assets/screenshot2028115829.png)


1. 在命令提示符下，使用以下命令导航到 **c:\git** 文件夹：

   ```Shell
   cd c:\git
   ```

1. 按列出的顺序运行以下命令以创建名为 mui 的文件夹，并使用以下命令导航到 mui 文件夹：

   ```Shell
   mkdir mui
   
   cd mui
   ```

1. 使用以下命令克隆自适应表单 React 初学者项目：

   ```Shell
   git clone -b mui https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028126529.png)

1. 按照列出的顺序使用以下命令导航到 **react-starter-kit-aem-headless-forms** 文件夹，并在 Visual Studio Code 中打开代码：

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028126829.png)

要呈现在云服务发布环境中托管的表单，请执行以下操作：

1. 将 **env_template** 文件重命名为 **.env** 文件。要重命名，请右键单击 **env_template** 文件并选择&#x200B;**重命名**。

   ![](/help/forms/assets/screenshot2028126629.png)

1. 为 .env 文件中的变量设置以下值。更新变量后，保存文件。使用 **Ctrl + S** 开关组合来保存文件。

   * **AEM_URL**：指定云服务发布环境的 URL。例如，[https://publish-p105303-e986623.adobeaemcloud.com](https://publish-p105303-e986623.adobeaemcloud.com/)

   * **AEM_FORM_PATH**：指定上一节课中创建的自适应表单的路径。例如，/content/forms/af/registration/

      ![](/help/forms/assets/screenshot2028126929.png)

1. 打开命令窗口，确保您位于 **react-starter-kit-aem-headless-forms** 目录中，然后运行以下命令：

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028127029.png)

1. 在命令提示符窗口中，运行以下命令：

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028127129.png)

   该命令将启动一个本地开发服务器，并使用 Google Material UI 前端库以 Headless 方式呈现从 AEM 获取的表单定义。

   >[!NOTE]
   >
   >如果在执行 `npm start` 命令超过 3-4 分钟后，浏览器出现黑屏，请将浏览器 URL 中的 `localhost` 更改为 127.0.0.1，并点按 **Enter**。

   ![](/help/forms/assets/screenshot2028127229.png)

1. 要评估同一业务逻辑在此表单演绎版中的执行情况，请执行以下操作：

   选择&#x200B;**选中框以接收 5% 的折扣**。后续选项&#x200B;**您想申请 We Finance 公司信用卡表单吗？**&#x200B;已被禁用。

   ![](/help/forms/assets/screenshot2028127329.png)

## 第 6 课

### 目标

使用 Material UI 组件变体创建 Headless 表单的替代外观

### 课程背景

在本课中，作为前端开发人员，您将了解如何使用 Material UI 为商业用户之前创建的自适应表单创建不同组件的替代表示形式。

### 练习

更新 Headless 项目中的组件变体。要将 Material UI 文本输入组件的变体更改为 `OutlinedInput`，请执行以下操作：

1. 在 Visual Code 中，通过打开位于 `src/components/textinput/index.tsx` 的 `index.tsx` 文件来导航到文本输入组件。

1. 在代码行 103 的开头添加 `//`。它将行转换为注释。

   ```Shell
   //const Cmp = \'outlined\' === appliedCssClassNames ? OutlinedInput: Input;
   ```

1. 在第 104 行添加以下内容以使用不同的组件变体并保存文件。使用 **Ctrl + S** 开关组合来保存文件。

   ```Shell
   const Cmp = OutlinedInput;
   ```

   ![](/help/forms/assets/screenshot2028127629.png)

   必须为“OutlinedInput”变体使用正确的大写形式，否则编译将失败。本地开发环境编译自动在命令提示符处开始。等待，直到您看到以下消息

   `webpack 5.75.0 compiled with 3 warnings in 6659 ms`
   `inside proxy req`
   `setting new origin header`

1. 刷新浏览器（如果它未自动刷新）可以看到文本输入组件使用了其他变体。

   ![](/help/forms/assets/screenshot2028127729.png)


   对于最终用户来说，无需对 AEM Forms Server 中的表单定义进行任何更改即可进行此更改，并且它特定于正在考虑的 Headless 渠道。例如，本实验室中的 Web 渠道。

   ![](/help/forms/assets/screenshot2028127529.png)


1. 关闭 Visual Studio Code 和命令提示符窗口。

## 常见问题解答 (FAQ)

+++ 自适应表单向导是否公开可用？

是的，它与 AEM Forms as Cloud Service 一起提供。

+++


+++ 核心组件是否公开可用？

是的，自适应表单核心组件与 AEM Forms as Cloud Service 一起提供。

+++

+++ Headless 表单是否公开可用？

是的，Headless 表单与 AEM Forms as Cloud Service 一起提供。

+++

+++ Headless 表单是否需要单独的许可证？

否，Headless 表单使用相同的许可价值指标，即表单提交次数。

+++

+++ AEM 6.5 Forms 是否提供核心组件和 Headless 表单？

是的，AEM Forms 6.5 Service Pack 16 及更高版本都提供自适应表单核心组件和 Headless 表单。

+++


## 后续步骤

现在，您已了解如何构建自适应表单并使用 Headless 表单将它们传送到多个渠道，您应尝试将您的新技能付诸实践。通过为您的最终用户大规模创建和提供卓越的数据捕获体验，享受其中的乐趣并继续前进！

## 资源

* [自适应表单核心组件简介](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)

* [使用核心组件创建自适应表单](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html)

* [更新基于核心组件的 AF 的样式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html?lang=en)

* [Headless 自适应表单](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=en)

* [使用 Headless React 初学者套件](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/get-started/create-and-publish-a-headless-form.html?lang=en)


