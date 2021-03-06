---
title: IDebugDocumentTextEvents2 | Документы Microsoft
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugDocumentTextEvents2
helpviewer_keywords:
- IDebugDocumentTextEvents2 interface
ms.assetid: a10cbb6b-11a8-4056-b42a-2ecebf0e690d
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 0f34bb09847659fdfc1dfcbd036aef2a47c8bd5b
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2018
ms.locfileid: "31107674"
---
# <a name="idebugdocumenttextevents2"></a>IDebugDocumentTextEvents2
Этот интерфейс используется для уведомления об изменениях в исходном документе, поставляемые модуль отладки Visual Studio.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
IDebugDocumentTextEvents2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Примечания для разработчиков  
 DE реализует этот интерфейс для поддержки внесения изменений в исходный код. Обычно этот интерфейс реализуется на тот же объект, реализующий [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) интерфейса.  
  
## <a name="notes-for-callers"></a>Примечания для вызывающих объектов  
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] Получает этого интерфейса через вызов <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint.Advise%2A> метод. <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint> Интерфейс получается из вызова <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer.EnumConnectionPoints%2A> метод. <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer> Интерфейс получается путем вызова метода [QueryInterface](/cpp/atl/queryinterface) метод [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) интерфейса.  
  
## <a name="methods-in-vtable-order"></a>Методы в порядке таблицы Vtable  
 В следующей таблице показаны методы `IDebugDocumentTextEvents2`.  
  
|Метод|Описание|  
|------------|-----------------|  
|[onDestroy](../../../extensibility/debugger/reference/idebugdocumenttextevents2-ondestroy.md)|Указывает, что весь документ был удален.|  
|[onInsertText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-oninserttext.md)|Уведомляет отладочный пакет вставки текста в документ.|  
|[onRemoveText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onremovetext.md)|Уведомляет отладочный пакет о том, что текст был удален из документа.|  
|[onReplaceText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onreplacetext.md)|Уведомляет отладочный пакет замены, текст в документе.|  
|[onUpdateTextAttributes](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onupdatetextattributes.md)|Уведомляет отладочный пакет об обновлении атрибуты текста в документе.|  
|[onUpdateDocumentAttributes](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onupdatedocumentattributes.md)|Уведомляет приемника события, что атрибуты были обновлены.|  
  
## <a name="remarks"></a>Примечания  
 Только модули отладки, которые поставляют своих собственных документов может воспользоваться преимуществами `IDebugDocumentTextEvent2` интерфейса. Примером будет модуля отладки скрипта. В процессе интерпретации скриптов, новый исходный код может быть создан, не присутствует в любом файле диска и известен только DE.  
  
## <a name="requirements"></a>Требования  
 Заголовок: msdbg.h  
  
 Пространство имен: Microsoft.VisualStudio.Debugger.Interop  
  
 Сборка: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>См. также  
 [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)   
 [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)