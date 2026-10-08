---
modificationDate: August 18, 2026
title: DockedSearchBar
description: A Jetpack Compose DockedSearchBar component for displaying an inline search input.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['android', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# DockedSearchBar

A Jetpack Compose DockedSearchBar component for displaying an inline search input.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/jetpack-compose/dockedsearchbar/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/jetpack-compose/dockedsearchbar/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > Jetpack Compose (51 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, Included in Expo Go

Expo UI DockedSearchBar matches the official Jetpack Compose [SearchBar API](https://developer.android.com/develop/ui/compose/components/search-bar) and displays a search input that remains anchored in its parent layout rather than expanding to full screen.

Image: Material 3 docked search bar with search icon and placeholder text

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

### Basic docked search bar

```tsx BasicDockedSearchBarExample.tsx
import { useState } from 'react';
import { Host, DockedSearchBar } from '@expo/ui/jetpack-compose';

export default function BasicDockedSearchBarExample() {
  const [query, setQuery] = useState('');

  return (
    <Host matchContents>
      <DockedSearchBar onQueryChange={setQuery} />
    </Host>
  );
}
```

### With placeholder and leading icon

Use the `DockedSearchBar.Placeholder` and `DockedSearchBar.LeadingIcon` slot components to customize the search bar appearance.

```tsx DockedSearchBarWithSlotsExample.tsx
import { useState } from 'react';
import {
  Host,
  DockedSearchBar,
  Text,
} from '@expo/ui/jetpack-compose';

export default function DockedSearchBarWithSlotsExample() {
  const [query, setQuery] = useState('');

  return (
    <Host matchContents>
      <DockedSearchBar onQueryChange={setQuery}>
        <DockedSearchBar.Placeholder>
          <Text>Search items...</Text>
        </DockedSearchBar.Placeholder>
        <DockedSearchBar.LeadingIcon>
          <Text>🔍</Text>
        </DockedSearchBar.LeadingIcon>
      </DockedSearchBar>
    </Host>
  );
}
```

## API

```tsx
import { DockedSearchBar } from '@expo/ui/jetpack-compose';
```

## Components

### `DockedSearchBar`

Supported platforms: Android.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[DockedSearchBarProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/dockedsearchbar.md#dockedsearchbarprops)\>

DockedSearchBarProps

### `children`

Supported platforms: Android.

Optional • Type: [ReactNode](https://reactnative.dev/docs/react-node)

The children of the component.

### `modifiers`

Supported platforms: Android.

Optional • Type: `ModifierConfig[]`

Modifiers for the component.

### `onQueryChange`

Supported platforms: Android.

Optional • Type: `(query: string) => void`

Callback function that is called when the search query changes.

### `DockedSearchBarLeadingIcon`

Supported platforms: Android.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<LeadingIconProps\>

### `DockedSearchBarPlaceholder`

Supported platforms: Android.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<PlaceholderProps\>
