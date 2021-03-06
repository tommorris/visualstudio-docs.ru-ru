---
title: Проверить значения переменных в окне "Видимые" и "Локальные" Windows | Документация Майкрософт
ms.custom: H1Hack27Feb2017
ms.date: 04/17/2017
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.autos
- vs.debug.locals
helpviewer_keywords:
- debugger, variable windows
- debugging [Visual Studio], variable windows
ms.assetid: bb6291e1-596d-4af0-9f22-5fd713d6b84b
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 956b3afe1308ee748ee9efa6292834754f7e8124
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2018
ms.locfileid: "42626474"
---
# <a name="inspect-variables-in-the-autos-and-locals-windows-in-visual-studio"></a>Проверить переменные в окне "Видимые" и "Локальные" Windows в Visual Studio
**"Видимые"** окна (во время отладки, **CTRL + ALT + V, A**, или **Отладка > Windows > видимые**) и **"Локальные"** окна (во время отладки **CTRL + ALT + V, L**, или **Отладка > Windows > "Локальные"**) являются весьма полезен, если вы хотите просмотреть значения переменных при отладке. В окне **Локальные** отображаются переменные, которые определены в локальной области, которой обычно является функция или метод, выполняемые в текущий момент. В окне **Видимые** отображаются переменные, используемые вокруг текущей строки (места, где остановилось выполнение отладчика). Точно переменных, которые будут отображаться в этом окне отличается на разных языках. См. раздел [What variables appear in the Autos Window?](#bkmk_whatvariables) ниже.  
  
Более подробную информацию об основных принципах отладки см. в разделе [Getting Started with the Debugger](../debugger/getting-started-with-the-debugger.md).  
  
## <a name="looking-at-objects-in-the-autos-and-locals-windows"></a>Просмотр объектов в окнах "Видимые" и "Локальные"  
Массивы и объекты отображаются в окнах "Видимые" и "Локальные" как элементы управления типа "дерево". Щелкните стрелку слева от имени переменной, чтобы развернуть представление и увидеть поля и свойства. Ниже приведен пример <xref:System.IO.FileStream?displayProperty=fullName> объекта в **"Локальные"** окна:  
  
![Локальные переменные&#45;FileStream](../debugger/media/locals-filestream.png "FileStream \"Локальные\"")  
  
## <a name="bkmk_whatvariables"></a> Какие переменные отображаются в окне "Видимые"?  
 Окно **Видимые** можно использовать в коде C#, Visual Basic и C++. Окно **Видимые** не поддерживает JavaScript и F#.  
  
 При использовании C# или Visual Basic в окне **Видимые** отображаются все переменные, используемые в текущей или предыдущей строках. Предположим, что вы объявили четыре переменных и задали их значения следующим образом:

```csharp
    public static void Main()
    {
       int a, b, c, d;
       a = 1;
       b = 2;
       c = 3;
       d = 4;
    }
```

 Если установить точку останова в строке `c = 3`и запустить отладчик, то после остановки выполнения окно **Видимые** будет выглядеть так:  

 ![Видимые&#45;CSharp](../debugger/media/autos-csharp.png "CSharp \"Видимые\"")  

 Обратите внимание на то, что значение `c` равно 0, так как строка `c = 3` еще не была выполнена.  

 При использовании C++ в окне **Видимые** отображаются переменные, которые используются по крайней мере в трех строках до текущей строки (строки, в которой выполнение остановилось). Предположим, вы объявили шесть переменных:

```C++
    void main() {
        int a, b, c, d, e, f;
        a = 1;
        b = 2;
        c = 3;
        d = 4;
        e = 5;
        f = 6;
    }
```

 Если установить точку останова в строке `e = 5;` и запустить отладчик, то после остановки выполнения окно **Видимые** будет выглядеть так:  
  
 ![Видимые&#45;Cplus](../debugger/media/autos-cplus.png "Cplus \"Видимые\"")  
  
 Обратите внимание на то, что переменная не инициализирована, так как код в строке `e = 5;` еще не выполнен.  
  
 При определенных условиях также можно увидеть возвращаемые значения функций и методов. См. раздел [View return values of method calls](#bkmk_returnValue) ниже.  
  
##  <a name="bkmk_returnValue"></a> View return values of method calls  
 В коде .NET и C++ можно просматривать возвращаемые значения при выполнении шага с обходом вызова метода или выходом из него. Эта функция полезна в ситуации, когда результат вызова метода не сохраняется в локальной переменной (например, в случае, когда метод используется в качестве параметра или возвращаемого значения другого метода).  
  
 Следующий код C# добавляет возвращаемые значения двух функций:  

```csharp
static void Main(string[] args)  
{  
    int a, b, c, d;  
    a = 1;  
    b = 2;  
    c = 3;  
    d = 4;  
    int x = sumVars(a, b) + subtractVars(c, d);  
}  
  
private static int sumVars(int i, int j)  
{  
    return i + j;  
}  
  
private static int subtractVars(int i, int j)  
{  
    return j - i;  
}  
```

 Установите точку останова на строке `int x = sumVars(a, b) + subtractVars(c, d);`.  
  
 Начните отладку и, когда выполнение остановится в первой точке останова, нажмите клавишу **F10 (шаг с обходом)**. Окно **Видимые** должно выглядеть так:  
  
 ![AutosReturnValueCSharp2](../debugger/media/autosreturnvaluecsharp2.png "AutosReturnValueCSharp2")  
  
## <a name="why-are-variable-values-sometimes-red-in-locals-and-autos-windows"></a>Почему значения переменных иногда выделяются красным цветом в окнах "Локальные" и "Видимые"?  
Иногда можно заметить, что значение переменной в окне **Локальные** или **Видимые** выделено красным цветом. Это означает, что значения изменились с момента последнего вычисления. Изменение могло произойти во время предыдущего сеанса отладки или быть внесено в окне.  
  
## <a name="changing-the-numeric-format-of-a-variable-window"></a>Изменение числового формата окна переменных  
По умолчанию используется десятичный числовой формат, но его можно изменить на шестнадцатеричный. Щелкните правой кнопкой мыши в окне **Локальные** или **Видимые** и выберите пункт **Шестнадцатеричный вывод**. Изменение распространяется на все окна отладчика.  
  
## <a name="editing-a-value-in-a-variable-window"></a>Изменение значения в окне переменной  
Вы можете изменять значения большинства переменных, отображаемых в окнах **Видимые**, **Локальные**, **Контрольные значения**и **быстрая проверка** . Информацию об окнах **Контрольные значения** и **Быстрая проверка** см. в разделе [Watch and QuickWatch Windows](../debugger/watch-and-quickwatch-windows.md). Просто дважды щелкните значение, которое нужно изменить, и введите новое значение.  
  
В качестве значения можно ввести выражение, например `a + b`. Отладчик принимает большинство допустимых выражений языка.  
  
При работе с машинным кодом C++ может потребоваться определить контекст имени переменной. Для получения дополнительной информации см. [Context Operator (C++)](../debugger/context-operator-cpp.md).  
 
Однако при изменении значений следует соблюдать осторожность. Некоторые из возможных причин:  
  
-   Вычисление некоторых выражений может привести к изменению значения некоторой переменной или иным образом повлиять на состояние программы. Например, вычисление `var1 = ++var2` изменяет значения `var1` и `var2`.  
  
     Выражения, которые изменяют данные, — это [выражения с побочными эффектами](https://en.wikipedia.org/wiki/Side_effect_\(computer_science\)). Они могут привести к непредсказуемым результатам, если не учитывать возможные последствия их выполнения. Перед внесением такого изменения нужно оценить его последствия.  
  
-   Изменение значений с плавающей запятой может привести к незначительной погрешности, связанной с преобразованием дробных компонентов из десятичной формы в двоичную. Даже внешне кажущееся безвредным редактирование может привести к изменениям некоторых младших разрядов переменной с плавающей запятой.  
  
## <a name="changing-the-window-context"></a>Изменение контекста окна  
Можно использовать **место отладки** инструментов для выбора нужной функции, потока или процесса, который изменяет контекст для окна переменных. Задайте точку останова и начните отладку. (Если эта панель инструментов не отображается, включите ее, щелкнув в пустой области панели инструментов. Должен появиться список панелей инструментов. Выберите панель **Место отладки**). При достижении точки останова выполнение останавливается и вы можете см. в разделе панели инструментов "Место отладки", являющийся нижней строке ниже.
  
![DebugLocationToolbar](../debugger/media/debuglocationtoolbar.png "DebugLocationToolbar")   
  
## <a name="see-also"></a>См. также  
 [Окна отладчика](../debugger/debugger-windows.md)
