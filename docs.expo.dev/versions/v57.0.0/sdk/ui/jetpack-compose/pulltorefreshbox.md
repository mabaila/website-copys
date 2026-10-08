---
modificationDate: August 18, 2026
title: PullToRefreshBox
description: A Jetpack Compose PullToRefreshBox component for pull-to-refresh interactions.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['android', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# PullToRefreshBox

A Jetpack Compose PullToRefreshBox component for pull-to-refresh interactions.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/jetpack-compose/pulltorefreshbox/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/jetpack-compose/pulltorefreshbox/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > Jetpack Compose (51 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, Included in Expo Go

> For a cross-platform list with pull-to-refresh, see [`List`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/universal/list.md) — built on top of `PullToRefreshBox` on Android.

Expo UI PullToRefreshBox matches the official Jetpack Compose [PullToRefreshBox](https://developer.android.com/reference/kotlin/androidx/compose/material3/pulltorefresh/package-summary#PullToRefreshBox\(kotlin.Boolean,kotlin.Function0,androidx.compose.ui.Modifier,androidx.compose.material3.pulltorefresh.PullToRefreshState,androidx.compose.ui.Alignment,kotlin.Function1,kotlin.Function1\)) API. It wraps scrollable content and shows a refresh indicator when pulled.

Image: PullToRefreshBox showing the Material 3 loading indicator above a list

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

### Basic pull to refresh

Wrap scrollable content in a `PullToRefreshBox` to add pull-to-refresh behavior.

```tsx BasicPullToRefresh.tsx
import { useState, useCallback } from 'react';
import {
  Host,
  PullToRefreshBox,
  LazyColumn,
  ListItem,
  Text,
} from '@expo/ui/jetpack-compose';

export default function BasicPullToRefresh() {
  const [refreshing, setRefreshing] = useState(false);

  const onRefresh = useCallback(() => {
    setRefreshing(true);
    setTimeout(() => {
      setRefreshing(false);
    }, 2000);
  }, []);

  return (
    <Host style={{ height: 400 }}>
      <PullToRefreshBox
        isRefreshing={refreshing}
        onRefresh={onRefresh}>
        <LazyColumn>
          <ListItem>
            <ListItem.HeadlineContent>
              <Text>Item 1</Text>
            </ListItem.HeadlineContent>
          </ListItem>
          <ListItem>
            <ListItem.HeadlineContent>
              <Text>Item 2</Text>
            </ListItem.HeadlineContent>
          </ListItem>
          <ListItem>
            <ListItem.HeadlineContent>
              <Text>Item 3</Text>
            </ListItem.HeadlineContent>
          </ListItem>
          <ListItem>
            <ListItem.HeadlineContent>
              <Text>Item 4</Text>
            </ListItem.HeadlineContent>
          </ListItem>
          <ListItem>
            <ListItem.HeadlineContent>
              <Text>Item 5</Text>
            </ListItem.HeadlineContent>
          </ListItem>
        </LazyColumn>
      </PullToRefreshBox>
    </Host>
  );
}
```

### Custom indicator colors

Use the `indicator` prop to customize the spinner and container colors.

```tsx CustomIndicatorColors.tsx
import { useState, useCallback } from 'react';
import {
  Host,
  PullToRefreshBox,
  LazyColumn,
  ListItem,
  Text,
} from '@expo/ui/jetpack-compose';

export default function CustomIndicatorColors() {
  const [refreshing, setRefreshing] = useState(false);

  const onRefresh = useCallback(() => {
    setRefreshing(true);
    setTimeout(() => {
      setRefreshing(false);
    }, 2000);
  }, []);

  return (
    <Host style={{ height: 400 }}>
      <PullToRefreshBox
        isRefreshing={refreshing}
        onRefresh={onRefresh}
        indicator={{ color: '#6200EE', containerColor: '#F5F5F5' }}>
        <LazyColumn>
          <ListItem>
            <ListItem.HeadlineContent>
              <Text>Item 1</Text>
            </ListItem.HeadlineContent>
          </ListItem>
          <ListItem>
            <ListItem.HeadlineContent>
              <Text>Item 2</Text>
            </ListItem.HeadlineContent>
          </ListItem>
          <ListItem>
            <ListItem.HeadlineContent>
              <Text>Item 3</Text>
            </ListItem.HeadlineContent>
          </ListItem>
        </LazyColumn>
      </PullToRefreshBox>
    </Host>
  );
}
```

## API

```tsx
import { PullToRefreshBox } from '@expo/ui/jetpack-compose';
```

## Component

### `PullToRefreshBox`

Supported platforms: Android.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[PullToRefreshBoxProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/pulltorefreshbox.md#pulltorefreshboxprops)\>

A pull-to-refresh container that wraps scrollable content and shows a refresh indicator when pulled, matching Compose's `PullToRefreshBox`.

PullToRefreshBoxProps

### `children`

Supported platforms: Android.

Type: [ReactNode](https://reactnative.dev/docs/react-node)

The content to refresh.

### `contentAlignment`

Supported platforms: Android.

Optional • Type: `ContentAlignment` • Default: `'topStart'`

Alignment of children within the box.

### `indicator`

Supported platforms: Android.

Optional • Type: `PullToRefreshIndicatorProps`

Configuration for the loading indicator shown during pull-to-refresh.

### `isRefreshing`

Supported platforms: Android.

Optional • Type: `boolean` • Default: `false`

Whether the content is refreshing.

### `modifiers`

Supported platforms: Android.

Optional • Type: `ModifierConfig[]`

Modifiers for the component.

### `onRefresh`

Supported platforms: Android.

Optional • Type: `() => void`

Callback that is called when the user pulls to refresh.
