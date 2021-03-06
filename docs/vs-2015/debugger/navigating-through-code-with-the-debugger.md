---
title: 使用调试器在代码中导航 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.execution
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
helpviewer_keywords:
- stepping
- debugging [Visual Studio], execution control
- execution, controlling in debugger
ms.assetid: 759072ba-4aaa-447e-8e51-0dd1456fe896
caps.latest.revision: 47
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f79ece781db19f2483ef1dd6cb0a81ff7cf78e06
ms.sourcegitcommit: 4be64917e4224fd1fb27ba527465fca422bc7d62
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "88608938"
---
# <a name="navigating-through-code-with-the-debugger"></a>使用调试器浏览代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

熟悉命令和快捷方式，以便在调试器中导航代码，从而更快、更轻松地在应用程序中查找和解决问题。 在调试器中导航代码时，可以 [检查应用的状态](https://msdn.microsoft.com/library/mt243867.aspx#BKMK_Inspect_Variables) ，或了解有关其执行流程的详细信息。  
  
## <a name="start-debugging"></a>开始调试  
 通常，可以使用**F5** (**调试**  /  **启动**调试) 来启动调试会话。 此命令在附加调试器的情况下启动应用。  
  
 绿色箭头还会启动调试器 (与 **F5**) 相同。  
  
 ![DBG&#95;基础知识&#95;开始&#95;调试](../debugger/media/dbg-basics-start-debugging.png "DBG_Basics_Start_Debugging")  
  
 还可以通过其他一些方式在附加了调试器的情况下启动应用程序，包括 **F11** ([单步执行代码](#BKMK_Step_into__over__or_out_of_the_code)) ，  **F10** ([逐过程执行代码](#BKMK_Step_over_Step_out)) ，或使用 " **运行到光标处**"。  有关这些选项的作用的信息，请参阅本主题中的其他部分。  
  
 调试时，黄色线条将显示下一步要执行的代码。  
  
 ![DBG&#95;基础知识&#95;中断&#95;模式](../debugger/media/dbg-basics-break-mode.png "DBG_Basics_Break_Mode")  
  
 调试时，可以在 **F5**、 **F11** 和使用本主题中所述的其他功能 (例如断点）之间进行切换，) 以快速找到要查看的代码。  
  
 大多数调试器功能（如在 "局部变量" 窗口中查看变量值或在监视窗口中计算表达式）仅在调试器暂停时才可用 (也称为 *中断模式*) 。 暂停调试器后，当函数、变量和对象保留在内存中时，应用状态将挂起。 在中断模式下，你可以检查元素的位置和状态以查找冲突或 bug。 对于某些项目类型，你还可以在中断模式下对应用进行调整。  
  
## <a name="step-into-code-line-by-line"></a><a name="BKMK_Step_into__over__or_out_of_the_code"></a> 逐行执行代码  
 若要在调试时在每个代码行上停止 (每个语句) ，请在菜单) 上，使用**F11**键盘快捷方式 (或 "**调试**  /  **单步执行**"。  
  
> [!TIP]
> 执行每行代码时，可以将鼠标悬停在变量上以查看其值，或者使用 " [局部变量](../debugger/autos-and-locals-windows.md) " 和 " [监视](../debugger/autos-and-locals-windows.md) " 窗口来监视它们的值更改。  
  
 下面是有关 **单步**执行的行为的一些详细信息：  
  
- 在嵌套函数调用上， **“逐语句”** 将进入并单步执行嵌套最深的函数。 如果对类似 **的调用使用** “逐语句” `Func1(Func2())`，调试器将进入并单步执行函数 `Func2`。  
  
- 实际上，调试器逐句通过代码语句，而不是物理行。 例如， `if` 子句可以写在一行内：  
  
  ```csharp  
  int x = 42;  
  string s = "Not answered";  
  if( int x == 42) s = "Answered!";  
  ```  
  
  ```vb  
  Dim x As Integer = 42  
  Dim s As String = "Not answered"  
  If x = 42 Then s = "Answered!"  
  ```  
  
   当你单步执行此行时，调试器将该条件视为一步，将结果视为另一步（在此示例中，条件为 true）。  
  
  若要在单步执行函数时以可视化方式跟踪调用堆栈，请参阅 [在调试时映射调用堆栈上的方法](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)。  
  
## <a name="step-through-code-skipping-functions"></a><a name="BKMK_Step_over_Step_out"></a> 单步执行代码，跳过函数  
 当在调试器中运行代码时，您通常会发现，无需查看特定函数中发生的情况 (您不关心它，或者您知道它的工作原理，如) 的经过充分测试的库代码。 当然，使用这些命令跳过代码 (仍执行的函数，但调试器会跳过它们) 。  
  
|键盘命令|菜单命令|描述|  
|----------------------|------------------|-----------------|  
|**F10**|**逐过程**|如果当前行包含函数调用，则 **逐过程** 运行代码，然后在被调用函数返回后，在代码的第一行处挂起执行。|  
|**Shift+F11**|**步出**|当当前函数返回 (调试器跳过当前函数) 时，**单步**执行将继续运行代码并挂起执行。|  
  
> [!TIP]
> 如果需要在应用中查找入口点，请从 **F10** 或 **F11**开始。 检查应用状态或尝试查找有关其执行流的详细信息时，这些命令通常非常有用。  
  
## <a name="run-to-a-specific-location-or-function"></a><a name="BKMK_Break_into_code_by_using_breakpoints_or_Break_All"></a>运行到特定位置或函数  
 通常，调试代码的首选方法是，当你确切知道要检查的代码，或者至少知道想要开始调试的位置时，这些方法非常有用。  
  
- **在代码中设置断点**  
  
     若要在代码中设置简单断点，请打开 Visual Studio 编辑器中的源文件。 在要挂起执行的代码行处设置光标，然后在代码窗口中右键单击以查看上下文菜单，并选择 " **断点"/"插入断点** " (或按 **F9**) 。 调试器将在执行行之前挂起执行。  
  
     ![设置断点](../debugger/media/dbg-basics-setbreakpoint.png "DBG_Basics_SetBreakpoint")  
  
     Visual Studio 中的断点提供了一组丰富的附加功能，例如条件断点和跟踪点。 请参阅 [使用断点](../debugger/using-breakpoints.md)。  
  
- **运行到光标处**  
  
     若要运行到光标位置，请将光标放在源窗口中可执行的代码行上。 在编辑器的上下文菜单中 (右键单击编辑器) ，选择 " **运行到光标处**"。 这类似于设置临时断点。  
  
- **手动中断代码**  
  
     若要在正在执行的应用程序上，中断下一个可用的代码行，请选择 **“调试”**、 **“全部中断”** （键盘： **Ctrl+Alt+Break**）。  
  
     如果中断正在执行的代码，而没有响应的源或符号 (.pdb) 文件，调试器将显示“未找到源文件” **** 或“未找到符号” **** 页面，帮助你找到相应的文件。 请参阅 [指定符号 ( .pdb) 文件和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)。 如果你无法访问支持文件，仍可以在“反汇编”窗口中调试汇编指令。  
  
- **在调用堆栈上运行到函数**  
  
     在 " **调用堆栈** " 窗口中 (调试时可用) ，请选择该函数，右键单击并选择 " **运行到光标处**"。 若要直观地跟踪调用堆栈，请参阅[调试时映射调用堆栈上的方法](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)。  
  
- **运行到通过名称指定的函数**  
  
     可以告诉调试器运行应用程序，直到它到达指定的函数。 你可以通过名称指定函数，也可以从调用堆栈中选择函数。  
  
     若要通过名称指定函数，请选择 **“调试”**、 **“新建断点”**、 **“在函数处中断”**，然后输入函数名称和其他标识信息。  
  
     ![“新建断点”对话框](../debugger/media/dbg-execution-newbreakpoint.png "DBG_Execution_NewBreakpoint")  
  
     如果是重载函数，或者函数在多个命名空间，你可以在 **“选择断点”** 对话框中选择想要的函数。  
  
     !["选择断点" 对话框](../debugger/media/dbg-execution-overloadedbreakpoints.png "DBG_Execution_OverloadedBreakpoints")  
  
## <a name="move-the-pointer-to-change-the-execution-flow"></a><a name="BKMK_Set_the_next_statement_to_execute"></a>移动指针以更改执行流  
 调试器暂停时，你可以移动指令指针，以设置要执行的下一条代码语句。 源窗口或“反汇编”窗口的空白区域中的黄色箭头标记要执行的下一条语句的位置。 通过移动此箭头，可以跳过部分代码或返回到以前执行过的行。 在某些情况下可以使用此方法，例如，跳过包含已知 bug 的代码段。  
  
 ![示例 2](../debugger/media/dbg-basics-example2.png "DBG_Basics_Example2")  
  
 要设置下一条要执行的语句，请使用以下过程之一：  
  
- 在源窗口中，将黄色箭头拖动希望执行下一语句的位置，该位置应在同一源文件。  
  
- 在源窗口中，将光标置于要接下来执行的行，右键单击并选择 " **设置下一语句**"。  
  
- 在 "反汇编" 窗口中，将光标置于想要接下来执行的程序集指令上，右键单击并选择 " **设置下一语句**"。  
  
> [!CAUTION]
> 设置下一条语句将导致程序计数器直接跳到新位置。 使用此命令时要小心：  
> 
> - 不执行旧执行点和新执行点之间的指令。  
>   - 如果向后移动执行点，则不撤消插入的指令。  
>   - 将下一条语句移动到另一个函数或范围通常会导致调用堆栈损坏，导致一个运行时错误或异常。 如果尝试将下一条语句移动到另一个范围，则调试器将打开一个含有警告的对话框，并提供一个取消该操作的机会。 在 Visual Basic 中，不能将下一条语句移动到另一个范围或函数。  
>   - 在本机 C++ 中，如果已启用运行时检查，设置下一条语句会导致执行到达方法的结尾时引发异常。  
>   - 当启用“编辑并继续”时，如果你进行了“编辑并继续”无法立即重新映射的编辑，那么 **“设置下一语句”** 将失败。 例如，如果你编辑了 catch 块中的代码，将发生这种情况。 发生这种情况时，你将看到一条错误消息，告诉你该操作不受支持。  
> 
> [!NOTE]
> 在托管代码中，在以下情况下不能移动下一条语句：  
> 
> - 下一条语句与当前语句不在同一个方法中。  
>   - 使用实时调试启动调试。  
>   - 正在展开一个调用堆栈。  
>   - 已引发一个 System.StackOverflowException 或 System.Threading.ThreadAbortException 异常。  
  
 应用程序处于活动运行状态时不能设置下一条语句。 要设置下一语句，调试器必须处于中断模式。  
  
## <a name="step-into-non-user-code"></a>单步执行非用户代码  
 默认情况下，调试程序在调试时只会尝试显示您的应用程序代码，这由名为 *仅我的代码*的调试程序设置确定。  (请参阅 [仅我的代码](../debugger/just-my-code.md) 以了解其如何适用于不同的项目类型和语言以及如何自定义该行为 ) 。不过，有时在调试时，可能需要查看框架代码、第三方库代码或对操作系统的调用 (系统调用) 。  
  
 转到 "**工具**" "  /  **选项**  /  " "**调试**"，然后清除 "**启用仅我的代码**" 复选框，可以关闭仅我的代码。  
  
 禁用仅我的代码后，调试器可以单步执行非用户代码，而非用户代码将出现在调试器窗口中。  
  
> [!NOTE]
> 设备项目不支持“仅我的代码”。  
  
 **单步执行系统调用**  
  
 如果已加载系统代码的调试符号并且未启用仅我的代码，则可以单步执行系统调用，就像对任何其他调用一样。  
  
 若要访问 Microsoft 符号文件，请参阅在[指定符号 ( pdb) 和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)主题中的[使用符号服务器查找未在本地计算机上的符号文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md#BKMK_Use_symbol_servers_to_find_symbol_files_not_on_your_local_machine)。  
  
 在调试时加载特定系统组件的符号：  
  
1. 打开“模块”窗口（键盘： **Ctrl+Alt+U**）。  
  
2. 选择要加载符号的模块。  
  
     查看 **“符号状态”** 列可以了解哪些模块加载了符号。  
  
3. 在上下文菜单中选择 **“加载符号”** 。  
  
## <a name="step-into-properties-and-operators-in-managed-code"></a><a name="BKMK_Step_into_properties_and_operators_in_managed_code"></a> 单步执行托管代码中的属性和运算符  
 默认情况下，调试器将逐过程执行托管代码中的属性和运算符。 在多数情况下，这会提供较好的调试体验。 若要启用单步执行属性或运算符，请选择“调试” / “选项” 。 在 "**调试**  /  **常规**" 页上，清除 "**逐过程执行属性和运算符 (仅限托管) ** " 复选框
