---
title: IDebugEngine2::RemoveAllSetExceptions | Документы Microsoft
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugEngine2::RemoveAllSetExceptions
helpviewer_keywords:
- IDebugEngine2::RemoveAllSetExceptions
ms.assetid: 165fbe89-802d-4d99-85ca-c10fd6cccc09
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: e3446b910aa1e728319d0f4c7acdbf65b01d1cb4
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2018
ms.locfileid: "31106868"
---
# <a name="idebugengine2removeallsetexceptions"></a>IDebugEngine2::RemoveAllSetExceptions
Удаляет из списка исключений, заданные в Интегрированной среде разработки для конкретной архитектуры во время выполнения или языка.  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
HRESULT RemoveAllSetExceptions(   
   REFGUID guidType  
);  
```  
  
```csharp  
int RemoveAllSetExceptions(   
   ref Guid guidType  
);  
```  
  
#### <a name="parameters"></a>Параметры  
 `guidType`  
 [in] Идентификатор GUID для языка или идентификатор GUID для отладчик, соответствующий архитектуре во время выполнения.  
  
## <a name="return-value"></a>Возвращаемое значение  
 В случае успеха возвращает `S_OK`; в противном случае возвращается код ошибки.  
  
## <a name="remarks"></a>Примечания  
 Удалены этим методом исключения заданные предыдущих вызовов [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md) метод.  
  
 Чтобы удалить конкретное исключение, вызовите [RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md) метод.  
  
## <a name="see-also"></a>См. также  
 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)   
 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)   
 [RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md)