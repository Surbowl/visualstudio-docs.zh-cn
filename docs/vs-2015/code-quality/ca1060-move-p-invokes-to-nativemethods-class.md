---
title: CA1060：将 P 调用移到 NativeMethods 类 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- MovePInvokesToNativeMethodsClass
- CA1060
helpviewer_keywords:
- MovePInvokesToNativeMethodsClass
- CA1060
ms.assetid: 06686c8c-6ad3-42f7-a355-cbaefa347cfc
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: e01ad9fc4fc57917c123404d8863d04240585793
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85533427"
---
# <a name="ca1060-move-pinvokes-to-nativemethods-class"></a>CA1060：将 P/Invoke 移动到 NativeMethods 类
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|MovePInvokesToNativeMethodsClass|
|CheckId|CA1060|
|类别|Microsoft. Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 方法使用平台调用服务来访问非托管代码，而不是**NativeMethods**类之一的成员。

## <a name="rule-description"></a>规则描述
 平台调用方法（如使用特性标记的方法 <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName> 或使用中的关键字定义的方法）可 `Declare` [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 访问非托管代码。 这些方法应为以下类之一：

- **NativeMethods** -此类不取消托管代码权限的堆栈行走。 （ <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute?displayProperty=fullName> 不能应用于此类。）此类用于可在任何位置使用的方法，因为将执行堆栈遍历。

- **SafeNativeMethods** -此类取消托管代码权限的堆栈行走。 （ <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute?displayProperty=fullName> 将应用于此类。）此类适用于任何人都可以调用的安全方法。 这些方法的调用方不需要执行完整安全检查以确保使用是安全的，因为这些方法对于任何调用方是无害的。

- **UnsafeNativeMethods** -此类取消托管代码权限的堆栈行走。 （ <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute?displayProperty=fullName> 将应用于此类。）此类适用于有潜在危险的方法。 这些方法的任何调用方都必须执行完整安全检查，以确保使用是安全的，因为不会执行任何堆栈遍历。

  这些类声明为 `internal` （ `Friend` 在 Visual Basic 中），并声明一个私有构造函数来阻止创建新实例。 这些类中的方法应为 `static` 和 `internal` （ `Shared` `Friend` 在 Visual Basic 中）。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将方法移动到相应的**NativeMethods**类中。 对于大多数应用程序，将 P/Invoke 移动到名为**NativeMethods**的新类就足够了。

 但是，如果要开发在其他应用程序中使用的库，应考虑定义两个称为**SafeNativeMethods**和**UnsafeNativeMethods**的其他类。 这些类类似于**NativeMethods**类;但是，它们使用名为**SuppressUnmanagedCodeSecurityAttribute**的特殊属性进行标记。 应用此特性时，运行时不会执行完整的堆栈审核，以确保所有调用方都具有**UnmanagedCode**权限。 运行时通常会在启动时检查此权限。 由于未执行检查，因此它可以极大地提高对这些非托管方法的调用的性能，同时还允许具有受限权限的代码调用这些方法。

 不过，您应该非常小心地使用此属性。 如果未正确实现，则可能会产生严重的安全隐患。

 有关如何实现这些方法的信息，请参阅**NativeMethods**示例、 **SafeNativeMethods**示例和**UnsafeNativeMethods**示例。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例声明了违反此规则的方法。 若要更正此冲突，应将**RemoveDirectory** P/Invoke 移动到设计为仅保存 P/invoke 的适当的类。

 [!code-csharp[FxCop.Design.DllImportNativeMethods#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.DllImportNativeMethods/cs/FxCop.Design.DllImportNativeMethods.cs#1)]
 [!code-vb[FxCop.Design.DllImportNativeMethods#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.DllImportNativeMethods/vb/FxCop.Design.DllImportNativeMethods.vb#1)]

## <a name="nativemethods-example"></a>NativeMethods 示例

### <a name="description"></a>描述
 由于**NativeMethods**类不应使用**SuppressUnmanagedCodeSecurityAttribute**进行标记，因此，放入它的 P/invoke 将需要**UnmanagedCode**权限。 由于大多数应用程序都从本地计算机运行并与完全信任一起运行，因此通常不会出现问题。 但是，如果要开发可重用的库，应考虑定义**SafeNativeMethods**或**UnsafeNativeMethods**类。

 下面的示例演示了**一个**MessageBeep 函数，该方法用于包装来自 user32.dll 的**MessageBeep**函数。 **MessageBeep** P/Invoke 置于**NativeMethods**类中。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Design.NativeMethods#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.NativeMethods/cs/FxCop.Design.NativeMethods.cs#1)]
 [!code-vb[FxCop.Design.NativeMethods#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.NativeMethods/vb/FxCop.Design.NativeMethods.vb#1)]

## <a name="safenativemethods-example"></a>SafeNativeMethods 示例

### <a name="description"></a>描述
 可以安全地公开给任何应用程序并没有任何副作用的 P/Invoke 方法应放在名为**SafeNativeMethods**的类中。 您无需权限，并且无需特别注意从其调用的位置。

 下面的示例演示了一个**environment.tickcount**属性，该属性将**GetTickCount**函数从 kernel32.dll 中包装。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Design.NativeMethodsSafe#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.NativeMethodsSafe/cs/FxCop.Design.NativeMethodsSafe.cs#1)]
 [!code-vb[FxCop.Design.NativeMethodsSafe#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.NativeMethodsSafe/vb/FxCop.Design.NativeMethodsSafe.vb#1)]

## <a name="unsafenativemethods-example"></a>UnsafeNativeMethods 示例

### <a name="description"></a>描述
 不能安全调用并且可能导致副作用的 P/Invoke 方法应放在名为**UnsafeNativeMethods**的类中。 应严格检查这些方法，以确保不会无意中向用户公开这些方法。 规则[CA2118：查看 SuppressUnmanagedCodeSecurityAttribute 用法](../code-quality/ca2118-review-suppressunmanagedcodesecurityattribute-usage.md)有助于此操作。 此外，这些方法在使用时，还应具有其他所需的权限，而不是**UnmanagedCode** 。

 下面的示例演示了一个**Cursor。 Hide**方法，该方法可从 user32.dll 包装**ShowCursor**函数。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Design.NativeMethodsUnsafe#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.NativeMethodsUnsafe/cs/FxCop.Design.NativeMethodsUnsafe.cs#1)]
 [!code-vb[FxCop.Design.NativeMethodsUnsafe#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.NativeMethodsUnsafe/vb/FxCop.Design.NativeMethodsUnsafe.vb#1)]

## <a name="see-also"></a>另请参阅
 [设计警告](../code-quality/design-warnings.md)
