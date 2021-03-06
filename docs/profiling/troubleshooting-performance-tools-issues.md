---
title: Устранение неполадок средств профилирования | Документы Майкрософт
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 0b61cdf7-75b7-4abd-aff2-7bd997717626
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 531080945413bbc0959d2cdf91e2096c1e51f61d
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/06/2018
ms.locfileid: "35669333"
---
# <a name="troubleshoot-performance-tools-issues"></a>Диагностика проблем со средствами оценки производительности
При использовании средств профилирования может возникнуть одна из следующих проблем:  
  
-   [Средства профилирования не собирают данные](#no-data-is-collected-by-the-profiling-tools)  
  
-   [В представлениях и отчетах по производительности вместо имен функций отображаются номера](#performance-views-and-reports-display-numbers-for-function-names)  
  
## <a name="no-data-is-collected-by-the-profiling-tools"></a>Средства профилирования не собирают данные  
 После профилирования приложения файл данных профилирования (*VSP*) не создается, и появляется следующее предупреждение в окне **вывода** или в командном окне:  
  
 PRF0025. Данные не собраны.  
  
 Эта проблема может возникнуть по нескольким причинам.  
  
-   Процесс, профилируемый с помощью выборки или метода памяти .NET, запускает дочерний процесс, который становится процессом, выполняющим работу приложения. Например, некоторые приложения выполняют чтение командной строки для определения того, были ли они запущены как приложения Windows или как приложения командной строки. Если было запрошено приложение Windows, исходный процесс запускает новый процесс, настроенный как приложение Windows, после чего исходный процесс завершается. Так как средства профилирования не собирают данные для дочерних процессов автоматически, данные не собираются.  
  
     В этом случае для сбора данных профилирования присоедините профилировщик к дочернему процессу вместо запуска приложения с профилировщиком. Дополнительные сведения см. в разделах [Практическое руководство. Подключение средств оценки производительности к выполняющимся процессам и отключение от этих процессов](../profiling/how-to-attach-and-detach-performance-tools-to-running-processes.md) и [Attach (VSPerfCmd)](../profiling/attach.md)  
  
## <a name="performance-views-and-reports-display-numbers-for-function-names"></a>В представлениях и отчетах по производительности вместо имен функций отображаются номера  
 После профилирования приложения вместо имен функций в отчетах и представлениях отображаются номера.  
  
 Эта проблема вызвана тем, что модулю анализа средств профилирования не удается найти *PDB*-файлы, содержащие символьную информацию, сопоставляющую информацию исходного кода, такую как имена функций и номера строк, со скомпилированным файлом. По умолчанию компилятор создает *PDB*-файл при сборке файла приложения. Ссылка на локальный каталог *PDB*-файла хранится в скомпилированном приложении. Модуль анализа выполняет поиск *PDB*-файла в каталоге, на который указывает ссылка, а затем в файле, который в данный момент содержит файл приложения. Если *PDB*-файл не найден, модуль анализа использует смещения функций, а не имена функций.  
  
 Решить проблему можно одним из двух способов:  
  
-   найти *PDB*-файлы и поместить их в тот же каталог, что файлы приложения;  
  
-   внедрить символьную информацию в файл данных профилирования (*VSP*). Дополнительные сведения см. в разделе [Сохранение символьной информации с файлами данных производительности](../profiling/saving-symbol-information-with-performance-data-files.md).  
  
> [!NOTE]
>  Для модуля анализа требуется *PDB*-файл той же версии, что и файл скомпилированного приложения. *PDB*-файл более ранней или более поздней сборки файла приложения не будет работать.