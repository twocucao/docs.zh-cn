---
title: 异步文件 I/O
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- streams, synchronous streams
- asynchronous I/O
- synchronous I/O
- streams, asynchronous streams
- I/O [.NET Framework], asynchronous I/O
- Stream class, synchronous I/O
- data streams, asynchronous streams
- Stream class, asynchronous I/O
- multiple I/O requests
- data streams, synchronous streams
ms.assetid: dbdd55e7-d6b9-4f9e-8abb-ab0edd4457f7
author: mairaw
ms.author: mairaw
ms.openlocfilehash: b175d3f8f7fe453596d346949700e220950358c7
ms.sourcegitcommit: 4735bb7741555bcb870d7b42964d3774f4897a6e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66377535"
---
# <a name="asynchronous-file-io"></a>异步文件 I/O

异步操作使您能在不阻塞主线程的情况下执行占用大量资源的 I/O 操作。 在 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 应用或 [!INCLUDE[desktop_appname](../../../includes/desktop-appname-md.md)] 应用中一个耗时的流操作可能阻塞 UI 线程并让您的应用看起来好像不工作时，这种性能的考虑就显得尤为重要了。

从 .NET Framework 4.5 开始，I/O 类型包括异步方法来简化异步操作。 异步方法在其名称中包括 `Async` ，例如 <xref:System.IO.Stream.ReadAsync%2A>、 <xref:System.IO.Stream.WriteAsync%2A>、 <xref:System.IO.Stream.CopyToAsync%2A>、 <xref:System.IO.Stream.FlushAsync%2A>、 <xref:System.IO.TextReader.ReadLineAsync%2A>和 <xref:System.IO.TextReader.ReadToEndAsync%2A>。 这些异步方法基于流类（例如 <xref:System.IO.Stream>、 <xref:System.IO.FileStream>和 <xref:System.IO.MemoryStream>）和用来向流中读出或写入数据的类（例如 <xref:System.IO.TextReader> 和 <xref:System.IO.TextWriter>）实现。

在 .NET Framework 4 和更早的版本中，您必须使用 <xref:System.IO.Stream.BeginRead%2A> 和 <xref:System.IO.Stream.EndRead%2A> 之类的方法来实现异步 I/O 操作。 这些方法仍然在 .NET Framework 4.5 中可用，从而支持传统的代码；但是，异步方法能帮助你更轻松地实现异步 I/O 操作。

C# 和 Visual Basic 分别具有两个用于异步编程的关键字：

- `Async` (Visual Basic) 或 `async` (C#) 修饰符，您可以用来标记包含异步操作的方法。

- `Await` (Visual Basic) 或 `await` (C#) 运算符，可以应用到异步方法的结果中。

如下面的示例所示，若要实现异步 I/O 操作，请把这些关键字和异步方法结合使用。 有关详细信息，请参阅[使用 async 和 await 的异步编程 (C#)](../../csharp/programming-guide/concepts/async/index.md) 或 [使用 Async 和 Await 的异步编程 (Visual Basic)](../../visual-basic/programming-guide/concepts/async/index.md)。

下面的示例演示如何使用两个 <xref:System.IO.FileStream> 对象把文件从一个目录异步复制到另一个目录。 需要注意 <xref:System.Web.UI.WebControls.Button.Click> 控件的 <xref:System.Windows.Controls.Button> 事件处理程序具有 `async` 修饰符标记，因为它调用异步方法。

[!code-csharp[Asynchronous_File_IO_async#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Asynchronous_File_IO_async/cs/example.cs#1)]
[!code-vb[Asynchronous_File_IO_async#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Asynchronous_File_IO_async/vb/example.vb#1)]

下一个例子类似于前面的例子，但是使用 <xref:System.IO.StreamReader> 和 <xref:System.IO.StreamWriter> 对象以异步方式读取和写入文本文件的内容。

[!code-csharp[Asynchronous_File_IO_async#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Asynchronous_File_IO_async/cs/example2.cs#2)]
[!code-vb[Asynchronous_File_IO_async#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Asynchronous_File_IO_async/vb/example2.vb#2)]

下一个例子演示用于在 <xref:System.IO.Stream> 应用中以 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 的形式打开文件的代码隐藏文件和 XAML 文件，并且通过使用 <xref:System.IO.StreamReader> 类的实例来读取其内容。 它使用异步方法以流的形式打开文件并读取其内容。

[!code-csharp[System.IO.WindowsRuntimeStorageExtensions#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.windowsruntimestorageextensions/cs/blankpage.xaml.cs#2)]
[!code-vb[System.IO.WindowsRuntimeStorageExtensions#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.windowsruntimestorageextensions/vb/blankpage.xaml.vb#2)]

[!code-xaml[System.IO.WindowsRuntimeStorageExtensions#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.windowsruntimestorageextensions/cs/blankpage.xaml#1)]

## <a name="see-also"></a>请参阅

- <xref:System.IO.Stream>
- [文件和流 I/O](index.md)
- [使用 Async 和 Await 的异步编程 (C#)](../../csharp/programming-guide/concepts/async/index.md)
- [使用 Async 和 Await 的异步编程 (Visual Basic)](../../visual-basic/programming-guide/concepts/async/index.md)
