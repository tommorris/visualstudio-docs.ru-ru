---
title: IDiaSession::getEnumTables | Документы Microsoft
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::getEnumTables method
ms.assetid: 66e0fba2-ca63-4e24-a46a-c99c7fb61dd1
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 7556999e1455dcfa0d79b131ee4661a77732990f
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/18/2018
ms.locfileid: "31460945"
---
# <a name="idiasessiongetenumtables"></a>IDiaSession::getEnumTables
Возвращает перечислитель для всех таблиц, содержащихся в хранилище символов.  
  
## <a name="syntax"></a>Синтаксис  
  
```C++  
HRESULT getEnumTables (   
   IDiaEnumTables** ppEnumTables  
);  
```  
  
#### <a name="parameters"></a>Параметры  
 `ppEnumTables`  
 [out] Возвращает [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md) объекта. Этот интерфейс можно используйте для перечисления таблиц в хранилище символов.  
  
## <a name="return-value"></a>Возвращаемое значение  
 В случае успеха возвращает `S_OK`; в противном случае возвращается код ошибки.  
  
## <a name="example"></a>Пример  
 В этом примере представлены общие функции, использующей `getEnumTables` метод, чтобы получить объект определенного перечислителя. При обнаружении перечислителя, функция возвращает указатель, который может быть приведен к нужному интерфейсу; в противном случае функция возвращает `NULL`.  
  
```C++  
IUnknown *GetTable(IDiaSession *pSession, REFIID iid)  
{  
    IUnknown *pUnknown = NULL;  
    if (pSession != NULL)  
    {  
        CComPtr<IDiaEnumTables> pEnumTables;  
        if (pSession->getEnumTables(&pEnumTables) == S_OK)  
        {  
             CComPtr<IDiaTable> pTable;  
             DWORD celt = 0;  
             while(pEnumTables->Next(1,&pTable,&celt) == S_OK &&  
                   celt == 1)  
             {  
                  if (pTable->QueryInterface(iid, (void **)pUnknown) == S_OK)  
                  {  
                       break;  
                  }  
                  pTable = NULL;  
             }  
        }  
    }  
    return(pUnknown);  
}  
```  
  
## <a name="see-also"></a>См. также  
 [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)   
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)