---
title: "CA2214: Do not call overridable methods in constructors"
ms.date: 05/29/2016
ms.topic: reference
f1_keywords:
  - "DoNotCallOverridableMethodsInConstructors"
  - "CA2214"
helpviewer_keywords:
  - "CA2214"
  - "DoNotCallOverridableMethodsInConstructors"
ms.assetid: 335b57ca-a6e8-41b4-a20e-57ee172c97c3
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
 - CSharp
 - VB
ms.workload:
  - "multiple"
---
# CA2214: Do not call overridable methods in constructors

|||
|-|-|
|TypeName|DoNotCallOverridableMethodsInConstructors|
|CheckId|CA2214|
|Category|Microsoft.Usage|
|Breaking Change|Non Breaking|

## Cause

The constructor of an unsealed type calls a virtual method defined in its class.

## Rule description

When a virtual method is called, the actual type that executes the method is not selected until run time. When a constructor calls a virtual method, it's possible that the constructor for the instance that invokes the method has not executed.

> [!NOTE]
> The legacy analysis implementation of this rule has a different diagnostic message of "**\[Constructor name] contains a call chain that results in a call to a virtual method defined by the class. Review the following call stack for unintended consequences**". The [FxCop analyzers](install-fxcop-analyzers.md) implementation of this rule has a diagnostic message of "**Do not call overridable methods in constructors**".

## How to fix violations

To fix a violation of this rule, do not call a type's virtual methods from within the type's constructors.

## When to suppress warnings

Do not suppress a warning from this rule. The constructor should be redesigned to eliminate the call to the virtual method.

## Example

The following example demonstrates the effect of violating this rule. The test application creates an instance of `DerivedType`, which causes its base class (`BadlyConstructedType`) constructor to execute. `BadlyConstructedType`'s constructor incorrectly calls the virtual method `DoSomething`. As the output shows, `DerivedType.DoSomething()` executes before `DerivedType`'s constructor executes.

[!code-csharp[FxCop.Usage.CtorVirtual#1](../code-quality/codesnippet/CSharp/ca2214-do-not-call-overridable-methods-in-constructors_1.cs)]
[!code-vb[FxCop.Usage.CtorVirtual#1](../code-quality/codesnippet/VisualBasic/ca2214-do-not-call-overridable-methods-in-constructors_1.vb)]

This example produces the following output:

```txt
Calling base ctor.
Derived DoSomething is called - initialized ? No
Calling derived ctor.
```