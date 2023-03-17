---
title: 使用核心组件和无头构建引人入胜的Forms
seo-title: Build Engaging Forms Using Core Components and Headless
description: 使用核心组件和无头构建引人入胜的Forms
seo-description: Build Engaging Forms Using Core Components and Headless
topic-tags: develop
hide: true
hidefromtoc: true
source-git-commit: f65c5241e1e61e5a0bd9981778939caa313de76a
workflow-type: tm+mt
source-wordcount: '3412'
ht-degree: 3%

---


# 使用核心组件和无头构建引人入胜的Forms

## 实验室概述

在这个动手实验室中，您会学到：

如何使用AEM Forms使用与AEM Sites一致的最新核心组件轻松创建自适应表单，通过将自适应表单作为无头表单提供到Web、移动设备和聊天，从而实现全方位的数据捕获体验。 您还可以学习有关样式设置、自定义和前端开发的最佳实践。

## 主要优点

* **业务敏捷性**:作为企业用户，我可以轻松地为多个渠道创作表单体验。

* **前端开发人员功能**:作为前端开发人员，我可以使用无头表单控制最终用户体验。

* **开发人员周转率**:作为开发人员，我可以轻松且一致地自定义站点和Forms组件。

## 前提条件


+++AEM Forms作为Cloud Service沙盒



<table>
        <thead>
            <tr><th>实验室ID</th><th>创作实例URL</th><th>发布实例URL</th></tr>           
        </thead>
        <tbody>
            <tr><td>L716001</td><td>https://author-p105303-e986623.adobeaemcloud.com</td><td>https://publish-p105303-e986623.adobeaemcloud.com</td></tr><tr><td>L716002</td><td>https://author-p106405-e993047.adobeaemcloud.com</td><td>https://publish-p106405-e993047.adobeaemcloud.com</td></tr><tr><td>L716003</td><td>https://author-p106406-e993049.adobeaemcloud.com</td><td>https://publish-p106406-e993049.adobeaemcloud.com</td></tr><tr><td>L716004</td><td>https://author-p106398-e993114.adobeaemcloud.com</td><td>https://publish-p106398-e993114.adobeaemcloud.com</td></tr><tr><td>L716005</td><td>https://author-p106407-e993048.adobeaemcloud.com</td><td>https://publish-p106407-e993048.adobeaemcloud.com</td></tr><tr><td>L716006</td><td>https://author-p106408-e993155.adobeaemcloud.com</td><td>https://publish-p106408-e993155.adobeaemcloud.com</td></tr><tr><td>L716007</td><td>https://author-p106343-e993067.adobeaemcloud.com</td><td>https://publish-p106343-e993067.adobeaemcloud.com</td></tr><tr><td>L716008</td><td>https://author-p106399-e993108.adobeaemcloud.com</td><td>https://publish-p106399-e993108.adobeaemcloud.com</td></tr><tr><td>L716009</td><td>https://author-p106344-e993064.adobeaemcloud.com</td><td>https://publish-p106344-e993064.adobeaemcloud.com</td></tr><tr><td>L716010</td><td>https://author-p106409-e993051.adobeaemcloud.com</td><td>https://publish-p106409-e993051.adobeaemcloud.com</td></tr><tr><td>L716011</td><td>https://author-p106345-e993060.adobeaemcloud.com</td><td>https://publish-p106345-e993060.adobeaemcloud.com</td></tr><tr><td>L716012</td><td>https://author-p106346-e993061.adobeaemcloud.com</td><td>https://publish-p106346-e993061.adobeaemcloud.com</td></tr><tr><td>L716013</td><td>https://author-p106410-e993153.adobeaemcloud.com</td><td>https://publish-p106410-e993153.adobeaemcloud.com</td></tr><tr><td>L716014</td><td>https://author-p106502-e993073.adobeaemcloud.com</td><td>https://publish-p106502-e993073.adobeaemcloud.com</td></tr><tr><td>L716015</td><td>https://author-p106401-e993112.adobeaemcloud.com</td><td>https://publish-p106401-e993112.adobeaemcloud.com</td></tr><tr><td>L716016</td><td>https://author-p106452-e993115.adobeaemcloud.com</td><td>https://publish-p106452-e993115.adobeaemcloud.com</td></tr><tr><td>L716017</td><td>https://author-p106453-e993113.adobeaemcloud.com</td><td>https://publish-p106453-e993113.adobeaemcloud.com</td></tr><tr><td>L716018</td><td>https://author-p106411-e993050.adobeaemcloud.com</td><td>https://publish-p106411-e993050.adobeaemcloud.com</td></tr><tr><td>L716019</td><td>https://author-p106454-e993116.adobeaemcloud.com</td><td>https://publish-p106454-e993116.adobeaemcloud.com</td></tr><tr><td>L716020</td><td>https://author-p106347-e993063.adobeaemcloud.com</td><td>https://publish-p106347-e993063.adobeaemcloud.com</td></tr><tr><td>L716021</td><td>https://author-p106455-e993109.adobeaemcloud.com</td><td>https://publish-p106455-e993109.adobeaemcloud.com</td></tr><tr><td>L716022</td><td>https://author-p106456-e993110.adobeaemcloud.com</td><td>https://publish-p106456-e993110.adobeaemcloud.com</td></tr><tr><td>L716023</td><td>https://author-p106466-e993291.adobeaemcloud.com</td><td>https://publish-p106466-e993291.adobeaemcloud.com</td></tr><tr><td>L716024</td><td>https://author-p106413-e993156.adobeaemcloud.com</td><td>https://publish-p106413-e993156.adobeaemcloud.com</td></tr><tr><td>L716025</td><td>https://author-p106348-e993066.adobeaemcloud.com</td><td>https://publish-p106348-e993066.adobeaemcloud.com</td></tr><tr><td>L716026</td><td>https://author-p106414-e993154.adobeaemcloud.com</td><td>https://publish-p106414-e993154.adobeaemcloud.com</td></tr><tr><td>L716027</td><td>https://author-p106349-e993065.adobeaemcloud.com</td><td>https://publish-p106349-e993065.adobeaemcloud.com</td></tr><tr><td>L716028</td><td>https://author-p106415-e993152.adobeaemcloud.com</td><td>https://publish-p106415-e993152.adobeaemcloud.com</td></tr><tr><td>L716029</td><td>https://author-p106350-e993068.adobeaemcloud.com</td><td>https://publish-p106350-e993068.adobeaemcloud.com</td></tr><tr><td>L716030</td><td>https://author-p106351-e993062.adobeaemcloud.com</td><td>https://publish-p106351-e993062.adobeaemcloud.com</td></tr><tr><td>L716031</td><td>https://author-p106417-e993158.adobeaemcloud.com</td><td>https://publish-p106417-e993158.adobeaemcloud.com</td></tr><tr><td>L716032</td><td>https://author-p106418-e993159.adobeaemcloud.com</td><td>https://publish-p106418-e993159.adobeaemcloud.com</td></tr><tr><td>L716033</td><td>https://author-p106503-e993080.adobeaemcloud.com</td><td>https://publish-p106503-e993080.adobeaemcloud.com</td></tr><tr><td>L716034</td><td>https://author-p106457-e993125.adobeaemcloud.com</td><td>https://publish-p106457-e993125.adobeaemcloud.com</td></tr><tr><td>L716035</td><td>https://author-p106504-e993081.adobeaemcloud.com</td><td>https://publish-p106504-e993081.adobeaemcloud.com</td></tr><tr><td>L716036</td><td>https://author-p106458-e993120.adobeaemcloud.com</td><td>https://publish-p106458-e993120.adobeaemcloud.com</td></tr><tr><td>L716037</td><td>https://author-p106419-e993160.adobeaemcloud.com</td><td>https://publish-p106419-e993160.adobeaemcloud.com</td></tr><tr><td>L716038</td><td>https://author-p106420-e993162.adobeaemcloud.com</td><td>https://publish-p106420-e993162.adobeaemcloud.com</td></tr><tr><td>L716039</td><td>https://author-p106517-e993235.adobeaemcloud.com</td><td>https://publish-p106517-e993235.adobeaemcloud.com</td></tr><tr><td>L716040</td><td>https://author-p106506-e993079.adobeaemcloud.com</td><td>https://publish-p106506-e993079.adobeaemcloud.com</td></tr><tr><td>L716041</td><td>https://author-p106507-e993074.adobeaemcloud.com</td><td>https://publish-p106507-e993074.adobeaemcloud.com</td></tr><tr><td>L716042</td><td>https://author-p106508-e993075.adobeaemcloud.com</td><td>https://publish-p106508-e993075.adobeaemcloud.com</td></tr><tr><td>L716043</td><td>https://author-p106421-e993163.adobeaemcloud.com</td><td>https://publish-p106421-e993163.adobeaemcloud.com</td></tr><tr><td>L716044</td><td>https://author-p106459-e993121.adobeaemcloud.com</td><td>https://publish-p106459-e993121.adobeaemcloud.com</td></tr><tr><td>L716045</td><td>https://author-p106467-e993292.adobeaemcloud.com</td><td>https://publish-p106467-e993292.adobeaemcloud.com</td></tr><tr><td>L716046</td><td>https://author-p106518-e993234.adobeaemcloud.com</td><td>https://publish-p106518-e993234.adobeaemcloud.com</td></tr><tr><td>L716047</td><td>https://author-p106511-e993076.adobeaemcloud.com</td><td>https://publish-p106511-e993076.adobeaemcloud.com</td></tr><tr><td>L716048</td><td>https://author-p106512-e993077.adobeaemcloud.com</td><td>https://publish-p106512-e993077.adobeaemcloud.com</td></tr><tr><td>L716049</td><td>https://author-p106460-e993124.adobeaemcloud.com</td><td>https://publish-p106460-e993124.adobeaemcloud.com</td></tr><tr><td>L716050</td><td>https://author-p106519-e993237.adobeaemcloud.com</td><td>https://publish-p106519-e993237.adobeaemcloud.com</td></tr><tr><td>L716051</td><td>https://author-p106513-e993084.adobeaemcloud.com</td><td>https://publish-p106513-e993084.adobeaemcloud.com</td></tr><tr><td>L716052</td><td>https://author-p106461-e993122.adobeaemcloud.com</td><td>https://publish-p106461-e993122.adobeaemcloud.com</td></tr><tr><td>L716053</td><td>https://author-p106514-e993082.adobeaemcloud.com</td><td>https://publish-p106514-e993082.adobeaemcloud.com</td></tr><tr><td>L716054</td><td>https://author-p106462-e993123.adobeaemcloud.com</td><td>https://publish-p106462-e993123.adobeaemcloud.com</td></tr><tr><td>L716055</td><td>https://author-p106463-e993127.adobeaemcloud.com</td><td>https://publish-p106463-e993127.adobeaemcloud.com</td></tr><tr><td>L716056</td><td>https://author-p106515-e993083.adobeaemcloud.com</td><td>https://publish-p106515-e993083.adobeaemcloud.com</td></tr><tr><td>L716057</td><td>https://author-p106464-e993126.adobeaemcloud.com</td><td>https://publish-p106464-e993126.adobeaemcloud.com</td></tr><tr><td>L716058</td><td>https://author-p106520-e993236.adobeaemcloud.com</td><td>https://publish-p106520-e993236.adobeaemcloud.com</td></tr><tr><td>L716059</td><td>https://author-p106423-e993161.adobeaemcloud.com</td><td>https://publish-p106423-e993161.adobeaemcloud.com</td></tr><tr><td>L716060</td><td>https://author-p106516-e993078.adobeaemcloud.com</td><td>https://publish-p106516-e993078.adobeaemcloud.com</td></tr><tr><td>L716061</td><td>https://author-p106521-e993240.adobeaemcloud.com</td><td>https://publish-p106521-e993240.adobeaemcloud.com</td></tr><tr><td>L716062</td><td>https://author-p106424-e993308.adobeaemcloud.com</td><td>https://publish-p106424-e993308.adobeaemcloud.com</td></tr><tr><td>L716063</td><td>https://author-p106468-e993295.adobeaemcloud.com</td><td>https://publish-p106468-e993295.adobeaemcloud.com</td></tr><tr><td>L716064</td><td>https://author-p106425-e993309.adobeaemcloud.com</td><td>https://publish-p106425-e993309.adobeaemcloud.com</td></tr><tr><td>L716065</td><td>https://author-p106426-e993314.adobeaemcloud.com</td><td>https://publish-p106426-e993314.adobeaemcloud.com</td></tr><tr><td>L716066</td><td>https://author-p106469-e993293.adobeaemcloud.com</td><td>https://publish-p106469-e993293.adobeaemcloud.com</td></tr><tr><td>L716067</td><td>https://author-p106522-e993238.adobeaemcloud.com</td><td>https://publish-p106522-e993238.adobeaemcloud.com</td></tr><tr><td>L716068</td><td>https://author-p106470-e993299.adobeaemcloud.com</td><td>https://publish-p106470-e993299.adobeaemcloud.com</td></tr><tr><td>L716069</td><td>https://author-p106427-e993311.adobeaemcloud.com</td><td>https://publish-p106427-e993311.adobeaemcloud.com</td></tr><tr><td>L716070</td><td>https://author-p106428-e993310.adobeaemcloud.com</td><td>https://publish-p106428-e993310.adobeaemcloud.com</td></tr><tr><td>L716071</td><td>https://author-p106471-e993298.adobeaemcloud.com</td><td>https://publish-p106471-e993298.adobeaemcloud.com</td></tr><tr><td>L716072</td><td>https://author-p106429-e993315.adobeaemcloud.com</td><td>https://publish-p106429-e993315.adobeaemcloud.com</td></tr><tr><td>L716073</td><td>https://author-p106523-e993239.adobeaemcloud.com</td><td>https://publish-p106523-e993239.adobeaemcloud.com</td></tr><tr><td>L716074</td><td>https://author-p106472-e993300.adobeaemcloud.com</td><td>https://publish-p106472-e993300.adobeaemcloud.com</td></tr><tr><td>L716075</td><td>https://author-p106430-e993312.adobeaemcloud.com</td><td>https://publish-p106430-e993312.adobeaemcloud.com</td></tr><tr><td>L716076</td><td>https://author-p106524-e993241.adobeaemcloud.com</td><td>https://publish-p106524-e993241.adobeaemcloud.com</td></tr><tr><td>L716077</td><td>https://author-p106431-e993313.adobeaemcloud.com</td><td>https://publish-p106431-e993313.adobeaemcloud.com</td></tr><tr><td>L716078</td><td>https://author-p106473-e993294.adobeaemcloud.com</td><td>https://publish-p106473-e993294.adobeaemcloud.com</td></tr><tr><td>L716079</td><td>https://author-p106474-e993297.adobeaemcloud.com</td><td>https://publish-p106474-e993297.adobeaemcloud.com</td></tr><tr><td>L716080</td><td>https://author-p106475-e993296.adobeaemcloud.com</td><td>https://publish-p106475-e993296.adobeaemcloud.com</td></tr><tr><td>L716081</td><td>https://author-p106476-e993353.adobeaemcloud.com</td><td>https://publish-p106476-e993353.adobeaemcloud.com</td></tr><tr><td>L716082</td><td>https://author-p106525-e993247.adobeaemcloud.com</td><td>https://publish-p106525-e993247.adobeaemcloud.com</td></tr><tr><td>L716083</td><td>https://author-p106526-e993244.adobeaemcloud.com</td><td>https://publish-p106526-e993244.adobeaemcloud.com</td></tr><tr><td>L716084</td><td>https://author-p106527-e993243.adobeaemcloud.com</td><td>https://publish-p106527-e993243.adobeaemcloud.com</td></tr><tr><td>L716085</td><td>https://author-p106477-e993356.adobeaemcloud.com</td><td>https://publish-p106477-e993356.adobeaemcloud.com</td></tr><tr><td>L716086</td><td>https://author-p106478-e993355.adobeaemcloud.com</td><td>https://publish-p106478-e993355.adobeaemcloud.com</td></tr><tr><td>L716087</td><td>https://author-p106528-e993245.adobeaemcloud.com</td><td>https://publish-p106528-e993245.adobeaemcloud.com</td></tr><tr><td>L716088</td><td>https://author-p106432-e993316.adobeaemcloud.com</td><td>https://publish-p106432-e993316.adobeaemcloud.com</td></tr><tr><td>L716089</td><td>https://author-p106529-e993242.adobeaemcloud.com</td><td>https://publish-p106529-e993242.adobeaemcloud.com</td></tr><tr><td>L716090</td><td>https://author-p106436-e993320.adobeaemcloud.com</td><td>https://publish-p106436-e993320.adobeaemcloud.com</td></tr><tr><td>L716091</td><td>https://author-p106480-e993301.adobeaemcloud.com</td><td>https://publish-p106480-e993301.adobeaemcloud.com</td></tr><tr><td>L716092</td><td>https://author-p106530-e993246.adobeaemcloud.com</td><td>https://publish-p106530-e993246.adobeaemcloud.com</td></tr><tr><td>L716093</td><td>https://author-p106481-e993352.adobeaemcloud.com</td><td>https://publish-p106481-e993352.adobeaemcloud.com</td></tr><tr><td>L716094</td><td>https://author-p106482-e993354.adobeaemcloud.com</td><td>https://publish-p106482-e993354.adobeaemcloud.com</td></tr><tr><td>L716095</td><td>https://author-p106531-e993248.adobeaemcloud.com</td><td>https://publish-p106531-e993248.adobeaemcloud.com</td></tr><tr><td>L716096</td><td>https://author-p106483-e993357.adobeaemcloud.com</td><td>https://publish-p106483-e993357.adobeaemcloud.com</td></tr><tr><td>L716097</td><td>https://author-p106433-e993318.adobeaemcloud.com</td><td>https://publish-p106433-e993318.adobeaemcloud.com</td></tr><tr><td>L716098</td><td>https://author-p106532-e993249.adobeaemcloud.com</td><td>https://publish-p106532-e993249.adobeaemcloud.com</td></tr><tr><td>L716099</td><td>https://author-p106434-e993317.adobeaemcloud.com</td><td>https://publish-p106434-e993317.adobeaemcloud.com</td></tr><tr><td>L716100</td><td>https://author-p106435-e993319.adobeaemcloud.com</td><td>https://publish-p106435-e993319.adobeaemcloud.com</td></tr>
        </tbody>
</table>

+++

## 第1课

### 目标

熟悉AEM Formsas a Cloud Service环境。

### 课程上下文

在本课程中，您通过导航用户界面来熟悉AEM Formsas a Cloud Service环境。

### 练习

1. 打开您的浏览器并输入Cloud Service创作环境的URL。 例如：
   [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/start.html](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/start.html)

1. 登录到Cloud Service创作环境。 在实验期间，将与您共享创作环境的登录凭据。

1. 登录后，导航到AEM Forms UI。 单击 **Forms**.

   ![](/help/forms/assets/screenshot2028113829.png)

1. 单击 **Forms和文档**. 关闭任何与首选项或信息相关的弹出窗口。

   ![](/help/forms/assets/screenshot2028113929.png)

   将显示所有可用的表单。

   ![](/help/forms/assets/screenshot2028114029.png)

## 第2课

### 目标

使用最新的核心组件创作自适应表单，配置并提交表单。

### 课程上下文

在本课程中，作为企业用户，您将使用带有标准化OOTB核心组件的自适应表单创作功能，为多个渠道（如Web、移动设备和聊天）创作自适应表单，以获取数据。

### 练习

1. 为表单创建提交端点：

   1. 打开 <https://requestbin.com/> 的子菜单。
      ![](/help/forms/assets/screenshot2028114329.png)

   1. 单击 **创建公共站** 和复制端点URL。
      ![](/help/forms/assets/screenshot202023-03-0120at206.10.0020pm.png)

1. 使用向导界面创作自适应表单：

   1. 在第1课中使用的浏览器选项卡中，导航到AEM Forms作为Cloud ServiceWeb界面，然后导航到Forms和文档。
      ![](/help/forms/assets/screenshot2028114029.png)

   1. 单击 **创建** ，然后选择“自适应表单”。
      ![](/help/forms/assets/screenshot2028114629.png)

   1. 选择 **包含核心组件的空白** 模板，如下所示：
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.1520pm.png)

   1. 单击 **样式** ，然后选择 **wknd主题** 主题如下所示：
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.2320pm.png)

   1. 单击 **提交** ，然后选择 **提交到REST端点** 卡，并在
      **POST请求的URL** 字段，如下所示：
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.5320pm.png)

   1. 单击&#x200B;**创建**。为表单指定名称和标题。 例如， **contactus**. 单击&#x200B;**创建**。
      ![](/help/forms/assets/screenshot2028123329.png)

   1. 此时将打开自适应表单编辑器。 关闭任何弹出窗口或对话框以获取首选项或信息。 单击左边栏上的组件浏览器，然后添加 **页脚** 组件。
      ![](/help/forms/assets/screenshot2028121929.png)

   1. 标题是自适应表单模板的一部分。 它允许以一种简单的方式在所有自适应表单中提供一致的页眉/页脚。 或者，您也可以选择在表单中保持其可编辑 — 如下一步中页脚组件所示。

   1. 添加 **标题** 组件。
      ![](/help/forms/assets/screenshot2028122129.png)

   1. 添加 **文本输入** 组件。
      ![](/help/forms/assets/screenshot2028122329.png)

   1. 添加 **数字输入** 组件。
      ![](/help/forms/assets/screenshot2028122429.png)

   1. 添加 **提交按钮** 组件。
      ![](/help/forms/assets/screenshot2028122529.png)

   1. 单击 **标题** 组件 **弹出菜单** 中。 单击 **“编辑”图标** ，以编辑标签。
      ![](/help/forms/assets/screenshot2028122629.png)

   1. 输入 `Contact Us` 作为标题文本。
      ![](/help/forms/assets/screenshot2028122829.png)

   1. 单击 **文本输入** 组件，以便显示弹出菜单。 单击 **“编辑”图标** ，以编辑标签。
      ![](/help/forms/assets/screenshot2028122929.png)

   1. 输入 **全名** 作为字段标签。
      ![](/help/forms/assets/screenshot2028123029.png)

   1. 单击 **数字输入** 组件，以便显示弹出菜单。 单击 **“编辑”图标** ，以编辑标签。
      ![](/help/forms/assets/screenshot2028123129.png)

   1. 输入 **电话号码** 作为字段标签。
      ![](/help/forms/assets/screenshot2028123829.png)


1. 向表单添加验证：

   1. 单击 **电话号码** 组件，以便显示弹出菜单。 单击 **扳手图标** ，以配置字段。
      ![](/help/forms/assets/screenshot2028123429.png)

   1. 打开 **“验证”选项卡**，标记字段 **必需**，然后单击 **完成**. 将显示成功消息。
      ![](/help/forms/assets/screenshot2028123529.png)

      ![](/help/forms/assets/screenshot2028123629.png)

   1. 单击 **预览** 从最终用户的角度预览表单。
      ![](/help/forms/assets/screenshot2028125529.png)

   1. 使用虚拟数据填写表单
      ![](/help/forms/assets/screenshot2028125629.png)

   1. 提交表单
      ![](/help/forms/assets/screenshot2028125729.png)

   1. 在请求站选项卡中，检查提交的数据。
      ![](/help/forms/assets/screenshot2028125829.png)

现在，为了完成其余练习，请使用预先创建的注册表单。

1. 打开AEM Forms管理界面，例如， `https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments`，然后选择注册表单。

   ![](/help/forms/assets/screenshot2028115529.png)

1. 单击&#x200B;**发布**。

   ![](/help/forms/assets/screenshot2028115629.png)

   将显示成功消息。

   ![](/help/forms/assets/screenshot2028115729.png)

   表单的发布URL应类似于 `https://publish-p105303-e986623.adobeaemcloud.com/content/forms/af/registration.html`.

1. 要查看发布的表单，请将上述URL中的项目ID(pXXXXX)和环境ID(eXXXXX)替换为您环境的ID。

## 第3课

### 目标

使用前端开发最佳实践更新样式。

### 课程上下文

在本课程中，作为前端开发人员，您将了解如何轻松更新之前创建的自适应表单的样式。

### 练习

设置主题的本地存储库：

1. 打开具有管理员权限的命令提示符或外壳程序：

   ![](/help/forms/assets/screenshot2028115829.png)

1. 在命令提示符下，使用以下命令导航到 **c:\git** 文件夹

   ```Shell
   cd c:\git
   ```

1. 使用以下命令克隆主题前端代码：

   ```Shell
   git clone -b WKND https://github.com/adobe/aem-forms-theme-canvas
   ```


1. 按所列顺序使用以下命令导航到 **aem-forms-theme-canvas** 目录和打开Visual Studio代码。

   ```Shell
   cd aem-forms-theme-canvas
   code .
   ```

   ![](/help/forms/assets/screenshot2028126029.png)

1. 选择 **信任父文件夹中所有文件的作者** 单击 **是的，我相信作者**.

   ![](/help/forms/assets/screenshot2028116229.png)

1. 要渲染云服务发布环境中托管的表单，请重命名 `env_template` 文件。  要重命名文件，请右键单击 **env_template** 文件，然后选择 **重命名** 选项。

   ![](/help/forms/assets/screenshot2028116429.png)

   </br>

   ![](/help/forms/assets/screenshot2028116529.png)

1. 在.env文件中为变量设置以下值并保存文件：

   * **AEM_URL**:指定云服务发布环境。 例如，`https://publish-p105303-e986623.adobeaemcloud.com/`

   * **AEM_ADAPTIVE_FORM**:指定表单的路径。 例如，如果表单路径为 `/content/forms/af/registration`，则此变量的值将为 `registration`.

   ![](/help/forms/assets/screenshot2028116429.png)


1. 在命令提示符窗口中，运行以下命令：

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028117029.png)

   >[!NOTE]
   >
   > * 如果您收到一条消息，要求通过 `npm notice Run npm nstall -g npm@9.6.0`，则忽略消息。
   > * 除非工作簿中有说明，否则不要运行其他npm命令。


1. 现在，运行以下命令以预览表单。

   ```Shell
   npm run live
   ```

   ![](/help/forms/assets/screenshot2028117229.png)

   执行上述命令后，等待 `webpack compiled` 消息。 表单显示在浏览器选项卡中。

   >[!NOTE]
   >
   >如果您在执行 `npm run live` 命令超过3-4分钟，请更改 `localhost` 在浏览器URL中点击127.0.0.1 **输入**.


   ![](/help/forms/assets/screenshot2028115129.png)


1. 在Visual Studio代码中，打开 `PROJECT\src\site\_variables.scss` 文件。 请注意 `$error` 颜色为红色阴影。

   ![](/help/forms/assets/screenshot2028120729.png)

1. 在浏览器中，提交表单以在 **名字** 字段。

   ![](/help/forms/assets/screenshot2028120829.png)

1. 设置 **$error** 颜色 **#5736eb** 并保存文件。

   ![](/help/forms/assets/screenshot2028120729.png)

1. 刷新浏览器并提交表单。 请注意，名字字段上的错误颜色已相应地发生更改。

   ![](/help/forms/assets/screenshot2028121129.png)

1. 在命令提示符下，按 **CTRL+C**，输入 **Y**，然后按 **输入** 用于终止npm进程的键。 务必停止npm服务器，以使其与下一组练习不冲突。
1. 关闭Visual Studio代码和命令提示符窗口。

## 第4课

### 目标

将表单渲染到Web/移动设备和其他界面中，作为无头表单。

### 课程上下文

在本课程中，作为前端开发人员，您将了解如何使用react spectrum design框架将之前创建的自适应表单渲染为无头表单。

### 练习

使用react starter项目设置本地存储库：

1. 使用管理员权限打开命令提示符。

   ![](/help/forms/assets/screenshot2028115829.png)

1. 在命令提示符下，使用以下命令导航到 **c:\git** 文件夹

   ```Shell
   cd c:\git
   ```

1. 使用以下命令克隆自适应表单react starter项目：

   ```Shell
   git clone https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028117329.png)

1. 按所列顺序使用以下命令导航到 **react-starter-kit-aem-headless forms** 目录和打开Visual Studio代码。

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028117529.png)


   将打开Visual Studio代码窗口。

   ![](/help/forms/assets/screenshot2028117429.png)

要渲染在云服务发布环境中托管的表单，请执行以下操作：

1. 将env_template文件重命名为.env文件。 要重命名，请右键单击 **env_template** 文件，然后选择 **重命名** 选项。

   ![](/help/forms/assets/screenshot2028117629.png)

   ![](/help/forms/assets/screenshot2028117729.png)

1. 为.env文件中的变量设置以下值。 更新变量后，保存文件。

   * **AEM_URL**:指定云服务发布环境的URL。 例如，`https://publish-p105303-e986623.adobeaemcloud.com`

   * **AEM_FORM_PATH**:指定在上一课程中创建的自适应表单的路径。 例如，`/content/forms/af/registration/`

      ![](/help/forms/assets/screenshot202023-03-0820at202.49.1820pm.png)

1. 打开命令窗口，确保您位于react-starter-kit-aem-headless-forms目录下，然后运行以下命令：

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028118029.png)


1. 在命令提示符窗口中，运行以下命令：

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028118129.png)

   上述命令启动本地开发服务器，该服务器将使用react-spectrum frontend库以无头方式呈现从AEM获取的表单定义。

   >[!NOTE]
   >
   > 
   > 如果您在执行 `npm start` 命令超过3-4分钟，请更改 `localhost` 在浏览器URL中点击127.0.0.1 **输入**.

   ![](/help/forms/assets/screenshot2028118229.png)

让我们检查此无头表单中规则的执行情况：

1. 选择 **选中该框可享受5%的优惠** 选项。 后续的信用卡申请选项被禁用。

   ![](/help/forms/assets/screenshot2028126229.png)

1. 取消选中 **选中该框可享受5%的优惠** 启用信用卡选项。

   ![](/help/forms/assets/screenshot2028126329.png)

让我们作为业务用户对服务器上的表单进行更改，并自动查看无标题表单中反映的更改。

1. 在浏览器中打开AEM Forms管理界面。 例如， [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/forms.html/content/dam/formsanddocuments](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments).

1. 选择 **注册** 表单并单击 **编辑。** 它会在自适应表单编辑器中打开表单。

   ![](/help/forms/assets/screenshot2028118529.png)

1. 选择 **电话号码** 字段，然后单击 **编辑图标（铅笔图标）** 中。 如果看不到弹出工具栏，请通过单击 **编辑** 按钮，从左到右 **预览** 按钮。

   ![](/help/forms/assets/screenshot2028119629.png)

1. 将标签更改为“Mobile Number”。 单击表单中的任何空白，即会保存对表单所做的更改。

   ![](/help/forms/assets/screenshot2028119729.png)

让我们发布更新后的表单以将更改传播到发布环境。

1. 在AEM Forms管理界面选项卡中，选择注册表单，然后单击 **取消发布**. 如果您没有看到 **取消发布** 按钮，跳到步骤3以直接发布更改。

   ![](/help/forms/assets/screenshot2028119829.png)

1. 单击 **取消发布**. 单击 **关闭** 对话框。

   ![](/help/forms/assets/screenshot2028119929.png)

   ![](/help/forms/assets/screenshot2028120029.png)


1. 浏览器刷新后，选择注册表单并单击 **发布**.

   ![](/help/forms/assets/screenshot2028120129.png)


1. 单击&#x200B;**发布**。单击 **关闭** 对话框。

   ![](/help/forms/assets/screenshot2028120329.png)

   ![](/help/forms/assets/screenshot2028120429.png)

1. 使用显示的无标题表单刷新浏览器选项卡。 请注意，“电话号码”标签已更改为“手机号码”。

   ![](/help/forms/assets/screenshot2028120529.png)

1. 打开用于启动 **react-starter-kit-aem-headless forms** 项目，按 **CTRL+C**，然后输入 **Y** 然后按Enter键终止npm进程。 务必停止npm服务器，以使其与下一组练习不冲突。

1. 关闭Visual Studio代码和命令提示符窗口。


## 第5课

### 目标

使用Google Material UI将表单渲染为无头表单

### 课程上下文

在本课程中，作为前端开发人员，您将学习如何使用Google Material UI呈现之前创建的自适应表单作为无头表单。

### 练习

使用“材料UI”入门项目设置本地存储库：

1. 使用管理员权限打开命令提示符。

   ![](/help/forms/assets/screenshot2028115829.png)


1. 在命令提示符下，使用以下命令导航到 **c:\git** 文件夹：

   ```Shell
   cd c:\git
   ```

1. 按所列顺序运行以下命令以创建名为mui的文件夹，并使用以下命令导航到mui文件夹：

   ```Shell
   mkdir mui
   
   cd mui
   ```

1. 使用以下命令克隆自适应表单react starter项目：

   ```Shell
   git clone -b mui https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028126529.png)

1. 按所列顺序使用以下命令导航到 **react-starter-kit-aem-headless forms** 文件夹，然后在Visual Studio代码中打开代码：

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028126829.png)

要渲染在云服务发布环境中托管的表单，请执行以下操作：

1. 重命名 **env_template** 文件到 **.env** 文件。 要重命名，请右键单击 **env_template** 文件，选择 **重命名**.

   ![](/help/forms/assets/screenshot2028126629.png)

1. 为.env文件中的变量设置以下值。 更新变量后，保存文件。 使用 **CTRL + S** 切换组合以保存文件。

   * **AEM_URL**:指定云服务发布环境的URL。 例如， [https://publish-p105303-e986623.adobeaemcloud.com](https://publish-p105303-e986623.adobeaemcloud.com/)

   * **AEM_FORM_PATH**:指定在上一课程中创建的自适应表单的路径。 例如， /content/forms/af/registration/

      ![](/help/forms/assets/screenshot2028126929.png)

1. 打开命令窗口，确保您位于 **react-starter-kit-aem-headless forms** 目录，并运行以下命令：

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028127029.png)

1. 在命令提示符窗口中，运行以下命令：

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028127129.png)

   该命令将启动本地开发服务器，并使用Google Material UI前端库以无头方式呈现从AEM获取的表单定义。

   >[!NOTE]
   >
   >如果您在执行 `npm start` 命令超过3-4分钟，请更改 `localhost` 在浏览器URL中点击127.0.0.1 **输入**.

   ![](/help/forms/assets/screenshot2028127229.png)

1. 要评估此表单演绎版中相同业务逻辑的执行情况，请执行以下操作：

   选择 **选中该框可享受5%的优惠**. 后续选项 **您想申请We.Finance公司信用卡表吗？** 被禁用。

   ![](/help/forms/assets/screenshot2028127329.png)

## 第6课

### 目标

使用“材料”UI组件变体创建无头表单的替代外观

### 课程上下文

在本课程中，作为前端开发人员，您将学习如何使用材料UI为之前由业务用户创建的自适应表单创建不同组件的替代表示形式。

### 练习

更新无头项目中组件的变体。 将材料UI文本输入组件的变体更改为 `OutlinedInput`:

1. 在可视代码中，通过打开 `index.tsx` 文件位置 `src/components/textinput/index.tsx`.

1. 添加 `//` 代码行103的开头。 它会将行转换为评论。

   ```Shell
   //const Cmp = \'outlined\' === appliedCssClassNames ? OutlinedInput: Input;
   ```

1. 在第104行添加以下内容，以使用组件的其他变体并保存文件。 使用 **CTRL + S** 切换组合以保存文件。

   ```Shell
   const Cmp = OutlinedInput;
   ```

   ![](/help/forms/assets/screenshot2028127629.png)

   必须对“OhuredInput”变体使用正确的大小写，否则编译会失败。 本地开发环境编译在命令提示符下自动开始。 请等待您看到以下消息

   `webpack 5.75.0 compiled with 3 warnings in 6659 ms`
   `inside proxy req`
   `setting new origin header`

1. 如果浏览器没有自动刷新，请刷新该浏览器以查看文本输入组件使用的是其他变体。

   ![](/help/forms/assets/screenshot2028127729.png)


   此更改适用于最终用户，但AEM Forms Server的表单定义没有任何更改，且特定于正在考虑的无头渠道。 例如，本实验中的Web渠道。

   ![](/help/forms/assets/screenshot2028127529.png)


1. 关闭Visual Studio代码和命令提示符窗口。

## 常见问题解答(FAQ)

+++ 自适应表单向导是否可公开使用？

是，它可与AEM Forms一起用作Cloud Service。

+++


+++ 核心组件是否可公开使用？

是，自适应Forms核心组件可以与AEM Forms一起作为Cloud Service。

+++

+++ 无头表单是否可公开使用？

是，无头表单可以与AEM Forms一起用作Cloud Service。

+++

+++ 无头表单是否需要单独的许可证？

否，无头表单使用相同的许可值量度和表单提交数。

+++

+++ AEM 6.5 Forms中是否提供核心组件和无头表单？

是的，AEM Forms 6.5 Service Pack 16及以上版本提供了自适应表单核心组件和无头表单。

+++


## 下面的步骤

现在，您已了解如何构建自适应表单并使用无头表单将其交付到多个渠道，接下来您应该尝试运用新技能。 通过创建卓越的数据捕获体验并将其大规模提供给最终用户，玩得开心且继续！

## 资源

* [自适应表单核心组件简介](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)

* [使用核心组件创建自适应表单](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html)

* [更新基于核心组件的AF的样式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html?lang=en)

* [无头自适应表单](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=en)

* [使用无头React启动器套件](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/get-started/create-and-publish-a-headless-form.html?lang=en)


