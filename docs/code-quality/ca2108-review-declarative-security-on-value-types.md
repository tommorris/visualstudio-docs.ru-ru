---
title: 'CA2108: проверьте объявляемые параметры безопасности типов значений'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ReviewDeclarativeSecurityOnValueTypes
- CA2108
helpviewer_keywords:
- ReviewDeclarativeSecurityOnValueTypes
- CA2108
ms.assetid: d62bffdd-3826-4d52-a708-1c646c5d48c2
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e2d76a0ecf6a2eeac677475eb25efe495129c213
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/13/2018
ms.locfileid: "45548521"
---
# <a name="ca2108-review-declarative-security-on-value-types"></a>CA2108: проверьте объявляемые параметры безопасности типов значений

|||
|-|-|
|TypeName|ReviewDeclarativeSecurityOnValueTypes|
|CheckId|CA2108|
|Категория|Microsoft.Security|
|Критическое изменение|Не критическое|

## <a name="cause"></a>Причина

Открытый или защищенный тип значения защищен [данные и моделирование](/dotnet/framework/data/index) или [требования связывания](/dotnet/framework/misc/link-demands).

## <a name="rule-description"></a>Описание правила

Типы значений выделенных и инициализировать с конструкторы по умолчанию до выполнения других конструкторов. Если тип значения защищен Demand или LinkDemand и вызывающий объект не имеет разрешений, которые не удовлетворяют проверки безопасности, какому-либо конструктору по умолчанию не удастся и будет выдано исключение безопасности. Тип значения не освобождается; он остается в состоянии, задайте его конструктором по умолчанию. Не следует предполагать, что вызывающий объект, который передает экземпляр типа значения имеет разрешение на создание или доступ к экземпляру.

## <a name="how-to-fix-violations"></a>Устранение нарушений

Невозможно устранить нарушение этого правила, если не удалить проверку безопасности на основе типа и проверки безопасности на уровне метода используйте вместо него. Таким способом устранения нарушения не запрещает вызывающие объекты с соответствующими разрешениями, получать экземпляры типа значения. Необходимо убедиться, что экземпляр типа значения, в состоянии по умолчанию, не содержит конфиденциальную информацию и нельзя использовать в злонамеренных целях.

## <a name="when-to-suppress-warnings"></a>Отключение предупреждений

Можно подавить предупреждение из этого правила, если любой вызывающий объект может получить экземпляры типа значения в состоянии по умолчанию без создания угроз безопасности.

## <a name="example-1"></a>Пример 1

В следующем примере показано это библиотека, содержащая тип значения, который нарушает это правило. `StructureManager` Тип предполагает, что вызывающий объект, который передает экземпляр типа значения имеет разрешение на создание или доступ к экземпляру.

[!code-csharp[FxCop.Security.DemandOnValueType#1](../code-quality/codesnippet/CSharp/ca2108-review-declarative-security-on-value-types_1.cs)]

## <a name="example-2"></a>Пример 2

В следующем приложении демонстрируется уязвимость библиотеки.

[!code-csharp[FxCop.Security.TestDemandOnValueType#1](../code-quality/codesnippet/CSharp/ca2108-review-declarative-security-on-value-types_2.cs)]

В этом примере выводятся следующие данные:

```txt
Structure custom constructor: Request failed.
New values SecuredTypeStructure 100 100
New values SecuredTypeStructure 200 200
```

## <a name="see-also"></a>См. также

- [Требования связывания](/dotnet/framework/misc/link-demands)
- [Данные и моделирование](/dotnet/framework/data/index)
