---
title: 'CA2138: прозрачные методы не должны вызывать методы с атрибутом SuppressUnmanagedCodeSecurity'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2138
ms.assetid: a14c4d32-f079-4f3a-956c-a1657cde0f66
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- cplusplus
ms.openlocfilehash: 1c05d8f6218166dc57e832412649bb04d9151f36
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/13/2018
ms.locfileid: "45549816"
---
# <a name="ca2138-transparent-methods-must-not-call-methods-with-the-suppressunmanagedcodesecurity-attribute"></a>CA2138: прозрачные методы не должны вызывать методы с атрибутом SuppressUnmanagedCodeSecurity
|||
|-|-|
|TypeName|TransparentMethodsMustNotCallSuppressUnmanagedCodeSecurityMethods|
|CheckId|CA2138|
|Категория|Microsoft.Security|
|Критическое изменение|Критическое|

## <a name="cause"></a>Причина
 Прозрачный безопасности метод вызывает метод, отмеченный атрибутом <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> атрибута.

## <a name="rule-description"></a>Описание правила
 Это правило срабатывает для любого прозрачного метода, который напрямую вызывает машинный код, например, с помощью P/Invoke (неуправляемого) вызова. P/Invoke и COM-взаимодействия методы, помеченные атрибутом <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> атрибут приводят LinkDemand эти операции выполняются в вызывающий метод. Поскольку прозрачного кода безопасности нельзя было удовлетворять LinkDemands, код также не может вызывать методы, помеченные атрибутом SuppressUnmanagedCodeSecurity или методы класса, помеченный атрибутом SuppressUnmanagedCodeSecurity. Метод завершится с ошибкой, или по требованию будут преобразовываться в полное требование.

 Нарушение этого правила приводит к <xref:System.MethodAccessException> в уровня 2 модели прозрачности безопасности, а также полное требование для <xref:System.Security.Permissions.SecurityPermissionAttribute.UnmanagedCode%2A> в рамках модели прозрачности уровня 1.

## <a name="how-to-fix-violations"></a>Устранение нарушений
 Чтобы устранить нарушение этого правила, удалите <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> атрибут и пометьте метод <xref:System.Security.SecurityCriticalAttribute> или <xref:System.Security.SecuritySafeCriticalAttribute> атрибута.

## <a name="when-to-suppress-warnings"></a>Отключение предупреждений
 Для этого правила отключать вывод предупреждений не следует.

## <a name="example"></a>Пример
 [!code-csharp[FxCop.Security.CA2138.TransparentMethodsMustNotCallSuppressUnmanagedCodeSecurityMethods#1](../code-quality/codesnippet/CSharp/ca2138-transparent-methods-must-not-call-methods-with-the-suppressunmanagedcodesecurity-attribute_1.cs)]