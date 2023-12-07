---
title: Acrobat Reader DC扩展使用的证书类型
description: 了解Acrobat Reader DC扩展使用的证书类型。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 800bffd5-0cdc-4251-bba4-e350f226f019
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 2%

---

# Acrobat Reader DC扩展使用的证书类型 {#certificate-types-used-by-acrobat-reader-dc-extensions}

证书查看器提供有关证书的以下信息：

* 证书“友好”名称
* 证书配置文件
* 有效期
* Acrobat Reader DC扩展使用权限

## 证书“友好”名称 {#certificate-friendly-name}

Acrobat Reader DC扩展证书的“友好”名称是一个描述证书属性的字符串，如以下示例所示：

是2D条形码完全生产V6.1 P8 0002054

该字符串包含以下元素：

**证书类型：** 描述证书激活的AEM表单模块以及激活级别，例如“ARE 2D条形码已满”。 有关可用的证书类型列表，请参阅证书配置文件部分的表中的类型列。

**部署类型：** 指示证书的预期用途，如生产。 该值可以是“评估”或“生产”。 有关与每种证书类型关联的部署类型列表，请参阅证书配置文件部分的表中的部署类型列。

**使用权限版本：** 描述证书可用于的使用权限算法的版本，例如V6.1。此版本不表示Acrobat或Acrobat Reader DC扩展的版本。

**配置文件代码：** 配置文件代码是对完整证书属性的简短描述，例如P8。 有关与每种文件类型关联的配置文件代码的列表，请参阅证书配置文件部分表中配置文件代码列。

**序列号：** 序列号将分配给Adobe颁发的每个证书，如0002054。 Adobe企业支持或Adobe企业客户代表可以使用此序列号来跟踪到特定产品订单或OEM关系的证书。

## 证书配置文件 {#certificate-profiles}

下表列出了在分析Acrobat Reader DC扩展证书时可能遇到的证书配置文件。

<table>
 <thead>
  <tr>
   <th><p>配置文件代码</p></th>
   <th><p>类型</p></th>
   <th><p>有效期</p></th>
   <th><p>部署类型</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>P1</p></td>
   <td><p>SAP生产</p></td>
   <td><p>Max</p></td>
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
   <td><p>Acrobat Reader DC扩展，生产</p></td>
   <td><p>Max</p></td>
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
   <td><p>Acrobat Reader DC扩展，评估</p></td>
   <td><p>60 天</p></td>
   <td><p>评估</p></td>
  </tr>
  <tr>
   <td><p>P8</p></td>
   <td><p>Forms，生产</p></td>
   <td><p>Max</p></td>
   <td><p>生产</p></td>
  </tr>
  <tr>
   <td><p>P9</p></td>
   <td><p>Adobe Acrobat 7.x，生产</p></td>
   <td><p>Max</p></td>
   <td><p>生产</p></td>
  </tr>
  <tr>
   <td><p>I10</p></td>
   <td><p>Forms；可供OEM使用</p></td>
   <td><p>Max</p></td>
   <td><p>生产和评估</p></td>
  </tr>
  <tr>
   <td><p>I11</p></td>
   <td><p>Forms；可供OEM使用</p></td>
   <td><p>Max</p></td>
   <td><p>生产和评估</p></td>
  </tr>
  <tr>
   <td><p>I12</p></td>
   <td><p>仅签名；可由OEM使用</p></td>
   <td><p>Max</p></td>
   <td><p>生产和评估</p></td>
  </tr>
  <tr>
   <td><p>I13</p></td>
   <td><p>仅离线注释；可由OEM使用</p></td>
   <td><p>Max</p></td>
   <td><p>生产和评估</p></td>
  </tr>
  <tr>
   <td><p>I14</p></td>
   <td><p>仅注释；可由OEM使用</p></td>
   <td><p>Max</p></td>
   <td><p>生产和评估</p></td>
  </tr>
  <tr>
   <td><p>I15</p></td>
   <td><p>完全权限；可由OEM使用</p></td>
   <td><p>Max</p></td>
   <td><p>生产和评估</p></td>
  </tr>
 </tbody>
</table>

## 有效期 {#validity-period}

评估证书将颁发给客户和开发人员，以便他们能够评估和开发产品的示例应用程序。 这些证书的有效期为60至90天。 它们会在发布数据后的第二个月末过期。

合作伙伴集成证书将颁发给Adobe业务合作伙伴，以支持软件开发、集成、原型制作和演示。 这些证书自签发之日起有效期为两年。

Adobe内使用Adobe内部使用证书来支持软件开发、集成、原型制作和演示。 这些证书自签发之日起有效期为两年。

生产证书将颁发给购买了Acrobat Reader DC扩展的客户。 这些证书在证书颁发机构(CA)允许的最长有效期内有效，如下所示 *Max* 在证书配置文件表中。

## Acrobat Reader DC扩展使用权限 {#acrobat-reader-dc-extensions-usage-rights}

在证书查看器中检查Acrobat Reader DC扩展证书时，您可以从详细信息选项卡（如果已配置）中选择使用权限项，以查看证书可以启用的Adobe Reader使用权限的明细列表。 在特定文档上启用的使用权限可以是证书启用的使用权限的子集。

如果在非协作环境中需要在线评论，请联系Adobe支持以获取更多信息。 Mode属性与部署类型匹配，并且 *生产* 或 *评估*.

允许的Acrobat Reader DC扩展使用权限由一个或多个特定元素组成。 这些元素以不同的组合使用，以实现各种许可的产品功能。

<table>
 <thead>
  <tr>
   <th><p>使用权限元素</p></th>
   <th><p>查看启用了权限的PDF文档时在Adobe Reader中启用的功能</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>FormFillInAndSave</p></td>
   <td><p>填写表单字段并在本地保存文件。</p></td>
  </tr>
  <tr>
   <td><p>FormImportExport</p></td>
   <td><p>将表单数据导入和导出为FDF、XFDF、XML和XDP文件。</p></td>
  </tr>
  <tr>
   <td><p>FormAddDelete</p></td>
   <td><p>添加、更改或删除PDF表单中的字段和字段属性。</p></td>
  </tr>
  <tr>
   <td><p>SubmitStandalone</p></td>
   <td><p>如果数据不在浏览器会话中运行，请通过电子邮件或脱机将其提交到服务器。</p></td>
  </tr>
  <tr>
   <td><p>SpawnTemplate</p></td>
   <td><p>在同一PDF表单中从模板页面创建页面。</p></td>
  </tr>
  <tr>
   <td><p>签名</p></td>
   <td><p>数字签名和保存PDF文档，并清除数字签名。</p></td>
  </tr>
  <tr>
   <td><p>AnnotModify</p></td>
   <td><p>创建和修改文档注释，如注释。</p></td>
  </tr>
  <tr>
   <td><p>AnnotImportExport</p></td>
   <td><p>将注释（如注释）保存在单独的数据文件中，并从文件中加载注释。</p></td>
  </tr>
  <tr>
   <td><p>条形码纯文本</p></td>
   <td><p>打印文档，其中表单数据以非加密形式进行条形码，不需要获得许可的服务器软件解码。</p></td>
  </tr>
  <tr>
   <td><p>AnnotOnline</p></td>
   <td><p>将批注（例如批注）上载到联机文档审阅和批注服务器或从联机文档审阅和批注服务器下载批注。</p></td>
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
>Acrobat Reader DC扩展使用权限只能通过某些可一起使用的组合从Adobe进行许可。 无法单独许可这些功能。 有关可用使用权限组合的信息，请联系AEM Forms客户代表。
