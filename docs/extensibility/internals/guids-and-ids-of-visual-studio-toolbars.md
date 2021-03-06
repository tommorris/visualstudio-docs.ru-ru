---
title: Идентификаторы GUID и идентификаторы панелей инструментов Visual Studio | Документация Майкрософт
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- visual studio groups
- toolbars
- visual studio toolbar
- id
- toolgar group
- tool window toolbar
- guid
ms.assetid: c9cacd57-9225-450f-a9ac-cbf3168ea844
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 6982835b9d3b6259a47439dbe7b1b9252edc3dbe
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2018
ms.locfileid: "39499010"
---
# <a name="guids-and-ids-of-visual-studio-toolbars"></a>Идентификаторы GUID и идентификаторы Visual Studio панелей инструментов
В этом разделе перечисляются значения GUID и идентификатор панели инструментов, включенных в среде разработки Visual Studio (IDE) и групп они содержат. Эти значения определены в *.vsct* файлы, которые устанавливаются как часть Visual Studio SDK. Дополнительные сведения см. в разделе [команды, определенные в интегрированной среде разработки, меню и групп](../../extensibility/internals/ide-defined-commands-menus-and-groups.md).  
  
> [!NOTE]
>  Многие из панели инструментов, доступные в Visual Studio не определены, Visual Studio, а также их GUID и идентификатор значения не являются открытыми. В этом разделе перечислены только панели инструментов, которые определены в пакете SDK для Visual Studio *.vsct* файлов.  
  
 Дополнительные сведения о том, как работать с объектами интегрированной среды разработки, которые определены в *.vsct* файлы, см. в разделе [расширить меню и команд](../../extensibility/extending-menus-and-commands.md).  
  
 Панели инструментов по умолчанию, предоставляемые Visual Studio IDE используйте GUID `guidSHLMainMenu`, за исключением случаев, указано с помощью `GUID:ID` синтаксис.  
  
## <a name="ide-toolbars"></a>Панели инструментов IDE  
 Следующие панели инструментов, предоставляемых Visual Studio IDE. Можно отобразить, выбрав их на панели инструментов **панелей инструментов** подменю **средства** меню. Панели инструментов окна инструментов не включаются в этом разделе.  
  
 Только группы можно полученные непосредственно из панели инструментов. Чтобы добавить группу, установите его родительского GUID и идентификатор панели инструментов. Чтобы добавить кнопку на панель инструментов, присвоить его родительского группы на панели инструментов.  
  
|Toolbar|ID|  
|-------------|--------|  
|Стандартный|IDM_VS_TOOL_STANDARD|  
|Построить|IDM_VS_TOOL_BUILD|  
|Текстовый редактор|IDM_VS_TOOL_TEXTEDITOR|  
|Отладка|guidVSDebugGroup:IDM_DEBUG_TOOLBAR|  
|Место отладки|guidVSDebugGroup:IDM_DEBUG_CONTEXT_TOOLBAR|  
  
### <a name="special-toolbars"></a>Специальные панели инструментов  
 Эти панели инструментов определяются с помощью Visual Studio IDE, но они будут выполнять специализированные функции и не размещайте группы команд.  
  
|Toolbar|ID|  
|-------------|--------|  
|Команда Add|IDM_VS_TOOL_ADDCOMMAND|  
|Не определено|IDM_VS_TOOL_UNDEFINED|  
|XML-схемы|IDM_VS_TOOL_SCHEMA|  
|данные XML|IDM_VS_TOOL_DATA|  
  
## <a name="groups-on-the-ide-toolbars"></a>Группы на панели инструментов интегрированной среды разработки  
 Чтобы добавить кнопку на стандартной панели инструментов, задайте одно из следующих групп с родительским. Группы сортируются по родительской панели инструментов.  
  
### <a name="standard-toolbar-groups"></a>Стандартная панель инструментов группы  
  
|name|ID|  
|----------|--------|  
|Сохранение и открытие|IDG_VS_TOOLSB_SAVEOPEN|  
|Вырезания или копирования данных|IDG_VS_TOOLSB_CUTCOPY|  
|Отменить/Повторить|IDG_VS_TOOLSB_UNDOREDO|  
|Запуск/Build|IDG_VS_TOOLSB_RUNBUILD|  
|Поиск|IDG_VS_TOOLSB_SEARCH|  
|Windows|IDG_VS_TOOLSB_WINDOWS|  
|Новые окна|IDG_VS_TOOLSB_NEWWINDOWS|  
|Загрузки или сохранения|IDG_VS_WINDOWUI_LOADSAVE|  
|Датчик|IDG_VS_TOOLSB_GAUGE|  
  
### <a name="build-toolbar-groups"></a>Формировать группы панели инструментов  
  
|name|ID|  
|----------|--------|  
|Панель сборки|IDG_VS_BUILDBAR|  
|Отмена|IDG_VS_BUILD_CANCEL|  
  
### <a name="text-editor-toolbar-groups"></a>Группы панели инструментов текстового редактора  
  
|name|ID|  
|----------|--------|  
|Завершение|IDM_VS_TOOL_TEXTEDITOR|  
|Отступ|IDG_VS_EDITTOOLBAR_INDENT|  
|Комментарий|IDG_VS_EDITTOOLBAR_COMMENT|  
|Закладки|IDG_VS_EDITTOOLBAR_TEMPBOOKMARKS|  
  
### <a name="debug-toolbar-groups"></a>Отладка группы панели инструментов  
  
|name|ID|  
|----------|--------|  
|Выполнение|IDM_DEBUG_TOOLBAR|  
|Отладка по шагам|IDG_DEBUG_TOOLBAR_STEPPING|  
|Контрольное значение|IDG_DEBUG_TOOLBAR_WATCH|  
|Windows|IDG_DEBUG_TOOLBAR_WINDOWS|  
  
### <a name="debug-location-toolbar-groups"></a>Отладка расположение панели инструментов группы  
  
|name|ID|  
|----------|--------|  
|Место отладки|IDG_DEBUG_CONTEXT_TOOLBAR|  
  
## <a name="tool-window-toolbars"></a>Панели инструментов окна инструментов  
 Панели инструментов могут появляться непосредственно в интегрированной среде разработки или в окнах инструментов **обозревателе решений**. Так как окна инструментов не определены в *.vsct* файлы, панели инструментов окна инструментов не определили родительских элементов. Вместо этого они размещаются в коде. Следующая таблица показывает, панелей инструментов, которые отображаются в окнах инструментов в интегрированной среде разработки и группы команд, которые они содержат.  
  
> [!NOTE]
>  Панели инструментов и группы используют идентификатор GUID `guidSHLMainMenu`, за исключением случаев, указано с помощью синтаксиса GUID: ID. Там, где для панели инструментов указан идентификатор GUID, оно также применяется в группы, которые получены из панели инструментов.  
  
|Окно инструментов|Toolbar|Группы|  
|-----------------|-------------|------------|  
|обозреватель решений|IDM_VS_TOOL_PROJWIN|IDG_VS_PROJ_TOOLBAR1... 5|  
|обозревателя серверов|guid_SE_MenuGroup:IDM_SE_TOOLBAR_SERVEREXPLORER|IDG_SE_TOOLBAR_REFRESH|  
|Свойства|IDM_VS_TOOL_PROPERTIES|IDG_VS_PROPERTIES_SORT<br /><br /> IDG_VS_PROPERTIES_PAGES|  
|Представление классов|IDM_VS_TOOL_CLASSVIEW|IDG_VS_CLASSVIEW_FOLDERS<br /><br /> IDG_VS_CLASSVIEW_SEARCH<br /><br /> IDG_VS_CLASSVIEW_SETTINGS|  
|Представление классов|IDM_VS_TOOL_CLASSVIEW_GO|IDG_VS_CLASSVIEW_SEARCH2|  
|Обозреватель объектов|IDM_VS_TOOL_OBJBROWSER|IDG_VS_OBJBROWSER_SUBSETS<br /><br /> IDG_VS_OBJBROWSER_SEARCH<br /><br /> IDG_VS_OBJBROWSER_ADDREFERENCE<br /><br /> IDG_VS_OBJBROWSER_BROWSERSETTINGS|  
|Обозреватель объектов|IDM_VS_TOOL_OBJECT_BROWSER_GO|IDG_VS_OBJBROWSER_SEARCH2|  
|Вывод|IDM_VS_TOOL_OUTPUTWINDOW|IDG_VS_OUTPUTWINDOW_SELECT<br /><br /> IDG_VS_OUTPUTWINDOW_GOTO<br /><br /> IDG_VS_OUTPUTWINDOW_NEXTPREV<br /><br /> IDG_VS_OUTPUTWINDOW_CLEAR<br /><br /> IDG_VS_OUTPUTWINDOW_WORDWRAP|  
|Поиск и замена|IDM_VS_TOOL_UNIFIEDFIND|IDG_VS_FINDTAB<br /><br /> IDG_VS_REPLACETAB|  
|Результаты поиска 1|IDM_VS_TOOL_FINDRESULTS1|IDG_VS_FINDRESULTS1_GOTO<br /><br /> IDG_VS_FINDRESULTS1_NEXTPREV<br /><br /> IDG_VS_FINDRESULTS1_CLEAR<br /><br /> IDG_VS_FINDRESULTS1_STOPFIND|  
|Результаты поиска 2|IDM_VS_TOOL_FINDRESULTS2|IDG_VS_FINDRESULTS2_GOTO<br /><br /> IDG_VS_FINDRESULTS2_NEXTPREV<br /><br /> IDG_VS_FINDRESULTS2_CLEAR<br /><br /> IDG_VS_FINDRESULTS2_STOPFIND|  
|Фрагмент кода|IDM_VS_TOOL_SNIPPETMENUS|IDG_VS_SNIPPET_REPL<br /><br /> IDG_VS_SNIPPET_REF<br /><br /> IDG_VS_SNIPPET_PROP|  
|Закладки|IDM_VS_TOOL_BOOKMARKWIND|IDG_VS_BWNEWFOLDER<br /><br /> IDG_VS_BWNEXTBM<br /><br /> IDG_VS_BWNEXTBMF<br /><br /> IDG_VS_BWENABLE<br /><br /> IDG_VS_BWDELETE|  
|список задач|IDM_VS_TOOL_TASKLIST|IDG_VS_TASKLIST_PROVIDERLIST|  
|Задачи пользователя|IDM_VS_TOOL_USERTASKS|IDG_VS_TASKLIST_PROVIDERLIST<br /><br /> IDG_VS_USERTASKS_EDIT|  
|Список ошибок|IDM_VS_TOOL_ERRORLIST|IDG_VS_ERRORLIST_ERRORGROUP<br /><br /> IDG_VS_ERRORLIST_WARNINGGROUP<br /><br /> IDG_VS_ERRORLIST_MESSAGEGROUP|  
|Обозреватель вызовов|IDM_VS_TOOL_CALLBROWSER1... 16|IDG_VS_TOOLBAR_CALLBROWSER1_ACTIONS<br /><br /> IDG_VS_TOOLBAR_CALLBROWSER1_TYPE<br /><br /> IDG_VS_TOOLBAR_CALLBROWSER1_CBSETTINGS|  
|Точки останова|guidVSDebugGroup:IDM_BREAKPOINTS_WINDOW_TOOLBAR|IDG_BREAKPOINTS_WINDOW_NEW<br /><br /> IDG_BREAKPOINTS_WINDOW_DELETE<br /><br /> IDG_BREAKPOINTS_WINDOW_ALL<br /><br /> IDG_BREAKPOINTS_WINDOW_VIEW<br /><br /> IDG_BREAKPOINTS_WINDOW_EDIT<br /><br /> IDG_BREAKPOINTS_WINDOW_COLUMNS|  
|Дизассемблированный код|guidVSDebugGroup:IDM_DISASM_WINDOW_TOOLBAR|IDG_DISASM_WINDOW_TOOLBAR|  
|Память 1 – 4|guidVSDebugGroup:IDM_MEMORY_WINDOW_TOOLBAR1... 4|IDG_MEMORY_EXPRESSION1... 4<br /><br /> IDG_MEMORY_COLUMNS1... 4|  
|Процессы|guidVSDebugGroup:IDM_ATTACHED_PROCS_TOOLBAR|IDG_ATTACHED_PROCS_EXECCNTRL IDG_ATTACHED_PROCS_STEPPING<br /><br /> IDG_ATTACHED_PROCS_EXECCNTRL2<br /><br /> IDG_ATTACHED_PROCS_ATTACH<br /><br /> IDG_ATTACHED_PROCS_COLUMNS|  
  
## <a name="see-also"></a>См. также  
 [Добавить контроллер меню в панели инструментов](../../extensibility/adding-a-menu-controller-to-a-toolbar.md)   
 [Добавление панели инструментов окна инструментов](../../extensibility/adding-a-toolbar-to-a-tool-window.md)   
 [Меню идентификаторы GUID и идентификаторы Visual Studio](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)