---
title: GetRequestedRuntimeVersion 函数
ms.date: 03/30/2017
api_name:
- GetRequestedRuntimeVersion
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- GetRequestedRuntimeVersion
helpviewer_keywords:
- GetRequestedRuntimeVersion function [.NET Framework hosting]
ms.assetid: 82f596a4-483d-4509-b0c5-a84c53c3da1b
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: cbc77195c3fe2581475d768b59993de274ac06a6
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2019
ms.locfileid: "66490328"
---
# <a name="getrequestedruntimeversion-function"></a>GetRequestedRuntimeVersion 函数
获取公共语言运行时 (CLR) 请求指定的应用程序的版本号。 如果未安装该版本，获取所请求的版本之前已安装的最新版本。  
  
 .NET Framework 4 中已弃用此函数。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT GetRequestedRuntimeVersion (  
    [in]  LPWSTR  pExe,   
    [out] LPWSTR  pVersion,   
    [in]  DWORD   cchBuffer,   
    [out] DWORD  *pdwLength  
);  
```  
  
## <a name="parameters"></a>参数  
 `pExe`  
 [in]应用程序的名称。  
  
 `pVersion`  
 [out]包含成功完成后的版本字符串的缓冲区。  
  
 `cchBuffer`  
 [in]版本缓冲区的长度。  
  
 `pdwLength`  
 [out]指向的版本号字符串长度的指针。  
  
## <a name="return-value"></a>返回值  
 此方法返回标准的组件对象模型 (COM) 错误代码，定义在 WinError.h，除了以下值。  
  
|返回代码|描述|  
|-----------------|-----------------|  
|S_OK|该方法已成功完成。|  
|ERROR_INSUFFICIENT_BUFFER|版本缓冲区不足够空间来存储的版本字符串。|  
|E_POINTER|`pdwLength` 为 null。|  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** MSCorEE.h  
  
 **库：** MSCorEE.dll  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v11plus](../../../../includes/net-current-v11plus-md.md)]  
  
## <a name="see-also"></a>请参阅

- [GetRequestedRuntimeInfo 函数](../../../../docs/framework/unmanaged-api/hosting/getrequestedruntimeinfo-function.md)
- [GetVersionFromProcess 函数](../../../../docs/framework/unmanaged-api/hosting/getversionfromprocess-function.md)
- [弃用的 CLR 承载函数](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
