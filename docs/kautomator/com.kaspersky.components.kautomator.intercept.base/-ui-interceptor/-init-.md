[kautomator](../../index.md) / [com.kaspersky.components.kautomator.intercept.base](../index.md) / [UiInterceptor](index.md) / [&lt;init&gt;](./-init-.md)

# &lt;init&gt;

`UiInterceptor(onCheck: `[`UiInterception`](../-ui-interception/index.md)`<(Interaction, Assertion) -> `[`Unit`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-unit/index.html)`>?, onPerform: `[`UiInterception`](../-ui-interception/index.md)`<(Interaction, Action) -> `[`Unit`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-unit/index.html)`>?, onAll: `[`UiInterception`](../-ui-interception/index.md)`<(Interaction) -> `[`Unit`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-unit/index.html)`>?)`

Base class for intercepting the call chain from Kautomator to UiAutomator.

Interceptors can be provided through [KautomatorConfigurator](../../com.kaspersky.components.kautomator/-kautomator-configurator/index.md) runtime,
different [UiScreens](#) as well as [UiViews](../../com.kaspersky.components.kautomator.component.common.views/-ui-base-view/index.md).

Interceptors are stacked during the runtime for any UiAutomator_DSL-UiAutomator `check` and `perform` operations.
The stack ordering is following: UiView interceptor -&gt; UiScreen interceptors -&gt; UiAutomatorDsl interceptor.

Any of the interceptors in the chain can break the chain call by setting `isOverride` to true
in [onCheck](-builder/on-check.md), [onPerform](-builder/on-perform.md) or [onAll](-builder/on-all.md) interception
functions during the configuration. Doing this will not only prevent underlying
interceptors from being invoked, but prevents UiAutomator from executing the operation. In that case,
responsibility for actually making UiAutomator call lies on developer.

For each operation the interceptor invocation cycle will be as follows:

```
// For check operation
onAll?.invoke()
onCheck?.invoke()

// For perform operation
onAll?.invoke()
onPerform?.invoke()
```

**See Also**

[com.kaspersky.components.kautomator.KautomatorConfigurator](../../com.kaspersky.components.kautomator/-kautomator-configurator/index.md)

[com.kaspersky.components.kautomator.component.screen.UiScreen](#)

[com.kaspersky.components.kautomator.component.common.views.UiBaseView](../../com.kaspersky.components.kautomator.component.common.views/-ui-base-view/index.md)

