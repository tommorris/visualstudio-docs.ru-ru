---
title: Использование файлов дампа | Документация Майкрософт
ms.custom: H1HackMay2017
ms.date: 03/08/2017
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.crashdump
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- dumps, about dumps
- crash dumps
- dump files
- dumps
ms.assetid: b71be6dc-57e0-4730-99d2-b540a0863e49
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: d072dcf839f31df2dba14a3293ed962cd3a68fce
ms.sourcegitcommit: 1ab675a872848c81a44d6b4bd3a49958fe673c56
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2018
ms.locfileid: "44281030"
---
# <a name="use-dump-files-with-visual-studio"></a>Использование файлов дампа с помощью Visual Studio
Файлы дампа с кучами или без куч; Создание файла дампа; Открытие файла дампа; Поиск двоичных файлов, PDB-файла и исходного файла для файла дампа.

##  <a name="BKMK_What_is_a_dump_file_"></a> Что такое файл дампа?
 Объект *файл дампа* представляет собой моментальный снимок приложения в точку во времени, берется дампа. Он показывает, какой процесс исполнялся и какие модули были загружены в момент создания дампа. Если дамп был сохранен с данными кучи, файл дампа содержит снимок того, что находилось в памяти приложения в тот момент времени. Открытие файла дампа с кучей в Visual Studio похоже на остановку в точке останова в сеансе отладки. Хотя выполнение продолжить невозможно, можно просмотреть стеки, потоки и значения переменных приложения, соответствующие моменту времени создания дампа.

 Дампы в основном используются для отладки проблемы, возникающие на компьютерах, которые разработчик не имеет доступа к. Например можно использовать файл дампа с компьютера клиента, если не удается воспроизвести сбоя клиента или зависает на вашем компьютере. Дампы также создаются тест-инженерами с целью сохранения данных сбоя или зависания, чтобы можно было продолжить использовать тестовый компьютер для других операций тестирования. Отладчик Visual Studio может сохранять файлы дампа для управляемого и машинного кода. Отладчик может загружать файлы дампа, созданные в Visual Studio или другим программам, сохранять файлы в *минидампа* формат.

##  <a name="BKMK_Dump_files__with_or_without_heaps"></a> Файлы дампа с кучами или без куч
 Можно создавать файлы дампа со сведениями кучи или без них.

-   **Файлы дампа с кучами** содержат снимок памяти приложения. Сюда входят значения переменных в момент создания дампа. После загрузки файла дампа, сохраненного с кучей, Visual Studio может загружать символы, даже если двоичный файл приложения не найден. Visual Studio также сохраняет в файле дампа двоичные файлы загруженных модулей машинного кода, что может значительно упростить отладку.

-   **Файлы дампа без куч** гораздо меньше, чем дампы со сведениями кучи. Однако в этом случае для поиска сведений о символах отладчик должен загружать двоичные файлы приложения. Двоичные файлы должны в точности соответствовать двоичным файлам, которые использовались при создании дампа. В файлах дампа без данных кучи хранятся только значения переменных стека.

##  <a name="BKMK_Requirements_and_limitations"></a> Требования и ограничения

-   Отладка с использованием файлов дампа оптимизированного кода может сопровождаться ложной информацией. К примеру, встраивание компилятором функций может приводить к непредвиденным стекам вызовов, а другие виды оптимизации могут изменять время существования переменных.

-   Отладка с использованием файла дампа, созданного на 64-разрядном компьютере, должна производиться в экземпляре Visual Studio, работающем на 64-разрядном компьютере.

-   В версиях Visual Studio до VS 2013 невозможно открыть дампы 32-разрядных приложений, выполняющихся на 64-разрядных компьютерах, которые были собраны определенными средствами (например, диспетчером задач и 64-разрядной версией WinDbg). В VS 2013 это ограничение снято.

-   Visual Studio поддерживает отладку файлов дампа, создаваемых приложениями в машинных кодах на устройствах ARM. Visual Studio также поддерживает отладку файлов дампа, создаваемых управляемыми приложениями на устройствах ARM, но только в отладчике машинного кода.

-   Для отладки [режима ядра](/windows-hardware/drivers/debugger/kernel-mode-dump-files) файлы дампа, загрузите средства отладки для Windows, который является частью [набор драйверов Windows (WDK)](/windows-hardware/drivers/download-the-wdk).

-   Visual Studio не поддерживает отладку файлов дампа, сохраненных в старом формате, известном как [дампа пользовательского режима полного](http://msdn.microsoft.com/library/windows/hardware/ff545506.aspx). Обратите внимание, что "полный дамп в режиме пользователя" и "дамп с кучей" — это не одно и то же.

-   Для отладки с помощью [SOS.dll (расширение отладки SOS)](/dotnet/framework/tools/sos-dll-sos-debugging-extension) в Visual Studio, необходимо установить средства отладки для Windows, который является частью [набор драйверов Windows (WDK)](/windows-hardware/drivers/download-the-wdk)

##  <a name="BKMK_Create_a_dump_file"></a> Создание файла дампа
 Создание файла дампа с использованием Visual Studio:

-   При отладке процесса в Visual Studio можно сохранить файл дампа, когда отладчик останавливает выполнение в точке останова или при возникновении исключения. Выберите **Отладка**, затем **Сохранение дампа**, затем **Отладка**. В **Сохранение дампа** отображаемое в диалоговом окне **тип** списка, можно выбрать **минидампа** или **малый дамп с кучей** (по умолчанию).

-   С помощью [JIT-отладка](../debugger/just-in-time-debugging-in-visual-studio.md) включен, вы можете подключить отладчик к аварийному процессу, который выполняется вне отладчика, а затем сохраните файл дампа. См. в разделе [присоединение к выполняемым процессам](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)

 Файлы дампа также можно создавать с помощью любой программы, которая поддерживает формат минидампов Windows. Например **Procdump** программы командной строки из [Windows Sysinternals](http://technet.microsoft.com/sysinternals/default) можно создавать файлы аварийного дампа процесса на основе триггеров или по требованию. См. в разделе [требования и ограничения](../debugger/using-dump-files.md#BKMK_Requirements_and_limitations) в этом разделе, Дополнительные сведения об использовании других средств для создания файлов дампа.

##  <a name="BKMK_Open_a_dump_file"></a> Открытие файла дампа

1.  В Visual Studio, выберите **файл**, **откройте**, **файл**.

2.  В **открыть файл** диалогового окна найдите и выберите файл дампа. Обычно они имеют расширение DMP. Затем выберите **ОК**.

3.  **Сводка файла дампа** появится окно. В этом окне можно просмотреть сведения об отладке для файла дампа, установить путь символов, запустить отладку и скопировать сводку в буфер.

     ![Страница сводки минидампа](../debugger/media/dbg_dump_summarypage.png "DBG_DUMP_SummaryPage")

4.  Чтобы начать отладку, перейдите к **действия** раздела и выберите либо **отладки с помощью только управляемый код**, **только машинный код** или **Отладка в смешанном режиме**.

##  <a name="BKMK_Find_binaries__symbol___pdb__files__and_source_files"></a> Поиск двоичных файлов, файлов символов (.pdb) и исходных файлов
 Чтобы можно было использовать все возможности Visual Studio для отладки файла дампа, необходимо иметь доступ к следующим файлам:

-   EXE-файл, для которого был получен дамп, и другие двоичные файлы (DLL и т. п.), которые использовались в процессе, для которого был создан дамп.

     Если для отладки используется дамп с данными кучи, Visual Studio может справиться с отсутствием двоичных файлов для некоторых модулей, но должен иметь двоичные файлы для достаточного количества модулей, чтобы создавать допустимые стеки вызовов. Visual Studio включает модули машинного кода в файл дампа с кучей.

-   Файлы символов (.pdb) для EXE-файлов и других двоичных файлов.

-   Исходные файлы для нужных модулей.

     Исполняемый файл и PDB-файлы должны точно соответствовать версии и сборке файлов, которые использовались при создании дампа.

     Для отладки можно использовать Дизассемблированный код модулей, если не удается найти исходные файлы

 **Пути поиска по умолчанию для исполняемых файлов**

 Visual Studio автоматически ищет исполняемые файлы, которые не включены в файл дампа в следующих расположениях:

1.  Каталог, содержащий файл дампа.

2.  Путь к модулю, указанный в файле дампа. Это путь к модулю на компьютере, на котором был создан дамп.

3.  Путей к символам, указанные в **Отладка**, **параметры**, **символы** странице Visual Studio **средства**, **параметры**  диалоговое окно. При необходимости на этой странице можно добавить другие расположения для поиска.

 **С помощью двоичного нет > символ > источника страниц**

 Если Visual Studio не удается найти файлы, необходимые для отладки модуля в дампе, отображается соответствующая страница (**двоичных не найдены**, **символы не найдены**, или **исходный код не найден**). Эти страницы предоставляют подробные сведения о причине проблемы, а также ссылки на действия, которые могут помочь определить правильное расположение файлов. См. статью [Указание файлов символов (.pdb) и файлов с исходным кодом в отладчике Visual Studio](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).

## <a name="see-also"></a>См. также

- [JIT-отладка](../debugger/just-in-time-debugging-in-visual-studio.md)
- [Указание файлов символов (.pdb) и файлов с исходным кодом](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
- [IntelliTrace](../debugger/intellitrace.md)