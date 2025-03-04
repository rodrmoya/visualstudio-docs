---
title: "CA1409: Com visible types should be creatable"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "ComVisibleTypesShouldBeCreatable"
  - "CA1409"
helpviewer_keywords:
  - "ComVisibleTypesShouldBeCreatable"
  - "CA1409"
ms.assetid: 9f59569b-de15-4a38-b7cb-cff152972243
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "multiple"
---
# CA1409: Com visible types should be creatable

|||
|-|-|
|TypeName|ComVisibleTypesShouldBeCreatable|
|CheckId|CA1409|
|Category|Microsoft.Interoperability|
|Breaking Change|Non-breaking|

## Cause
A reference type that is specifically marked as visible to Component Object Model (COM) contains a public parameterized constructor but does not contain a public default (parameterless) constructor.

## Rule description
A type without a public default constructor cannot be created by COM clients. However, the type can still be accessed by COM clients if another means is available to create the type and pass it to the client (for example, through the return value of a method call).

The rule ignores types that are derived from <xref:System.Delegate?displayProperty=fullName>.

By default, the following are visible to COM: assemblies, public types, public instance members in public types, and all members of public value types.

## How to fix violations
To fix a violation of this rule, add a public default constructor or remove the <xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName> from the type.

## When to suppress warnings
It is safe to suppress a warning from this rule if other ways are provided to create and pass the object to the COM client.

## Related rules
[CA1017: Mark assemblies with ComVisibleAttribute](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)

## See also

- [Qualifying .NET Types for Interoperation](/dotnet/framework/interop/qualifying-net-types-for-interoperation)
- [Interoperating with Unmanaged Code](/dotnet/framework/interop/index)