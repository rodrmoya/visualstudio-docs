---
title: "CA1012: Abstract types should not have constructors"
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
  - "AbstractTypesShouldNotHaveConstructors"
  - "CA1012"
helpviewer_keywords:
  - "CA1012"
ms.assetid: 09f458ac-dd88-4cd7-a47f-4106c1e80ece
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
 - CSharp
 - VB
ms.workload:
  - "multiple"
---
# CA1012: Abstract types should not have constructors

|||
|-|-|
|TypeName|AbstractTypesShouldNotHaveConstructors|
|CheckId|CA1012|
|Category|Microsoft.Design|
|Breaking Change|Non-breaking|

## Cause

A type is abstract and has a constructor.

By default, this rule only looks at externally visible types, but this is [configurable](#configurability).

## Rule description

Constructors on abstract types can be called only by derived types. Because public constructors create instances of a type and you cannot create instances of an abstract type, an abstract type that has a public constructor is incorrectly designed.

## How to fix violations

To fix a violation of this rule, either make the constructor protected or don't declare the type as abstract.

## When to suppress warnings

Do not suppress a warning from this rule. The abstract type has a public constructor.

## Configurability

If you're running this rule from [FxCop analyzers](install-fxcop-analyzers.md) (and not with legacy analysis), you can configure which parts of your codebase to run this rule on, based on their accessibility. For example, to specify that the rule should run only against the non-public API surface, add the following key-value pair to an .editorconfig file in your project:

```ini
dotnet_code_quality.ca1012.api_surface = private, internal
```

You can configure this option for just this rule, for all rules, or for all rules in this category (Design). For more information, see [Configure FxCop analyzers](configure-fxcop-analyzers.md).

## Example

The following code snippet contains an abstract type that violates this rule.

[!code-vb[FxCop.Design.AbstractTypeBad#1](../code-quality/codesnippet/VisualBasic/ca1012-abstract-types-should-not-have-constructors_1.vb)]
[!code-csharp[FxCop.Design.AbstractTypeBad#1](../code-quality/codesnippet/CSharp/ca1012-abstract-types-should-not-have-constructors_1.cs)]

The following code snippet fixes the previous violation by changing the accessibility of the constructor from `public` to `protected`.

[!code-csharp[FxCop.Design.AbstractTypeGood#1](../code-quality/codesnippet/CSharp/ca1012-abstract-types-should-not-have-constructors_2.cs)]
[!code-vb[FxCop.Design.AbstractTypeGood#1](../code-quality/codesnippet/VisualBasic/ca1012-abstract-types-should-not-have-constructors_2.vb)]