---
title: Função IsFrameworkAssembly
ms.date: 03/30/2017
api_name:
- IsFrameworkAssembly
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IsFrameworkAssembly
helpviewer_keywords:
- IsFrameworkAssembly function [.NET Framework fusion]
ms.assetid: b0c6f19b-d4fd-4971-88f0-12ffb5793da3
topic_type:
- apiref
ms.openlocfilehash: e30b6f2d2254d2d107c4c82a2c5664850ce6ec23
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2019
ms.locfileid: "73123065"
---
# <a name="isframeworkassembly-function"></a>Função IsFrameworkAssembly
Obtém um valor que indica se o assembly especificado é gerenciado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT IsFrameworkAssembly (  
    [in]  LPCWSTR pwzAssemblyReference,  
    [out] LPBOOL  pbIsFrameworkAssembly,  
    [in]  LPWSTR  pwzFrameworkAssemblyIdentity,  
    [in]  LPDWORD pccSize  
 );  
```  
  
## <a name="parameters"></a>Parâmetros  
 `pwzAssemblyReference`  
 no O nome do assembly a ser verificado.  
  
 `pbIsFrameworkAssembly`  
 fora Um valor booliano que indica se o assembly é gerenciado.  
  
 `pwzFrameworkAssemblyIdentity`  
 no Uma cadeia de caracteres não canônica que contém a identidade exclusiva do assembly.  
  
 `pccSize`  
 [in] O tamanho do `pwzFrameworkAssemblyIdentity`.  
  
## <a name="remarks"></a>Comentários  
 O parâmetro `pwzAssemblyReference` é um ponteiro para uma cadeia de caracteres que contém o nome de um assembly.  
  
 Se esse assembly fizer parte do .NET Framework, o parâmetro `pbIsFrameworkAssembly` conterá um valor booliano de `true`.  
  
 Se o assembly nomeado não fizer parte do .NET Framework, ou se o parâmetro `pwzAssemblyReference` não nomear um assembly, `pbIsFrameworkAssembly` conterá um valor booliano de `false`.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
## <a name="see-also"></a>Consulte também

- [Funções estáticas globais de fusão](fusion-global-static-functions.md)
