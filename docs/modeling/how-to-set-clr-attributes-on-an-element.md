---
title: 如何：在元素上设置 CLR 特性
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.dsltools.EditAttributesDialog
helpviewer_keywords:
- Domain-Specific Language, custom attrributes
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ebda963bf1afa55fa8d7f98774c72a75d242ceef
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85532452"
---
# <a name="how-to-set-clr-attributes-on-an-element"></a>如何：在元素上设置 CLR 特性
自定义属性是可以添加到域元素、形状、连接符和关系图中的特殊属性。 可以添加从类继承的任何属性 `System.Attribute` 。

### <a name="to-add-a-custom-attribute"></a>添加自定义属性

1. 在 " **DSL 资源管理器**" 中，选择要向其添加自定义属性的元素。

2. 在 "**属性**" 窗口中，在 "**自定义属性**" 属性旁边，单击 "浏览（**...**）" 图标。

     此时将打开 "**编辑属性**" 对话框。

3. 在 "**名称**" 列中，单击 **\<add attribute>** 并键入属性的名称。 按 Enter。

4. 属性名称下面的行显示括号。 在此行上，键入属性的参数类型（例如 `string` ），然后按 enter。

5. 在 "**名称属性**" 列中，键入适当的名称，例如 `MyString` 。

6. 单击 **“确定”** 。

     "**自定义属性**" 属性现在按以下格式显示属性：

     `[`*AttributeName* `(`*ParameterName* `=`*类型*`)]`

## <a name="see-also"></a>请参阅

- [域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)