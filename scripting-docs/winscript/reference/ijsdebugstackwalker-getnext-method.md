---
title: Метод IJsDebugStackWalker::GetNext | Документы Microsoft
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugStackWalker.GetNext
apilocation:
- jscript9diag.dll
ms.assetid: 0b124768-50d3-4a69-876c-1aa337839a4e
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 695bb6cecc2a27565dce21b4a965ad08d90d7be7
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/27/2017
ms.locfileid: "24728444"
---
# <a name="ijsdebugstackwalkergetnext-method"></a>Метод IJsDebugStackWalker::GetNext
Возвращает следующий кадр.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT GetNext(  
   IJsDebugFrame **ppFrame  
);  
```  
  
#### <a name="parameters"></a>Параметры  
 `ppFrame`  
 [out] Объект, представляющий кадра стека.  
  
## <a name="return-value"></a>Возвращаемое значение  
  
## <a name="remarks"></a>Примечания  
 Возвращает E_JsDEBUG_OUTSIDE_OF_VM, если отсутствуют дополнительные кадры стека для перечисления  
  
## <a name="requirements"></a>Требования  
 **Заголовок:** jscript9diag.h  
  
## <a name="see-also"></a>См. также  
 [Интерфейс IJsDebugStackWalker](../../winscript/reference/ijsdebugstackwalker-interface.md)