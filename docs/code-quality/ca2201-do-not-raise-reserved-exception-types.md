---
title: 'CA2201: не вызывайте зарезервированные типы исключений'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotRaiseReservedExceptionTypes
- CA2201
helpviewer_keywords:
- CA2201
- DoNotRaiseReservedExceptionTypes
ms.assetid: dd14ef5c-80e6-41a5-834e-eba8e2eae75e
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 763c8656507f8a1d9c1f59bd548469c338aeb012
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/13/2018
ms.locfileid: "45547523"
---
# <a name="ca2201-do-not-raise-reserved-exception-types"></a>CA2201: не вызывайте зарезервированные типы исключений

|||
|-|-|
|TypeName|DoNotRaiseReservedExceptionTypes|
|CheckId|CA2201|
|Категория|Microsoft.Usage|
|Критическое изменение|Критическое|

## <a name="cause"></a>Причина

Метод создает тип исключения, который является слишком общим или, зарезервированные для среды выполнения.

## <a name="rule-description"></a>Описание правила

Следующие типы исключений имеют слишком общий характер, чтобы предоставляет достаточно сведений для пользователя:

- <xref:System.Exception?displayProperty=fullName>

- <xref:System.ApplicationException?displayProperty=fullName>

- <xref:System.SystemException?displayProperty=fullName>

Следующие типы исключений зарезервированы и должен быть создан только действием среда CLR:

- <xref:System.ExecutionEngineException?displayProperty=fullName>

- <xref:System.IndexOutOfRangeException?displayProperty=fullName>

- <xref:System.NullReferenceException?displayProperty=fullName>

- <xref:System.OutOfMemoryException?displayProperty=fullName>

**Не создавайте общих исключений**

Если вы throw исключения общего типа, таких как <xref:System.Exception> или <xref:System.SystemException> в библиотеке или платформе, вынуждает объекты-получатели перехватывать все исключения, включая неизвестных исключений, которые они не знают, как обрабатывать.

Вместо этого создать более производный тип, уже существует в структуре или создать собственный тип, производный от <xref:System.Exception>.

**Генерировать определенные исключения**

В следующей таблице показаны параметры и исключения, которые могут вызывать при проверке параметров, включая значение параметра в методе доступа set свойства:

|Описание параметра|Исключение|
|---------------------------|---------------|
|`null` Справочник по|<xref:System.ArgumentNullException?displayProperty=fullName>|
|За пределами допустимого диапазона значений (таких как индекс для коллекции или перечня)|<xref:System.ArgumentOutOfRangeException?displayProperty=fullName>|
|Недопустимый `enum` значение|<xref:System.ComponentModel.InvalidEnumArgumentException?displayProperty=fullName>|
|Содержит формат, который не соответствует спецификациям параметров метода (например, строка формата для `ToString(String)`)|<xref:System.FormatException?displayProperty=fullName>|
|В противном случае недопустим|<xref:System.ArgumentException?displayProperty=fullName>|

Когда операция недопустима для текущего состояния объекта throw <xref:System.InvalidOperationException?displayProperty=fullName>

Исключение при выполнении операции над объект, который был удален <xref:System.ObjectDisposedException?displayProperty=fullName>

Если операция не поддерживается (например, в переопределенный **методы Stream.Write** в Stream, открыт для чтения) throw <xref:System.NotSupportedException?displayProperty=fullName>

Если преобразование может привести к переполнению (например, перегрузка оператора явного приведения) исключение <xref:System.OverflowException?displayProperty=fullName>

В других случаях, рекомендуется создать собственный тип, производный от <xref:System.Exception> и создает исключение, которое.

## <a name="how-to-fix-violations"></a>Устранение нарушений

Чтобы устранить нарушение этого правила, измените тип вызванного исключения для определенного типа, который не является одним из зарезервированных типов.

## <a name="when-to-suppress-warnings"></a>Отключение предупреждений

Для этого правила отключать вывод предупреждений не следует.

## <a name="related-rules"></a>Связанные правила

- [CA1031: не перехватывайте типы общих исключений](../code-quality/ca1031-do-not-catch-general-exception-types.md)