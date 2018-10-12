---
title: 如何： 分配存储的过程以便执行更新、 插入和删除操作 （O-R 设计器） |Microsoft Docs
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e88224ab-ff61-4a3a-b6b8-6f3694546cac
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 802627f59f54b9a4b1179ba5c643b4671f4f7ce0
ms.sourcegitcommit: 71218ffc33da325cc1b886f69ff2ca50d44f5f33
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2018
ms.locfileid: "48878948"
---
# <a name="how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-or-designer"></a>如何： 分配存储的过程以便执行更新、 插入和删除操作 （O/R 设计器）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题的最新版本，请参阅[如何： 分配存储的过程以便执行更新、 插入和删除操作 （O-R 设计器）](https://docs.microsoft.com/visualstudio/data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer)。  
  
  
可以将存储过程添加到 O/R 设计器并作为典型的 <xref:System.Data.Linq.DataContext> 方法执行。 将更改从实体类保存到数据库时（例如在调用 [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] 方法时），还可以使用存储过程重写执行插入、更新和删除操作的默认 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 运行时行为。  
  
> [!NOTE]
>  如果存储过程的返回值需要发送回客户端（例如在存储过程中计算出的值），则在存储过程中创建输出参数。 如果无法使用输出参数，则编写分部方法实现，而不是依靠 O/R 设计器生成的重写。 在成功完成 INSERT 或 UPDATE 操作后，需要将映射到数据库生成的值的成员设置为相应的值。 有关详细信息，请参阅[开发人员在重写默认行为的职责](http://msdn.microsoft.com/library/c6909ddd-e053-46a8-980c-0e12a9797be1)。  
  
> [!NOTE]
>  [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] 会自动为标识（自动递增）列、rowguidcol（数据库生成的 GUID）列和时间戳列处理数据库生成的值。 在其他列类型中，数据库生成的值将意外导致 Null 值。 若要返回数据库生成的值，应手动将 <xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A> 设置为 `true` 并将 <xref:System.Data.Linq.Mapping.ColumnAttribute.AutoSync%2A> 设置为下列值之一：<xref:System.Data.Linq.Mapping.AutoSync>、<xref:System.Data.Linq.Mapping.AutoSync> 或 <xref:System.Data.Linq.Mapping.AutoSync>。  
  
## <a name="configuring-the-update-behavior-of-an-entity-class"></a>配置实体类的更新行为  
 默认情况下，在使用对 [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] 实体类中的数据所做的更改来更新数据库（插入、更新和删除）时，更新逻辑是由 [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] 运行时提供的。 在运行时创建默认的基于表 （列和主键信息） 的架构的 Insert、 Update 和 Delete 命令。 当不需要默认行为时，可以通过分配特定的存储过程，以执行操作表中数据所必需的插入、更新和删除来配置更新行为。 在不生成默认行为时（例如，实体类映射到视图时），也可以这样做。 最后，在数据库要求通过存储过程访问表时，您可以重写默认的更新行为。  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
#### <a name="to-assign-stored-procedures-to-override-the-default-behavior-of-an-entity-class"></a>指定存储过程以重写实体类的默认行为  
  
1.  打开**LINQ to SQL**在设计器中的文件。 (双击.dbml 文件中的**解决方案资源管理器**。)  
  
2.  在中**服务器资源管理器**/**数据库资源管理器**，展开**存储过程**并找到想要用于插入、 更新、 存储的过程和/或删除的实体类的命令。  
  
3.  将该存储过程拖到 O/R 设计器上。  
  
     该存储过程将作为 <xref:System.Data.Linq.DataContext> 方法添加到方法窗格中。 有关详细信息，请参阅[DataContext 方法 （O/R 设计器）](../data-tools/datacontext-methods-o-r-designer.md)。  
  
4.  选择要使用存储过程对其执行更新的实体类。  
  
5.  在中**属性**窗口中，选择要重写的命令 (**插入**，**更新**，或者**删除**)。  
  
6.  单击旁边的省略号 （...）**使用运行时**以打开**配置行为**对话框。  
  
7.  选择**自定义**。  
  
8.  选择所需的存储的过程中**自定义**列表。  
  
9. 检查的列表**方法自变量**并**类属性**若要验证**方法自变量**映射到相应**类属性**. 映射原始方法自变量 (Original_*ArgumentName*) 到原始属性 (*PropertyName* （原始）) 的 Update 和 Delete 命令。  
  
    > [!NOTE]
    >  默认情况下，名称匹配时方法自变量映射到类属性。 如果更改的属性名称在表和实体类之间不再匹配，而设计器无法确定正确的映射，您可能需要选择等效的类属性进行映射。  
  
10. 单击**确定**或**应用**。  
  
    > [!NOTE]
    >  你可以继续配置，只要你单击每个类/行为组合的行为**应用**每次更改后。 如果您更改的类或行为之前单击**应用**、 提供商机应用任何更改将出现一个警告对话框。  
  
     若要恢复为使用默认运行时逻辑进行更新，请单击 Insert、 Update、 旁边的省略号或 Delete 中的命令**属性**窗口，然后选择**使用运行时**中**配置行为**对话框。  
  
## <a name="see-also"></a>请参阅  
 [LINQ to SQL 工具在 Visual Studio 中](../data-tools/linq-to-sql-tools-in-visual-studio2.md)   
 [DataContext 方法 （O/R 设计器）](../data-tools/datacontext-methods-o-r-designer.md)   
 [演练： 创建 LINQ to SQL 类 （O-R 设计器）](http://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233)   
 [演练： 为 Northwind Customers 表创建更新存储过程](../data-tools/walkthrough-creating-update-stored-procedures-for-the-northwind-customers-table.md)   
 [LINQ to SQL](http://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)   
 [插入、更新和删除操作](http://msdn.microsoft.com/library/26a43a4f-83c9-4732-806d-bb23aad0ff6b)
