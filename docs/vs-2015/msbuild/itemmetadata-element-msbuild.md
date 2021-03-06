---
title: ItemMetadata 元素 (MSBuild) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- ItemMetadata Element [MSBuild]
- <ItemMetadata> Element [MSBuild]
ms.assetid: e3db5122-202d-43a9-b2f4-3e0ec4ed3d08
caps.latest.revision: 20
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8e3d9f72abfd095288b50ab8de9b9bc3eae4cc51
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68162374"
---
# <a name="itemmetadata-element-msbuild"></a>ItemMetadata 元素 (MSBuild)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

包含用户定义的项元数据键，其中包含项元数据值。 一个项可能具有任意数量的元数据键值对。  
  
 \<Project>  
 \<ItemGroup>  
 \<Item>  
  
## <a name="syntax"></a>语法  
  
```  
<ItemMetadataName> Item Metadata value</ItemMetadataName>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|说明|  
|---------------|-----------------|  
|`Condition`|可选特性。<br /><br /> 要计算的条件。 有关详细信息，请参阅[条件](../msbuild/msbuild-conditions.md)。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|说明|  
|-------------|-----------------|  
|[Item](../msbuild/item-element-msbuild.md)|为生成过程定义输入的用户定义元素。|  
  
## <a name="text-value"></a>文本值  
 文本值是可选的。  
  
 此文本指定项元数据值可以是文本，也可以是 XML。  
  
## <a name="remarks"></a>备注  
  
## <a name="example"></a>示例  
 下面的代码示例演示如何将具有值 `fr` 的 `Culture` 元数据添加到项 `CSFile`。  
  
```  
<ItemGroup>  
    <CSFile Include="main.cs" >  
        <Culture>fr</Culture>  
    </CSFile>  
</ItemGroup>  
```  
  
## <a name="see-also"></a>另请参阅  
 [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)   
 [项](../msbuild/msbuild-items.md)
