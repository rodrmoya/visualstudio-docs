---
title: "CA1026: Default parameters should not be used"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "CA1026"
  - "DefaultParametersShouldNotBeUsed"
helpviewer_keywords:
  - "CA1026"
  - "DefaultParametersShouldNotBeUsed"
ms.assetid: 09643415-36ef-4d0f-9411-5721e14e2512
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "multiple"
---
# CA1026: Default parameters should not be used

|||
|-|-|
|TypeName|DefaultParametersShouldNotBeUsed|
|CheckId|CA1026|
|Category|Microsoft.Design|
|Breaking Change|Breaking|

## Cause
An externally visible type contains an externally visible method that uses a default parameter.

## Rule description
Methods that use default parameters are allowed under the Common Language Specification (CLS); however, the CLS allows compilers to ignore the values that are assigned to these parameters. Code that is written for compilers that ignore default parameter values must explicitly provide arguments for each default parameter. To maintain the behavior that you want across programming languages, methods that use default parameters should be replaced with method overloads that provide the default parameters.

The compiler ignores the values of default parameters for Managed Extension for C++ when it accesses managed code. The Visual Basic compiler supports methods that have default parameters that use the [Optional](/dotnet/visual-basic/language-reference/modifiers/optional) keyword.

## How to fix violations
To fix a violation of this rule, replace the method that uses default parameters with method overloads that supply the default parameters.

## When to suppress warnings
Do not suppress a warning from this rule.

## Example
The following example shows a method that uses default parameters, and the overloaded methods that provide an equivalent functionality.

[!code-vb[FxCop.Design.DefaultParameters#1](../code-quality/codesnippet/VisualBasic/ca1026-default-parameters-should-not-be-used_1.vb)]

## Related rules
[CA1025: Replace repetitive arguments with params array](../code-quality/ca1025-replace-repetitive-arguments-with-params-array.md)

## See also
[Language Independence and Language-Independent Components](/dotnet/standard/language-independence-and-language-independent-components)