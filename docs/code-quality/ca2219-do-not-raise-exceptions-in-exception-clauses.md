---
title: "CA2219: Do not raise exceptions in exception clauses"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "DoNotRaiseExceptionsInExceptionClauses"
  - "CA2219"
helpviewer_keywords:
  - "DoNotRaiseExceptionsInExceptionClauses"
  - "CA2219"
ms.assetid: 7b9b0bee-4e8e-49a4-8c40-52142b49061f
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "multiple"
---
# CA2219: Do not raise exceptions in exception clauses

|||
|-|-|
|TypeName|DoNotRaiseExceptionsInExceptionClauses|
|CheckId|CA2219|
|Category|Microsoft.Usage|
|Breaking Change|Non Breaking, Breaking|

## Cause
An exception is thrown from a `finally`, filter, or fault clause.

## Rule description
When an exception is raised in an exception clause, it greatly increases the difficulty of debugging.

When an exception is raised in a `finally` or fault clause, the new exception hides the active exception, if present. This makes the original error hard to detect and debug.

When an exception is raised in a filter clause, the runtime silently catches the exception, and causes the filter to evaluate to false. There is no way to tell the difference between the filter evaluating to false and an exception being throw from a filter. This makes it hard to detect and debug errors in the filter's logic.

## How to fix violations
To fix this violation of this rule, do not explicitly raise an exception from a `finally`, filter, or fault clause.

## When to suppress warnings
Do not suppress a warning for this rule. There are no scenarios under which an exception raised in an exception clause provides a benefit to the executing code.

## Related rules
[CA1065: Do not raise exceptions in unexpected locations](../code-quality/ca1065-do-not-raise-exceptions-in-unexpected-locations.md)

## See also
[Design Warnings](../code-quality/design-warnings.md)