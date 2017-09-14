---
title: "Обновление и перенос решений Office"
ms.custom: ""
ms.date: "02/02/2017"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "office-development"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "приложения Office [разработка решений Office в Visual Studio], обновление"
  - "проекты Office [разработка решений Office в Visual Studio], обновление"
  - "обновление приложений [разработка решений Office в Visual Studio]"
  - "обновление решений Office в Visual Studio"
  - "перенос решений Office в Visual Studio"
ms.assetid: cc60cdcb-593d-498a-8358-f1f3ac673fe1
caps.latest.revision: 105
author: "kempb"
ms.author: "kempb"
manager: "ghogen"
caps.handback.revision: 101
---
# Обновление и перенос решений Office
  Если проект Microsoft Office был создан в более ранней версии Visual Studio, его необходимо обновить для использования в текущей версии Visual Studio. Чтобы обновить проект Microsoft Office, откройте его в версии Visual Studio, имеющей в своем составе инструменты разработчика Microsoft Office. Дополнительные сведения о версиях Visual Studio, имеющих в составе Инструменты разработчика Microsoft Office, см. в разделе [Настройка компьютера для разработки решений Office](../vsto/configuring-a-computer-to-develop-office-solutions.md).  
  
> [!NOTE]  
>  Visual Studio не может обновлять проекты шаблонов форм InfoPath, созданные с помощью предыдущих версий Visual Studio. Проекты этого типа в текущей версии Visual Studio не поддерживаются.  
  
## Изменения в обновленных проектах  
 При обновлении проекта Microsoft Office среда Visual Studio вносит изменения в проект, чтобы обеспечить ориентацию на следующие элементы:  
  
-   Среда выполнения набора средств Visual Studio 2010 для Office Дополнительные сведения см. в разделе [Общие сведения об инструментах Visual Studio для среды выполнения Office](../vsto/visual-studio-tools-for-office-runtime-overview.md).  
  
-   Ссылки текущей сборки.  
  
-   Версия платформы .NET Framework, поддерживаемая типом проекта \(только при обновлении до Visual Studio 2013\).  
  
-   Версия Microsoft Office, поддерживаемая типом проекта \(только при обновлении до Visual Studio 2013\).  
  
## Ссылки на сборки  
 Visual Studio обновляет следующие ссылки на сборки в проекте:  
  
-   Основные сборки взаимодействия Microsoft Office \(PIA\).  
  
-   Сборки в [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]. Дополнительные сведения об этих сборках см. в разделе [Общие сведения об инструментах Visual Studio для среды выполнения Office](../vsto/visual-studio-tools-for-office-runtime-overview.md).  
  
-   Новые или обновленные версии зависимых сборок.  
  
## Версия .NET Framework, на которую производится ориентация  
 При обновлении проекта до Visual Studio 2013 среда Visual Studio вносит изменения в проект, чтобы ориентироваться на [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] или [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]. Версия платформы .NET Framework, на которую производится ориентация проекта, зависит от того, какая версия Office установлена на компьютере. Если установлена [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)], Visual Studio ориентирует проект на [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]. В противном случае Visual Studio ориентирует проект на [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)].  
  
> [!NOTE]  
>  При запуске переориентированного решения на компьютере разработчика или конечного пользователя могут потребоваться некоторые дополнительные действия. Кроме того, проект может перестать компилироваться, если в нем используются некоторые функции. Для получения дополнительной информации см. [Перенос решений Office на платформу .NET Framework 4 или более поздней версии](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md).  
  
 Если вы ориентируете проект Office на [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] или более позднюю версию, то можете использовать некоторые функции, недоступные для .NET Framework 3.5. Для получения дополнительной информации см. [Проектирование и создание решений Office](../vsto/designing-and-creating-office-solutions.md).  
  
## Ориентированное приложение Office  
 При обновлении проекта Office до Visual Studio 2013 среда Visual Studio ориентирует проект на версию Microsoft Office, поддерживаемую типом проекта, например проектом настройки на уровне документа или проектом надстройки VSTO.  
  
 Проекты Office в Visual Studio 2013 могут ориентироваться на приложения [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] и [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]. Visual Studio изменяет проект с целью ориентации на последнюю установленную версию Office. Если ни одна из этих версий Office не установлена, Visual Studio не обновляет проект.  
  
> [!NOTE]  
>  При обновлении проекта надстройки VSTO для ориентации на [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] или более позднюю версию убедитесь в том, что обработчик событий `ThisAddIn_Startup` надстройки VSTO не содержит код, обращающийся к документу в приложении. Для получения дополнительной информации см. [Обращение к документу при запуске приложения Office](../vsto/programming-vsto-add-ins.md#AccessingDocuments).  
  
 При настройке на уровне документа [!INCLUDE[vs_current_short](../sharepoint/includes/vs-current-short-md.md)] преобразует документы проекта, имеющие двоичный формат, например документы с расширениями XLS или DOC, в формат Office Open XML. Подробнее об Open XML см. в статье [Общие сведения о новых расширениях имен файлов и форматах Open XML](https://support.office.com/en-nz/article/Introduction-to-new-file-name-extensions-eca81dcb-5626-4e5b-8362-524d13ae4ec1).  
  
> [!NOTE]  
>  Не рекомендуется использовать смарт\-теги в Excel 2010 и Word 2010. Таким образом, если в решении используются смарт\-теги, их необходимо удалить перед началом тестирования и отладки в Visual Studio 2013 или Visual Studio 2015.  
  
## Обновление проектов Microsoft Office 2003  
 При обновлении настроек на уровне документа и надстроек VSTO, предназначенных для Microsoft Office 2003, необходимо учитывать дополнительные факторы.  
  
### Проекты уровня документа  
 Если документ в проекте содержит элементы управления Windows Forms, то перед обновлением проекта необходимо убедиться, что установлена среда выполнения набора средств Visual Studio 2005 для Office \(второй выпуск\). Если эта версия среды выполнения не будет установлена на компьютере разработчика перед обновлением проекта, то обновленный проект может содержать ошибки компиляции или ошибки времени выполнения. После завершения обновления проекта можно удалить среду выполнения набора средств Visual Studio 2005 для Office \(второй выпуск\) с компьютера разработчика, если она не используется другими решениями Office. Эта версия среды выполнения доступна в виде распространяемого пакета в Центре загрузки Майкрософт на странице [Среда выполнения набора средств Microsoft Visual Studio 2005 для Office \(второй выпуск\) \(VSTO 2005 SE\) \(x86\)](http://go.microsoft.com/fwlink/?linkid=49612).  
  
### Проекты надстроек VSTO  
 Если файл решения для исходного проекта содержал проект установки или проект InstallShield Limited Edition, настроенный на установку надстройки VSTO, среда Visual Studio обновляет проект, но не вносит в него никаких изменений. Если вы хотите продолжать использовать файл установщика Windows для развертывания надстройки VSTO, необходимо внести в проект установки или проект InstallShield Limited Edition изменения, касающиеся установки новых необходимых компонентов, таких как [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)], среда выполнения набора средств Visual Studio 2010 для Office и, при необходимости, основных сборок взаимодействия, на которые есть ссылки в надстройке VSTO. Для получения дополнительной информации см. [Развертывание решения Office с помощью установщика Windows](../vsto/deploying-an-office-solution-by-using-windows-installer.md).  
  
 Если вы хотите использовать ClickOnce для развертывания надстройки VSTO, можно полностью удалить проект установки или проект InstallShield Limited Edition. Дополнительные сведения о развертывании надстроек VSTO с использованием ClickOnce см. в разделе [Развертывание решения Office](../vsto/deploying-an-office-solution.md).  
  
## См. также  
 [Практическое руководство. Обновление решений Office](http://msdn.microsoft.com/ru-ru/a269e539-b717-4680-a568-2152b070347e)   
 [Перенос решений Office на платформу .NET Framework 4 или более поздней версии](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)   
 [Обновление проекта. Диалоговое окно "Параметры"](../vsto/project-upgrade-options-dialog-box.md)  
  
  