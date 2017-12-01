---
title: "Рекомендации для разработки и рекомендации по COM, VSTO и VBA надстройки Office | Документы Microsoft"
ms.custom: 
ms.date: 07/25/2017
ms.reviewer: 
ms.suite: 
ms.technology: office-development
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: 
helpviewer_keywords: 
ms.assetid: 810a6648-fece-4b43-9eb6-948d28ed2158
caps.latest.revision: "33"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 55b3a2cbaf98eeacb78f55bea23d638cd4a1ab6d
ms.sourcegitcommit: 26419ab0cccdc30d279c32d6a841758cfa903806
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/11/2017
---
# <a name="development-best-practices-for-com-vsto-and-vba--add-ins-in-office"></a>Рекомендации по разработке для COM, VSTO и VBA надстройки Office
  При разработке надстройки COM VSTO и VBA для Office, выполните рекомендации по разработке описано в этой статье.   Это позволит обеспечить:

-  Совместимость надстроек между различными версиями и развертывание пакета Office.
-  Снижение сложности развертывания надстройки для пользователей и ИТ-администраторов.
-  Непредвиденные сбоев установки или среды выполнения для надстройки не возникают.

>Примечание: С помощью [Desktop моста](https://docs.microsoft.com/en-us/windows/uwp/porting/desktop-to-uwp-root) для подготовки вашей модели COM, VSTO и VBA надстройки для магазина Windows не поддерживается. Надстройки COM, VSTO и VBA не может распространяться в магазине Windows или магазин Office. 
  
## <a name="do-not-check-for-office-during-installation"></a>Не устанавливайте флажок для Office во время установки  
 Не рекомендуется использовать надстройки обнаружения установки во время установки надстройки Office. Если Microsoft Office не установлен, можно установить надстройки и пользователь будет иметь доступ к его после установки Office. 
  
## <a name="use-embedded-interop-types-nopia"></a>Используйте типы внедренных сборок взаимодействия (NoPIA)  
Если решение использует .NET 4.0 или более поздней версии, используйте типы внедренных сборок взаимодействия (NoPIA) вместо в зависимости от Office основной взаимодействия сборки (PIA) распространяемого пакета. С помощью внедрения типа уменьшает размер установки решения и обеспечивает совместимость с будущими версиями. Office 2010 была последняя версия Office, которая поставлялась распространяемую сборку PIA. Дополнительные сведения см. в разделе [Пошаговое руководство: внедрение сведений о типах из сборок Microsoft Office](https://msdn.microsoft.com/en-us/library/ee317478.aspx) и [эквивалентности типов и внедренных типов взаимодействия](https://docs.microsoft.com/en-us/dotnet/framework/interop/type-equivalence-and-embedded-interop-types). 

Если в решении используется более ранняя версия .NET, рекомендуется обновить решение для использования .NET 4.0 или более поздней версии. С помощью .NET 4.0 или более поздней уменьшает необходимых компонентов среды выполнения на более новых версиях Windows.
  
## <a name="avoid-depending-on-specific-office-versions"></a>Избегайте в зависимости от конкретных версий Office  
Если решение использует функциональные возможности, которые доступны только в более новых версиях Office, проверьте возможность (если это возможно, на уровне компонентов) во время выполнения (например, с помощью исключения, обработка и проверив версию). Проверка минимальные версии вместо конкретных версий, с помощью поддерживаемых API объектной модели, например [Application.Version свойства](https://msdn.microsoft.com/en-us/library/office/microsoft.office.interop.excel._application.version.aspx). Мы не рекомендуем зависит от двоичных метаданных Office, пути установки или разделов реестра, так как они могут меняться в различных установок, сред и версий.

## <a name="enable-both-32-bit-and-64-bit-office-usage"></a>Включить использование Office 32-разрядных и 64-разрядные   
Целевые сборки по умолчанию должен поддерживать (x86) 32-разрядных и 64-разрядных (x64), если решение зависит от библиотеки, которые доступны только для определенной разрядности. 64-разрядной версии Office продолжает расти внедрения, особенно в средах с большими данными. Поддерживающие 32-разрядных и 64-разрядных упрощает для пользователей для перехода между 32-разрядных и 64-разрядной версии Office.

При написании кода VBA, используйте 64-разрядных safe инструкции declare и преобразовать переменных соответствующим образом. Кроме того убедитесь, что документы могут совместно использоваться пользователями под управлением 32-разрядной или 64-разрядной версии Office, предоставив код для каждого разрядности. Дополнительные сведения см. в разделе [64-разрядных Visual Basic для приложений Обзор](https://msdn.microsoft.com/en-us/library/office/gg264421.aspx).

## <a name="support-restricted-environments"></a>Поддерживать среды с ограниченным доступом   
Решение не требуется повышение прав учетной записи пользователя или администратора привилегии. Кроме того решение не следует полагаться на задание или изменение:

- Текущий рабочий каталог.
- Каталоги загрузки библиотеки DLL.
- Переменной PATH.

## <a name="change-the-save-location-of-shared-data-and-settings"></a>Изменить сохранения расположение общие данные и параметры
Если решение состоит из надстройки и процесс, который находится за пределами Office, не используйте папку данных приложения пользователя или в реестре для обмена данными или параметров между надстройкой и внешний процесс. Вместо этого рассмотрите возможность с помощью временной папки, папки документов или каталог установки вашего решения.

## <a name="increment-the-version-number-with-each-update"></a>Увеличение номера версии при каждом обновлении
Задать номер версии двоичных файлов в решении и увеличить его при каждом обновлении. Это облегчит для пользователей определить различия между версиями и оценки совместимости.

## <a name="provide-support-statements-for-the-latest-versions-of-office"></a>Укажите положения о поддержке для последних версий Office
Клиенты просим независимые поставщики программного обеспечения для предоставления положения о поддержке для их COM, VSTO и VBA надстроек, работающих в Microsoft Office. Перечисление явной поддержки операторов помогает клиентам с помощью Office 365 профессиональный плюс средства оценки готовности понять технической поддержки. 

Для предоставления положения о поддержке для клиентских приложений Office (например, Word или Excel), сначала убедитесь, что надстройки выполняются в текущей версии Office и затем фиксировать для предоставления обновлений, если добавить в приостанавливает выполнение в будущем выпуске. Необходимо протестировать надстроек, когда корпорация Майкрософт выпускает новую сборку или обновление для Office. Microsoft редко изменяются платформой расширяемости COM, VSTO и VBA в Office, и эти изменения будут также отражены в.

>Важно: Корпорации Майкрософт существует список поддерживаемых надстроек для отчеты о готовности и контактные сведения независимых поставщиков программного обеспечения. Для получения надстройки в списке в разделе [https://aka.ms/readyforwindows](https://aka.ms/readyforwindows).

## <a name="use-process-monitor-to-help-debug-installation-or-loading-issues"></a>Монитор процесса можно использовать для отладки установки или загрузки проблемы
Если надстройка имеет проблемы совместимости, во время установки или загрузки, они могут свидетельствовать о проблемы с доступом к файлу или реестру. Используйте [монитор процесса](https://docs.microsoft.com/en-us/sysinternals/downloads/procmon) или аналогичное средство отладки для входа и сравнивается поведение для рабочей среды для выявления проблемы. 