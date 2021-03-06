---
title: Краткое руководство. Создание первого приложения Node.js с помощью Visual Studio
description: В этом кратком руководстве вы создадите приложение Node.js в Visual Studio.
ms.date: 06/27/2018
ms.prod: visual-studio-dev15
ms.technology: vs-nodejs
ms.topic: quickstart
ms.devlang: javascript
ms.assetid: b0e4ebed-1a01-41ef-aad1-4d8465ce5322
author: mikejo5000
ms.author: mikejo
manager: douge
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: e18f1e2063fd4007eba13d76473d634265b6a51f
ms.sourcegitcommit: 7a11a094a353f2e2a2077ad863ca4c0fb97f7ec5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2018
ms.locfileid: "39131860"
---
# <a name="quickstart-use-visual-studio-to-create-your-first-nodejs-app"></a>Краткое руководство. Создание первого приложения Node.js с помощью Visual Studio

В рамках этого краткого (на 5–10 минут) знакомства с возможностями интегрированной среды разработки (IDE) Visual Studio вы создадите простое веб-приложение Node.js. Установите Visual Studio 2017 бесплатно со страницы [скачиваемых материалов Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017), если еще не сделали этого.

## <a name="create-a-project"></a>Создание проекта

Сначала вы создадите проект веб-приложения Node.js.

1. Если у вас не установлена среда выполнения Node.js, установите версию LTS с веб-сайта [Node.js](https://nodejs.org/en/download/).

    Как правило, Visual Studio автоматически обнаруживает установленную среду выполнения Node.js. Если установленная среда выполнения не обнаружена, вы можете настроить проект так, чтобы он ссылался на установленную среду выполнения, на странице свойств (после создания проекта щелкните его узел правой кнопкой мыши и выберите пункт **Свойства**).

1. Откройте Visual Studio 2017.

1. В верхней строке меню выберите **Файл** > **Создать** > **Проект**.

1. В левой области диалогового окна **Новый проект** разверните узел **JavaScript** и выберите **Node.js**. В средней области выберите **Пустое веб-приложение Node.js** и нажмите кнопку **ОК**.

     Если шаблон проекта **Пустое веб-приложение Node.js** отсутствует, щелкните ссылку **Открыть установщик Visual Studio** в левой области диалогового окна **Новый проект**. Запускается Visual Studio Installer. Выберите рабочую нагрузку **Разработка Node.js**, а затем элемент **Изменить**.

     ![Рабочая нагрузка Node.js в установщике Visual Studio](../ide/media/quickstart-nodejs-workload.png)

    После того как вы выберете шаблон **Пустое веб-приложение Node.js** и нажмете **ОК**, Visual Studio создаст решение и откроет проект. Файл *server.js* откроется в редакторе в левой области.

## <a name="explore-the-ide"></a>Изучение интегрированной среды разработки

1. Посмотрите на **обозреватель решений** в правой области.

   ![обозреватель решений](../ide/media/quickstart-nodejs-solution-explorer.png)

   - Полужирным шрифтом выделен ваш проект, имя которого вы указали в окне **Новый проект**. На диске этот проект представлен файлом *NJSPROJ* в папке проекта.

   - На верхнем уровне находится решение, имя которого по умолчанию совпадает с именем проекта. Решение, представленное на диске файлом *SLN*, является контейнером для одного или нескольких связанных проектов.

   - В узле npm представлены все установленные пакеты npm. Вы можете щелкнуть узел npm правой кнопкой мыши, чтобы найти и установить пакеты npm с помощью диалогового окна.

1. Чтобы установить пакеты npm или команды Node.js из командной строки, щелкните узел проекта правой кнопкой мыши и выберите пункт **Открыть командную строку здесь**.

   ![Командная строка Node.js](../ide/media/quickstart-nodejs-command-prompt.png)

1. В редакторе, в котором открыт файл *server.js*, выберите `http.createServer` и нажмите клавишу **F12** или выберите пункт **Перейти к определению** в контекстном меню. Эта команда выполняет переход к определению функции `createServer` в *index.d.ts*.

   ![Контекстное меню "Перейти к определению"](../ide/media/quickstart-nodejs-gotodefinition.png)

1. Вернитесь к файлу *server.js*, установите курсор в конце строки кода `res.end('Hello World\n');` и измените ее следующим образом:

    `res.end('Hello World\n' + res.connection.`

    При вводе `connection.` технология IntelliSense предлагает варианты автозавершения.

   ![Автозавершение IntelliSense](../ide/media/quickstart-nodejs-intellisense.png)

1. Выберите **localPort**, а затем введите `);`, чтобы завершить оператор. Он должен выглядеть следующим образом:

    `res.end('Hello World\n' + res.connection.localPort);`

## <a name="run-the-application"></a>Запуск приложения

1. Чтобы запустить приложение, нажмите клавиши **CTRL**+**F5** (или последовательно выберите **Отладка > Запуск без отладки**). Приложение откроется в браузере.

1. В окне браузера вы увидите надпись "Hello World" и номер локального порта.

1. Закройте веб-браузер.

Поздравляем с завершением этого краткого руководства, в котором вы получили основные сведения о работе с интегрированной средой разработки Visual Studio и Node.js. Если вы хотите ознакомиться с возможностями этого продукта более подробно, продолжите работу с руководством из раздела **Руководства** в содержании.

## <a name="next-steps"></a>Следующие шаги

> [!div class="nextstepaction"]
> [Развертывание приложения в службе приложений Linux](../javascript/publish-nodejs-app-azure.md)

- [Руководство по Node.js и выпуску Express](../javascript/tutorial-nodejs.md)
- [Руководство по Node.js и React](../javascript/tutorial-nodejs-with-react-and-jsx.md)