---
title: "CA2232: Mark Windows Forms entry points with STAThread"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "MarkWindowsFormsEntryPointsWithStaThread"
  - "CA2232"
helpviewer_keywords:
  - "CA2232"
  - "MarkWindowsFormsEntryPointsWithStaThread"
ms.assetid: a3c95130-8e7f-4419-9fcd-b67d077e8efb
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
 - CSharp
 - VB
ms.workload:
  - "multiple"
---
# CA2232: Mark Windows Forms entry points with STAThread

|||
|-|-|
|TypeName|MarkWindowsFormsEntryPointsWithStaThread|
|CheckId|CA2232|
|Category|Microsoft.Usage|
|Breaking Change|Non Breaking|

## Cause
An assembly references the <xref:System.Windows.Forms> namespace, and its entry point is not marked with the <xref:System.STAThreadAttribute?displayProperty=fullName> attribute.

## Rule description
 <xref:System.STAThreadAttribute> indicates that the COM threading model for the application is single-threaded apartment. This attribute must be present on the entry point of any application that uses Windows Forms; if it is omitted, the Windows components might not work correctly. If the attribute is not present, the application uses the multithreaded apartment model, which is not supported for Windows Forms.

> [!NOTE]
> [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] projects that use the Application Framework do not have to mark the **Main** method with STAThread. The [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] compiler does it automatically.

## How to fix violations
To fix a violation of this rule, add the <xref:System.STAThreadAttribute> attribute to the entry point. If the <xref:System.MTAThreadAttribute?displayProperty=fullName> attribute is present, remove it.

## When to suppress warnings
It is safe to suppress a warning from this rule if you are developing for the .NET Compact Framework, for which the <xref:System.STAThreadAttribute> attribute is unnecessary and not supported.

## Example
The following examples demonstrate the correct usage of <xref:System.STAThreadAttribute>:

[!code-csharp[FxCop.Usage.StaThread#1](../code-quality/codesnippet/CSharp/ca2232-mark-windows-forms-entry-points-with-stathread_1.cs)]
[!code-vb[FxCop.Usage.StaThread#1](../code-quality/codesnippet/VisualBasic/ca2232-mark-windows-forms-entry-points-with-stathread_1.vb)]