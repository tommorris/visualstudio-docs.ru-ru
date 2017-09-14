---
title: "Метод valueOf (Error) | Microsoft Docs"
ms.custom: ""
ms.date: "01/18/2017"
ms.prod: "windows-client-threshold"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-javascript"
ms.tgt_pltfrm: ""
ms.topic: "language-reference"
dev_langs: 
  - "JavaScript"
  - "TypeScript"
  - "DHTML"
ms.assetid: ca25c57d-c9ad-445b-8235-561390de680c
caps.latest.revision: 2
author: "mikejo5000"
ms.author: "mikejo"
manager: "ghogen"
caps.handback.revision: 2
---
# Метод valueOf (Error)
Возвращает строковое значение ошибки.  
  
## Синтаксис  
  
```  
  
error.valueOf()  
```  
  
#### Параметры  
 Объект `error` — любой экземпляр Error.  
  
## Возвращаемое значение  
 Строка "Error: " и сообщение об ошибке.  
  
## Пример  
 В следующем примере показано использование метода `valueOF` с датой.  
  
```javascript  
var myError = new Error();  
myError.message = "This is an error.";  
var value = myError.valueOf();  
document.write(value);  
  
// Output: Error: This is an error.  
  
```  
  
## Требования  
 [!INCLUDE[jsv2](../../javascript/reference/includes/jsv2-md.md)]