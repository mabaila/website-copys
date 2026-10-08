---
modificationDate: August 18, 2026
title: AccessoryWidgetBackground
description: A SwiftUI adaptive background view that provides a standard appearance based on the widget's environment.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['ios', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# AccessoryWidgetBackground

A SwiftUI adaptive background view that provides a standard appearance based on the widget's environment.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/swift-ui/accessorywidgetbackground/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/swift-ui/accessorywidgetbackground/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > SwiftUI (45 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
iOS, Included in Expo Go

Expo UI AccessoryWidgetBackground matches the official SwiftUI [AccessoryWidgetBackground API](https://developer.apple.com/documentation/widgetkit/accessorywidgetbackground) and creates an adaptive background view that provides a standard appearance based on the widget's environment.

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

### Basic accessory widget background

```tsx BasicAccessoryWidgetBackground.tsx
import {
  AccessoryWidgetBackground,
  VStack,
  Text,
  ZStack,
} from '@expo/ui/swift-ui';

export default function BasicAccessoryWidgetBackground() {
  return (
    <ZStack>
      <AccessoryWidgetBackground />
      <VStack>
        <Text>MON</Text>
      </VStack>
    </ZStack>
  );
}
```

## API

```tsx
import { AccessoryWidgetBackground } from '@expo/ui/swift-ui';
```

## Component

### `AccessoryWidgetBackground`

Supported platforms: iOS.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[AccessoryWidgetBackgroundProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/accessorywidgetbackground.md#accessorywidgetbackgroundprops)\>

AccessoryWidgetBackgroundProps

#### Inherited props

-   [CommonViewModifierProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md)
