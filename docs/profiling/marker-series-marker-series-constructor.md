---
title: Конструктор marker_series::marker_series | Документы Майкрософт
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- cvmarkersobj/Concurrency::diagnostic::marker_series::marker_series
helpviewer_keywords:
- Concurrency::diagnostic::marker_series constructor
ms.assetid: 042c7d23-f1d8-4e09-9e76-a21c30243790
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: bbc397fa88c722f6a7f16ac92f4388525073c0fa
ms.sourcegitcommit: ce154aee5b403d5c1c41da42302b896ad3cf8d82
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2018
ms.locfileid: "34845627"
---
# <a name="markerseriesmarkerseries-constructor"></a>Конструктор marker_series::marker_series
Инициализирует новый экземпляр класса `marker_series`.  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
marker_series();  
marker_series(  
   _In_ LPCTSTR _SeriesName  
);  
marker_series(  
   _In_ const GUID* _ProviderGuid  
);  
marker_series(  
   _In_ const GUID* _ProviderGuid,  
   _In_ LPCTSTR _SeriesName  
);  
```  
  
#### <a name="parameters"></a>Параметры  
 `_SeriesName`  
 Имя создаваемой последовательности.  
  
 `_ProviderGuid`  
 Идентификатор GUID поставщика последовательности.  
  
## <a name="requirements"></a>Требования  
 **Заголовок:** *cvmarkersobj.h*  
  
 **Пространство имен:** Concurrency::diagnostic  
  
## <a name="see-also"></a>См. также  
 [Класс marker_series](../profiling/marker-series-class.md)