---
title: 'Практическое: программное добавление строк и столбцов в таблицы Word'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- rows [Office development in Visual Studio], adding to Word tables
- tables [Office development in Visual Studio], adding rows and columns
- columns [Office development in Visual Studio], adding to Word tables
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 865a33e181d761665dbe2e44976f171a2b60d433
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/11/2018
ms.locfileid: "35255893"
---
# <a name="how-to-programmatically-add-rows-and-columns-to-word-tables"></a>Практическое: программное добавление строк и столбцов в таблицы Word
  В таблице Microsoft Office Word ячейки организованы по строкам и столбцам. Вы можете использовать метод <xref:Microsoft.Office.Interop.Word.Rows.Add%2A> объекта <xref:Microsoft.Office.Interop.Word.Rows> для добавления строк в таблицу и метод <xref:Microsoft.Office.Interop.Word.Columns.Add%2A> объекта <xref:Microsoft.Office.Interop.Word.Columns> для добавления столбцов.  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
## <a name="document-level-customization-examples"></a>Примеры настройки уровня документа  
 Следующие примеры кода можно использовать в настройке на уровне документа. Чтобы использовать эти примеры, выполняйте их из класса `ThisDocument` в своем проекте. В этих примерах предполагается, что документ, связанный с настройкой, уже содержит по крайней мере одну таблицу.  
  
> [!IMPORTANT]  
>  Этот код выполняется только в тех проектах, которые создаются с помощью любого из следующих шаблонов проекта:  
>   
> -   Документ Word 2013  
> -   Шаблон Word 2013  
> -   Документ Word 2010  
> -   Шаблон Word 2010  
>   
>  Если вы хотите выполнить эту задачу в проекте любого другого типа, необходимо добавить ссылку на **Microsoft.Office.Interop.Word** сборки, а затем использовать классы из этой сборки для добавления строк и столбцов для таблицы. Дополнительные сведения см. в разделе [как: Target Office приложений с помощью основных сборок взаимодействия](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md) и [Справочник по основной сборке взаимодействия Word 2010](http://go.microsoft.com/fwlink/?LinkId=189588).  
  
### <a name="to-add-a-row-to-a-table"></a>Добавление строки в таблицу  
  
1.  Используйте метод <xref:Microsoft.Office.Interop.Word.Rows.Add%2A>, чтобы добавить строку в таблицу.  
  
     [!code-vb[Trin_VstcoreWordAutomation#95](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#95)]
     [!code-csharp[Trin_VstcoreWordAutomation#95](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#95)]  
  
### <a name="to-add-a-column-to-a-table"></a>Добавление столбца в таблицу  
  
1.  Используйте метод <xref:Microsoft.Office.Interop.Word.Columns.Add%2A>, а затем метод <xref:Microsoft.Office.Interop.Word.Columns.DistributeWidth%2A>, чтобы сделать все столбцы одинаковой ширины.  
  
     [!code-vb[Trin_VstcoreWordAutomation#96](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#96)]
     [!code-csharp[Trin_VstcoreWordAutomation#96](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#96)]  
  
## <a name="vsto-add-in-examples"></a>Примеры надстройки VSTO  
 Следующие примеры кода можно использовать в надстройке VSTO. Чтобы использовать эти примеры, выполняйте их из класса `ThisAddIn` в своем проекте. В этих примерах предполагается, что активный документ содержит хотя бы одну таблицу.  
  
> [!IMPORTANT]  
>  Этот код выполняется только в тех проектах, которые создаются с помощью шаблонов Word VSTO.  
>   
>  Если вы хотите выполнить эту задачу в проекте любого другого типа, необходимо добавить ссылку на **Microsoft.Office.Interop.Word** сборки, а затем использовать классы из этой сборки для добавления строк и столбцов для таблицы. Дополнительные сведения см. в разделе [как: Target Office приложений с помощью основных сборок взаимодействия](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md) и [Справочник по основной сборке взаимодействия Word 2010](http://go.microsoft.com/fwlink/?LinkId=189588).  
  
### <a name="to-add-a-row-to-a-table"></a>Добавление строки в таблицу  
  
1.  Используйте метод <xref:Microsoft.Office.Interop.Word.Rows.Add%2A>, чтобы добавить строку в таблицу.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#95](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#95)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#95](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#95)]  
  
### <a name="to-add-a-column-to-a-table"></a>Добавление столбца в таблицу  
  
1.  Используйте метод <xref:Microsoft.Office.Interop.Word.Columns.Add%2A>, а затем метод <xref:Microsoft.Office.Interop.Word.Columns.DistributeWidth%2A>, чтобы сделать все столбцы одинаковой ширины.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#96](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#96)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#96](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#96)]  
  
## <a name="see-also"></a>См. также  
 [Практическое: программное создание таблиц Word](../vsto/how-to-programmatically-create-word-tables.md)   
 [Практическое: программное добавление текста и форматирования в ячейки таблиц Word](../vsto/how-to-programmatically-add-text-and-formatting-to-cells-in-word-tables.md)   
 [Практическое: программное заполнение таблиц Word свойствами документа](../vsto/how-to-programmatically-populate-word-tables-with-document-properties.md)  
  
  