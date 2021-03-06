---
title: 嵌套函数没有与委托“<delegatename>”兼容的签名。
ms.date: 07/20/2015
f1_keywords:
- vbc36532
- bc36532
helpviewer_keywords:
- BC36532
ms.assetid: 493f292c-d81e-40ef-8b47-61f020571829
ms.openlocfilehash: 28d07f01c0fd467cb68d73749988273eee95edf4
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409421"
---
# <a name="nested-function-does-not-have-a-signature-that-is-compatible-with-delegate-delegatename"></a>嵌套函数没有与委托“\<delegatename>”兼容的签名。

已将 lambda 表达式分配给具有不兼容签名的委托。 例如，在下面的代码中，委托 `Del` 具有两个整数参数。

```vb
Delegate Function Del(ByVal p As Integer, ByVal q As Integer) As Integer
```

如果将带一个自变量的 lambda 表达式声明为类型，则会引发此错误 `Del` ：

```vb
' Neither of these is valid.
' Dim lambda1 As Del = Function(n As Integer) n + 1
' Dim lambda2 As Del = Function(n) n + 1
```

**错误 ID：** BC36532

## <a name="to-correct-this-error"></a>更正此错误

调整委托定义或指定的 lambda 表达式，使签名兼容。

## <a name="see-also"></a>另请参阅

- [宽松委托转换](../../programming-guide/language-features/delegates/relaxed-delegate-conversion.md)
- [Lambda 表达式](../../programming-guide/language-features/procedures/lambda-expressions.md)
