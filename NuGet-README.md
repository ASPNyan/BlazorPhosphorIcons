# Phosphor Icons

A Blazor component wrapper for [Phosphor Icons](https://phosphoricons.com/), providing all icon variants as strongly-typed, composable Razor components.

## Installation

Add a reference to the `PhosphorIcons` project or package in your Blazor application.

Then add the namespace to your `_Imports.razor`:

````razor
@using Phosphor.Icons
````

## Usage

Each icon is its own Razor component, named after the Phosphor icon it represents (e.g. `PhAcorn`, `PhArrowLeft`).
Every icon component accepts a `Type` parameter of type `IconType` to select the visual style, as well as any additional HTML attributes which are forwarded directly to the underlying `<svg>` element.

Icons don't come with a default size, so you are responsible for sizing all of your icons. SVGs expose `width` and
`height` attributes that accept the same values as `style="width: {WIDTH}; height: {HEIGHT}"`, so opting for
`width="1em"` and `height="1em"` may be preferred over a `style` attribute.

### Basic Example

```razor
<PhAcorn Type="IconType.Regular" />
```

### With Additional SVG Attributes

Because icons support attribute splatting, you can pass any standard HTML/SVG attribute directly to the component:

```razor
<PhAcorn Type="IconType.Bold" class="my-icon" width="1em" height="1em" style="color: hotpink;" aria-hidden="true" />
```

### Dynamic Usage

Icons can be rendered dynamically using `DynamicComponent` — useful for rendering icons from a data-driven list:

```razor
<DynamicComponent Type="@iconType" Parameters='new Dictionary<string, object> { ["Type"] = IconType.Regular }' />
```

All available icon component types can be discovered at runtime via reflection:

```razor
Assembly.GetAssembly(typeof(PhAcorn))!
        .GetTypes()
        .Where(t => !t.IsEnum && typeof(IComponent).IsAssignableFrom(t));
```

## Icon Types

The `IconType` enum controls the visual style of every icon:

| Value     | Description                                            |
|-----------|--------------------------------------------------------|
| `Regular` | Standard weight outline style                          |
| `Bold`    | Heavier stroke weight                                  |
| `Thin`    | Lighter, finer stroke weight                           |
| `Light`   | Between thin and regular                               |
| `Duotone` | Two-tone style with a semi-transparent secondary layer |
| `Fill`    | Fully filled / solid style                             |

## Parameters

All icon components share the same parameter surface:

| Parameter                | Type                                   | Required | Description                                                                                       |
|--------------------------|----------------------------------------|----------|---------------------------------------------------------------------------------------------------|
| `Type`                   | `IconType`                             | Yes      | Selects the icon style variant to render.                                                         |
| _(unmatched attributes)_ | `IReadOnlyDictionary<string, object?>` | No       | Any additional attributes (e.g. `class`, `style`, `aria-*`) are forwarded to the `<svg>` element. |

## Preview / Test Project

A preview project is included under `Test/` targeting `net11.0` and `net10.0`. It renders every icon in the library in a filterable, colour-configurable grid, allowing you to browse all available icons and styles interactively.

To run it:

```
dotnet run --project Test/Test.csproj
```

The preview supports:

* Filtering icons by name via a search input
* Switching between all `IconType` variants via a dropdown
* Choosing a custom colour applied to the icon grid

## Licence

See [LICENSE](./LICENSE) for details.
