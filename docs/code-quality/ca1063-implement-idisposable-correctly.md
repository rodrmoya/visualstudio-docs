---
title: "CA1063: Implement IDisposable correctly"
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
  - "ImplementIDisposableCorrectly"
  - "CA1063"
helpviewer_keywords:
  - "CA1063"
  - "ImplementIDisposableCorrectly"
ms.assetid: 12afb1ea-3a17-4a3f-a1f0-fcdb853e2359
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
 - "CSharp"
ms.workload:
  - "multiple"
---
# CA1063: Implement IDisposable correctly

|||
|-|-|
|TypeName|ImplementIDisposableCorrectly|
|CheckId|CA1063|
|Category|Microsoft.Design|
|Breaking Change|Non-breaking|

## Cause

The <xref:System.IDisposable?displayProperty=nameWithType> interface is not implemented correctly. Possible reasons for this include:

- <xref:System.IDisposable> is reimplemented in the class.

- `Finalize` is overridden again.

- `Dispose()` is overridden.

- The `Dispose()` method is not public, [sealed](/dotnet/csharp/language-reference/keywords/sealed), or named **Dispose**.

- `Dispose(bool)` is not protected, virtual, or unsealed.

- In unsealed types, `Dispose()` must call `Dispose(true)`.

- For unsealed types, the `Finalize` implementation does not call either or both `Dispose(bool)` or the base class finalizer.

Violation of any one of these patterns triggers warning CA1063.

Every unsealed type that declares and implements the <xref:System.IDisposable> interface must provide its own `protected virtual void Dispose(bool)` method. `Dispose()` should call `Dispose(true)`, and the finalizer should call `Dispose(false)`. If you create an unsealed type that declares and implements the <xref:System.IDisposable> interface, you must define `Dispose(bool)` and call it. For more information, see [Clean up unmanaged resources (.NET guide)](/dotnet/standard/garbage-collection/unmanaged) and [Dispose pattern](/dotnet/standard/design-guidelines/dispose-pattern).

By default, this rule only looks at externally visible types, but this is [configurable](#configurability).

## Rule description

All <xref:System.IDisposable> types should implement the [Dispose pattern](/dotnet/standard/design-guidelines/dispose-pattern) correctly.

## How to fix violations

Examine your code and determine which of the following resolutions will fix this violation:

- Remove <xref:System.IDisposable> from the list of interfaces that are implemented by your type, and override the base class Dispose implementation instead.

- Remove the finalizer from your type, override Dispose(bool disposing), and put the finalization logic in the code path where 'disposing' is false.

- Override Dispose(bool disposing), and put the dispose logic in the code path where 'disposing' is true.

- Make sure that Dispose() is declared as public and [sealed](/dotnet/csharp/language-reference/keywords/sealed).

- Rename your dispose method to **Dispose** and make sure that it's declared as public and [sealed](/dotnet/csharp/language-reference/keywords/sealed).

- Make sure that Dispose(bool) is declared as protected, virtual, and unsealed.

- Modify Dispose() so that it calls Dispose(true), then calls <xref:System.GC.SuppressFinalize%2A> on the current object instance (`this`, or `Me` in Visual Basic), and then returns.

- Modify your finalizer so that it calls Dispose(false) and then returns.

- If you create an unsealed type that declares and implements the <xref:System.IDisposable> interface, make sure that the implementation of <xref:System.IDisposable> follows the pattern that is described earlier in this section.

## When to suppress warnings

Do not suppress a warning from this rule.

## Configurability

If you're running this rule from [FxCop analyzers](install-fxcop-analyzers.md) (and not with legacy analysis), you can configure which parts of your codebase to run this rule on, based on their accessibility. For example, to specify that the rule should run only against the non-public API surface, add the following key-value pair to an .editorconfig file in your project:

```ini
dotnet_code_quality.ca1063.api_surface = private, internal
```

You can configure this option for just this rule, for all rules, or for all rules in this category (Design). For more information, see [Configure FxCop analyzers](configure-fxcop-analyzers.md).

## Pseudo-code example

The following pseudo-code provides a general example of how Dispose(bool) should be implemented in a class that uses managed and native resources.

```csharp
public class Resource : IDisposable
{
    private IntPtr nativeResource = Marshal.AllocHGlobal(100);
    private AnotherResource managedResource = new AnotherResource();

    // Dispose() calls Dispose(true)
    public void Dispose()
    {
        Dispose(true);
        GC.SuppressFinalize(this);
    }

    // NOTE: Leave out the finalizer altogether if this class doesn't
    // own unmanaged resources, but leave the other methods
    // exactly as they are.
    ~Resource()
    {
        // Finalizer calls Dispose(false)
        Dispose(false);
    }

    // The bulk of the clean-up code is implemented in Dispose(bool)
    protected virtual void Dispose(bool disposing)
    {
        if (disposing)
        {
            // free managed resources
            if (managedResource != null)
            {
                managedResource.Dispose();
                managedResource = null;
            }
        }
        // free native resources if there are any.
        if (nativeResource != IntPtr.Zero)
        {
            Marshal.FreeHGlobal(nativeResource);
            nativeResource = IntPtr.Zero;
        }
    }
}
```

## See also

- [Dispose pattern (framework design guidelines)](/dotnet/standard/design-guidelines/dispose-pattern)
- [Clean up unmanaged resources (.NET guide)](/dotnet/standard/garbage-collection/unmanaged)