---
title: "CA1601: Do not use timers that prevent power state changes"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "CA1601"
  - "DoNotUseTimersThatPreventPowerStateChanges"
helpviewer_keywords:
  - "CA1601"
  - "DoNotUseTimersThatPreventPowerStateChanges"
ms.assetid: b8028c92-0696-4c54-9773-0028f29bda9a
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "multiple"
---
# CA1601: Do not use timers that prevent power state changes

|||
|-|-|
|TypeName|DoNotUseTimersThatPreventPowerStateChanges|
|CheckId|CA1601|
|Category|Microsoft.Mobility|
|Breaking Change|Breaking|

## Cause
A timer has an interval set to occur more than one time per second.

## Rule description
Do not poll more often than one time per second or use timers that occur more frequently than one time per second. Higher-frequency periodic activity will keep the CPU busy and interfere with power-saving idle timers that turn off the display and hard disks.

## How to fix violations
Set timer intervals to occur less than one time per second.

## When to suppress warnings
This rule should be suppressed only if firing the timer more than one time per second is required and mobility considerations can safely be ignored.