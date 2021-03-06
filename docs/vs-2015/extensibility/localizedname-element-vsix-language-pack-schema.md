---
title: " (VSIX 语言包架构) 的 LocalizedName 元素 |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
ms.assetid: 57b7f502-3b04-42d9-90d5-f57772a7c757
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 64d8430dbcf563ca232d1b8d850678925770219f
ms.sourcegitcommit: d9254e54079ae01cdf2d07b11f988faf688f80fc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/11/2020
ms.locfileid: "88114165"
---
# <a name="localizedname-element-vsix-language-pack-schema"></a>LocalizedName 元素（VSIX 语言包架构）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

必需。 要安装的扩展的本地化名称。  
  
## <a name="syntax"></a>语法  
  
```  
<Name>Localized name of the extension</Name>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|说明|  
|---------------|-----------------|  
|None||  
  
### <a name="child-elements"></a>子元素  
  
|元素|说明|  
|-------------|-----------------|  
|None||  
  
### <a name="parent-elements"></a>父元素  
  
|元素|说明|  
|-------------|-----------------|  
|[VSIX LanguagePack 元素](../extensibility/vsixlanguagepack-element-vsix-language-pack-schema.md)|必需。 提供 VSIX 语言包的根元素。|  
  
## <a name="text-value"></a>文本值  
 必需。 目标语言中的语言包的名称。  
  
## <a name="element-information"></a>元素信息  

:::row:::
    :::column:::
        命名空间
    :::column-end:::
    :::column:::
        `http://schemas.microsoft.com/developer/vsx-schema-lp/2010`
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        架构名称
    :::column-end:::
    :::column:::
        VSIX 语言包架构
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        验证文件
    :::column-end:::
    :::column:::
        VSIXLanguagePackSchema
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        可以为空
    :::column-end:::
    :::column:::
        不适用
    :::column-end:::
:::row-end:::
  
## <a name="see-also"></a>另请参阅  
 [VSX 语言包架构引用](../extensibility/vsx-language-pack-schema-reference.md)   
 [本地化 VSIX 包](../extensibility/localizing-vsix-packages.md)   
 [VSIX 扩展架构1.0 引用](/previous-versions/dd393700(v=vs.110))
