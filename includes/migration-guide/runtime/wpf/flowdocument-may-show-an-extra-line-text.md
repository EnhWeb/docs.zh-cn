---
ms.openlocfilehash: 0470cefc05fb5da6a6195ee0a96f04feef01fd10
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619882"
---
### <a name="flowdocument-may-show-an-extra-line-of-text"></a>FlowDocument 可能显示额外的文本行

#### <a name="details"></a>详细信息

在某些情况下，当 <xref:System.Windows.Documents.FlowDocument> 元素在 .NET Framework 4.5 上运行时，可能显示额外的文本行，这是与它在 .NET Framework 4.0 上运行时显示的不同之处。 暂未出现已知的案例显示此更改导致任意文本难以阅读或显示不明，但是它可能导致出现之前 <xref:System.Windows.Documents.FlowDocument> 视图中忽略的文本。

#### <a name="suggestion"></a>建议

在某些情况下，减少一个显示元素的 PageHeight 属性可能还原之前显示的行数。

| “属性”    | “值”       |
|:--------|:------------|
| 范围   |边缘|
|Version|4.5|
|类型|运行时

#### <a name="affected-apis"></a>受影响的 API

-<xref:System.Windows.Documents.FlowDocument.%23ctor></li><li><xref:System.Windows.Documents.FlowDocument.%23ctor(System.Windows.Documents.Block)></li><li><xref:System.Windows.Controls.FlowDocumentReader.%23ctor></li><li><xref:System.Windows.Controls.FlowDocumentPageViewer.%23ctor></li><li><xref:System.Windows.Controls.Primitives.DocumentPageView.%23ctor></li></ul>|
