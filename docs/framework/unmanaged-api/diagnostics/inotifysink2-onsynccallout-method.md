---
title: INotifySink2::OnSyncCallOut 方法
ms.date: 03/30/2017
api_name:
- INotifySink2.OnSyncCallOut
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- INotifySink2::OnSyncCallOut
helpviewer_keywords:
- INotifySink2::OnSyncCallOut method [.NET Framework debugging]
- OnSyncCallOut method [.NET Framework debugging]
ms.assetid: 97f15656-8677-4079-8553-a1d8603355d6
topic_type:
- apiref
ms.openlocfilehash: ce0e192a9d7d5abf56a55f844cf886c386f1c563
ms.sourcegitcommit: 7b1497c1927cb449cefd313bc5126ae37df30746
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2020
ms.locfileid: "83441989"
---
# <a name="inotifysink2onsynccallout-method"></a>INotifySink2::OnSyncCallOut 方法
在调用时调用。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT OnSyncCallOut  
(  
    [in]  CALL_ID  in_CallID,  
    [out, size_is(, *out_pBufferSize)] BYTE**  out_ppBuffer,  
    [out] DWORD*   out_pBufferSize  
);  
```  
  
## <a name="parameters"></a>参数  
 `in_CallID`  
 中传出的调用的 ID。请参阅[CALL_ID 结构](call-id-structure.md)。  
  
 `out_ppBuffer`  
 弄调用缓冲区。  
  
 `out_pBufferSize`  
 弄调用缓冲区的大小（以字节为单位）。  
  
## <a name="return-value"></a>返回值  
 如果方法成功，则 S_OK。  
  
## <a name="requirements"></a>要求  
 **标头：** ProtocolNotify2 .idl  
  
## <a name="see-also"></a>另请参阅

- [INotifySink2 接口](inotifysink2-interface.md)
- [INotifySource2 接口](inotifysource2-interface.md)
- [INotifyConnection2 接口](inotifyconnection2-interface.md)
