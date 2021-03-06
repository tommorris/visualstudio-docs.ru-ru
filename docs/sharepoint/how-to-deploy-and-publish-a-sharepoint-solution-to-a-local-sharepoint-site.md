---
title: 'Практическое: развертывание и публикация решения SharePoint на локальном сайте SharePoint | Документация Майкрософт'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- deploying [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, deploying
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: e288b5a284ca4155cf70f4458b5b490ca4289cbe
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/29/2018
ms.locfileid: "37119809"
---
# <a name="how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site"></a>Практическое: развертывание и публикация решения SharePoint на локальном сайте SharePoint
  Можно развернуть или публикации решений SharePoint на локальном сервере SharePoint на компьютере разработчика. Копии процесса развертывания *.wsp* файл на сервер SharePoint, устанавливает решение и активация компонентов. Публикация обрабатывать только копии *.wsp* файл на сервер SharePoint и устанавливает его. Необходимо вручную активировать его, чтобы включить эту функцию в SharePoint.  
  
## <a name="to-deploy-a-sharepoint-solution-to-the-local-sharepoint-server"></a>Для развертывания решения SharePoint на локальном сервере SharePoint  
  
1.  В **обозревателе решений**, выберите проект, который вы хотите развернуть.  
  
2.  В строке меню выберите **построения**, **развернуть решение**.  
  
     *.Wsp* файл создается и устанавливается на локальном сервере SharePoint. Кроме того активируются функции.  
  
## <a name="to-publish-a-sharepoint-solution-to-a-local-sharepoint-server"></a>Для публикации решения SharePoint на локальном сервере SharePoint  
  
1.  В **обозревателе решений**, откройте контекстное меню для проекта SharePoint, который требуется опубликовать, а затем выберите **публикации**.  
  
2.  В **публикации** диалоговом окне выберите **опубликовать в файловой системе** переключатель.  
  
3.  В **целевое расположение** текстовом поле введите локальный путь, а затем нажмите **публикации** кнопки.  
  
     Ход выполнения публикации отображается в Visual Studio **вывода** окна. После завершения процесса решения (*.wsp*) файл устанавливается на локальном сервере SharePoint. Тем не менее он еще необходимо активировать для использования в SharePoint. Если файл решения уже существует, происходит ошибка и запрашивает, следует ли перезаписать существующий файл. Сведения об обновлении пакета см. в разделе об обновлении удаленные пакеты в [как: развертывание, публикация и обновление решений SharePoint на удаленном сервере](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md).  
  
## <a name="see-also"></a>См. также
 [Практическое: развертывание, публикация и обновление решений SharePoint на удаленном сервере](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)   
 [Создание пакетов решений SharePoint](../sharepoint/creating-sharepoint-solution-packages.md)   
 [Практическое: Настройка пакета решения SharePoint](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)   
 [Практическое: Добавление и удаление компонентов и элементов в пакете с помощью конструктора пакетов](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)  
  
