---
title: 'Практическое: программное исключение знаков абзаца при создании диапазонов'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], excluding paragraphs
- ranges, excluding paragraph marks in Word
- documents [Office development in Visual Studio], paragraph marks
- paragraphs, controlling structure
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 11015f0afb59f0d1aa71bad4adbc48b6c99887a2
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/06/2018
ms.locfileid: "35673929"
---
# <a name="how-to-programmatically-exclude-paragraph-marks-when-creating-ranges"></a>Практическое: программное исключение знаков абзаца при создании диапазонов
  При каждом создании объекта <xref:Microsoft.Office.Interop.Word.Range> на основе абзаца все непечатаемые символы, такие как знаки абзаца, включаются в диапазон. Можно вставить текст из исходного абзаца в целевой абзац. Если вы не хотите разделять целевой абзац на отдельные абзацы, то необходимо сначала удалить знаки абзаца из исходного абзаца. Кроме того, поскольку сведения о форматировании абзаца хранятся в знаке абзаца, вы можете не захотеть включать их при вставке диапазона в существующий абзац.  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
 В приведенной ниже процедуре объявляются две строковые переменные, извлекается содержимое первого и второго абзаца в активном документе, а потом их содержимое обменивается. Затем в примере демонстрируется удаление знака абзаца из диапазона с помощью метода <xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A> и вставка текста в абзаце.  
  
## <a name="to-control-paragraph-structure-when-inserting-text"></a>Управление структурой абзаца при вставке текста  
  
1.  Создайте две переменные диапазона для первого и второго абзаца и извлеките их содержимое при помощи свойства <xref:Microsoft.Office.Interop.Word.Range.Text%2A> .  
  
     Следующий пример кода можно использовать в настройке на уровне документа.  
  
     [!code-vb[Trin_VstcoreWordAutomation#27](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#27)]
     [!code-csharp[Trin_VstcoreWordAutomation#27](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#27)]  
  
     Приведенный ниже пример кода можно использовать в надстройке VSTO уровня приложения. В этом примере кода используется активный документ.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#27](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#27)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#27](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#27)]  
  
2.  Назначьте свойство <xref:Microsoft.Office.Interop.Word.Range.Text%2A> , переключающее текст между двумя абзацами.  
  
     [!code-vb[Trin_VstcoreWordAutomation#28](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#28)]
     [!code-csharp[Trin_VstcoreWordAutomation#28](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#28)]  
  
3.  По очереди выбирайте каждый диапазон и делайте паузу, чтобы отобразить результаты в окне сообщения.  
  
     [!code-vb[Trin_VstcoreWordAutomation#29](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#29)]
     [!code-csharp[Trin_VstcoreWordAutomation#29](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#29)]  
  
4.  Настройте `firstRange` с помощью метода <xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A> , чтобы символ абзаца больше не являлся частью `firstRange`.  
  
     [!code-vb[Trin_VstcoreWordAutomation#30](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#30)]
     [!code-csharp[Trin_VstcoreWordAutomation#30](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#30)]  
  
5.  Замените оставшийся текст в первом абзаце, назначив новую строку в свойстве <xref:Microsoft.Office.Interop.Word.Range.Text%2A> диапазона.  
  
     [!code-vb[Trin_VstcoreWordAutomation#31](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#31)]
     [!code-csharp[Trin_VstcoreWordAutomation#31](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#31)]  
  
6.  Замените текст в `secondRange`, включая знак абзаца.  
  
     [!code-vb[Trin_VstcoreWordAutomation#32](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#32)]
     [!code-csharp[Trin_VstcoreWordAutomation#32](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#32)]  
  
7.  Выберите `firstRange` и сделайте паузу для отображения результатов в окне сообщения, а затем сделайте то же самое с `secondRange`.  
  
     Поскольку `firstRange` был переопределен, чтобы исключить знак абзаца, первоначальное форматирование абзаца сохраняется. Однако вместо знака абзаца в `secondRange`было вставлено предложение, удаляющее отдельный абзац.  
  
     [!code-vb[Trin_VstcoreWordAutomation#33](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#33)]
     [!code-csharp[Trin_VstcoreWordAutomation#33](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#33)]  
  
     Исходное содержимое обоих диапазонов было сохранено в виде строк, поэтому можно восстановить исходное состояние документа.  
  
8.  Перенастроить `firstRange` для включения знак абзаца с помощью <xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A> метод для позиции 1 символа.  
  
     [!code-vb[Trin_VstcoreWordAutomation#34](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#34)]
     [!code-csharp[Trin_VstcoreWordAutomation#34](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#34)]  
  
9. Удалите `secondRange`. Это восстановит третий абзац в исходное положение.  
  
     [!code-vb[Trin_VstcoreWordAutomation#35](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#35)]
     [!code-csharp[Trin_VstcoreWordAutomation#35](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#35)]  
  
10. Восстановите первоначальный текст абзаца в `firstRange`.  
  
     [!code-vb[Trin_VstcoreWordAutomation#36](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#36)]
     [!code-csharp[Trin_VstcoreWordAutomation#36](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#36)]  
  
11. Используйте метод <xref:Microsoft.Office.Interop.Word.Range.InsertAfter%2A> объекта <xref:Microsoft.Office.Interop.Word.Range> для вставки исходного содержимого второго абзаца после `firstRange`, а затем выберите `firstRange`.  
  
     [!code-vb[Trin_VstcoreWordAutomation#37](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#37)]
     [!code-csharp[Trin_VstcoreWordAutomation#37](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#37)]  
  
## <a name="document-level-customization-example"></a>Пример настройки на уровне документа  
  
### <a name="to-control-paragraph-structure-when-inserting-text-in-document-level-customizations"></a>Управление структурой абзаца при вставке текста в настройках уровня документа  
  
1.  В следующем примере показан полный метод для настройки на уровне документа. Чтобы использовать этот пример кода, запустите его из класса `ThisDocument` в своем проекте.  
  
     [!code-vb[Trin_VstcoreWordAutomation#26](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#26)]
     [!code-csharp[Trin_VstcoreWordAutomation#26](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#26)]  
  
## <a name="vsto-add-in-example"></a>Пример надстройки VSTO  
  
### <a name="to-control-paragraph-structure-when-inserting-text-in-a-vsto-add-in"></a>Управление структурой абзаца при вставке текста в надстройке VSTO  
  
1.  В следующем примере показан полный метод для надстройки VSTO. Чтобы использовать этот пример кода, запустите его из класса `ThisAddIn` в своем проекте.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#26](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#26)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#26](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#26)]  
  
## <a name="see-also"></a>См. также  
 [Практическое: программное расширение диапазонов в документах](../vsto/how-to-programmatically-extend-ranges-in-documents.md)   
 [Практическое: программное свертывание диапазонов и выделений в документах](../vsto/how-to-programmatically-collapse-ranges-or-selections-in-documents.md)   
 [Практическое: программная Вставка текста в документы Word](../vsto/how-to-programmatically-insert-text-into-word-documents.md)   
 [Практическое: программно сброс диапазонов в документах Word](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)   
 [Практическое: программное определение и выделение диапазонов в документах](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)   
 [Необязательные параметры в решениях Office](../vsto/optional-parameters-in-office-solutions.md)  
  
  