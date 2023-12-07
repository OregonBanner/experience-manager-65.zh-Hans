---
title: 性能树
description: 了解对AEM中的性能问题进行故障排除所需执行的步骤。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: f2f968b8-b21c-487d-bc0d-ed60903bc4bf
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 9%

---

# 性能树{#performance-tree}

## 范围 {#scope}

下图旨在提供有关解决性能问题应采取的步骤的指导。 为了便于阅读，它分为五个部分。

图中的每个步骤都链接到文档资源或推荐。

## 先决条件和假设 {#prerequisites-and-assumptions}

假设在给定页面(AEM控制台或网页)上发现性能问题并且可以一致地复制。 在开始调查之前，必须具备测试或监控性能的方法。

分析从步骤0开始。 目标是确定哪个实体(Dispatcher、外部主机或AEM)应对性能问题负责，然后确定应调查哪个区域（服务器或网络）。

### 章节 1 {#section}

![chlimage_1-103](assets/chlimage_1-103.png)

### 章节 2 {#section-1}

![chlimage_1-104](assets/chlimage_1-104.png)

### 章节 3 {#section-2}

![chlimage_1-105](assets/chlimage_1-105.png)

### 章节 4 {#section-3}

![chlimage_1-106](assets/chlimage_1-106.png)

### 章节 5 {#section-4}

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
   <td>分析请求流程</td>
   <td><p>您可以在浏览器中使用标准HTTP请求分析来分析请求流。 有关如何在Chrome上执行此分析的更多信息，请参阅：<br /> </p> <p><a href="https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/resource-loading">https://developer.chrome.com/docs/devtools/</a><br /> </p> </td>
  </tr>
  <tr>
   <td><strong>步骤 2</strong></td>
   <td>请求是否来自外部主机？</td>
   <td>您可以在浏览器中使用标准HTTP请求分析来分析请求流。 请参阅上面的链接，了解如何在Chrome上执行此分析。<br /> </td>
  </tr>
  <tr>
   <td><strong>步骤 3</strong></td>
   <td>是否可以缓存请求？</td>
   <td>有关可缓存的请求和一般Dispatcher性能优化建议的更多信息，请参阅 <a href="/help/sites-deploying/configuring-performance.md#optimizing-performance-when-using-the-dispatcher">Dispatcher性能优化</a>.</td>
  </tr>
  <tr>
   <td><strong>步骤 4</strong></td>
   <td>是否来自Dispatcher的请求？</td>
   <td><p>要查看请求是否正确缓存，请检查 <a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#debugging">Dispatcher调试文档</a>.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>步骤 5</strong></td>
   <td>Dispatcher是否尝试通过AEM验证每个请求？</td>
   <td>检查Dispatcher是否发送 <code>HEAD</code> 请求AEM进行身份验证，然后再传递缓存的资源。 查找 <code>HEAD</code> AEM中的请求 <code>access.log</code>. 有关更多信息，请参阅 <a href="/help/sites-deploying/configure-logging.md">记录</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>步骤 6</strong></td>
   <td>Dispatcher的地理位置是否远离用户？</td>
   <td>将Dispatcher移到离用户更近的位置。</td>
  </tr>
  <tr>
   <td><strong>步骤 7</strong></td>
   <td>Dispatcher的网络层是否正常？</td>
   <td><br /> 调查网络层的饱和度和延迟问题。<p> </p> </td>
  </tr>
  <tr>
   <td><strong>步骤 8</strong></td>
   <td>慢度是否可以在本地实例中重现？</td>
   <td><br /> <p>使用 <a href="/help/sites-developing/tough-day.md">艰难的一天</a> 从生产实例中复制“真实”条件。 如果此场景对于开发空间并不现实，请确保在不同的网络上下文中测试生产实例（或相同的暂存实例）。<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>步骤 9</strong></td>
   <td>服务器的地理位置是否远离用户？</td>
   <td>将服务器移到离用户更近的位置。</td>
  </tr>
  <tr>
   <td><strong>步骤10和29</strong></td>
   <td>调查网络层</td>
   <td><p>调查网络层的饱和度和延迟问题。</p> <p>对于创作层，建议延迟不超过100毫秒。</p> <p>有关性能优化提示的更多信息，请参阅 <a href="https://helpx.adobe.com/customer-care-office-hours/aem/6x-performance-tuning-best-practices.html">此页面</a>.</p> </td>
  </tr>
  <tr>
   <td><strong>步骤 11</strong></td>
   <td>使服务器更近或为每个区域添加一个</td>
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
   <td>查看文档： <a href="/help/managing/hardware-sizing-guidelines.md">硬件大小调整准则</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>步骤 14</strong></td>
   <td>检查性能问题的常见原因</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>步骤 15</strong></td>
   <td>查找慢速请求</td>
   <td><p>您可以通过分析 <code>request.log</code> 或使用 <code>rlog.jar</code>.</p> <p>有关使用rlog.jar的详细信息，请参阅此页。</p> <p>请参阅 <a href="/help/sites-deploying/monitoring-and-maintaining.md#using-rlog-jar-to-find-requests-with-long-duration-times">使用rlog.jar查找持续时间较长的请求</a>.<br /> </p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>步骤 16</strong></td>
   <td>配置文件服务器</td>
   <td><p>有关可与AEM一起使用的性能分析工具的信息，请参见 <a href="/help/sites-deploying/monitoring-and-maintaining.md#tools-for-monitoring-and-analyzing-performance">用于监控和分析性能的工具</a>.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>步骤 17</strong></td>
   <td>在性能分析中查找较慢的方法</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>步骤 18</strong></td>
   <td>配置文件的常见方案</td>
   <td>请参阅 <a href="/help/sites-deploying/monitoring-and-maintaining.md#analyzing-specific-scenarios">分析特定方案</a> 在“性能优化”部分中。<br /> </td>
  </tr>
  <tr>
   <td><strong>步骤 19</strong></td>
   <td>100% CPU</td>
   <td><a href="/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance">https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html</a></td>
  </tr>
  <tr>
   <td><strong>步骤 20</strong></td>
   <td>内存不足</td>
   <td><br />
    <ol>
     <li><a href="/help/sites-deploying/monitoring-and-maintaining.md#out-of-memory">内存不足</a></li>
     <li><a href="/help/sites-deploying/troubleshooting.md">我的应用程序引发内存不足错误</a></li>
     <li><a href="https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html?lang=en">分析内存问题。</a><br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>步骤 21</strong></td>
   <td>磁盘I/O</td>
   <td><p>请参阅 <a href="/help/sites-deploying/monitoring-and-maintaining.md#disk-i-o">磁盘I/O</a> 部分（位于“监测和维护”文档中）。</p> </td>
  </tr>
  <tr>
   <td><strong>步骤22和22.1</strong></td>
   <td>缓存比率</td>
   <td>请参阅 <a href="/help/sites-deploying/configuring-performance.md#calculating-the-dispatcher-cache-ratio">计算Dispatcher缓存比率</a>.<br /> <br /> </td>
  </tr>
  <tr>
   <td><strong>步骤 23</strong></td>
   <td>查询速度慢</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">有关查询和索引的最佳实践</a></td>
  </tr>
  <tr>
   <td><strong>步骤 24</strong></td>
   <td>存储库调整</td>
   <td>
    <ul>
     <li><a href="https://helpx.adobe.com/customer-care-office-hours/aem/6x-performance-tuning-best-practices.html">性能调整提示</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#configuring-for-performance">配置性能</a></li>
     <li><a href="https://www.slideshare.net/jukka/repository-performance-tuning">存储库性能优化</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>步骤 25</strong></td>
   <td>正在运行工作流</td>
   <td>
    <ul>
     <li><a href="/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing">并发工作流处理</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#configure-the-queue-for-a-specific-workflow">为特定工作流配置队列</a></li>
     <li><a href="/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances">定期清除工作流实例</a></li>
     <li><a href="/help/sites-developing/workflows.md#transient-workflows">瞬态工作流</a><br /> </li>
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
     <li><a href="/help/sites-deploying/configuring-performance.md#cq-dam-asset-synchronization-service">资源同步服务</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#multiple-dam-instances">多个DAM实例</a></li>
     <li>性能调整提示文章 <a href="https://helpx.adobe.com/customer-care-office-hours/aem/6x-performance-tuning-best-practices.html">此处</a>.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>步骤 28</strong></td>
   <td>未关闭的会话</td>
   <td><p> </p> <p><a href="/help/sites-administering/troubleshoot.md#checking-for-unclosed-jcr-sessions">检查未关闭的JCR会话</a></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>步骤 30</strong></td>
   <td>更接近Dispatcher（是否为“区域”添加一个？）</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>步骤 31</strong></td>
   <td>在Dispatcher之前使用CDN</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hans#using-dispatcher-with-a-cdn">将Dispatcher与CDN结合使用</a><br /> </td>
  </tr>
  <tr>
   <td><strong>步骤 32</strong></td>
   <td>要卸载AEM服务器，请使用Dispatcher级别的会话管理</td>
   <td><p><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#enabling-secure-sessions-sessionmanagement">启用安全会话</a></p> </td>
  </tr>
  <tr>
   <td><strong>步骤 33</strong></td>
   <td>使请求可缓存</td>
   <td>
    <ol>
     <li><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=en">常规Dispatcher配置</a></li>
     <li><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-the-dispatcher-cache-cache">配置Dispatcher缓存</a></li>
    </ol> <p>如何提高缓存率；使请求能够缓存（Dispatcher最佳实践）</p> <p>此外，请考虑以下设置以优化缓存配置<br /> </p>
    <ol>
     <li>为非GET的HTTP请求设置无缓存规则</li>
     <li>将查询字符串配置为不可缓存</li>
     <li>不缓存缺少扩展名的URL</li>
     <li>缓存身份验证标头（自Dispatcher版本4.1.10之后可能提供）</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>步骤 34</strong></td>
   <td>升级Dispatcher版本</td>
   <td><p>您可以在此位置下载最新的Dispatcher版本：</p> <p><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html?lang=en">关注链接</a></p> </td>
  </tr>
  <tr>
   <td><strong>步骤 35</strong></td>
   <td>配置Dispatch</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hans">配置Dispatcher</a><br /> </td>
  </tr>
  <tr>
   <td><strong>步骤 36</strong></td>
   <td>检查缓存失效</td>
   <td><br />
    <ul>
     <li><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=en#invalidating-dispatcher-cache-from-the-authoring-environment">创作层的缓存失效；</a></li>
     <li><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=en#invalidating-dispatcher-cache-from-a-publishing-instance">发布层的缓存失效。</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>步骤37和38</strong></td>
   <td>延迟加载</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2016/aem-web-performance.html?lang=en">请参阅有关AEM Web性能的Gem会话。</a><br /> </td>
  </tr>
  <tr>
   <td><strong>步骤 39</strong></td>
   <td>使用预连接以减少连接开销</td>
   <td>请参阅上述Gem讲座。 此外，关于W3c的其他预连接文档：<a href="https://html.spec.whatwg.org/#linkTypes"> https://html.spec.whatwg.org/#linkTypes</a></td>
  </tr>
  <tr>
   <td><strong>步骤40和41</strong><br /> </td>
   <td>外部主机延迟和响应时间</td>
   <td>调查外部主机的等待时间和响应时间。</td>
  </tr>
  <tr>
   <td><strong>步骤45<br /> 和47</strong><br /> </td>
   <td>使用HTTP/2</td>
   <td>有关步骤37、38和39，请参阅Gem会议。 另外，签出 <a href="https://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.topic.html/forum__kdzc-does_anyoneknowwhe.html">此</a> 有关HTTP/2支持的论坛帖子。<br /> </td>
  </tr>
  <tr>
   <td><strong>步骤 49</strong></td>
   <td>缩小有效负载大小</td>
   <td><a href="/help/sites-deploying/osgi-configuration-settings.md">启用Gzip</a> 和 <a href="https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2016/aem-web-performance.html?lang=en">缩小图像大小</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>步骤42和43</strong></td>
   <td>保持活动状态</td>
   <td><p>是 <code>Keep-Alive</code> 标头存在于不同的请求中以重用连接？ 否则，这意味着每个请求都会导致另一个连接建立，从而带来不必要的开销。 （浏览器中的标准HTTP请求分析）</p> <p>您可以检查 <a href="/help/sites-administering/proxy-jar.md">代理服务器工具</a> 检查保持活动状态连接。<br /> </p> </td>
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
     <li>连接资源（图像、CSS脚本、JSON）<br /> </li>
     <li>Clientlibs嵌入：
      <ol>
       <li><a href="/help/sites-developing/clientlibs.md#creating-client-library-folders">创建客户端库文件夹</a>  — 请参阅标题使用嵌入以最大限度地减少请求</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>步骤 48</strong></td>
   <td>有效负载的大小是多少？</td>
   <td>浏览器中的标准HTTP请求分析</td>
  </tr>
  <tr>
   <td><strong>步骤50和51</strong></td>
   <td>JS代码阻止</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2016/aem-web-performance.html?lang=en">https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2016/aem-web-performance.html?lang=en</a></td>
  </tr>
 </tbody>
</table>
