---
title: Использование карт кода для отладки приложений
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio Ultimate, visualizing code
- Visual Studio Ultimate, navigating code visually
- Visual Studio Ultimate, understanding code
- Visual Studio Ultimate, mapping code relationships
- Visual Studio Ultimate, code maps
- mapping code relationships
- code maps
- mapping relationships in code
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 006db4f3fd820a25b0c413deabce3da5faa70cec
ms.sourcegitcommit: 58052c29fc61c9a1ca55a64a63a7fdcde34668a4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2018
ms.locfileid: "34750276"
---
# <a name="use-code-maps-to-debug-your-applications"></a>Использование карт кода для отладки приложений
Карты кода помогают не запутаться в больших базах кода, малознакомом или устаревшем коде. Например при отладке, может потребоваться просмотреть код во множестве файлов и проектов. Используйте карты кода для перехода между частями кода и просмотра связей между ними. Таким образом, вам не нужно держать весь этот код у себя в голове или рисовать отдельную схему. Карты кода помогут вспомнить особенности кода в случае перерыва в работе.

 ![Карта кода &#45; сопоставление отношений в коде](../modeling/media/codemapstoryboardpaint.png)

 **Зеленая стрелка показывает, где отображается курсор в редакторе**

 Дополнительные сведения о командах и действиях, которые можно использовать при работе с картами кода см. в разделе [Просмотр и переупорядочение карт кода](../modeling/browse-and-rearrange-code-maps.md).

## <a name="understand-the-problem"></a>Определение проблемы
 Предположим, что возникла ошибка в программе рисования, над которой вы работаете. Для воспроизведения ошибки, откройте решение в Visual Studio и нажать клавишу **F5** для запуска отладки.

 Если нарисовать линию и выберите **отменить последнюю линию**, ничего не происходит, пока не будет нарисована следующая линия.

 ![Карта кода &#45; воспроизведение ошибки](../modeling/media/codemapstoryboardpaint0.png)

 Таким образом, вы начинаете поиск ошибки с поиска метода `Undo`. Он находится в классе `PaintCanvas`.

 ![Карта кода &#45; поиск кода](../modeling/media/codemapstoryboardpaint1.png)

## <a name="start-mapping-the-code"></a>Запуск сопоставления кода
 Теперь можно начинать сопоставление метода `undo` и его отношений. В редакторе кода добавьте метод `undo` и поля, на которые он ссылается, в новую карту кода. При создании новой карты потребуется какое-то время на индексацию кода. Благодаря этому последующие операции выполняются быстрее.

 ![Карта кода &#45; отображение метода и соответствующих полей](../modeling/media/codemapstoryboardpaint3.png)

> [!TIP]
>  Зеленым цветом выделены последние элементы, добавленные на карту. Зеленая стрелка указывает положение курсора в коде. Стрелки между элементами представляют различные отношения. Можно получить дополнительные сведения об элементах на карте, наведя на них указатель мыши и изучив подсказки.

 ![Карта кода &#45; отображение всплывающих подсказок](../modeling/media/codemapstoryboardpaint4.png)

## <a name="navigate-and-examine-code-from-the-map"></a>Навигация и просмотр кода из сопоставления
 Для просмотра определения кода для каждого поля, дважды щелкните поле на карте, или выберите поле и нажмите клавишу **F12**. Зеленая стрелка перемещается между элементами на карте. Курсор в редакторе кода также перемещается автоматически.

 ![Карта кода &#45; Проверка определения поля](../modeling/media/codemapstoryboardpaint5.png)

 ![Карта кода &#45; Проверка определения поля](../modeling/media/codemapstoryboardpaint5a.png)

> [!TIP]
>  Кроме того, для перемещения зеленой стрелки на карте можно перемещать курсор в редакторе кода.

## <a name="understand-relationships-between-pieces-of-code"></a>Отношения между частями кода
 Теперь необходимо узнать, какой другой код взаимодействует с полями `history` и `paintObjects`. Можно добавить все методы, которые ссылаются на эти поля, на карту. Это можно сделать из карты или из редактора кода.

 ![Карта кода &#45; поиск всех ссылок](../modeling/media/codemapstoryboardpaint6.png)

 ![Открытие карты кода из редактора кода](../modeling/media/codemapstoryboardpaint6a.png)

> [!NOTE]
>  Если вы добавляете элементы из проекта, который совместно используется несколькими приложениями, такими как приложения Windows Phone или Магазина Windows, эти элементы всегда отображаются вместе с текущим активным проектом приложения на карте. Таким образом, при изменении контекста на другой проект приложения контекст на карте для вновь добавленных элементов из общего проекта также изменяется. Операции, выполняемые с элементом в сопоставлении, применяются только к тем элементам, которые используют тот же контекст.

 Измените макет, чтобы изменить поток отношений и упростить чтение карты. Также можно перемещать элементы по карте, перетаскивая их.

 ![Карта кода &#45; изменение макета](../modeling/media/codemapstoryboardpaint7a.png)

> [!TIP]
>  По умолчанию **последовательный макет** включен. Это значит, что изменение макета карты будет минимальным при добавлении новых элементов. Чтобы макет всей карты, каждый раз при добавлении новых элементов, отключите **последовательный макет**.

 ![Карта кода &#45; изменение макета](../modeling/media/codemapstoryboardpaint7.png)

 Рассмотрим эти методы. На карте, дважды щелкните **PaintCanvas** метод, или выберите этот метод и нажмите клавишу **F12**. Этот метод создаст `history` и `paintObjects` как пустые списки.

 ![Карта кода &#45; Проверка определения метода](../modeling/media/codemapstoryboardpaint8.png)

 Теперь повторите эти же шаги, чтобы просмотреть определение метода `clear`. Метод `clear` выполнит некоторые задачи с `paintObjects` и `history`. Затем он вызовет метод `Repaint`.

 ![Карта кода &#45; Проверка определения метода](../modeling/media/codemapstoryboardpaint9.png)

 Теперь просмотрите определение метода `addPaintObject`. Он также выполнит некоторые задачи с `history` и `paintObjects`. Он также вызовет `Repaint`.

 ![Карта кода &#45; Проверка определения метода](../modeling/media/codemapstoryboardpaint10.png)

## <a name="find-the-problem-by-examining-the-map"></a>Поиск проблемы путем анализа сопоставления
 Кажется, что все методы, изменяющие `history` и `paintObjects`, вызывают `Repaint`. Однако метод `undo` не вызывает `Repaint`, даже если `undo` изменяет те же поля. Поэтому эту проблему можно решить, вызвав метод `Repaint` из `undo`.

 ![Карта кода &#45; поиск отсутствующего вызова метода](../modeling/media/codemapstoryboardpaint11.png)

 Если бы не было карты, на которой можно проверить этот отсутствующий вызов, найти эту проблему было бы сложнее, особенно в более сложном коде.

## <a name="share-your-discovery-and-next-steps"></a>Совместное использование обнаружения и следующие действия
 Прежде чем вы или кто-то другой исправит эту ошибку, можно оставить на карте примечания о проблеме и о том, как ее исправить.

 ![Карта кода &#45; комментирование и пометка элементов для отслеживания](../modeling/media/codemapstoryboardpaint12.png)

 Например, можно добавить комментарии на карту и отметить элементы с помощью цветов.

 ![Карта кода &#45; комментария и отмеченные элементы](../modeling/media/codemapstoryboardpaint12a.png)

 Если установлена программа Microsoft Outlook, можно отправить карту другим пользователям по электронной почте. Можно также экспортировать карту в виде изображения или в другом формате.

 ![Карта кода &#45; общую папку экспорта, почта](../modeling/media/codemapstoryboardpaint13.png)

## <a name="fix-the-problem-and-show-what-you-did"></a>Устранение проблемы и отображение сделанного
 Чтобы исправить ошибку, добавьте вызов `Repaint` в `undo`.

 ![Карта кода &#45; Добавление отсутствующего вызова метода](../modeling/media/codemapstoryboardpaint14.png)

 Чтобы убедиться, что ошибка исправлена, перезапустите сеанс отладки и попробуйте воспроизвести ошибку. Теперь команда **отменить последнюю линию** работает должным образом и подтверждает внесенные правильным решением.

 ![Карта кода &#45; подтверждение исправления кода](../modeling/media/codemapstoryboardpaint15.png)

 Можно обновить карту для отображения внесенного исправления.

 ![Карта кода &#45; обновление карты с учетом отсутствующего вызова метода](../modeling/media/codemapstoryboardpaint16.png)

 Теперь на карте отображается связь между **отменить** и **перерисовать**.

 ![Карта кода &#45; обновленная карта с вызовом метода](../modeling/media/codemapstoryboardpaint17.png)

> [!NOTE]
>  При обновлении карты можно увидеть сообщение об обновлении индекса кода, используемого для создания карты. Это значит, что кто-то изменил код, в результате чего ваша карта не соответствует текущему коду. Это не помешает обновить карту, однако может потребоваться заново создать карту, чтобы убедиться, что она соответствует коду.

 После завершения работы с расследования. Вы успешно нашли и устранили проблему путем сопоставления кода. Также у вас есть карта, с помощью которой можно переходить по коду, вспоминать предыдущие действия и просматривать действия, предпринятые для решения проблемы.

## <a name="see-also"></a>См. также

- [Сопоставление методов в стеке вызовов при отладке](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)
- [Визуализация кода](../modeling/visualize-code.md)
