---
title: return 语句 - C# 参考
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- return_CSharpKeyword
- return
helpviewer_keywords:
- return statement [C#]
- return keyword [C#]
ms.assetid: 6da6e152-5b58-4448-8f3f-470dd0617ecd
ms.openlocfilehash: 3e89f2f854d1f66ca2d7bf1cfa5a507c267798f8
ms.sourcegitcommit: 10986410e59ff29f2ec55c6759bde3eb4d1a00cb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/31/2019
ms.locfileid: "66422729"
---
# <a name="return-c-reference"></a>return（C# 参考）

`return` 语句可终止它所在的方法的执行，并将控制权返回给调用方法。 它还可以返回可选值。 如果方法是 `void` 类型，则 `return` 语句可以省略。

 如果 return 语句位于 `try` 块中，则 `finally` 块（如果存在）会在控制权返回给调用方法之前进行执行。

## <a name="example"></a>示例

 在下面的示例中，方法 `CalculateArea()` 以 [double](double.md) 值的形式返回本地变量 `area`。

[!code-csharp[csrefKeywordsJump#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsJump/CS/csrefKeywordsJump.cs#6)]  

## <a name="c-language-specification"></a>C# 语言规范

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 关键字](index.md)
- [return 语句](/cpp/cpp/return-statement-cpp)
