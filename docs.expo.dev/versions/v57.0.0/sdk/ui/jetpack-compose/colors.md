---
modificationDate: August 18, 2026
title: Material Colors
description: Read the Material 3 color palette (including Material 3 Dynamic Colors) from JavaScript.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['android', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# Material Colors

Read the Material 3 color palette (including Material 3 Dynamic Colors) from JavaScript.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/jetpack-compose/colors/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/jetpack-compose/colors/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > Jetpack Compose (51 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, Included in Expo Go

Expo UI Jetpack Compose exposes the [Material 3 color palette](https://m3.material.io/styles/color/system/overview) used by Jetpack Compose so you can pick a palette source and have every component under a [`<Host>`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/host.md) theme from it consistently.

The palette source depends on the options you pass:

-   **Wallpaper-derived:** Default on Android 12+ when no `seedColor` is given. Uses [Material 3 Dynamic Colors](https://m3.material.io/styles/color/dynamic-color/overview) (Material You).
-   **Static [Material 3 baseline](https://m3.material.io/styles/color/roles):** Default fallback on Android 11 and below when no `seedColor` is given.
-   **Seeded from a color:** When you pass a `seedColor`, the full palette is derived using the same algorithm that Material 3 Dynamic Colors use for wallpaper-based colors. Works on every Android API level and is independent of the wallpaper.

## Installation

```sh
# npm
npx expo install @expo/ui

# yarn
yarn expo install @expo/ui

# pnpm
pnpm expo install @expo/ui

# bun
bun expo install @expo/ui
```

If you are installing this in an [existing React Native app](https://docs.expo.dev/bare/overview.md), make sure to [install `expo`](https://docs.expo.dev/bare/installing-expo-modules.md) in your project.

## Usage

### Theming `<Host>` from a seed color

[`Host`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/host.md) accepts `seedColor` and `colorScheme` props directly. This is the recommended way to theme a Compose subtree. Native Compose components under this `Host` render with the seeded palette and any descendant that calls [`useMaterialColors()`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#usematerialcolorsoptions) without arguments receives the same palette from the Host's context.

```tsx BrandedHostExample.tsx
import { Button, Host, Text } from '@expo/ui/jetpack-compose';

export default function BrandedHostExample() {
  return (
    <Host seedColor="#8E24AA" colorScheme="dark" matchContents>
      <Button onClick={() => {}}>
        <Text>Themed from the seed</Text>
      </Button>
    </Host>
  );
}
```

### Reading the current palette inside Host

Call [`useMaterialColors()`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#usematerialcolorsoptions) without arguments inside a [`<Host>`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/host.md) to read the Host's current palette. The hook returns a reference-stable [`MaterialColors`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#materialcolors) object and does not cross the native bridge on re-renders.

```tsx MaterialColorsExample.tsx
import {
  Column,
  Host,
  Surface,
  Text,
  useMaterialColors,
} from '@expo/ui/jetpack-compose';
import { padding } from '@expo/ui/jetpack-compose/modifiers';

export default function MaterialColorsExample() {
  return (
    <Host style={{ flex: 1 }}>
      <Surface>
        <PaletteInspector />
      </Surface>
    </Host>
  );
}

function PaletteInspector() {
  const colors = useMaterialColors();
  return (
    <Column
      modifiers={[padding(16, 16, 16, 16)]}
      verticalArrangement={{ spacedBy: 8 }}>
      <Text>Primary: {colors.primary}</Text>
      <Text>Surface: {colors.surface}</Text>
    </Column>
  );
}
```

### Computing a specific palette with arguments

Pass arguments to [`useMaterialColors()`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#usematerialcolorsoptions) to compute a palette on demand, even outside a `<Host>`. The `colorScheme` takes `'light'` or `'dark'`, you can omit it to follow the system.

```tsx UseMaterialColorsExample.tsx
import {
  Column,
  Host,
  Surface,
  Text,
  useMaterialColors,
} from '@expo/ui/jetpack-compose';
import { padding } from '@expo/ui/jetpack-compose/modifiers';

export default function UseMaterialColorsExample() {
  const dark = useMaterialColors({ colorScheme: 'dark' });
  const brand = useMaterialColors({ seedColor: '#8E24AA' });
  const brandedDark = useMaterialColors({
    colorScheme: 'dark',
    seedColor: '#8E24AA',
  });

  return (
    <Host style={{ flex: 1 }}>
      <Surface>
        <Column
          modifiers={[padding(16, 16, 16, 16)]}
          verticalArrangement={{ spacedBy: 8 }}>
          <Text>Dark primary: {dark.primary}</Text>
          <Text>Brand primary: {brand.primary}</Text>
          <Text>Branded dark primary: {brandedDark.primary}</Text>
        </Column>
      </Surface>
    </Host>
  );
}
```

### Reading colors outside React components

```tsx GetMaterialColorsExample.tsx
import {
  getMaterialColors,
  isDynamicColorAvailable,
} from '@expo/ui/jetpack-compose';

const palette = getMaterialColors({ seedColor: '#8E24AA' });
console.log(
  'available:',
  isDynamicColorAvailable,
  'primary:',
  palette.primary
);
```

## API

## Constants

### `MaterialColors.isDynamicColorAvailable`

Supported platforms: Android.

Type: `boolean`

Whether the current device supports Material You dynamic colors (Android 12+). When `false`, [`getMaterialColors`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#materialcolorsgetmaterialcolorsoptions) and [`useMaterialColors`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#usematerialcolorsoptions) return the static Material 3 baseline palette unless a `seedColor` is provided — seed-based palettes work on every Android API level.

## Hooks

### `useMaterialColors(options)`

Supported platforms: Android.

| Parameter | Type |
| --- | --- |
| `options`(optional) | [UseMaterialColorsOptions](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#usematerialcolorsoptions) |

  

Returns the Material 3 color palette. Call with no arguments inside a `<Host>` to get the palette that `<Host>` is themed with. Pass `scheme` and/or `seedColor` to get a specific palette.

Returns: `MaterialColors`

## Methods

### `MaterialColors.getMaterialColors(options)`

Supported platforms: Android.

| Parameter | Type |
| --- | --- |
| `options`(optional) | [MaterialColorsOptions](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#materialcolorsoptions) |

  

Get the Material 3 color palette.

Returns: `MaterialColors`

## Types

### `MaterialColors`

Supported platforms: Android.

Material 3 color palette exposed to TypeScript/JavaScript as `#RRGGBBAA` strings.

On Android 12+ devices these values are derived from the app user's wallpaper (Material You). On older devices they fall back to the static Material 3 baseline palette. Use [`isDynamicColorAvailable`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#materialcolorsisdynamiccoloravailable) to distinguish the two at runtime.

| Property | Type | Description |
| --- | --- | --- |
| background | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | The background color that appears behind scrollable content. |
| error | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | The error color is used to indicate errors in components, such as invalid text in a text field. |
| errorContainer | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | The preferred tonal color of error containers. |
| inverseOnSurface | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | A color that contrasts well with `inverseSurface`. Useful for content that sits on top of containers that are `inverseSurface`. |
| inversePrimary | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | Color to be used as a "primary" color in places where the inverse color scheme is needed, such as the button on a SnackBar. |
| inverseSurface | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | A color that contrasts sharply with `surface`. Useful for surfaces that sit on top of other surfaces with surface color. |
| onBackground | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | Color used for text and icons displayed on top of the background color. |
| onError | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | Color used for text and icons displayed on top of the error color. |
| onErrorContainer | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | The color (and state variants) that should be used for content on top of `errorContainer`. |
| onPrimary | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | Color used for text and icons displayed on top of the primary color. |
| onPrimaryContainer | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | The color (and state variants) that should be used for content on top of `primaryContainer`. |
| onPrimaryFixed | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | Color used for text and icons displayed on top of `primaryFixed` or `primaryFixedDim`. Maintains the same tone in light and dark themes. |
| onPrimaryFixedVariant | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | An `onPrimaryFixed` variant which provides less emphasis. Useful when a strong contrast is not required. |
| onSecondary | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | Color used for text and icons displayed on top of the secondary color. |
| onSecondaryContainer | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | The color (and state variants) that should be used for content on top of `secondaryContainer`. |
| onSecondaryFixed | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | Color used for text and icons displayed on top of `secondaryFixed` or `secondaryFixedDim`. Maintains the same tone in light and dark themes. |
| onSecondaryFixedVariant | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | An `onSecondaryFixed` variant which provides less emphasis. Useful when a strong contrast is not required. |
| onSurface | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | Color used for text and icons displayed on top of the surface color. |
| onSurfaceVariant | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | The color (and state variants) that can be used for content on top of `surface`. |
| onTertiary | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | Color used for text and icons displayed on top of the tertiary color. |
| onTertiaryContainer | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | The color (and state variants) that should be used for content on top of `tertiaryContainer`. |
| onTertiaryFixed | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | Color used for text and icons displayed on top of `tertiaryFixed` or `tertiaryFixedDim`. Maintains the same tone in light and dark themes. |
| onTertiaryFixedVariant | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | An `onTertiaryFixed` variant which provides less emphasis. Useful when a strong contrast is not required. |
| outline | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | Subtle color used for boundaries. Outline color role adds contrast for accessibility purposes. |
| outlineVariant | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | Utility color used for boundaries for decorative elements when strong contrast is not required. |
| primary | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | The primary color is the color displayed most frequently across your app's screens and components. |
| primaryContainer | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | The preferred tonal color of containers. |
| primaryFixed | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | A primary variant that maintains the same tone in light and dark themes. The fixed color role may be used instead of the equivalent container role in situations where such fixed behavior is desired. |
| primaryFixedDim | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | A primary variant that maintains the same tone in light and dark themes. Dim roles provide a stronger, more emphasized tone relative to the equivalent fixed color. |
| scrim | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | Color of a scrim that obscures content. |
| secondary | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | The secondary color provides more ways to accent and distinguish your product. Secondary colors are best for:
-   Floating action buttons
-   Selection controls, like checkboxes and radio buttons
-   Highlighting selected text
-   Links and headlines

 |
| secondaryContainer | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | A tonal color to be used in containers. |
| secondaryFixed | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | A secondary variant that maintains the same tone in light and dark themes. The fixed color role may be used instead of the equivalent container role in situations where such fixed behavior is desired. |
| secondaryFixedDim | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | A secondary variant that maintains the same tone in light and dark themes. Dim roles provide a stronger, more emphasized tone relative to the equivalent fixed color. |
| surface | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | The surface color that affect surfaces of components, such as cards, sheets, and menus. |
| surfaceBright | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | A surface variant that is always brighter than `surface`, whether in light or dark mode. |
| surfaceContainer | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | A surface variant that affects containers of components, such as cards, sheets, and menus. |
| surfaceContainerHigh | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | A surface variant for containers with higher emphasis than `surfaceContainer`. Use this role for content which requires more emphasis than `surfaceContainer`. |
| surfaceContainerHighest | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | A surface variant for containers with higher emphasis than `surfaceContainerHigh`. Use this role for content which requires more emphasis than `surfaceContainerHigh`. |
| surfaceContainerLow | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | A surface variant for containers with lower emphasis than `surfaceContainer`. Use this role for content which requires less emphasis than `surfaceContainer`. |
| surfaceContainerLowest | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | A surface variant for containers with lower emphasis than `surfaceContainerLow`. Use this role for content which requires less emphasis than `surfaceContainerLow`. |
| surfaceDim | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | A surface variant that is always dimmer than `surface`, whether in light or dark mode. |
| surfaceTint | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | This color will be used by components that apply tonal elevation and is applied on top of `surface`. The higher the elevation the more this color is used. |
| surfaceVariant | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | Another option for a color with similar uses of `surface`. |
| tertiary | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | The tertiary color that can be used to balance primary and secondary colors, or bring heightened attention to an element such as an input field. |
| tertiaryContainer | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | A tonal color to be used in containers. |
| tertiaryFixed | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | A tertiary variant that maintains the same tone in light and dark themes. The fixed color role may be used instead of the equivalent container role in situations where such fixed behavior is desired. |
| tertiaryFixedDim | [RgbaHex](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#rgbahex) | A tertiary variant that maintains the same tone in light and dark themes. Dim roles provide a stronger, more emphasized tone relative to the equivalent fixed color. |

### `MaterialColorsOptions`

Supported platforms: Android.

Options common to [`getMaterialColors`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#materialcolorsgetmaterialcolorsoptions) and [`useMaterialColors`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#usematerialcolorsoptions).

| Property | Type | Description |
| --- | --- | --- |
| scheme(optional) | `'light' | 'dark'` | Force a specific appearance. When omitted, the palette follows the current system dark/light mode. |
| seedColor(optional) | [ColorValue](https://reactnative.dev/docs/colors) | Seed color used to generate the full Material 3 palette via the `SchemeTonalSpot` variant (the same one Material You uses). When set, the palette is derived from this color on every Android device, including those below Android 12 where wallpaper-based dynamic colors are not available. When omitted, the palette comes from the device wallpaper (Android 12+) or the static Material 3 baseline. |

### `RgbaHex`

Supported platforms: Android.

8-digit RGBA hex color string, always in `#RRGGBBAA` form (uppercase). Compatible with React Native's `ColorValue`.

String union of `string` values.

### `UseMaterialColorsOptions`

Supported platforms: Android.

Options for [`useMaterialColors`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#usematerialcolorsoptions).

Type: [Omit](https://www.typescriptlang.org/docs/handbook/utility-types.html#omittype-keys)<[MaterialColorsOptions](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md#materialcolorsoptions), 'scheme'\> extended by:

| Property | Type | Description |
| --- | --- | --- |
| colorScheme(optional) | `ColorSchemeName` | `'light'` or `'dark'` force a specific palette. `'unspecified'`, `null`, or omitted follows the system appearance. |
