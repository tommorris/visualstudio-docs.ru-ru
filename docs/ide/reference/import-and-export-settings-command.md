---
title: Импорт и экспорт параметров - команда
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- Tools.ImportandExportSettings
helpviewer_keywords:
- Tools.ImportandExportSettings
- Import and Export Settings command
ms.assetid: 94a06468-a44d-403d-a931-77bbc9d06e56
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 4119abf74281e3c0dbb2b3d5f3ef472a0527a08f
ms.sourcegitcommit: fe5a72bc4c291500f0bf4d6e0778107eb8c905f5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/07/2018
ms.locfileid: "33704591"
---
# <a name="import-and-export-settings-command"></a>Импорт и экспорт параметров - команда
Импортирует, экспортирует или сбрасывает параметры [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)].

## <a name="syntax"></a>Синтаксис

```cmd
Tools.ImportandExportSettings [/export:filename | /import:filename | /reset]
```

## <a name="switches"></a>Переключатели
 /export:`filename`

 Необязательный. Экспортирует текущие параметры в указанный файл

 /import:`filename`

 Необязательный. Импортирует текущие параметры в указанный файл

 /reset

 Необязательный. Сбрасывает текущие параметры

## <a name="remarks"></a>Примечания

Выполнение этой команды без параметров командной строки открывает мастер **Импорт и экспорт параметров**. Дополнительные сведения см. в описании [синхронизированных параметров](../../ide/synchronized-settings-in-visual-studio.md).

## <a name="example"></a>Пример

Следующая команда экспортирует текущие параметры в файл `MyFile.vssettings`.

```cmd
Tools.ImportandExportSettings /export:"c:\Files\MyFile.vssettings"
```

## <a name="see-also"></a>См. также

- [Персонализация интегрированной среды разработки Visual Studio](../../ide/personalizing-the-visual-studio-ide.md)
- [Команды Visual Studio](../../ide/reference/visual-studio-commands.md)