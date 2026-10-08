---
modificationDate: August 18, 2026
title: Badge
description: A Jetpack Compose Badge component for displaying status indicators and counts.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['android', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# Badge

A Jetpack Compose Badge component for displaying status indicators and counts.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/jetpack-compose/badge/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/jetpack-compose/badge/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > Jetpack Compose (51 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, Included in Expo Go

Expo UI Badge matches the official Jetpack Compose [`Badge`](https://developer.android.com/develop/ui/compose/components/badges) API. It renders as a small colored indicator dot, or with content such as a count number.

Image: Material 3 badges showing count and dot indicators on icons

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

### Indicator dot

A badge with no children renders as a small dot indicator.

```tsx BadgeDot.tsx
import { Host, Badge } from '@expo/ui/jetpack-compose';

export default function BadgeDot() {
  return (
    <Host matchContents>
      <Badge />
    </Host>
  );
}
```

### Badge with count

Pass a `Text` child to display a number or label.

```tsx BadgeCount.tsx
import { Host, Badge, Text } from '@expo/ui/jetpack-compose';

export default function BadgeCount() {
  return (
    <Host matchContents>
      <Badge containerColor="#EF5350" contentColor="#FFFFFF">
        <Text>3</Text>
      </Badge>
    </Host>
  );
}
```

## API

```tsx
import { Badge } from '@expo/ui/jetpack-compose';
```

## Component

### `Badge`

Supported platforms: Android.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[BadgeProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/badge.md#badgeprops)\>

A badge component matching Compose's `Badge`. Renders as a small colored indicator dot, or with content (for example, a count).

> **See:** [Jetpack Compose Badge](https://developer.android.com/develop/ui/compose/components/badges)

BadgeProps

### `children`

Supported platforms: Android.

Optional • Type: [ReactNode](https://reactnative.dev/docs/react-node)

Optional content inside the badge (for example, a `Text` with a count). When omitted, renders as a small indicator dot.

### `containerColor`

Supported platforms: Android.

Optional • Type: [ColorValue](https://reactnative.dev/docs/colors) • Default: `BadgeDefaults.containerColor`

Background color of the badge.

### `contentColor`

Supported platforms: Android.

Optional • Type: [ColorValue](https://reactnative.dev/docs/colors) • Default: `BadgeDefaults.contentColor`

Content color inside the badge (text/icon tint).

### `modifiers`

Supported platforms: Android.

Optional • Type: `ModifierConfig[]`

Modifiers for the component.
