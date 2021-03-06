---
title: Вопросы и ответы по отладке моментальных снимков | Документация Майкрософт
ms.date: 11/07/2017
ms.technology: vs-ide-debug
ms.topic: reference
helpviewer_keywords:
- debugger
ms.assetid: 944f1eb0-a74b-4d28-ae2b-a370cd869add
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 13b35746a7b0d639d4c954c8ef1a5221973e1abc
ms.sourcegitcommit: 0e5289414d90a314ca0d560c0c3fe9c88cb2217c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/19/2018
ms.locfileid: "39154350"
---
# <a name="frequently-asked-questions-for-snapshot-debugging-in-visual-studio"></a>Часто задаваемые вопросы по отладке моментальных снимков в Visual Studio

Ниже приведен список вопросов, которые могут устанавливаться во время отладки работающих приложениях Azure, с помощью отладчика моментальных снимков.

#### <a name="what-is-the-performance-cost-of-taking-a-snapshot"></a>Что такое снижение производительности с помощью снимка

При Snapshot Debugger создает снимок приложения, разветвление процесс приложения, а Приостановка разветвленного копирования. При отладке моментального снимка, отладка для разветвления копия процесса. Этот процесс достаточно 10 – 20 миллисекунд, но не копирует полной кучи приложения. Вместо этого он копирует только таблицы страниц и устанавливает страниц для копирования при записи. Если некоторые из объектов вашего приложения при изменении кучи, копируются соответствующих им страницах. Таким образом, каждый моментальный снимок содержит небольших затратах в памяти (порядка нескольких сотен килобайт для большинства приложений). 

#### <a name="what-happens-if-i-have-a-scaled-out-azure-app-service-multiple-instances-of-my-app"></a>Что произойдет, если у меня есть служба приложений Azure горизонтальным масштабированием (несколько экземпляров приложения)?

При наличии нескольких экземпляров приложения, точки прикрепления применяются к каждой одного экземпляра. Только первая точка прикрепления к условиям, заданным создает моментальный снимок. Если у вас есть несколько точек прикрепления, последующие моментальные снимки берутся тот же экземпляр, который создан первый снимок. Точек ведения журнала, отправленных в окно вывода будут отображаться сообщения из одного экземпляра только в том случае, хотя точек ведения журнала, отправляемые журналы приложений отправлять сообщения из каждого экземпляра. 

#### <a name="how-does-the-snapshot-debugger-load-symbols"></a>Как Snapshot Debugger загрузить символы

Отладчик моментальных снимков требуется наличие соответствующих символов для вашего приложения, развернутые или локальный к службе приложений Azure. (Внедренных PDB-файлов в настоящее время не поддерживаются.) Отладчик моментальных снимков автоматически загружает символы из службы приложений Azure. Начиная с Visual Studio 2017 версии 15.2, развертывание в службе приложений Azure, также развертывает символы приложения.

#### <a name="does-the-snapshot-debugger-work-against-release-builds-of-my-application"></a>Отладчик моментальных снимков работает для сборок выпуска моего приложения?

Да — Snapshot Debugger предназначена для работы от сборок выпуска. Когда точка прикрепления помещается в функции, ее повторной компиляции с отладочной версией, воплощение отлаживаемых. При остановке отладчика моментальных снимков, функции возвращаются их выпуска. 

#### <a name="can-logpoints-cause-side-effects-in-my-production-application"></a>Точек ведения журнала вызвать побочные эффекты в моем приложении рабочей среде

Не - практически оцениваются все сообщения журнала, добавление в приложение. Они не может вызывать никаких побочных эффектов в приложении. Тем не менее некоторые системные свойства могут оказаться недоступным с точки ведения журнала. 

#### <a name="does-the-snapshot-debugger-work-if-my-server-is-under-load"></a>Работает ли отладчика моментальных снимков, если Мой сервер испытывает нагрузку?

Да, отладка моментальных снимков можно использовать для серверов под нагрузкой. Отладчик моментальных снимков регулирует и не делать моментальные снимки в ситуациях, где имеется низкий объем свободной памяти на сервере.

#### <a name="how-do-i-uninstall-the-snapshot-debugger"></a>Как удалить Snapshot Debugger?

Расширение сайта Snapshot Debugger можно удалить в вашей службе приложений, сделав следующее:

1. Отключение приложения службы, либо с помощью Cloud Explorer в Visual Studio или портала Azure.
1. Перейдите на сайт Kudu службы приложений (то есть yourappservice. **SCM**. azurewebsites.net) и перейдите к **расширения сайта**.
1. Нажмите кнопку «X» на расширение сайта Snapshot Debugger удалить его.

## <a name="see-also"></a>См. также

[Отладка в Visual Studio](../debugger/index.md)  
[Отладка работающих приложений ASP.NET, с помощью отладчика моментальных снимков](../debugger/debug-live-azure-applications.md)  
[Устранение неполадок и известные проблемы для отладки моментальных снимков](../debugger/debug-live-azure-apps-troubleshooting.md)
