---
title: "CA1025: Replace repetitive arguments with params array"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "CA1025"
  - "ReplaceRepetitiveArgumentsWithParamsArray"
helpviewer_keywords:
  - "ReplaceRepetitiveArgumentsWithParamsArray"
  - "CA1025"
ms.assetid: f009b340-dea3-4459-8fe1-2143aa8b5d0b
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "multiple"
---
# CA1025: Replace repetitive arguments with params array

|||
|-|-|
|TypeName|ReplaceRepetitiveArgumentsWithParamsArray|
|CheckId|CA1025|
|Category|Microsoft.Design|
|Breaking Change|Non-breaking|

## Cause
A public or protected method in a public type has more than three parameters, and its last three parameters are the same type.

## Rule description
Use a parameter array instead of repeated arguments when the exact number of arguments is unknown and the variable arguments are the same type, or can be passed as the same type. For example, the <xref:System.Console.WriteLine%2A> method provides a general-purpose overload that uses a parameter array to accept any number of <xref:System.Object> arguments.

## How to fix violations
To fix a violation of this rule, replace the repeated arguments with a parameter array.

## When to suppress warnings
It is always safe to suppress a warning from this rule; however, this design might cause usability issues.

## Example
The following example shows a type that violates this rule.

[!code-csharp[FxCop.Design.RepeatArgs#1](../code-quality/codesnippet/CSharp/ca1025-replace-repetitive-arguments-with-params-array_1.cs)]