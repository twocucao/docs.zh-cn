---
title: CallFunctionShim 函数
ms.date: 03/30/2017
api_name:
- CallFunctionShim
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- CallFunctionShim
helpviewer_keywords:
- CallfunctionShim function [.NET Framework hosting]
ms.assetid: 37118465-ddf3-41f0-bf27-335b72777e63
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3dfe2c98fd5898a0ad5a1d4fd9e89c7f20741bb0
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2019
ms.locfileid: "66490693"
---
# <a name="callfunctionshim-function"></a>CallFunctionShim 函数
将指定的库中具有指定的名称和参数的函数调用。  
  
 .NET Framework 4 中已弃用此函数。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT CallFunctionShim (  
    [in] LPCWSTR     szDllName,  
    [in] LPCSTR      szFunctionName,  
    [in] LPVOID      lpvArgument1,  
    [in] LPVOID      lpvArgument2,  
    [in] LPCWSTR     szVersion,  
    [in] LPVOID      pvReserved  
);  
```  
  
## <a name="parameters"></a>参数  
 `szDllName`  
 [in]包含该函数的库的名称。  
  
 `szFunctionName`  
 [in]函数的名称。  
  
 `lpvArgument1`  
 [in]要传递给函数的第一个参数。  
  
 `lpvArgument2`  
 [in]要传递给函数的第二个参数。  
  
 `szVersion`  
 [in]包含该函数的库的版本。  
  
 `pvReserved`  
 [in]保留供将来使用。 此参数中传递零。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** MSCorEE.h  
  
 **库：** MSCorEE.dll  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅

- [弃用的 CLR 承载函数](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
