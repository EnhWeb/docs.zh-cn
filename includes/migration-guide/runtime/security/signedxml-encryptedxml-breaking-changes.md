---
ms.openlocfilehash: 8cc4f2ba2923774ef4e4e6861a89a7797ca988e1
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621049"
---
### <a name="signedxml-and-encryptedxml-breaking-changes"></a>SignedXml 和 EncryptedXml 的重大更改

#### <a name="details"></a>详细信息

在 .NET Framework 4.6.2 中，<xref:System.Security.Cryptography.Xml.SignedXml?displayProperty=fullName> 和 <xref:System.Security.Cryptography.Xml.EncryptedXml?displayProperty=fullName> 中的安全修复程序会导致不同的运行时行为。 例如，应用于对象的<ul><li>如果文档包含多个具有相同 <code>id</code> 特性的元素，并且签名将其中一个元素作为签名根的目标，则该文档现在将视为无效。</li><li>在引用中使用非规范 XPath 转换算法的文档现在视为无效。</li><li>在引用中使用非规范 XSLT 转换算法的文档现在视为无效。</li><li>任何利用外部资源拆离签名的程序都无法执行此操作。</li></ul>

#### <a name="suggestion"></a>建议

开发者应该检查 <xref:System.Security.Cryptography.Xml.XmlDsigXsltTransform> 和 <xref:System.Security.Cryptography.Xml.XmlDsigXsltTransform> 以及派生自 <xref:System.Security.Cryptography.Xml.Transform> 的类型的使用情况，因为文档接收器可能无法进行处理。

| “属性”    | 值       |
|:--------|:------------|
| 范围   |次要|
|Version|4.6.2|
|类型|运行时

#### <a name="affected-apis"></a>受影响的 API

-<xref:System.Security.Cryptography.Xml.Transform?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.Xml.XmlDsigXPathTransform?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.Xml.XmlDsigXsltTransform?displayProperty=nameWithType></li></ul>|
