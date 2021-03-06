---
title: Связывание области формы с классом сообщений Outlook
ms.custom: ''
ms.date: 02/02/2017
ms.technology: office-development
ms.prod: visual-studio-dev15
ms.topic: conceptual
f1_keywords:
- VSTO.NewFormRegionWizard.InvalidMessageClassName
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- FormRegionMessageClassAttribute
- form regions [Office development in Visual Studio], message classes
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: d6f48be189b7d7a35f713c224553dc9ad7c8a5c3
ms.sourcegitcommit: 209c2c068ff0975994ed892b62aa9b834a7f6077
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34268234"
---
# <a name="associate-a-form-region-with-an-outlook-message-class"></a>Связывание области формы с классом сообщений Outlook
  Можно указать, какие элементы Microsoft Office Outlook отображать область формы путем связывания области формы с классом сообщений каждого элемента. Например, если вы хотите добавить в конец почтового элемента области формы, можно связать область формы с `IPM.Note` класс message.  
  
 Чтобы связать область формы с классом сообщений, укажите имя класса сообщений в **новая область формы Outlook** мастер или применить атрибут класс фабрики областей формы.  
  
 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]  
  
## <a name="understand-outlook-message-classes"></a>Понять классы сообщений Outlook  
 Классом сообщений Outlook определяет тип элемента Outlook. В следующей таблице перечислены восемь стандартных типов элементов и их имен классов сообщений.  
  
|Тип элемента Outlook|Имя класса сообщений|  
|-----------------------|------------------------|  
|AppointmentItem|`IPM.Appointment`|  
|ContactItem|`IPM.Contact`|  
|DistListItem|`IPM.DistList`|  
|JournalItem|`IPM.Activity`|  
|MailItem|`IPM.Note`|  
|PostItem|`IPM.Post` или `IPM.Post.RSS`|  
|TaskItem|`IPM.Task`|  
  
 Можно также указать имена пользовательских классов сообщений. Пользовательские классы сообщений идентифицируют настраиваемые формы, определенные в Outlook.  
  
> [!NOTE]  
>  Для замены и заменить все области формы можно указать новое имя класса пользовательского сообщения. Необходимо использовать имя класса сообщений существующей пользовательской формы. Имя пользовательского класса должно быть уникальным. Является одним из способов обеспечить уникальность имени используется следующее соглашение об именовании: \< *StandardMessageClassName*>.\< *Компании*>.\< *MessageClassName*> (например: `IPM.Note.Contoso.MyMessageClass`).  
  
## <a name="associate-a-form-region-with-an-outlook-message-class"></a>Связывание области формы с классом сообщений Outlook  
 Связывание области формы с классом сообщений двумя способами.  
  
-   Используйте **новая область формы Outlook** мастера.  
  
-   Применение атрибутов классов.  
  
### <a name="use-the-new-outlook-form-region-wizard"></a>Используйте мастер создания области формы Outlook  
 На последней странице **новая область формы Outlook** мастера можно выбрать стандартные классы сообщений и ввести имена пользовательских классов сообщений, которую необходимо связать с областью формы.  
  
 Стандартные классы сообщений недоступны, если область формы предназначена для замены всей формы или страницы формы по умолчанию. Можно указать имена стандартных классов сообщений только для форм, добавьте новую страницу в форму или, добавляются в нижней части формы. Дополнительные сведения см. в разделе [как: Добавление области формы в проект надстройки Outlook](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md).  
  
 Чтобы включить один или несколько пользовательских классов сообщений, введите их имена в **каких классах пользовательских сообщений будет отображаться эта область формы?** поле.  
  
 Имена, которые типа вы должны соблюдать следующие рекомендации:  
  
-   Используйте полностью определенное имя класса сообщений (например: «IPM. Note.Contoso»).  
  
-   Используйте точку с запятой для разделения нескольких имен классов сообщений.  
  
-   Не включать стандартный класс сообщений Outlook, например «IPM. Примечание» или «IPM. "Contact». Включайте только пользовательские классы сообщений, например «IPM. Note.Contoso».  
  
-   Сам по себе не указан базового класса сообщений (например: «IPM»).  
  
-   Не превышать 256 символов для каждого имени класса сообщений.  
  
 **Новая область формы Outlook** мастер проверяет формата вводимых данных при нажатии кнопки **Готово**.  
  
> [!NOTE]  
>  **Новая область формы Outlook** мастер не проверку имен классов сообщений, которые вы указываете правильный или недопустимым.  
  
 После завершения работы мастера **новая область формы Outlook** мастер применяет атрибуты для класса области формы, который содержит указанные имена классов сообщений. Эти атрибуты можно применять вручную.  
  
### <a name="apply-class-attributes"></a>Применение атрибутов классов  
 Можно связать область формы с классом сообщений Outlook после завершения **новая область формы Outlook** мастера. Чтобы сделать это, необходимо Примените атрибуты к класс фабрики областей формы.  
  
 В следующем примере показаны два <xref:Microsoft.Office.Tools.Outlook.FormRegionMessageClassAttribute> атрибутов, которые были применены к фабрики класса области формы с именем `myFormRegion`. Первый атрибут связывает область формы с классом стандартных сообщений для формы сообщений. Второй атрибут связывает область формы с классом пользовательского сообщения `IPM.Task.Contoso`.  
  
 [!code-vb[Trin_Outlook_FR_Attributes#1](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Attributes/FormRegion1.vb#1)]
 [!code-csharp[Trin_Outlook_FR_Attributes#1](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Attributes/FormRegion1.cs#1)]  
  
 Атрибуты должны соответствовать приведенным ниже рекомендациям:  
  
-   Для пользовательских классов сообщений, используйте полностью определенное имя класса сообщений (например: «IPM. Note.Contoso»).  
  
-   Сам по себе не указан базового класса сообщений (например: «IPM»).  
  
-   Не превышать 256 символов для каждого имени класса сообщений.  
  
-   Не включать имена стандартных классов сообщений, если область формы заменяет всю форму или страницу по умолчанию формы. Можно указать имена стандартных классов сообщений только для форм, добавьте новую страницу в форму или, добавляются в нижней части формы. Дополнительные сведения см. в разделе [как: Добавление области формы в проект надстройки Outlook](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md).  
  
 Visual Studio выполняет проверку формата имен классов сообщений при построении проекта.  
  
> [!NOTE]  
>  Visual Studio не выполняет проверку правильности или допустимости имен классов сообщений, которые вы указываете.  
  
## <a name="see-also"></a>См. также  
 [Доступ к области формы во время выполнения](../vsto/accessing-a-form-region-at-run-time.md)   
 [Создание областей форм Outlook](../vsto/creating-outlook-form-regions.md)   
 [Пошаговое руководство: Разработка области формы Outlook](../vsto/walkthrough-designing-an-outlook-form-region.md)   
 [Рекомендации для создания областей формы Outlook](../vsto/guidelines-for-creating-outlook-form-regions.md)   
 [Общие сведения о классах имя формы и сообщений](http://msdn.microsoft.com/library/office/ff867629.aspx)   
 [Форм и элементов Outlook совместная работа](http://msdn.microsoft.com/library/office/ff869706.aspx)  
  
  