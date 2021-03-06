---
title: 'Практическое: программное сохранение документов Visio'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], saving Visio documents
- Visio [Office development in Visual Studio], saving Visio documents
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 4171f0237b7735748da567bd9482856c013759bc
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/06/2018
ms.locfileid: "35675108"
---
# <a name="how-to-programmatically-save-visio-documents"></a>Практическое: программное сохранение документов Visio
  Существует несколько способов сохранения документов Microsoft Office Visio.  
  
-   Сохранение изменений в существующем документе.  
  
-   Сохранение нового документа или сохранение документа с новым именем.  
  
-   Сохранение документ с заданными аргументами.  
  
 Дополнительные сведения см. в справочной документации VBA для метода [Microsoft.Office.Interop.Visio.Document.Save](https://msdn.microsoft.com/library/office/ff766478.aspx) , метода [Microsoft.Office.Interop.Visio.Document.SaveAs](https://msdn.microsoft.com/library/office/ff765824.aspx) и метода [Microsoft.Office.Interop.Visio.Document.SaveAsEx](https://msdn.microsoft.com/library/office/ff768149.aspx) .  
  
## <a name="save-an-existing-document"></a>Сохранение существующего документа  
  
### <a name="to-save-a-document"></a>Сохранение документа  
  
-   Вызовите `Microsoft.Office.Interop.Visio.Document.Save` метод `Microsoft.Office.Tools.Visio.Document` класса документа, который был ранее сохранен.  
  
     Чтобы использовать этот пример кода, запустите его из класса `ThisAddIn` в своем проекте.  
  
    > [!NOTE]  
    >  `Microsoft.Office.Interop.Visio.Document.Save` Метод вызывает исключение, если новый документ Visio еще не сохранен.  
  
     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#11](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#11)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#11](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#11)]  
  
## <a name="save-a-document-with-a-new-name"></a>Сохранение документа с новым именем  
 Используйте `Microsoft.Office.Interop.Visio.Document.SaveAs` метод для сохранения нового документа или документа с новым именем. Этот метод требует указания нового имени файла.  
  
### <a name="to-save-the-active-visio-document-with-a-new-name"></a>Сохранение активного документа Visio с новым именем  
  
-   Вызовите `Microsoft.Office.Interop.Visio.Document.SaveAs` метод `Microsoft.Office.Tools.Visio.Document` вы хотите сохранить, используя полный путь, включая имя файла. Если файл с таким именем уже существует в этой папке, он будет перезаписан без запроса подтверждения.  
  
     Чтобы использовать этот пример кода, запустите его из класса `ThisAddIn` в своем проекте.  
  
     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#10](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#10)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#10](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#10)]  
  
## <a name="save-a-document-with-a-new-name-and-specified-arguments"></a>Сохранение документа с новым именем и заданными аргументами  
 Используйте `Microsoft.Office.Interop.Visio.Document.SaveAsEx` метод, чтобы сохранить документ с новым именем и задайте любые допустимые аргументы для применения к документу.  
  
### <a name="to-save-document-with-a-new-name-and-specified-arguments"></a>Сохранение документа с новым именем и заданными аргументами  
  
-   Вызовите `Microsoft.Office.Interop.Visio.Document.SaveAsEx` метод `Microsoft.Office.Tools.Visio.Document` вы хотите сохранить, используя полный путь, включая имя файла. Если файл с таким именем уже существует в этой папке, возникает исключение.  
  
     В следующем примере кода выполняется сохранение активного документа с новым именем, пометка его как доступного только для чтения и отображение этого документа в списке последних использовавшихся документов. Чтобы использовать этот пример кода, запустите его из класса `ThisAddIn` в своем проекте.  
  
     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#12](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#12)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#12](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#12)]  
  
## <a name="compile-the-code"></a>Компиляция кода  
 Для этого примера кода требуется следующее.  
  
-   Для сохранения документа с новым именем, каталог с именем `Test` должен быть расположен в *Мои документы* папки (для Windows XP и более ранних версий) или *документов* папки (для Windows Vista).  
  
## <a name="see-also"></a>См. также  
 [Решения Visio](../vsto/visio-solutions.md)   
 [Обзор объектной модели Visio](../vsto/visio-object-model-overview.md)   
 [Практическое: программное создание документов Visio](../vsto/how-to-programmatically-create-new-visio-documents.md)   
 [Как: открытие документов Visio](../vsto/how-to-programmatically-open-visio-documents.md)   
 [Практическое: программное закрытие документов Visio](../vsto/how-to-programmatically-close-visio-documents.md)   
 [Практическое: программная печать документов Visio](../vsto/how-to-programmatically-print-visio-documents.md)  
  
  