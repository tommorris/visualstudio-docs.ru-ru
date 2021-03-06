---
title: 'Практическое: программное расширение диапазонов в документах'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, extending
- documents [Office development in Visual Studio], extending ranges
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: bd8eff41b0e76816114e9c634f5ad61b6db58baf
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/06/2018
ms.locfileid: "35674280"
---
# <a name="how-to-programmatically-extend-ranges-in-documents"></a>Практическое: программное расширение диапазонов в документах
  После определения объекта <xref:Microsoft.Office.Interop.Word.Range> в документе Microsoft Office Word вы изменяете его начальную и конечную точки с помощью методов <xref:Microsoft.Office.Interop.Word.Range.MoveStart%2A> и <xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A> . Методы <xref:Microsoft.Office.Interop.Word.Range.MoveStart%2A> и <xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A> принимают те же два аргумента, *Unit* и *Count*. Методы *Count* — это количество единиц для перемещения, и аргумент *Unit* может иметь одно из следующих <xref:Microsoft.Office.Interop.Word.WdUnits> значений:  
  
-   <xref:Microsoft.Office.Interop.Word.WdUnits.wdCharacter>  
  
-   <xref:Microsoft.Office.Interop.Word.WdUnits.wdWord>  
  
-   <xref:Microsoft.Office.Interop.Word.WdUnits.wdSentence>  
  
-   <xref:Microsoft.Office.Interop.Word.WdUnits.wdParagraph>  
  
-   <xref:Microsoft.Office.Interop.Word.WdUnits.wdSection>  
  
-   <xref:Microsoft.Office.Interop.Word.WdUnits.wdStory>  
  
-   <xref:Microsoft.Office.Interop.Word.WdUnits.wdCell>  
  
-   <xref:Microsoft.Office.Interop.Word.WdUnits.wdColumn>  
  
-   <xref:Microsoft.Office.Interop.Word.WdUnits.wdRow>  
  
-   <xref:Microsoft.Office.Interop.Word.WdUnits.wdTable>  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
 В следующем примере определяется диапазон в семь символов. Затем начальная позиция этого диапазона перемещается на семь символов после исходной начальной позиции. Поскольку конечная позиция диапазона также находится через семь символов после начальной позиции, результатом является диапазон, состоящий из нуля символов. Затем код перемещает конечную позицию на семь символов после текущей конечной позиции.  
  
## <a name="to-extend-a-range"></a>Расширение диапазона  
  
1.  Определите диапазон символов. Дополнительные сведения см. в разделе [как: программное определение и выделение диапазонов в документах](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md).  
  
     Следующий пример кода можно использовать в настройке на уровне документа.  
  
     [!code-vb[Trin_VstcoreWordAutomation#39](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#39)]
     [!code-csharp[Trin_VstcoreWordAutomation#39](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#39)]  
  
     Следующий пример кода можно использовать в надстройке VSTO. В этом примере используется активный документ.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#39](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#39)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#39](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#39)]  
  
2.  Используйте метод <xref:Microsoft.Office.Interop.Word.Range.MoveStart%2A> объекта <xref:Microsoft.Office.Interop.Word.Range> , чтобы переместить начальную позицию диапазона.  
  
     [!code-vb[Trin_VstcoreWordAutomation#40](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#40)]
     [!code-csharp[Trin_VstcoreWordAutomation#40](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#40)]  
  
3.  Используйте метод <xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A> объекта <xref:Microsoft.Office.Interop.Word.Range> , чтобы переместить конечную позицию диапазона.  
  
     [!code-vb[Trin_VstcoreWordAutomation#41](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#41)]
     [!code-csharp[Trin_VstcoreWordAutomation#41](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#41)]  
  
## <a name="document-level-customization-code"></a>Код настройки уровня документа  
  
### <a name="to-extend-a-range-in-a-document-level-customization"></a>Расширение диапазона в настройке на уровне документа  
  
1.  В следующем примере показан полный код для настройки на уровне документа. Чтобы использовать этот пример кода, запустите его из класса `ThisDocument` в своем проекте.  
  
     [!code-vb[Trin_VstcoreWordAutomation#38](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#38)]
     [!code-csharp[Trin_VstcoreWordAutomation#38](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#38)]  
  
## <a name="vsto-add-in-code"></a>Код надстройки VSTO  
  
### <a name="to-extend-a-range-in-an-application-level-vsto-add-in"></a>Расширение диапазона в надстройке VSTO уровня приложения  
  
1.  В следующем примере показан полный код для надстройки VSTO. Чтобы использовать этот пример кода, запустите его из класса `ThisAddIn` в своем проекте.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#38](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#38)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#38](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#38)]  
  
## <a name="see-also"></a>См. также  
 [Практическое: программно сброс диапазонов в документах Word](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)   
 [Практическое: программное свертывание диапазонов и выделений в документах](../vsto/how-to-programmatically-collapse-ranges-or-selections-in-documents.md)   
 [Практическое: программное определение и выделение диапазонов в документах](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)   
 [Практическое: программное Извлечение знаков начала и завершения в диапазонах](../vsto/how-to-programmatically-retrieve-start-and-end-characters-in-ranges.md)   
 [Практическое: программное исключение знаков абзаца при создании диапазонов](../vsto/how-to-programmatically-exclude-paragraph-marks-when-creating-ranges.md)  
  