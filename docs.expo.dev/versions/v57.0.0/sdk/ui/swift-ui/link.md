---
modificationDate: August 18, 2026
title: Link
description: A SwiftUI Link component for displaying clickable links.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['ios', 'tvos', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# Link

A SwiftUI Link component for displaying clickable links.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/swift-ui/link/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/swift-ui/link/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > SwiftUI (45 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
iOS, tvOS, Included in Expo Go

Expo UI Link matches the official SwiftUI [Link API](https://developer.apple.com/documentation/swiftui/link).

Image: Three Link rows opening external URLs

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

### Basic link

```tsx BasicLinkExample.tsx
import { Host, Link } from '@expo/ui/swift-ui';

export default function BasicLinkExample() {
  return (
    <Host style={{ flex: 1 }}>
      <Link label="Visit Expo" destination="https://expo.dev" />
    </Host>
  );
}
```

### Custom label content

You can pass custom components as `children` for more complex link label content.

```tsx CustomContentExample.tsx
import { Host, Link, VStack, Image, Text } from '@expo/ui/swift-ui';

export default function CustomContentExample() {
  return (
    <Host style={{ flex: 1 }}>
      <Link destination="https://expo.dev">
        <VStack spacing={4}>
          <Image systemName="link" />
          <Text>Expo</Text>
        </VStack>
      </Link>
    </Host>
  );
}
```

## API

```tsx
import { Link } from '@expo/ui/swift-ui';
```

## Component

### `Link`

Supported platforms: iOS, tvOS.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[LinkProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/link.md#linkprops)\>

Displays a native link component.

Example

```tsx
import { Link } from '@expo/ui/swift-ui';
import { foregroundStyle, font } from '@expo/ui/swift-ui/modifiers';

<Link
  label="Open"
  destination="https://expo.dev"
  modifiers={[
    foregroundStyle('red'),
    font({ size: 24, weight: 'bold' })
  ]}
/>
```

LinkProps

### `children`

Supported platforms: iOS, tvOS.

Optional • Literal type: `union`

Custom content for the link label. Use this for custom label views. Only nested elements are supported, not plain strings.

Acceptable values are: `ReactElement<unknown, string | JSXElementConstructor<any>>` | `ReactElement[]`

### `destination`

Supported platforms: iOS, tvOS.

Type: `string`

The URL for the link.

### `label`

Supported platforms: iOS, tvOS.

Optional • Type: `string`

The text label for the Link. Use this for simple text links.

#### Inherited props

-   [CommonViewModifierProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/modifiers.md)
