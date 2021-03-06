---
title: Вариант размера окна просмотра 1 x 1 | Документация Майкрософт
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 3dbc3247-00f5-4644-8ff9-72e9febcf09a
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 168b358bf58dcb2c91814f5460b203873255e275
ms.sourcegitcommit: 80f9daba96ff76ad7e228eb8716df3abfd115bc3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2018
ms.locfileid: "37433250"
---
# <a name="1x1-viewport-size-variant"></a>Вариант размера окна просмотра (1x1)
Размеры окна просмотра для всех целевых объектов отрисовки уменьшаются до 1 x 1 пикселей.  
  
## <a name="interpretation"></a>Интерпретация  
 Уменьшение окна просмотра снижает число пикселей, которое следует тень. Но Уменьшение окна просмотра не снижает число вершин, необходимые для процесса. Уменьшение размеров окна просмотра до 1 x 1 пикселя приводит к тому, что затенение пикселей в приложении не используется.  
  
 Если этот вариант дает прирост производительности, это может означать, что приложение потребляет слишком много коэффициент заполнения. Кроме того, разрешение может быть слишком большое для целевой платформы или приложения бы потратить много времени на затенение пикселей, которые затем перезаписываются, также известным как *перерисовывать*. Меньшего размера буфера кадров или уменьшение числа операций перекрытия улучшит производительность приложения.  
  
## <a name="remarks"></a>Примечания  
 Размеры окна просмотра устанавливаются равными 1 x 1 пиксель после каждого вызова метода `ID3D11DeviceContext::OMSetRenderTargets` или `ID3D11DeviceContext::RSSetViewports`.  
  
## <a name="example"></a>Пример  
 Этот вариант можно воспроизвести следующим кодом:  
  
```cpp
D3D11_VIEWPORT viewport;  
viewport.TopLeftX = 0;  
viewport.TopLeftY = 0;  
viewport.Width = 1;  
viewport.Height = 1;  
d3d_context->RSSetViewports(1, &viewport);  
```
