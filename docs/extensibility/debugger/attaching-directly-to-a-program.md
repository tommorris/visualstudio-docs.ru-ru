---
title: Подключение к программе | Документация Майкрософт
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debug engines, attaching to programs
ms.assetid: ad2b7db8-821c-440c-ba07-c55c6a395e0f
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: d1fa232e0e8bfca31d16209ca8cb7acd15954940
ms.sourcegitcommit: 0e5289414d90a314ca0d560c0c3fe9c88cb2217c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/19/2018
ms.locfileid: "39151789"
---
# <a name="attach-directly-to-a-program"></a>Присоединиться к программе
Пользователи, желающие Отладка программ в процессе, который обычно уже запущена, выполните следующие действия:  
  
1.  В Интегрированной среде разработки выберите **отладить процессы** команду **средства** меню.  
  
     Откроется диалоговое окно **Процессы**.  
  
2.  Выбор процесса и нажмите кнопку **Attach** кнопки.  
  
     **Присоединение к процессу** откроется диалоговое окно со списком всех отладчиков (DEs) установлен на компьютере.  
  
3.  Укажите DEs, использовать выбранный процесс отладки, а затем нажмите кнопку **ОК**.  
  
 Размер пакета отладки начнет сеанс отладки и передает ему список DEs. Сеанс отладки в свою очередь передает этот список, а также функцию обратного вызова для выбранного процесса и затем запрашивает процесс перечислить его запущенных программ.  
  
 Программным образом в ответ на запрос пользователя, размер пакета отладки создает диспетчер отладки сеансов (SDM) и передает ему список выбранных DEs. Вместе со списком, размер пакета отладки передает SDM [IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md) интерфейс. Размер пакета отладки передает список DEs для выбранного процесса путем вызова [IDebugProcess2::Attach](../../extensibility/debugger/reference/idebugprocess2-attach.md). Затем вызывает SDM [IDebugProcess2::EnumPrograms](../../extensibility/debugger/reference/idebugprocess2-enumprograms.md) через порт для программ, работающих в процессе перечисления.  
  
 С этого момента каждого модуля отладки присоединяется к программе, точно так, как описано в [присоединение после запуска](../../extensibility/debugger/attaching-after-a-launch.md), с двумя исключениями.  
  
 Для повышения эффективности DEs, которые реализуются для совместного использования адресное пространство с помощью SDM группируются таким образом, чтобы каждый DE имеет набор программ, которые он будет присоединен. В этом случае [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md) вызовы [IDebugEngine2::Attach](../../extensibility/debugger/reference/idebugengine2-attach.md) и передает его массив программ для присоединения к.  
  
 Второе исключение – то, что события запуска, отправленные DE, подключение к программе, на котором уже выполняется обычно не содержат точечное событие входа.  
  
## <a name="see-also"></a>См. также  
 [Отправка событий запуска после запуска](../../extensibility/debugger/sending-startup-events-after-a-launch.md)   
 [Задачи отладки](../../extensibility/debugger/debugging-tasks.md)