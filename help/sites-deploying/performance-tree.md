---
title: 性能树
seo-title: 性能树
description: 了解在AEM中解决性能问题时需要采取的步骤。
seo-description: 了解在AEM中解决性能问题时需要采取的步骤。
uuid: ab0624f7-6b39-4255-89e0-54c74b54cd98
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 5febbb1e-795c-49cd-a8f4-c6b4b540673d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 性能树{#performance-tree}

## 范围 {#scope}

下图旨在提供有关为解决性能问题需要采取的步骤的指导。 它分为5个部分，便于阅读。

图中的每个步骤都链接到文档资源或推荐。

## 先决条件和假设 {#prerequisites-and-assumptions}

假定在给定页面（AEM控制台或网页）上观察到性能问题，并且可以一致地重现。 在开始调查之前，要测试或监控性能，必须具备这样的方法。

分析从步骤0开始。 目标是确定哪个实体（调度程序、外部主机或AEM）负责性能问题，然后确定应调查的区域（服务器或网络）。

### 章节 1 {#section}

![chlimage_1-103](assets/chlimage_1-103.png)

### 章节 2 {#section-1}

![chlimage_1-104](assets/chlimage_1-104.png)

### 章节 3 {#section-2}

![chlimage_1-105](assets/chlimage_1-105.png)

### 章节 4 {#section-3}

![chlimage_1-106](assets/chlimage_1-106.png)

### Section 5 {#section-4}

![chlimage_1-107](assets/chlimage_1-107.png)

## 引用链接 {#reference-links}

<table>
 <tbody>
  <tr>
   <td><strong>步骤</strong></td>
   <td><strong>标题</strong></td>
   <td><strong>资源</strong></td>
  </tr>
  <tr>
   <td><strong>步骤 0</strong></td>
   <td>分析请求流</td>
   <td><p>您可以在浏览器中使用标准HTTP请求分析来分析请求流。 有关如何在Chrome上执行此操作的详细信息，请参阅：<br /> </p> <p><a href="https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/resource-loading">https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/resource-loading</a><a href="https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/understanding-resource-timing"><br /> https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/understanding-resource-timing</a><br /> </p> </td>
  </tr>
  <tr>
   <td><strong>步骤 2</strong></td>
   <td>请求是否来自外部主机？</td>
   <td>您可以在浏览器中使用标准HTTP请求分析来分析请求流。 请参阅上述链接，了解如何在Chrome上执行此操作。<br /> </td>
  </tr>
  <tr>
   <td><strong>步骤 3</strong></td>
   <td>是否可以缓存请求？</td>
   <td>有关可缓存请求和一般Dispatcher性能优化建议的详细信息，请参阅 <a href="/help/sites-deploying/configuring-performance.md#optimizing-performance-when-using-the-dispatcher">Dispatcher性能优化</a>。</td>
  </tr>
  <tr>
   <td><strong>步骤 4</strong></td>
   <td>请求是否来自Dispatcher?</td>
   <td><p>查看 <a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#debugging">Dispatcher调试文档</a> ，查看请求是否正确缓存。<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>步骤 5</strong></td>
   <td>调度程序是否正在尝试通过AEM验证每个请求？</td>
   <td>在传送缓存资源 <code>HEAD</code> 之前，检查调度程序是否向AEM发送请求以进行身份验证。 您可以通过在AEM中查找请 <code>HEAD</code> 求来完成此操作 <code>access.log</code>。 有关详细信息，请参 <a href="/help/sites-deploying/configure-logging.md">阅记录</a>。<br /> </td>
  </tr>
  <tr>
   <td><strong>步骤 6</strong></td>
   <td>调度程序的地理位置是否远离用户？</td>
   <td>将Dispatcher移近用户。</td>
  </tr>
  <tr>
   <td><strong>步骤 7</strong></td>
   <td>调度程序的网络层是否正常？</td>
   <td><br /> 调查网络层的饱和度和延迟问题。<p> </p> </td>
  </tr>
  <tr>
   <td><strong>步骤 8</strong></td>
   <td>缓慢是否可以通过本地实例重现？</td>
   <td><br /> <p>使 <a href="/help/sites-developing/tough-day.md">用Though Day</a> ，从生产实例中复制“真实世界”条件。 如果这对于您的开发解决方案不现实，请确保在不同的网络上下文中测试生产实例（或相同的分级实例）。<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>步骤 9</strong></td>
   <td>服务器的地理位置是否远离用户？</td>
   <td>将服务器移近用户。</td>
  </tr>
  <tr>
   <td><strong>步骤10和29</strong></td>
   <td>调查网络层</td>
   <td><p>调查网络层的饱和度和延迟问题。</p> <p>对于作者层，建议延迟不超过100毫秒。</p> <p>有关性能优化提示的更多信息，请参 <a href="https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html">阅此页</a>。</p> </td>
  </tr>
  <tr>
   <td><strong>步骤 11</strong></td>
   <td>靠近服务器或为每个区域添加一个</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>步骤 12</strong></td>
   <td>AEM服务器疑难解答</td>
   <td>有关详细信息，请查看图中的以下子步骤。</td>
  </tr>
  <tr>
   <td><strong>步骤 13</strong></td>
   <td>检查硬件要求</td>
   <td>查看有关硬件大小 <a href="/help/managing/hardware-sizing-guidelines.md">指南的文档</a>。<br /> </td>
  </tr>
  <tr>
   <td><strong>步骤 14</strong></td>
   <td>检查性能问题的常见原因</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>步骤 15</strong></td>
   <td>查找慢速请求</td>
   <td><p>您可以通过分析或使用来检查 <code>request.log</code> 请求速度慢 <code>rlog.jar</code>。</p> <p>有关使用rlog.jar的详细信息，请参阅此页。</p> <p>请参 <a href="/help/sites-deploying/monitoring-and-maintaining.md#using-rlog-jar-to-find-requests-with-long-duration-times">阅使用rlog.jar查找持续时间较长的请求</a>。<br /> </p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>步骤 16</strong></td>
   <td>配置文件服务器</td>
   <td><p>有关可与AEM一起使用的概要分析工具的信息，请参 <a href="/help/sites-deploying/monitoring-and-maintaining.md#tools-for-monitoring-and-analyzing-performance">阅监测和分析性能工具</a>。<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>步骤 17</strong></td>
   <td>查找分析中的慢速方法</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>步骤 18</strong></td>
   <td>概要分析的常见场景</td>
   <td>请参 <a href="/help/sites-deploying/monitoring-and-maintaining.md#analyzing-specific-scenarios">阅“性能优化</a> ”部分中的分析特定方案。<br /> </td>
  </tr>
  <tr>
   <td><strong>步骤 19</strong></td>
   <td>100% CPU</td>
   <td><a href="/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance">https://helpx.adobe.com/experience-manager/6-3/sites-deploying/monitoring-and-maintaining.html#MonitoringPerformance</a></td>
  </tr>
  <tr>
   <td><strong>步骤 20</strong></td>
   <td>内存不足</td>
   <td><br />
    <ol>
     <li><a href="/help/sites-deploying/monitoring-and-maintaining.md#out-of-memory">内存不足</a></li>
     <li><a href="/help/sites-deploying/troubleshooting.md">我的应用程序内存不足错误</a></li>
     <li><a href="https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html">分析Helpx上的内存问题。</a><br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>步骤 21</strong></td>
   <td>磁盘I/O</td>
   <td><p>请参 <a href="/help/sites-deploying/monitoring-and-maintaining.md#disk-i-o">阅监视和维护文档中的Disk I/O</a> （磁盘I/O）部分。</p> </td>
  </tr>
  <tr>
   <td><strong>步骤22和22.1</strong></td>
   <td>缓存比</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#calculating-the-dispatcher-cache-ratio"> 请参 </a>阅计算调度程序缓存比<br />。 <br /> </td>
  </tr>
  <tr>
   <td><strong>步骤 23</strong></td>
   <td>慢速查询</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">查询和索引的最佳实践</a></td>
  </tr>
  <tr>
   <td><strong>步骤 24</strong></td>
   <td>存储库优化</td>
   <td>
    <ul>
     <li><a href="https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html">性能调整提示</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#configuring-for-performance">性能配置</a></li>
     <li><a href="https://www.slideshare.net/jukka/repository-performance-tuning">存储库性能调整</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>步骤 25</strong></td>
   <td>运行的工作流</td>
   <td>
    <ul>
     <li><a href="/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing">并发工作流处理</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#configure-the-queue-for-a-specific-workflow">为特定工作流配置队列</a></li>
     <li><a href="/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances">定期清除工作流实例</a></li>
     <li><a href="/help/sites-developing/workflows.md#transient-workflows">临时工作流</a><br /> </li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>步骤 26</strong></td>
   <td>MSM基础架构</td>
   <td><p><a href="/help/sites-administering/msm-best-practices.md">多站点管理器最佳实践</a><br /> </p> </td>
  </tr>
  <tr>
   <td><strong>步骤 27</strong></td>
   <td>资产调整</td>
   <td>
    <ol>
     <li><a href="/help/sites-deploying/configuring-performance.md#cq-dam-asset-synchronization-service">资产同步服务</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#multiple-dam-instances">多个DAM实例</a></li>
     <li>性能调整提示文章 <a href="https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html">在此处</a> 和 <a href="https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html">此处</a>。<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>步骤 28</strong></td>
   <td>未结束的会话</td>
   <td><p> </p> <p><a href="/help/sites-administering/troubleshoot.md#checking-for-unclosed-jcr-sessions">检查未关闭的JCR会话</a></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>步骤 30</strong></td>
   <td>使调度程序更靠近（每个“区域”添加一个？）</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>步骤 31</strong></td>
   <td>在调度程序前使用CDN</td>
   <td><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn">将 Dispatcher 与 CDN 结合使用</a><br /> </td>
  </tr>
  <tr>
   <td><strong>步骤 32</strong></td>
   <td>使用调度程序级别的会话管理来卸载AEM服务器</td>
   <td><p><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement">启用安全会话</a></p> </td>
  </tr>
  <tr>
   <td><strong>步骤 33</strong></td>
   <td>使请求可缓存</td>
   <td>
    <ol>
     <li><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html">常规调度程序配置</a></li>
     <li><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache">配置调度程序缓存</a></li>
    </ol> <p>如何提高缓存率；使请求可缓存（调度程序最佳实践）</p> <p>此外，要优化缓存配置，请考虑以下设置<br /> </p>
    <ol>
     <li>为非GET的HTTP请求设置无缓存规则</li>
     <li>将查询字符串配置为不可缓存</li>
     <li>不缓存扩展名缺失的URL</li>
     <li>缓存身份验证头（可能自Dispatcher版本4.1.10起）</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>步骤 34</strong></td>
   <td>升级调度程序版本</td>
   <td><p>您可以在以下位置下载最新的Dispatcher版本：</p> <p><a href="https://helpx.adobe.com/experience-manager/dispatcher/release-notes.html">跟踪链接</a></p> </td>
  </tr>
  <tr>
   <td><strong>步骤 35</strong></td>
   <td>配置调度程序</td>
   <td><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html">配置调度程序</a><br /> </td>
  </tr>
  <tr>
   <td><strong>步骤 36</strong></td>
   <td>检查缓存失效</td>
   <td><br />
    <ul>
     <li><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-the-authoring-environment">作者层的缓存失效；</a></li>
     <li><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance">发布层的缓存失效。</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>步骤37和38</strong></td>
   <td>延迟加载</td>
   <td><a href="https://docs.adobe.com/ddc/en/gems/aem-web-performance.html">请参阅AEM web性能的Gem会话。</a><br /> </td>
  </tr>
  <tr>
   <td><strong>步骤 39</strong></td>
   <td>使用预连接可减少连接开销</td>
   <td>见上述Gem会议。 <a href="https://www.w3.org/TR/resource-hints/#dfn-preconnect"> 此外，W3c上的其他文档预先连接：https://www.w3.org/TR/resource-hints/#dfn-preconnect</a></td>
  </tr>
  <tr>
   <td><strong>步骤40和41</strong><br /> </td>
   <td>外部主机延迟和响应时间</td>
   <td>调查外部主机的延迟和响应时间。</td>
  </tr>
  <tr>
   <td><strong>第45步和<br /> 47步</strong><br /> </td>
   <td>使用HTTP/2</td>
   <td>有关步骤37、38和39，请参见创业板会议。 此外，请查看 <a href="https://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.topic.html/forum__kdzc-does_anyoneknowwhe.html">此论坛</a> ，了解HTTP/2支持。<br /> </td>
  </tr>
  <tr>
   <td><strong>步骤 49</strong></td>
   <td>缩小有效负荷大小</td>
   <td><a href="/help/sites-deploying/osgi-configuration-settings.md">启用Gzip</a> , <a href="https://docs.adobe.com/ddc/en/gems/aem-web-performance.html">缩小图像大小</a>。<br /> </td>
  </tr>
  <tr>
   <td><strong>步骤42和43</strong></td>
   <td>Keep-Alive</td>
   <td><p>不同 <code>Keep-Alive</code> 请求中是否存在重新使用连接的标题？ 否则，这意味着每个请求都会导致另一个连接建立，这会引入不必要的开销。 （浏览器中的标准HTTP请求分析）</p> <p>可以检查“代 <a href="/help/sites-administering/proxy-jar.md">理服务器”工具</a> ，以检查“保持连接”。<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>步骤 44</strong></td>
   <td>提出了多少个请求？</td>
   <td>在浏览器中执行标准HTTP请求分析。</td>
  </tr>
  <tr>
   <td><strong>步骤 46</strong></td>
   <td>减少请求数</td>
   <td>
    <ol>
     <li>连接资源（图像、CSS Sprite、JSON等）<br /> </li>
     <li>Clientlibs嵌入：
      <ol>
       <li><a href="/help/sites-developing/clientlibs.md#creating-client-library-folders">创建客户端库文件夹</a> -请参阅标题使用嵌入最小化请求</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>步骤 48</strong></td>
   <td>有效负荷的大小是多少？</td>
   <td>浏览器中的标准HTTP请求分析</td>
  </tr>
  <tr>
   <td><strong>步骤50和51</strong></td>
   <td>JS代码阻止</td>
   <td><a href="https://docs.adobe.com/ddc/en/gems/aem-web-performance.html">https://docs.adobe.com/ddc/en/gems/aem-web-performance.html</a></td>
  </tr>
 </tbody>
</table>

