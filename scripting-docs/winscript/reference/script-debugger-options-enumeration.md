---
title: Перечисление SCRIPT_DEBUGGER_OPTIONS | Документы Microsoft
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SCRIPT_DEBUGGER_OPTIONS Enumeration
ms.assetid: aef41ec0-6f65-48e8-a69e-44b4e4fb929f
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 54b910562670104f0fb5679f2b09780afcd17751
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/27/2017
ms.locfileid: "24734094"
---
# <a name="scriptdebuggeroptions-enumeration"></a>Перечисление SCRIPT_DEBUGGER_OPTIONS
Указывает набор параметров и (или) возможности, которые применяются к подключенному отладчику. Используется в [IDebugApplicationNode100::GetExcludedDocuments](../../winscript/reference/idebugapplicationnode100-getexcludeddocuments.md) и [IDebugApplicationNode100::SetFilterForEventSink](../../winscript/reference/idebugapplicationnode100-setfilterforeventsink.md)  
  
> [!IMPORTANT]
>  Эти константы реализованы в PDM v10.0 и более. Обнаружено в activdbg100.h.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
typedef SCRIPT_DEBUGGER_OPTIONS  
```  
  
## <a name="members"></a>Члены  
  
|Член|Значение|Описание|  
|------------|-----------|-----------------|  
|SDO_NONE|0x00000000|Параметры не заданы.|  
|SDO_ENABLE_FIRST_CHANCE_EXCEPTIONS|0x00000001|Указывает, что время выполнения скрипта, должны создавать события BREAKREASON_ERROR при возникновении исключения. Этот параметр может необходимо присвоить отладчиком, или код пользователя через `Debug.enableFirstChanceExceptions(<true&#124;false>)`.|  
|SDO_ENABLE_WEB_WORKER_SUPPORT|0x00000002|Указывает, что присоединенному отладчику поддерживает веб-процессов.|  
  
## <a name="see-also"></a>См. также  
 [Константы, перечисления и структуры отладчика активных скриптов](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)