---
title: ClrCreateManagedInstance 函数
ms.date: 03/30/2017
api_name:
- ClrCreateManagedInstance
api_location:
- mscoree.dll
- clr.dll
- mscorwks.dll
- mscoreei.dll
- mscorsvr.dll
api_type:
- DLLExport
f1_keywords:
- ClrCreateManagedInstance
helpviewer_keywords:
- ClrCreateManagedInstance function [.NET Framework hosting]
ms.assetid: 58ba42c0-4857-43bf-a039-73a4dc6544c2
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 67bd6e8a0519d35b867cb525d5ff7730c0459016
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2019
ms.locfileid: "66490683"
---
# <a name="clrcreatemanagedinstance-function"></a>ClrCreateManagedInstance 函数
创建指定的托管类型的实例。  
  
 .NET Framework 4 中已弃用此函数。 使用 COM 激活来创建的托管类型的实例或使用托管 (请参阅[CLR 承载接口中添加.NET Framework 4 和 4.5](../../../../docs/framework/unmanaged-api/hosting/clr-hosting-interfaces-added-in-the-net-framework-4-and-4-5.md))。  
  
## <a name="syntax"></a>语法  
  
```  
STDAPI ClrCreateManagedInstance (  
    [in]  LPCWSTR  pTypeName,   
    [in]  REFIID   riid,   
    [out] void     **ppObject  
);  
```  
  
## <a name="parameters"></a>参数  
 `pTypeName`  
 [in]指向所请求的实例类型的名称的指针。  
  
 `riid`  
 [in]`IID`的所请求的实例类型。  
  
 `ppObject`  
 [out]指向由调用方请求的托管类型的实例的指针指向的指针。  
  
## <a name="remarks"></a>备注  
 公共语言运行时应该已经加载到进程。 例如，它可以通过调用由加载[CorBindToRuntimeEx](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md)函数之前`ClrCreateManagedInstance`调用函数。 如果未加载运行时，`ClrCreateManagedInstance`首次尝试加载 v1.0.3705 的运行时。 如果失败，它尝试加载运行时的最新版本。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** MSCorEE.h  
  
 **库：** MSCorEE.dll  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅

- [弃用的 CLR 承载函数](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
- [承载](../../../../docs/framework/unmanaged-api/hosting/index.md)
