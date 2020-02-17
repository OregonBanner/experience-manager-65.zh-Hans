---
title: Acrobat Reader DC扩展使用的证书类型
seo-title: Acrobat Reader DC扩展使用的证书类型
description: 了解Acrobat Reader DC扩展使用的证书类型。
seo-description: 了解Acrobat Reader DC扩展使用的证书类型。
uuid: 93c02abc-2d5a-44ed-b93c-981afbd0553d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 331b9317-87b5-4a96-a1bc-429675ff90c5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Acrobat Reader DC扩展使用的证书类型 {#certificate-types-used-by-acrobat-reader-dc-extensions}

证书查看器提供有关证书的以下信息：

* 证书“友好”名称
* 证书配置文件
* 有效期
* Acrobat Reader DC扩展的使用权限

## 证书“友好”名称 {#certificate-friendly-name}

Acrobat Reader DC扩展证书的“友好”名称是描述证书属性的字符串，如以下示例所示：

ARE 2D Barcode Full Production V6.1 P8 0002054

该字符串包含以下元素：

**** 证书类型：描述证书激活的AEM表单模块和激活级别，如ARE 2D条形码已满。 有关可用证书类型的列表，请参阅证书配置文件部分表格中的“类型”列。

**** 部署类型：指示证书的预期用途，如生产。 该值可以是“评估”或“生产”。 有关与每个证书类型关联的部署类型列表，请参阅“证书配置文件”部分表格中的“部署类型”列。

**** 使用权限版本：描述证书可用于的使用权限算法版本，如V6.1。此版本不表示Acrobat或Acrobat Reader DC扩展的版本。

**** 个人资料代码：配置文件代码是完整证书属性的简短描述，例如P8。 有关与每个文件类型关联的配置文件代码的列表，请参阅“证书配置文件”部分表格中的“配置文件代码”列。

**** 序列号：将为Adobe颁发的每个证书分配一个序列号，如0002054。 Adobe企业支持或Adobe企业客户代表可以使用此序列号将证书跟踪到特定产品订单或OEM关系。

## 证书配置文件 {#certificate-profiles}

下表列出了在分析Acrobat Reader DC扩展证书时可能遇到的证书配置文件。

<table>
 <thead>
  <tr>
   <th><p>个人资料代码</p></th>
   <th><p>类型</p></th>
   <th><p>有效期</p></th>
   <th><p>部署类型</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>P1</p></td>
   <td><p>SAP Production</p></td>
   <td><p>最大</p></td>
   <td><p>生产</p></td>
  </tr>
  <tr>
   <td><p>P2</p></td>
   <td><p>SAP内部测试</p></td>
   <td><p>2年</p></td>
   <td><p>评估和测试</p></td>
  </tr>
  <tr>
   <td><p>P3</p></td>
   <td><p>Acrobat Reader DC扩展， Production</p></td>
   <td><p>最大</p></td>
   <td><p>生产</p></td>
  </tr>
  <tr>
   <td><p>P4</p></td>
   <td><p>Acrobat Reader DC扩展，内部Adobe使用</p></td>
   <td><p>2年</p></td>
   <td><p>生产</p></td>
  </tr>
  <tr>
   <td><p>P5</p></td>
   <td><p>Acrobat Reader DC扩展，合作伙伴集成</p></td>
   <td><p>2年</p></td>
   <td><p>评估和测试</p></td>
  </tr>
  <tr>
   <td><p>P6</p></td>
   <td><p>Acrobat Reader DC扩展，评估版</p></td>
   <td><p>60天</p></td>
   <td><p>评估</p></td>
  </tr>
  <tr>
   <td><p>P8</p></td>
   <td><p>表单、制作</p></td>
   <td><p>最大</p></td>
   <td><p>生产</p></td>
  </tr>
  <tr>
   <td><p>P9</p></td>
   <td><p>Adobe Acrobat 7.x，生产</p></td>
   <td><p>最大</p></td>
   <td><p>生产</p></td>
  </tr>
  <tr>
   <td><p>I10</p></td>
   <td><p>表单；可供OEM使用。</p></td>
   <td><p>最大</p></td>
   <td><p>生产和评估</p></td>
  </tr>
  <tr>
   <td><p>I11</p></td>
   <td><p>表单；可供OEM使用。</p></td>
   <td><p>最大</p></td>
   <td><p>生产和评估</p></td>
  </tr>
  <tr>
   <td><p>I12</p></td>
   <td><p>仅签名；可供OEM使用。</p></td>
   <td><p>最大</p></td>
   <td><p>生产和评估</p></td>
  </tr>
  <tr>
   <td><p>I13</p></td>
   <td><p>仅限脱机注释；可供OEM使用。</p></td>
   <td><p>最大</p></td>
   <td><p>生产和评估</p></td>
  </tr>
  <tr>
   <td><p>I14</p></td>
   <td><p>仅注释；可供OEM使用。</p></td>
   <td><p>最大</p></td>
   <td><p>生产和评估</p></td>
  </tr>
  <tr>
   <td><p>I15</p></td>
   <td><p>完全权限；可供OEM使用。</p></td>
   <td><p>最大</p></td>
   <td><p>生产和评估</p></td>
  </tr>
 </tbody>
</table>

## 有效期 {#validity-period}

评估证书颁发给客户和开发人员，以便他们能够评估和开发产品的示例应用程序。 这些证书的有效期为60至90天。 它们将在问题数据之后的第二个月结束时到期。

合作伙伴集成证书将颁发给Adobe业务合作伙伴，以支持软件开发、集成、原型构建和演示。 这些证书的有效期为自发行日期起计两年。

Adobe内部使用证书用于支持软件开发、集成、原型构建和演示。 这些证书的有效期为自发行日期起计两年。

生产证书将颁发给购买Acrobat Reader DC扩展的客户。 这些证书在认证中心(CA)允许的最长期限内有效，如“证书配置文件”(Certificate Profiles)表 *中* “最大”(Max)所示。

## Acrobat Reader DC扩展的使用权限 {#acrobat-reader-dc-extensions-usage-rights}

在“证书查看器”中检查Acrobat Reader DC扩展证书时，可以从“详细信息”选项卡（如果已配置）中选择使用权限项，以查看证书可启用的Adobe Reader使用权限的列表。 在特定文档上启用的使用权限可以是由证书启用的使用权限的子集。

如果非协作环境中需要在线注释，请与Adobe支持部门联系以了解更多信息。 “模式”属性与部署类型匹配，是生产 *类* 或评估 *类型*。

允许的Acrobat Reader DC扩展使用权限由一个或多个特定元素组成。 这些元素被用于不同的组合中，以实现各种授权产品功能。

<table>
 <thead>
  <tr>
   <th><p>使用权限元素</p></th>
   <th><p>查看启用了权限的PDF文档时在Adobe reader中启用的功能</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>FormFillIn和Save</p></td>
   <td><p>填写表单字段并将文件保存在本地。</p></td>
  </tr>
  <tr>
   <td><p>FormImportExport</p></td>
   <td><p>将表单数据导入和导出为FDF、XFDF、XML和XDP文件。</p></td>
  </tr>
  <tr>
   <td><p>FormAddDelete</p></td>
   <td><p>在PDF表单上添加、更改或删除字段和字段属性。</p></td>
  </tr>
  <tr>
   <td><p>SubmitStandalone</p></td>
   <td><p>当数据未在浏览器会话中运行时，通过电子邮件或离线将数据提交到服务器。</p></td>
  </tr>
  <tr>
   <td><p>SpawnTemplate</p></td>
   <td><p>从同一PDF表单中的模板页面创建页面。</p></td>
  </tr>
  <tr>
   <td><p>签名</p></td>
   <td><p>对PDF文档进行数字签名并保存，并清除数字签名。</p></td>
  </tr>
  <tr>
   <td><p>AnnotModify</p></td>
   <td><p>创建和修改文档注释，如注释。</p></td>
  </tr>
  <tr>
   <td><p>AnnotImportExport</p></td>
   <td><p>将注释（如注释）保存到单独的数据文件中，并从文件加载注释。</p></td>
  </tr>
  <tr>
   <td><p>BarcodePlaintext</p></td>
   <td><p>以未加密的形式打印包含表单数据栏的文档，该格式不需要获得许可的服务器软件进行解码。</p></td>
  </tr>
  <tr>
   <td><p>AnnotOnline</p></td>
   <td><p>在联机文档审阅和注释服务器上传和下载注释（如注释）。</p></td>
  </tr>
  <tr>
   <td><p>FormOnline</p></td>
   <td><p>连接到PDF表单中定义的Web服务或数据库。</p></td>
  </tr>
  <tr>
   <td><p>EFModif</p></td>
   <td><p>修改与PDF文档关联的嵌入文件对象。</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Acrobat Reader DC扩展的使用权限只能通过Adobe授权许可，但只能通过协同使用的某些组合进行许可。 不能单独许可这些功能。 有关可用的使用权限组合的信息，请与AEM表单帐户代表联系。

