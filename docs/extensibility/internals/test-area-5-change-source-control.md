---
title: 测试区域 5：更改源代码管理 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], changing
- source control plug-ins, changing source control
ms.assetid: fdf09e00-108c-4d51-bbd5-72452d52a490
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d1c0df31fbecd532e6a5f7f317730cd995cd8225
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704526"
---
# <a name="test-area-5-change-source-control"></a>测试区域 5：更改源代码管理
此源代码管理插件测试区域包括通过**更改源代码管理**命令更改源代码管理。

 **更改源代码管理**命令为用户提供了四个基本功能：

- **绑定：**

   允许用户在解决方案/项目和版本存储之间建立或重新建立源代码管理链接。

- **取消绑定：**

   根据每个连接从源代码管理中删除项目/解决方案。

- **连接/断开连接：**

  切换受控解决方案的连接或脱机状态，区域 3 中涵盖该状态。 有关详细信息，请参阅[测试区域 3：签出/撤消签出](../../extensibility/internals/test-area-3-check-out-undo-checkout.md)。

## <a name="command-menu-access"></a>命令菜单访问
 测试用例[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]中使用了以下集成开发环境菜单路径。

 更改源代码管理：**文件**，**源代码管理**，**更改源代码管理**。

## <a name="test-cases"></a>测试用例
 以下是**更改源代码管理**命令测试区域的特定测试用例。

### <a name="case-5a-bind"></a>案例 5a：绑定
 绑定允许用户向选定的项目和解决方案添加源代码控制信息。 通常提示用户标识要向其添加这些项的源代码管理中的项目。 用户不得在源代码管理中创建新项目作为此操作的一部分（与添加到源代码管理对比）。

| 操作 | 测试步骤 | 要验证的预期结果 |
| - | - | - |
| 绑定到空位置 | 1. 创建项目。<br />2. 将解决方案添加到源代码管理。<br />3. 开放**更改源代码管理**对话框（**文件**、**源代码管理**、**更改源代码管理**）。<br />4. 单击 **"取消绑定**"。<br />5. 如果出现警告对话框，则接受该对话框。<br />6. 选择所有项目。<br />7. 单击**绑定**。<br />8. 浏览到源代码管理存储中的空位置。<br />9. 单击 **"确定"** 关闭 **"更改源控制"** 对话框。<br />10. 在确认对话框中单击"**继续使用这些绑定**"。<br />11. 如果出现警告对话框中的 **"确定"，** 请单击"确定"。<br />12. 检查所有内容。 如果此步骤成功，请继续执行下一步。<br />13. 从源代码管理到新位置的开放解决方案。 | `Result from Step 12:`<br /><br /> 解决方案和项目绑定到版本存储中的新目标并写入。<br /><br /> 已签入解决方案和项目文件。<br /><br /> 版本存储项目层次结构与磁盘上项目的文件夹层次结构匹配。<br /><br /> `Result from Step 13:`<br /><br /> 下载所有项目项。 |
| 绑定到与客户端同步的位置 | 1. 创建项目。<br />2. 将解决方案添加到源代码管理。<br />3. 在版本存储中创建解决方案和项目的重复项（如果使用则[!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)]共享和分支）。<br />4. 开放**更改源代码管理**对话框（**文件**、**源代码管理**、**更改源代码管理**）。<br />5. 取消绑定所有。<br />6. 单击"**确定"** 关闭 **"更改源控制"** 对话框。<br />7. 重新打开**更改源控制**对话框。<br />8. 选择全部。<br />9. 单击**绑定**。<br />10. 浏览到解决方案和项目的分支位置（从步骤 3 开始）<br />11. 单击 **"确定"** 以关闭 **"更改源控制"** 对话框。<br />12. 对所有项目获取最新递归。 | 获取后的文件内容与获取之前的内容相同。 |
| 绑定到与客户端不同步的位置 | 1. 创建项目。<br />2. 将解决方案添加到源代码管理。<br />3. 在版本存储中创建解决方案和项目的重复项（如果使用则[!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)]共享和分支）。<br />4. 修改版本存储中的分支项目中的文件。<br />5. 开放**更改源代码管理**对话框（**文件**、**源代码管理**、**更改源代码管理**）。<br />6. 取消绑定所有。<br />7. 单击"**确定"** 关闭 **"更改源控制"** 对话框。<br />8. 重新打开**更改源控制**对话框。<br />9. 选择全部。<br />10. 单击**绑定**。<br />11. 浏览到分支位置，用于解决方案和项目。<br />12. 单击 **"确定"** 以关闭 **"更改源控制"** 对话框。<br />13. 如果出现警告对话框，则接受警告对话框。<br />14. 获取所有项目的最新递归。 | 步骤 4 中修改的文件也会在本地修改。 |
| 从未受源代码控制的解决方案绑定 | 1. 在源代码管理中创建一个空文件夹。<br />2. 创建客户端项目。<br />3. 开放**更改源代码管理**对话框（**文件**、**源代码管理**、**更改源代码管理**）。<br />4. 将解决方案绑定到源代码管理中的空位置。<br />5. 单击"**确定"** 关闭 **"更改源控制"** 对话框。<br />6. 在确认对话框中单击"**继续使用这些绑定**"。<br />7. 如果出现警告对话框中的 **"确定"，** 请单击"确定"。 | 解决方案将添加到源代码管理中。<br /><br /> 解决方案和项目已签出。 |
| 取消绑定 | 1. 创建项目。<br />2. 将解决方案添加到源代码管理。<br />3. 打开"更改源控制"对话框。<br />4. 取消绑定所有。<br />5. 单击 **"确定"** 按钮关闭对话框。 如果此步骤成功，请继续执行下一步。<br />6. 重新打开 **"更改源控制"** 对话框。<br />7. 绑定到不相关的位置。<br />8. 单击 **"取消**"。 | `Result from Step 5:`<br /><br /> 解决方案不再受源代码控制<br /><br /> `Result from Step 8:`<br /><br /> 解决方案仍不受源代码管理。 |

### <a name="case-5b-unbind"></a>案例 5b：取消绑定
 取消绑定会从项目及其解决方案中删除源代码控制信息。 受影响的项目和解决方案基于用户选择的组合以及项目如何添加到源代码管理。

|操作|测试步骤|要验证的预期结果|
|------------|----------------|--------------------------------|
|取消绑定解决方案，其中包含一个文件系统或本地 IIS Web 项目和一个客户端项目|1. 创建文件系统或本地 IIS Web 项目。<br />2. 将解决方案添加到源代码管理。<br />3. 向解决方案添加新的客户端项目。<br />4. 如果出现提示，则接受签出解决方案。<br />5. 打开 **"更改源控制"** 对话框。<br />6. 单击 **"取消绑定**"。<br />7. 单击 **"确定"** 关闭对话框。<br />8. 尝试签出解决方案、项目、解决方案项和项目项。|解决方案和项目不受源代码管理。<br /><br /> 源控制菜单命令不显示。|
|取消绑定|1. 创建项目。<br />2. 将解决方案添加到源代码管理。<br />3. 打开 **"更改源控制"** 对话框。<br />4. 单击 **"取消绑定所有**"。<br />5. 单击 **"取消**"。|解决方案在源代码管理之下。|

### <a name="case-5c-rebind"></a>案例 5c：重新绑定
 重新绑定只是取消绑定和绑定的组合 - 重新绑定以前处于源代码管理且未绑定的项目/解决方案的过程。

|操作|测试步骤|要验证的预期结果|
|------------|----------------|--------------------------------|
|在不关闭 **"更改源代码管理"** 对话框的情况下重新绑定解决方案和项目|1. 创建项目。<br />2. 将解决方案添加到源代码管理。<br />3. 打开 **"更改源控制"** 对话框。<br />4. 单击 **"取消绑定**"。<br />5. 选择所有行。<br />6. 单击**绑定**。<br />7. 单击"**确定"** 关闭 **"更改源控制"** 对话框。<br />8. 如果出现提示，则接受结帐。|解决方案和项目受源代码管理。|
|仅在不关闭 **"更改源控制"** 对话框的情况下重新绑定项目|1. 创建项目。<br />2. 仅使用（文件>源代码管理->将选定项目添加到源代码管理）中的项目。<br />3. 打开"更改源控制"对话框。<br />4. 仅取消绑定项目。<br />5. 仅绑定项目。|解决方案不受控制。<br /><br /> 项目保持受控。|
|仅在不关闭**更改源代码管理**对话框的情况下重新绑定解决方案|1. 创建项目。<br />2. 仅使用 （**文件**、**源代码管理**、**将选定项目添加到源代码管理**） 将解决方案添加到源代码管理。<br />3. 打开 **"更改源控制"** 对话框。<br />4. 仅取消绑定解决方案（不要关闭**更改源控制**对话框）。<br />5. 仅绑定解决方案。<br />6. 单击 **"确定"** 关闭对话框。<br />7. 查看解决方案和解决方案项目（如果有）。|解决方案保持受控状态。<br /><br /> 项目不受控制。|
|仅在同一目录中重新绑定解决方案/项目|1. 创建项目。<br />2. 仅使用 （**文件**、**源代码管理**、**将选定项目添加到源代码管理**） 将项目添加到源代码管理。<br />3. 关闭解决方案。<br />4. 创建至少两个项目的新解决方案。<br />5. 将解决方案添加到源代码管理。<br />6. 从源代码管理添加步骤 1 中创建的项目。<br />7. 如果出现提示，则接受解决方案的结帐。<br />8. 检查整个解决方案。<br />9. 打开 **"更改源控制"** 对话框。<br />10. 选择添加的项目（从步骤 6 中），然后单击 **"取消绑定**"。<br />11. 单击 **"确定"** 关闭对话框。<br />12. 如果出现提示，请接受结帐。<br />13. 重新打开**更改源代码管理**对话框。<br />14. 选择添加的项目（从步骤 6 中），然后单击 **"绑定**"。<br />15. 选择原始位置。|解决方案和项目仍然受控制。|

## <a name="see-also"></a>请参阅
- [源代码管理插件的测试指南](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)
