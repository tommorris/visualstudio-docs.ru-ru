---
title: Общие сведения о значениях данных по состязаниям за ресурсы | Документы Майкрософт
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- concurrency profiling method
- Profiling Tools, concurrency method
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: c06722e9270269ca674370d5bf8b1925d850ce00
ms.sourcegitcommit: 4cd4aef53e7035d23e7d1d0f66f51ac8480622a1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2018
ms.locfileid: "34477409"
---
# <a name="understand-resource-contention-data-values"></a>Общие сведения о значениях данных по конфликтам ресурсов

При профилировании состязаний за ресурсы происходит сбор подробных данных стека вызовов всякий раз, когда конкурирующие потоки в приложении вынуждены ожидать доступа к общему ресурсу.

В отчетах о состязании за ресурсы содержится общее число состязаний и общее время, затраченное на ожидание ресурса модулями, функциями, строками исходного кода и инструкциями.

- Инклюзивные значения позволяют определить общее число состязаний, ставших причиной ожидания в функции, для каждого состязания за ресурс, а также общее время ожидания.  В инклюзивных значениях учитываются состязания, которые были вызваны дочерними функциями, вызванными данной функцией.

- Эксклюзивные значения позволяют определить только общее число состязаний, ставших причиной ожидания в функции и вызванных кодом в ее теле. Состязания, вызванные дочерними функциями, не включаются. Эксклюзивное время функции также включает только время ожидания, вызванного операторами в теле функции.

Кроме того, в представлениях отчета о состязаниях за ресурсы содержатся графы временной шкалы, на которых показаны отдельные события состязания в течение времени, а также стеки вызовов, создавшие определенное событие. Дополнительные сведения см. в одном из следующих разделов.

- [Представление "Сведения о потоке"](../profiling/thread-details-view-contention-data.md)

- [Представление "Сведения о ресурсах"](../profiling/resource-details-view-contention-data.md)

Дополнительные сведения о втором режиме профилирования параллелизма см. в разделе [Визуализатор параллелизма](../profiling/concurrency-visualizer.md).