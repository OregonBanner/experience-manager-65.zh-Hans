---
title: HTML5表單服務Proxy
seo-title: HTML5 forms service proxy
description: HTML5 Forms Service Proxy是註冊提交服務Proxy的設定。 若要設定服務Proxy，請透過要求引數submissionServiceProxy指定提交服務的URL。
seo-description: HTML5 forms Service Proxy is a configuration to register a proxy for the submission service. To configure Service Proxy, specify the URL of submission service through request parameter submissionServiceProxy.
uuid: 42d6c1da-3945-469d-b429-c33e563ed70c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 081f7c17-4e5d-4c7e-a5c3-5541a29b9d55
docset: aem65
feature: Mobile Forms
exl-id: 8f9b10ae-1600-49c2-a061-153a2a89c67e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 1%

---

# HTML5表單服務Proxy{#html-forms-service-proxy}

HTML5 Forms Service Proxy是註冊提交服務Proxy的設定。 若要設定服務Proxy，請透過請求引數指定提交服務的URL *submissionServiceProxy*.

## Service Proxy的優點 {#benefits-of-service-proxy-br}

服務Proxy可消除下列專案：

* HTML5表單工作流程需要為HTML5表單使用者開啟提交服務「/content/xfaforms/submission/default」。 這會向更廣大的非預期受眾公開AEM伺服器。
* 服務URL內嵌於表單的執行階段模型中。 無法變更服務URL路徑。
* 提交分為兩個步驟。 若要提交表單資料，提交作業至少需要兩次前往伺服器的歷程。 因此，會增加伺服器的負載。
* HTML5表單會在POST要求中傳送資料，而非PDF要求。 對於同時涉及PDF和HTML5表單的工作流程，需要兩種不同的處理提交的方法。

### 拓撲 {#topologies-br}

HTML5表單可以使用以下拓撲來連線到AEM伺服器。

* AEM Server或HTML5表單用來透過POST將資料傳送至伺服器的拓撲。
* Proxy伺服器將POST資料傳送至伺服器的拓撲。

![HTML5 forms服務Proxy拓撲](assets/topology.png)

HTML5 forms服務Proxy拓撲

HTML5表單會連線至AEM伺服器，以執行伺服器端的指令碼、網頁服務和提交內容。 HTML5表單的XFA執行階段使用「/bin/xfaforms/submitaction」端點上的Ajax呼叫搭配各種引數來連線至AEM伺服器。 HTML5 forms連線AEM伺服器以執行下列操作：

#### 執行伺服器端指令碼和Web服務 {#execute-server-sided-scripts-and-web-services}

標示為在伺服器上執行的指令碼稱為伺服器端指令碼。 下表列出伺服器端指令碼和Web服務中使用的所有引數。

<table>
 <tbody>
  <tr>
   <td><p><strong>参数</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p>活動</p> </td>
   <td><p>活動包含觸發請求的事件。 例如點按、退出或變更</p> </td>
  </tr>
  <tr>
   <td><p>contextSom</p> </td>
   <td><p>contextSom包含執行事件的物件的SOM運算式。</p> </td>
  </tr>
  <tr>
   <td><p>模板</p> </td>
   <td><p>範本包含用於呈現表單的範本。</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>contentRoot包含用來呈現表單的範本根目錄。</p> </td>
  </tr>
  <tr>
   <td><p>数据</p> </td>
   <td><p>資料包含用於轉譯表單的bata位元組。</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>formDom包含JSON格式的HTML5表單的DOM。</p> </td>
  </tr>
  <tr>
   <td><p>封包</p> </td>
   <td><p>封包指定為表單。</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>debugDir包含用來轉譯表單的偵錯目錄。</p> </td>
  </tr>
 </tbody>
</table>

#### 提交資料 {#submit-data}

按一下提交按鈕後，HTML5表單會將資料傳送至伺服器。 下表列出HTML5表單傳送至伺服器的所有引數。

<table>
 <tbody>
  <tr>
   <td><p><strong>参数</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p>模板</p> </td>
   <td><p>用於呈現表單的範本。</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>用於呈現表單的範本根目錄。</p> </td>
  </tr>
  <tr>
   <td><p>数据</p> </td>
   <td><p>用於呈現表單的bata位元組。</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>JSON格式的HTML5表單的DOM。</p> </td>
  </tr>
  <tr>
   <td><p>submiturl</p> </td>
   <td><p>張貼資料XML的URL。</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>用於呈現表單的偵錯目錄。</p> </td>
  </tr>
 </tbody>
</table>

#### 提交代理的運作方式？ {#how-nbsp-the-nbsp-submit-proxy-works}

如果請求引數中不存在submiturl，則提交服務Proxy會作為傳遞。 它可作為傳遞。 它會傳送要求至/bin/xfaforms/submitaction端點，並將回應傳送至XFA執行階段。

如果要求引數中存在送出URL，送出服務Proxy會選取拓撲。

* 如果AEM伺服器發佈資料，Proxy服務會作為傳遞機制。 它會傳送要求至/bin/xfaforms/submitaction端點，並將回應傳送至XFA執行階段。
* 如果Proxy張貼資料，Proxy服務會將除submitUrl以外的所有引數傳遞給 */bin/xfaforms/submitaction* 結束點並接收xml位元組在回應資料流中。 接著，Proxy服務會將資料xml位元組張貼到submitUrl進行處理。

* 在將資料(POST要求)傳送至伺服器之前，HTML5表單會驗證伺服器的連線能力和可用性。 為了驗證連線能力和可用性，HTML表單會傳送空白標頭請求給伺服器。 如果伺服器可用，HTML5表單會將資料(POST請求)傳送至伺服器。 如果伺服器無法使用，則會出現錯誤訊息， *無法連線到伺服器，* 隨即顯示。 進階偵測可避免使用者重新填寫表單的麻煩。 Proxy servlet會處理head要求，不會擲回例外狀況。
