---
title: С помощью меток текста с помощью API прежних версий | Документация Майкрософт
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - text markers
ms.assetid: 937a0b19-1216-45d5-a7ad-4fe1d6f73097
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: bcfae4cc786fb7a3e0c2ccd48f867bb6c32530d6
ms.sourcegitcommit: 9765b3fcf89375ca499afd9fc42cf4645b66a8a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/20/2018
ms.locfileid: "46496133"
---
# <a name="using-text-markers-with-the-legacy-api"></a>С помощью меток текста с помощью API прежних версий
Текстовая метка — с плавающей запятой диапазон текста в буфере, которые могут повлиять на отображение и поведение области текста. Маркеры включают точки останова, закладок, волнистых линий и только для чтения областей. Текстовые метки, по сути отличаются от Цветовая подсветка синтаксиса. Цветовая подсветка синтаксиса — это быстрый способ взаимодействия синтаксис языка, который связан с области текста. Цветовая подсветка синтаксиса запрашивается обычно в том случае, когда Windows перерисовывает экрана, когда важна скорость. Цветовая подсветка синтаксиса изменяет цвет текста. Текстовые метки можно изменить множество других свойств текста. Текстовые метки можно «float» и применить специальное поведение и его выделение цветом.  
  
 Из-за снижению производительности, связанные с текстовые метки не следует создавать много маркеры для вашей текстовых буферов. Каждый маркер обновляется каждый раз, что пользователь редактирует содержимое буфера.  
  
> [!NOTE]
>  Пользователи могут изменять цвет тип видимым маркера, но не его форма и стиля. Дополнительные сведения см. в разделе [шрифты и цвета, среда, диалоговое окно параметров](../ide/reference/fonts-and-colors-environment-options-dialog-box.md).  
  
## <a name="related-topics"></a>См. также  
  
|Заголовок|Описание|  
|-----------|-----------------|  
|[Практическое руководство. Добавление стандартных текстовых маркеров](../extensibility/how-to-add-standard-text-markers.md)|Описывает способы добавления стандартного текста тип маркера, предоставляемые [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] базовым редактором для представления текста.|  
|[Практическое руководство. Реализация маркеров ошибок](../extensibility/how-to-implement-error-markers.md)|Описывается реализация экземпляр [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] маркер, который используется для указания ошибок с помощью красными волнистыми линиями.|  
|[Практическое руководство. Создание пользовательских текстовых маркеров](../extensibility/how-to-create-custom-text-markers.md)|Описывает, как создать и добавить пользовательский текстовый тип маркера для текстового представления.|  
|[Практическое руководство. Использование текстовых маркеров](../extensibility/how-to-use-text-markers.md)|Описание способов добавления меток текста.|  
|[Компоненты основного редактора](../extensibility/inside-the-core-editor.md)|Описание возможностей базовым редактором и подробные сведения о том, как настроить базовый редактор.|  
|[Возможности редактора](https://msdn.microsoft.com/library/bdac940d-1f14-4019-a01f-fd0bb3dc7198)|Описывает функции, доступные в [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] базовым редактором.|  
  
## <a name="reference"></a>Ссылка  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsPackageDefinedTextMarkerType>  
 Предоставляет единый механизм для получения информации о типом маркера определенный текст, предопределенных редактором или зарегистрированные пакетом VSPackage.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLineMarker>  
 Предоставляет доступ к и корректирует положение текстового маркера в текстовом буфере, используя двухмерные координаты.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarker>  
 Предоставляет методы для управления текстовыми маркерами.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient>  
 Предоставляет обратные вызовы [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] интегрированной среды разработки и другие процессы, которые используются для настройки текстового маркера.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClientAdvanced>  
 Расширяет функциональность, которая доступна через <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> интерфейса, предоставляя дополнительные обратные вызовы.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClientEx>  
 Расширяет функциональность, которая доступна через <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> интерфейса, предоставляя дополнительные обратные вызовы.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerColorSet>  
 Включает тип маркера определить, используют ли другие типы маркеров тот же набор цветов.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider>  
 Предоставляет контекст для меток текста в редакторе. Для каждого типа маркера текста в редакторе, IDE создает отдельный <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider> объекта.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerGlyphDropHandler>  
 Обработчик, который предоставляется для меток, глифы которых поддерживает редактирование перетаскивания и вставки. Глиф является значок, указывающий положение метки.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerTypeProvider>  
 Возвращает <xref:Microsoft.VisualStudio.TextManager.Interop.IVsPackageDefinedTextMarkerType> интерфейса из службы, предоставляет текст маркеров для других пакетов VSPackage.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStreamMarker>  
 Предоставляет доступ к и корректирует положение текстового маркера в текстовом буфере, с помощью одноразмерных координат. Если это возможно, не используйте этот интерфейс.