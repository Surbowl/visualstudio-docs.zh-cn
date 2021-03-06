---
title: 向 "数据源" 窗口添加自定义控件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
f1_keywords:
- vs.datasource.howtoaddcustomcontrol
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- Data Sources Window, adding controls
- controls [Visual Studio], adding to Data Sources Window
- DefaultBindingPropertyAttribute class, using
- LookupBindingPropertiesAttribute class, using
- ComplexBindingPropertiesAttribute class, using
- Data Sources Window, selecting controls
ms.assetid: 8c43e7d2-ba94-4d9b-96de-3aa971955afd
caps.latest.revision: 45
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 402e62602d99492730d3094965e76964cd5f8218
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72673084"
---
# <a name="add-custom-controls-to-the-data-sources-window"></a>向“数据源”窗口添加自定义控件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

将项从 "**数据源**" 窗口拖到设计图面以创建数据绑定控件时，可以选择您创建的控件类型。 窗口中的每个项都有一个下拉列表，其中显示了您可以选择的控件。 与每个项关联的控件集由项的数据类型确定。 如果您要创建的控件未出现在列表中，则可以按照本主题中的说明将该控件添加到列表中。

 有关选择要为 "**数据源**" 窗口中的项创建的数据绑定控件的详细信息，请参阅[设置从 "数据源" 窗口中拖动时要创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。

> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你的当前设置或版本。 若要更改设置，请在 "**工具**" 菜单上选择 "**导入和导出设置**"。 有关详细信息，请参阅[在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。

## <a name="customizinglist"></a>自定义数据类型的可绑定控件列表
 若要从 "**数据源**" 窗口中具有特定数据类型的项的可用控件列表中添加或删除控件，请执行以下步骤。

#### <a name="to-select-the-controls-to-be-listed-for-a-data-type"></a>选择要为数据类型列出的控件

1. 确保 WPF 设计器或 Windows 窗体设计器处于打开状态。

2. 在 "**数据源**" 窗口中，单击作为添加到窗口的数据源的一部分的项，然后单击该项的下拉菜单。

3. 在下拉菜单中，单击 "**自定义**"。 此时将打开下列对话框之一：

    - 如果 Windows 窗体设计器处于打开状态，则会打开 "**选项**" 对话框的 "**数据 UI 自定义**" 页。

    - 如果 WPF 设计器处于打开状态，则 "**自定义控件绑定**" 对话框将打开。

4. 在对话框中，从 "**数据类型**" 下拉列表中选择一种数据类型。

    - 若要自定义表或对象的控件列表，请选择 "**列表**"。

    - 若要为表的列或对象的属性自定义控件列表，请选择基础数据存储区中的列或属性的数据类型。

    - 若要自定义控件列表以显示具有用户定义的形状的数据对象，请选择 " **[其他]** "。 例如，如果您的应用程序具有可显示特定对象的多个属性的数据的自定义控件，则选择 " **[其他]** "。

5. 在 "**关联的控件**" 框中，选择要用于所选数据类型的每个控件，或取消选择要从列表中删除的任何控件。

    > [!NOTE]
    > 如果要选择的控件未出现在 "**关联的控件**" 框中，则必须将该控件添加到该列表中。 有关详细信息，请参阅[将控件添加到数据类型的关联控件列表](#addingcontrols)。

6. 单击“确定”。

7. 在 "**数据源**" 窗口中，单击与一个或多个控件关联的数据类型的项，然后单击该项的下拉菜单。

     此时，在 "关联的**控件**" 框中选择的控件将显示在该项的下拉菜单中。

## <a name="addingcontrols"></a>Addcontrols 到数据类型的关联控件列表
 如果要将控件与数据类型相关联，但控件未出现在 "**关联的控件**" 框中，则必须将该控件添加到列表中。 控件必须位于当前解决方案或引用的程序集中。 它还必须在**工具箱**中提供，并且具有指定控件的数据绑定行为的特性。

#### <a name="to-add-controls-to-the-list-of-associated-controls"></a>向关联控件列表添加控件

1. 右键单击**工具箱**并选择 "**选择项**"，将所需的控件添加到 "**工具箱**"。

     控件必须具有下列属性之一。

    |特性|描述|
    |---------------|-----------------|
    |<xref:System.ComponentModel.DefaultBindingPropertyAttribute>|在显示数据的单个列（或属性）的简单控件（如 <xref:System.Windows.Forms.TextBox>）上实现此特性。|
    |<xref:System.ComponentModel.ComplexBindingPropertiesAttribute>|在显示数据列表（或表）的控件上实现此特性，如 <xref:System.Windows.Forms.DataGridView>。|
    |<xref:System.ComponentModel.LookupBindingPropertiesAttribute>|在显示数据列表（或表）的控件上实现此属性，但也需要显示单个列或属性，例如 <xref:System.Windows.Forms.ComboBox>。|

2. 对于 Windows 窗体，请在 "**选项**" 对话框中打开 "**数据 UI 自定义**" 页。 或者，对于 WPF，打开 "**自定义控件绑定**" 对话框。 有关详细信息，请参阅[自定义数据类型的可绑定控件列表](#customizinglist)。

3. 在 "**关联的控件**" 框中，刚刚添加到 "**工具箱**" 中的控件现在应显示。

    > [!NOTE]
    > 只有位于当前解决方案或被引用程序集中的控件才能添加到关联控件列表中。 （这些控件还必须实现上一个表中的数据绑定特性之一。）若要将数据绑定到 "**数据源**" 窗口中不可用的自定义控件，请将该控件从 "**工具箱**" 拖动到设计图面上，然后从 "**数据源**" 窗口拖动该项到控件。

## <a name="see-also"></a>请参阅
 [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
