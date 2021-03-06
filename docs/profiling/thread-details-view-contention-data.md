---
title: Представление "Сведения о потоке" — сведения о состязаниях | Документы Майкрософт
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.view.threaddetails
helpviewer_keywords:
- Thread Details view
ms.assetid: 874c3b1c-88d8-479a-bb35-1291d9aa8e67
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 712fcfa369c4a324554bda38df671dab1a95a1f5
ms.sourcegitcommit: 4cd4aef53e7035d23e7d1d0f66f51ac8480622a1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2018
ms.locfileid: "34477357"
---
# <a name="thread-details-view---contention-data"></a>Представление "Сведения о потоке" — сведения о состязаниях
Представление "Сведения о потоке" представляет собой временную шкалу событий блокировки в выбранном потоке сеанса профилирования, обусловленных состязаниями за ресурсы. Событие блокировки возникает, когда поток вынужден приостановить выполнение, так как другой поток заблокировал доступ к ресурсу.  
  
 В этом представлении выполнение потока во времени представлено в виде горизонтальной полосы, а события блокировки — в виде вертикальной полосы на горизонтальной временной шкале потока. При необходимости можно увеличить отрезок временной шкалы для просмотра отдельных событий. Чтобы просмотреть путь выполнения функций, который привел к событию, щелкните событие на полосе. В окне **Стек вызовов** отобразятся функции. Если исходный код функции доступен, можно щелкнуть имя функции и отредактировать исходный файл в интегрированной среде разработки Visual Studio.  
  
## <a name="navigate-the-timeline"></a>Перемещение по временной шкале  
  
#### <a name="to-zoom-in-on-a-timeline-segment"></a>Увеличение сегмента временной шкалы  
  
-   Щелкните и перетащите указатель мыши, чтобы выбрать область временной шкалы.  
  
     Отпустите кнопку мыши, чтобы изменить соответствующим образом масштаб выбранных в представлении отрезков времени. Процесс можно повторить для получения более подробного представления. Ползунок полосы прокрутки времени указывает относительный размер отрезка времени, отображаемого в представлении.  
  
#### <a name="to-zoom-out-on-a-timeline"></a>Уменьшение масштаба временной шкалы  
  
-   Чтобы вернуться к прежнему масштабу, щелкните **Уменьшить**.  
  
-   Чтобы в представлении отобразилась вся временная шкала, щелкните **Сброс масштаба**.  
  
#### <a name="to-view-the-call-stack-of-an-event"></a>Просмотр стека вызовов события  
  
-   На временной шкале щелкните вертикальную полосу, которая представляет событие.  
  
#### <a name="to-view-or-edit-the-source-code-of-a-function-in-the-call-stack"></a>Просмотр или правка исходного кода функции в стеке вызовов  
  
-   В окне **Стек вызовов** щелкните имя функции.  
  
 Исходный код функции должен быть частью текущего проекта.  
  
#### <a name="to-view-the-contention-events-of-a-resource-in-all-threads-in-the-profiling-run"></a>Просмотр событий состязания за ресурсы во всех потоках сеанса профилирования  
  
-   На временной шкале щелкните имя или идентификатор ресурса.  
  
     Для выбранного ресурса отобразится представление [Сведения о ресурсах](../profiling/resource-details-view-contention-data.md).  
  
#### <a name="to-view-the-thread-contention-data-in-the-processes-window"></a>Просмотр сведений о состязаниях потока в окне процессов  
  
-   На временной шкале щелкните **Итого**.  
  
     Появится [представление "Процесс"](../profiling/process-view-contention-data.md) с выбранным потоком.