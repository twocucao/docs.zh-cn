---
title: ?:运算符 - C# 参考
ms.custom: seodec18
ms.date: 11/20/2018
f1_keywords:
- ?:_CSharpKeyword
- ?_CSharpKeyword
- :_CSharpKeyword
helpviewer_keywords:
- '?: operator [C#]'
- conditional operator (?:) [C#]
ms.assetid: e83a17f1-7500-48ba-8bee-2fbc4c847af4
ms.openlocfilehash: ae3039df2c1260211f4c7ec3e813db1d0c6cd42b
ms.sourcegitcommit: 5ae6affa0b171be3bb5f4729fb68ea4fe799f959
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/10/2019
ms.locfileid: "66815934"
---
# <a name="-operator-c-reference"></a>?:运算符（C# 参考）

条件运算符 (`?:`) 通常被称为三元条件运算符，用于计算 Boolean 表达式，并根据 Boolean 表达式的计算结果为 `true` 还是 `false` 来返回计算两个表达式其中之一的结果。 从 C# 7.2 开始，[ref 条件表达式](#conditional-ref-expression)将返回对两个表示式之一的结果的引用。

条件运算符的语法如下所示：

```csharp
condition ? consequent : alternative
```

`condition` 表达式的计算结果必须为 `true` 或 `false`。 若 `condition` 的计算结果为 `true`，将计算 `consequent`，其结果成为运算结果。 若 `condition` 的计算结果为 `false`，将计算 `alternative`，其结果成为运算结果。 只会计算 `consequent` 或 `alternative`。

`consequent` 和 `alternative` 的类型必须相同，或者必须存在从一种类型到另一种类型的隐式转换。

条件运算符为右联运算符，即形式的表达式

```csharp
a ? b : c ? d : e
```

计算结果为

```csharp
a ? b : (c ? d : e)
```

> [!TIP]
> 可以使用以下助记键设备记住条件运算符的计算方式：
>
> ```text
> is this condition true ? yes : no
> ```

下面的示例演示条件运算符的用法：

[!code-csharp-interactive[non ref conditional](~/samples/csharp/language-reference/operators/ConditionalOperator.cs#ConditionalValue)]

## <a name="conditional-ref-expression"></a>ref 条件表达式

从 C# 7.2 开始，可以使用 ref 条件表达式返回对两个表示式之一的结果的引用。 可以将该引用分配到 [ref local](../keywords/ref.md#ref-locals) 或 [ref readonly local](../keywords/ref.md#ref-readonly-locals) 变量，或将它用作[引用返回值](../keywords/ref.md#reference-return-values)或 [`ref` 方法参数](../keywords/ref.md#passing-an-argument-by-reference)。

ref 条件表达式的语法如下所示：

```csharp
condition ? ref consequent : ref alternative
```

ref 条件表达式与原始的条件运算符相似，仅计算两个表达式其中之一：`consequent` 或 `alternative`。

在 ref 条件表达式中，`consequent` 和 `alternative` 的类型必须相同。

下面的示例演示 ref 条件表达式的用法：

[!code-csharp-interactive[conditional ref](~/samples/csharp/language-reference/operators/ConditionalOperator.cs#ConditionalRef)]

有关详细信息，请参阅[功能建议说明](../../../../_csharplang/proposals/csharp-7.2/conditional-ref.md)。

## <a name="conditional-operator-and-an-ifelse-statement"></a>条件运算符和 `if..else` 语句

需要根据条件计算值时，在 [if-else](../keywords/if-else.md) 语句中使用条件运算符可以使代码更简洁。 下面的示例演示了将整数归类为负数或非负数的两种方法：

[!code-csharp[conditional and if-else](~/samples/csharp/language-reference/operators/ConditionalOperator.cs#CompareWithIf)]

## <a name="operator-overloadability"></a>运算符可重载性

无法重载条件运算符。

## <a name="c-language-specification"></a>C# 语言规范

有关详细信息，请参阅 [C# 语言规范](~/_csharplang/spec/introduction.md)的[条件运算符](~/_csharplang/spec/expressions.md#conditional-operator)部分。

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 运算符](index.md)
- [if-else 语句](../keywords/if-else.md)
- [?. 和 ?[] 运算符](member-access-operators.md#null-conditional-operators--and-)
- [?? 运算符](null-coalescing-operator.md)
- [ref 关键字](../keywords/ref.md)
