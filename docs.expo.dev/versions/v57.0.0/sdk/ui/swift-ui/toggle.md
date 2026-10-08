---
modificationDate: September 18, 2026
title: Toggle
description: A SwiftUI Toggle component for displaying native toggles.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['ios', 'tvos', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# Toggle

A SwiftUI Toggle component for displaying native toggles.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/swift-ui/toggle/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/swift-ui/toggle/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > SwiftUI (45 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
iOS, tvOS, Included in Expo Go

> For cross-platform usage, see the universal [`Switch`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/switch.md) — it renders the appropriate native component per platform.

Expo UI Toggle matches the official SwiftUI [Toggle API](https://developer.apple.com/documentation/swiftui/toggle) and supports styling via the [`toggleStyle`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md#togglestylestyle) modifier.

Image: Toggle rows inside a Form

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

### Basic toggle

```tsx BasicToggleExample.tsx
import { useState } from 'react';
import { Host, Toggle } from '@expo/ui/swift-ui';

export default function BasicToggleExample() {
  const [isOn, setIsOn] = useState(false);

  // A toggle row stretches to the width it is given, so give the host a size.
  return (
    <Host style={{ flex: 1 }}>
      <Toggle
        isOn={isOn}
        onIsOnChange={setIsOn}
        label="Enable feature"
      />
    </Host>
  );
}
```

### Toggle with system image

```tsx ToggleWithImageExample.tsx
import { useState } from 'react';
import { Host, Toggle } from '@expo/ui/swift-ui';

export default function ToggleWithImageExample() {
  const [airplaneMode, setAirplaneMode] = useState(false);

  return (
    <Host style={{ flex: 1 }}>
      <Toggle
        isOn={airplaneMode}
        onIsOnChange={setAirplaneMode}
        label="Airplane Mode"
        systemImage="airplane"
      />
    </Host>
  );
}
```

### Toggle styles

Use the `toggleStyle` modifier to change the toggle's appearance. Available styles are: `automatic`, `switch`, and `button`.

> **Note:** The `button` style is not available on tvOS.

```tsx ToggleStylesExample.tsx
import { useState } from 'react';
import { Host, Toggle, VStack } from '@expo/ui/swift-ui';
import { toggleStyle } from '@expo/ui/swift-ui/modifiers';

export default function ToggleStylesExample() {
  const [isOn, setIsOn] = useState(true);

  return (
    <Host style={{ flex: 1 }}>
      <VStack spacing={8}>
        <Toggle
          isOn={isOn}
          onIsOnChange={setIsOn}
          label="Switch Style"
          modifiers={[toggleStyle('switch')]}
        />
        <Toggle
          isOn={isOn}
          onIsOnChange={setIsOn}
          label="Button Style"
          modifiers={[toggleStyle('button')]}
        />
      </VStack>
    </Host>
  );
}
```

### Tinted toggle

Use the `tint` modifier to change the toggle's color.

```tsx TintedToggleExample.tsx
import { useState } from 'react';
import { Host, Toggle } from '@expo/ui/swift-ui';
import { tint } from '@expo/ui/swift-ui/modifiers';

export default function TintedToggleExample() {
  const [isOn, setIsOn] = useState(true);

  return (
    <Host matchContents>
      <Toggle
        isOn={isOn}
        onIsOnChange={setIsOn}
        label="Custom Color"
        modifiers={[tint('#FF9500')]}
      />
    </Host>
  );
}
```

### Custom label content

You can pass custom components as `children` for more complex toggle labels. Use multiple `Text` views where the first represents the title and the second represents the subtitle.

```tsx CustomLabelExample.tsx
import { useState } from 'react';
import { Host, Toggle, Text } from '@expo/ui/swift-ui';

export default function CustomLabelExample() {
  const [vibrateOnRing, setVibrateOnRing] = useState(false);

  return (
    <Host style={{ flex: 1 }}>
      <Toggle isOn={vibrateOnRing} onIsOnChange={setVibrateOnRing}>
        <Text>Vibrate on ring</Text>
        <Text>Enable vibration when the phone rings</Text>
      </Toggle>
    </Host>
  );
}
```

### Hidden label

Use the [`labelsHidden`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md#labelshidden) modifier to hide the label while keeping it for accessibility.

```tsx HiddenLabelExample.tsx
import { useState } from 'react';
import { Host, Toggle } from '@expo/ui/swift-ui';
import { labelsHidden } from '@expo/ui/swift-ui/modifiers';

export default function HiddenLabelExample() {
  const [isOn, setIsOn] = useState(false);

  return (
    <Host style={{ flex: 1 }}>
      <Toggle
        isOn={isOn}
        onIsOnChange={setIsOn}
        label="Hidden Label"
        modifiers={[labelsHidden()]}
      />
    </Host>
  );
}
```

## API

```tsx
import { Toggle } from '@expo/ui/swift-ui';
```

## Component

### `Toggle`

Supported platforms: iOS, tvOS.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[ToggleProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/toggle.md#toggleprops)\>

A control that toggles between on and off states.

ToggleProps

### `children`

Supported platforms: iOS, tvOS.

Optional • Type: [ReactNode](https://reactnative.dev/docs/react-node)

Custom content for the toggle label. Use multiple `Text` views where the first represents the title and the second represents the subtitle.

### `isOn`

Supported platforms: iOS, tvOS.

Optional • Type: `boolean`

A Boolean value that determines the on/off state of the toggle.

### `label`

Supported platforms: iOS, tvOS.

Optional • Type: `string`

A string that describes the purpose of the toggle.

### `onIsOnChange`

Supported platforms: iOS, tvOS.

Optional • Type: `(isOn: boolean) => void`

A callback that is called when the toggle's state changes.

`isOn: boolean`

The new state of the toggle.

### `systemImage`

Supported platforms: iOS, tvOS.

Optional • Type: [SFSymbols7_0](https://github.com/nandorojo/sf-symbols-typescript)

The name of the SF Symbol to display alongside the label.

#### Inherited props

-   [CommonViewModifierProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md)
