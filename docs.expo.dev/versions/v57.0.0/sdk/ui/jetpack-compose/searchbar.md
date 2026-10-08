---
modificationDate: August 18, 2026
title: SearchBar
description: A Jetpack Compose SearchBar component for search input functionality.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['android', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# SearchBar

A Jetpack Compose SearchBar component for search input functionality.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/jetpack-compose/searchbar/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/jetpack-compose/searchbar/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > Jetpack Compose (51 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, Included in Expo Go

Expo UI SearchBar matches the official Jetpack Compose [Search](https://developer.android.com/develop/ui/compose/components/search-bar) API and provides a search input with support for placeholder text and expanded full-screen search.

Image: Material 3 search bar with placeholder text

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

### Basic search bar

```tsx BasicSearchBarExample.tsx
import { useState } from 'react';
import { Host, SearchBar } from '@expo/ui/jetpack-compose';

export default function BasicSearchBarExample() {
  const [query, setQuery] = useState('');

  return (
    <Host matchContents>
      <SearchBar onSearch={searchText => setQuery(searchText)} />
    </Host>
  );
}
```

### Search bar with placeholder

Use the `SearchBar.Placeholder` sub-component to display hint text when the search field is empty.

```tsx SearchBarPlaceholderExample.tsx
import { useState } from 'react';
import { Host, SearchBar, Text } from '@expo/ui/jetpack-compose';

export default function SearchBarPlaceholderExample() {
  const [query, setQuery] = useState('');

  return (
    <Host matchContents>
      <SearchBar onSearch={searchText => setQuery(searchText)}>
        <SearchBar.Placeholder>
          <Text>Search items...</Text>
        </SearchBar.Placeholder>
      </SearchBar>
    </Host>
  );
}
```

## API

```tsx
import { SearchBar } from '@expo/ui/jetpack-compose';
```

## Components

### `ExpandedFullScreenSearchBar`

Supported platforms: Android.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<ExpandedFullScreenSearchBarProps\>

ExpandedFullScreenSearchBar component for SearchBar. This component marks its children to be rendered in the expanded full-screen search bar.

### `SearchBar`

Supported platforms: Android.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<SearchBarProps\>

Renders a `SearchBar` component.

SearchBarProps

### `children`

Supported platforms: Android.

Optional • Type: [ReactNode](https://reactnative.dev/docs/react-node)

The children of the component.

### `modifiers`

Supported platforms: Android.

Optional • Type: `ModifierConfig[]`

Modifiers for the component.

### `onSearch`

Supported platforms: Android.

Optional • Type: `(searchText: string) => void`

Callback function that is called when the search text is submitted.

### `SearchBarPlaceholder`

Supported platforms: Android.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<PlaceholderProps\>

Placeholder component for SearchBar. This component marks its children to be rendered in the placeholder slot.
