---
title: 泳道属性
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.dsltools.dsldesigner.swimlane
helpviewer_keywords:
- Domain-Specific Language, swimlane
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0cceeacab44f17eb30184c90f1128b8d2c3528bb
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76115365"
---
# <a name="properties-of-swimlanes"></a>泳道属性
可以向关系图中添加泳道。 泳道将关系图划分为垂直或水平区域。 您可以定义要在泳道内显示的其他形状。 有关详细信息，请参阅[如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)。 有关如何使用这些属性的详细信息，请参阅[自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

 泳道具有下表中列出的属性。

|Property|描述|默认值|
|-|-|-|
|正文填充颜色|泳道主体的填充颜色。|白色|
|标题填充颜色|泳道标头的填充颜色。|深灰色|
|分隔符颜色|分隔符线的颜色。|LightGray|
|分隔符线样式|分隔线的样式（`Solid`、`Dash`、`Dot`、`DashDot`、`DashDotDot`或 `Custom`）。|`Dash`|
|分隔符粗细|分隔线的粗细（英寸）。|0.03125|
|文本颜色|与此泳道关联的文本修饰器所使用的颜色。|Black|
|访问修饰符|类的访问级别（`public` 或 `internal`）。|公用|
|自定义特性|用于将特性添加到从此泳道生成的代码类。|\<none>|
|生成双派生|如果 `True`，则将生成基类和分部类（以支持通过重写进行自定义）。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|False|
|具有自定义构造函数|如果 `True`，将在源代码中提供自定义构造函数。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|False|
|继承修饰符|描述从泳道（`none`、`abstract` 或 `sealed`）生成的源代码类的继承类型。|无|
|基本泳道|此泳道的基类。|(无)|
|Name|此泳道的名称。|当前名称|
|命名空间|与此泳道关联的命名空间。|当前命名空间|
|Tooltip 类型|如何定义工具提示（`fixed`、`variable`或 `none`）。 如果 `fixed`，则使用 `Fixed Tooltip Text` 属性的值;如果 `variable`，则在自定义代码中定义工具提示。|\<none>|
|注释|与此泳道关联的非正式注释。|\<none>|
|对齐|水平或垂直对齐。|垂直|
|初始高度|此泳道的初始高度（英寸）。 仅适用于水平泳道。|0|
|初始宽度|此泳道的初始宽度（英寸）。 仅适用于垂直泳道。|0|
|公开文本颜色|如果 `True`，则用户可以在生成的设计器中设置泳道的颜色。 若要设置此项，请右键单击泳道形状，然后单击 "添加" "**公开**"。|False|
|描述|用于记录生成的设计器。|\<none>|
|显示名称|将在生成的设计器中显示以便引用此泳道类的名称。|\<none>|
|固定工具提示文本|用于固定工具提示的文本。|\<none>|
|帮助关键字|用于索引此泳道的 F1 帮助的关键字。|\<none>|

## <a name="see-also"></a>另请参阅

- [域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
