---
title: 'Практическое: создание ассоциаций файлов для приложения ClickOnce | Документация Майкрософт'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- file associations, ClickOnce applications
- ClickOnce deployment, file associations
ms.assetid: 835230c8-3177-440f-85e3-e40f1d8b4f9d
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3bcffae0cadfb5973b532fcca5b0356eba004762
ms.sourcegitcommit: 0e5289414d90a314ca0d560c0c3fe9c88cb2217c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/19/2018
ms.locfileid: "39152699"
---
# <a name="how-to-create-file-associations-for-a-clickonce-application"></a>Практическое: создание ассоциаций файлов для приложения ClickOnce
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] приложения могут быть связан один или несколько расширений имен файлов, так что приложение будет запускаться автоматически при открытии файла этих типов. Добавление поддержки расширения имени файла для [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] приложения прост.  
  
### <a name="to-create-file-associations-for-a-clickonce-application"></a>Создание ассоциаций файлов для приложения ClickOnce  
  
1.  Создание [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] приложения обычно или использовать имеющуюся [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] приложения.  
  
2.  Откройте манифест приложения в текстовом редакторе или редакторе XML, например в блокноте.  
  
3.  Найдите элемент `assembly`. Дополнительные сведения см. в разделе [манифест приложения ClickOnce](../deployment/clickonce-application-manifest.md).  
  
4.  Как дочерний `assembly` элемента, добавьте `fileAssociation` элемент. `fileAssociation` Элемент имеет четыре атрибута:  
  
    -   `extension`: Расширение имени файла, который вы хотите связать с приложением.  
  
    -   `description`: Описание типа файла, который будет отображаться в оболочке Windows.  
  
    -   `progid`: Строка, однозначно определяющая тип файла, чтобы пометить его в реестре.  
  
    -   `defaultIcon`: Значок, используемый для этого типа файлов. Значок должен быть добавлен как файловый ресурс в манифесте приложения. Для получения дополнительной информации см. [Практическое руководство. Включение файла данных в приложение ClickOnce](../deployment/how-to-include-a-data-file-in-a-clickonce-application.md).  
  
     Пример `file` и `fileAssociation` элементов, см. в разделе [ \<fileAssociation > элемент](../deployment/fileassociation-element-clickonce-application.md).  
  
5.  Если вы хотите связать с приложением более чем один тип файлов, добавьте дополнительные `fileAssociation` элементов. Обратите внимание, что `progid` атрибут должен быть уникальным для каждого.  
  
6.  После завершения работы в манифесте приложения, повторно подпишите манифест. Можно сделать это из командной строки с помощью *Mage.exe*.  
  
     `mage -Sign WindowsFormsApp1.exe.manifest -CertFile mycert.pfx`  
  
     Дополнительные сведения см. в разделе [Mage.exe (средство редактирования и создания)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)  
  
## <a name="see-also"></a>См. также  
 [\<fileAssociation > элемент](../deployment/fileassociation-element-clickonce-application.md)   
 [Манифест приложения ClickOnce](../deployment/clickonce-application-manifest.md)   
 [Mage.exe (средство создания и редактирования манифеста)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)