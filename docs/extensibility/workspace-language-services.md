---
title: Рабочие области и языковые службы в Visual Studio | Документы Microsoft
ms.custom: ''
ms.date: 02/21/2018
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8631ffea-83c8-4fd4-a01e-c59772e89c84
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: 59cf2936311bb94c2db1ada6a7a3d5ccf994f027
ms.sourcegitcommit: 768118d470da9c7164d2f23ca918dfe26a4be72f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="workspaces-and-language-services"></a>Рабочие области и языковой службы

Языковые службы может предоставить [открыть папку](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md) пользователям те же возможности богатый язык они используются для при работе с решениями и проектами. Языковая служба может самостоятельно активации на основе расширение файла или содержимого документа, открытого на то, что эта служба языка «свободный файл» ограничена подсветку синтаксиса. Требуются дополнительные сведения для предоставления более широкие возможности, когда изменение или просмотр исходного кода. Каждая языковая служба имеет свой собственный API-Интерфейс для инициализации этого дополнительную контекстную данными для документа. Обычно управляется системой проектов, который тесно связан для языковой службы и система построения.

## <a name="initialization"></a>Инициализация

В [рабочей](workspaces.md), инициализированную служб языка <xref:Microsoft.VisualStudio.Workspace.Intellisense.ILanguageServiceProvider> точки расширения, занимается языковой службы и ничего не знает о разработки сборки. Таким образом владелец службы языка может поддерживать один открыть папку с расширением независимо от того, сколько шаблонов существует внутри папки и файлы для выполнения их компилятора во время построения (например MSBuild, makefile-файлы, и т. д.). При изменении файлов, из которого был создан контекста файла на диске и контекст файла обновляется, поставщик службы языка уведомляется о обновленный набор контекстов файла. Поставщик службы языка можно обновить его модели.

При открытии документа в редакторе Visual Studio рассматривает только язык поставщики услуг, которые требуют контекста типы файлов, для которых можно найти соответствующий контекст поставщика файлов. Он затем передает файл контексты из соответствующие поставщики на выбранном языке поставщика услуг через `ILangaugeServiceProvider.InitializeAsync`. Поставщик службы языка назначение с помощью контекста является реализации поставщика службы языка, что ожидаемый имеет более широкие языковую службу, для открытия документа.

## <a name="using-ilanguageserviceprovider"></a>С помощью ILanguageServiceProvider

Языковая служба будет уведомлен, когда контекст файл создается с `ContextType` , совпадает с одним из `SupportedContextTypes` значений языка сервера export-атрибут.

Для поддержки службы языка, потребуется расширения:

- Уникальный `Guid`. Он будет использоваться для `SupportedContextTypes` аргументы атрибута и в `FileContext` объекта.
- Контекст файла языка
  - Фабрика поставщика
    - `ExportFileContextProviderAttribute` атрибут с указанных выше создан `Guid` в `SupportedContextTypes`
    - Реализует `IWorkspaceProviderFactory<IFileContextProvider>`
  - Используемая реализация поставщика `IFileContextProvider.GetContextsForFileAsync`
    - Создать новый `FileContext` с `contextType` аргумента конструктора как однозначно созданный `Guid`
    - Используйте `Context` свойство `FileContext` для предоставления дополнительных данных `ILanguageServiceProvider`
- Служба языка
  - Фабрика поставщика
    - `ExportLanguageServiceProvider` атрибут с указанных выше создан `Guid` в `SupportedContextTypes`
    - Реализует `IWorkspaceProviderFactory<ILanguageServiceProvider>`
  - Поставщик
    - Реализует `ILanguageServiceProvider`
    - Используйте `ILanguageServiceProvider.InitializeAsync` для включения службы языка для указанных аргументов при открытии файла
    - Используйте `ILanguageServiceProvider.UninitializeAsync` отключение службы языка для указанных аргументов при закрытии файла

>[!WARNING]
>`ILanguageServiceProvider` Методы могут вызываться в рабочей области, в основном потоке. Рассмотрите возможность планирования работы в другом потоке, чтобы избежать задержки пользовательского интерфейса.

## <a name="language-server-protocol"></a>Язык протокола сервера

`Microsoft.VisualStudio.Workspace.*` API-интерфейсы не единственный способ включения службы языка в открытой папке. Другим вариантом является использование языка сервера. Дополнительные сведения, узнайте, как [протокола сервера языка](language-server-protocol.md).

## <a name="related-interfaces"></a>Связанных интерфейсов

- <xref:Microsoft.VisualStudio.Workspace.Intellisense.ILanguageServiceProvider> вызывается при открытии или закрытии для редактирования файла сопоставления типов файлов.

## <a name="next-steps"></a>Следующие шаги

* [Рабочая область построения](workspace-build.md) -открыть папку поддерживает построение систем, таких как MSBuild и файлы makefile. 