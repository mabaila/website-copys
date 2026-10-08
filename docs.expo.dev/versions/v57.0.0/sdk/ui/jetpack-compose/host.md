---
modificationDate: August 18, 2026
title: Host
description: A Jetpack Compose Host component for bridging React Native and Jetpack Compose.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['android', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# Host

A Jetpack Compose Host component for bridging React Native and Jetpack Compose.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/jetpack-compose/host/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/jetpack-compose/host/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > Jetpack Compose (51 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, Included in Expo Go

> For cross-platform usage, see the universal [`Host`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/host.md) — it renders the appropriate native component per platform.

The `Host` component is the bridge between React Native and Jetpack Compose. Every Jetpack Compose component from `@expo/ui/jetpack-compose` must be wrapped in a `Host` to render correctly.

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

### Match contents

Use the `matchContents` prop to make the `Host` size itself to fit the content. You can pass a boolean or an object to control vertical and horizontal sizing independently.

```tsx MatchContents.tsx
import { Host, Button } from '@expo/ui/jetpack-compose';

export default function MatchContents() {
  return (
    <Host matchContents>
      <Button onClick={() => console.log('Pressed')}>
        Sized to content
      </Button>
    </Host>
  );
}
```

> **Note:** Do not use `matchContents` on the same axis as a scrollable child (`LazyRow`, `LazyColumn`, `Carousel`, or anything using `Modifier.horizontalScroll`/`verticalScroll`). Scrollables require a finite max constraint on their scroll axis and `matchContents` propagates an unbounded one.

The following example crashes:

```tsx MatchContentsCrash.tsx
import { Host, LazyRow, Text } from '@expo/ui/jetpack-compose';

export default function MatchContentsCrash() {
  return (
    <Host matchContents>
      <LazyRow>
        {Array.from({ length: 5 }).map((_, i) => (
          <Text key={i}>Item {i}</Text>
        ))}
      </LazyRow>
    </Host>
  );
}
```

Either drop `matchContents` on the scroll axis or give the `Host` a finite size on that axis via `style`:

```tsx MatchContentsFix.tsx
import { Host, LazyRow, Text } from '@expo/ui/jetpack-compose';

export default function MatchContentsFix() {
  return (
    <Host
      matchContents={{ vertical: true }}
      style={{ width: '100%' }}>
      <LazyRow>
        {Array.from({ length: 5 }).map((_, i) => (
          <Text key={i}>Item {i}</Text>
        ))}
      </LazyRow>
    </Host>
  );
}
```

### With style

Apply standard React Native styles to the `Host` wrapper.

```tsx HostWithStyle.tsx
import { Host, Button } from '@expo/ui/jetpack-compose';

export default function HostWithStyle() {
  return (
    <Host
      style={{
        padding: 16,
        backgroundColor: '#f0f0f0',
        borderRadius: 8,
      }}>
      <Button onClick={() => console.log('Pressed')}>
        Styled host
      </Button>
    </Host>
  );
}
```

## API

```tsx
import { Host } from '@expo/ui/jetpack-compose';
```

## Component

### `Host`

Supported platforms: Android.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[HostProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/host.md#hostprops)\>

HostProps

### `children`

Supported platforms: Android.

Type: [ReactNode](https://reactnative.dev/docs/react-node)

### `colorScheme`

Supported platforms: Android.

Optional • Type: `ColorSchemeName`

The color scheme of the host view. `'light'` / `'dark'` force a specific appearance; omitted follows the device setting. The palette itself follows the device wallpaper on Android 12+ (Material You) or the static Material 3 baseline otherwise — unless [`seedColor`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/host.md#seedcolor) is set.

### `ignoreSafeAreaKeyboardInsets`

Supported platforms: Android.

Optional • Type: `boolean` • Default: `false`

When `true`, the Compose content will not perform keyboard avoidance behaviour when keyboard is shown. Can be only set once on mount.

### `layoutDirection`

Supported platforms: Android.

Optional • Literal type: `string`

The layout direction for the content. Defaults to the current locale direction from I18nManager.

Acceptable values are: `'leftToRight'` | `'rightToLeft'`

### `matchContents`

Supported platforms: Android.

Optional • Literal type: `union` • Default: `false`

When true, the host view will update its size in the React Native view tree to match the content's layout from Jetpack Compose. Can be only set once on mount.

Acceptable values are: `boolean` | `{ horizontal: boolean, vertical: boolean }`

### `onLayoutContent`

Supported platforms: Android.

Optional • Type: `(event: { nativeEvent: { height: number, width: number } }) => void`

Callback function that is triggered when the Jetpack Compose content completes its layout. Provides the current dimensions of the content, which may change as the content updates.

### `pointerEvents`

Supported platforms: Android.

Optional • Literal type: `string`

Acceptable values are: `'box-none'` | `'none'` | `'box-only'` | `'auto'`

### `seedColor`

Supported platforms: Android.

Optional • Type: [ColorValue](https://reactnative.dev/docs/colors)

Seed color used to generate a Material 3 palette (`SchemeTonalSpot`) for this host. Combines with `colorScheme` (`'light'` / `'dark'` or omitted) to produce a seeded palette that themes Compose children and is available to descendants via `useMaterialColors()`.

### `style`

Supported platforms: Android.

Optional • Type: StyleProp<[ViewStyle](https://reactnative.dev/docs/view-style-props)\>

### `useViewportSizeMeasurement`

Supported platforms: Android.

Optional • Type: `boolean` • Default: `false`

When true and no explicit size is provided, the host will use the viewport size as the proposed size for Compose layout. This is particularly useful for views that need to fill their available space.

#### Inherited props

-   `PrimitiveBaseProps`
