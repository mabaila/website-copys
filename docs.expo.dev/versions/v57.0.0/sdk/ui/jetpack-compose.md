---
modificationDate: September 23, 2026
title: Jetpack Compose
description: Jetpack Compose components for building native Android interfaces with @expo/ui.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['android', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# Jetpack Compose

Jetpack Compose components for building native Android interfaces with @expo/ui.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/jetpack-compose/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/jetpack-compose/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > Jetpack Compose (51 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, Included in Expo Go

The Jetpack Compose components in `@expo/ui/jetpack-compose` allow you to build fully native Android interfaces using Jetpack Compose from React Native.

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

Using a component from `@expo/ui/jetpack-compose` requires wrapping it in a [`Host`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/host.md) component. The `Host` is a container for Jetpack Compose views.

```tsx
import { Host, Button } from '@expo/ui/jetpack-compose';

export function SaveButton() {
  return (
    <Host matchContents>
      <Button onClick={() => alert('Saved!')}>Save changes</Button>
    </Host>
  );
}
```

[Extending with Jetpack Compose](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/extending.md) — Create custom Jetpack Compose components and modifiers that integrate with Expo UI.

## Available components

| Component | Description |
| --- | --- |
| [`AlertDialog`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/alertdialog.md) | AlertDialog component for displaying native alert dialogs. |
| [`Badge`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/badge.md) | Badge component for displaying status indicators and counts. |
| [`BadgedBox`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/badgedbox.md) | BadgedBox component for overlaying badges on content. |
| [`BasicAlertDialog`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/basicalertdialog.md) | BasicAlertDialog component for displaying dialogs with custom content. |
| [`Box`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/box.md) | Box component for stacking child elements. |
| [`Button`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/button.md) | Button components for displaying native Material3 buttons. |
| [`Card`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/card.md) | Card component for displaying content in a styled container. |
| [`Carousel`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/carousel.md) | Carousel components for displaying scrollable collections of items. |
| [`Checkbox`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/checkbox.md) | Checkbox component for selection controls. |
| [`Chip`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/chip.md) | Chip components for displaying compact elements. |
| [`Column`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/column.md) | Column component for placing children vertically. |
| [`DateTimePicker`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/datetimepicker.md) | DateTimePicker component for selecting dates and times. |
| [`Divider`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/divider.md) | Divider components for creating visual separators. |
| [`DockedSearchBar`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/dockedsearchbar.md) | DockedSearchBar component for displaying an inline search input. |
| [`DropdownMenu`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/dropdownmenu.md) | DropdownMenu component for displaying dropdown menus. |
| [`ExposedDropdownMenuBox`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/exposeddropdownmenubox.md) | ExposedDropdownMenuBox component for displaying a dropdown menu with a customizable anchor. |
| [`FloatingActionButton`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/floatingactionbutton.md) | FloatingActionButton components following Material Design 3. |
| [`FlowRow`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/flowrow.md) | FlowRow component for wrapping children horizontally. |
| [`HorizontalFloatingToolbar`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/horizontalfloatingtoolbar.md) | HorizontalFloatingToolbar component for displaying a floating action bar. |
| [`HorizontalPager`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/horizontalpager.md) | HorizontalPager component for swipeable pages. |
| [`Host`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/host.md) | Host component for bridging React Native and Jetpack Compose. |
| [`Icon`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/icon.md) | Icon component for displaying icons. |
| [`IconButton`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/iconbutton.md) | IconButton components for displaying native Material3 icon buttons. |
| [`LazyColumn`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/lazycolumn.md) | LazyColumn component for displaying scrollable lists. |
| [`LazyRow`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/lazyrow.md) | LazyRow component for displaying horizontally scrolling lists. |
| [`ListItem`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/listitem.md) | ListItem component for displaying structured list entries. |
| [`LoadingIndicator`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/loadingindicator.md) | Loading indicator components for displaying loading state. |
| [`Material Colors`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/colors.md) | Read the Material 3 color palette (including Material 3 Dynamic Colors) from JavaScript. |
| [`ModalBottomSheet`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/bottomsheet.md) | ModalBottomSheet component that presents content from the bottom of the screen. |
| [`Modifiers`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/modifiers.md) | Layout modifiers for @expo/ui components. |
| [`NavigationBar`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/navigationbar.md) | NavigationBar component for Material 3 bottom navigation. |
| [`Progress indicators`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/progress.md) | Progress indicator components for displaying operation status. |
| [`PullToRefreshBox`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/pulltorefreshbox.md) | PullToRefreshBox component for pull-to-refresh interactions. |
| [`RadioButton`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/radiobutton.md) | RadioButton component for single-selection controls. |
| [`RNHostView`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/rnhostview.md) | A component that enables React Native views inside Jetpack Compose. |
| [`Row`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/row.md) | Row component for placing children horizontally. |
| [`SearchBar`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/searchbar.md) | SearchBar component for search input functionality. |
| [`SegmentedButton`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/segmentedbutton.md) | Segmented Button components for single or multi-choice selection. |
| [`Shape`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/shape.md) | Shape component for drawing geometric shapes. |
| [`Slider`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/slider.md) | Slider component for selecting values from a range. |
| [`Snackbar`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/snackbar.md) | A brief notification that appears at the bottom of the screen to provide feedback without interrupting the user. |
| [`Spacer`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/spacer.md) | Spacer component for adding flexible space between elements. |
| [`Surface`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/surface.md) | Surface component for styled content containers. |
| [`Switch`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/switch.md) | Switch component for toggle controls. |
| [`Text`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/text.md) | Text component for displaying styled text. |
| [`TextField`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/textfield.md) | TextField components for native Material3 text input. |
| [`ToggleButton`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/togglebutton.md) | ToggleButton components for displaying native Material3 toggle buttons. |
| [`Tooltip`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/tooltip.md) | Tooltip components for displaying contextual information on long-press. |
| [`useNativeState`](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/usenativestate.md) | A React hook that creates observable state shared between JavaScript and native Jetpack Compose views. |

## Examples

### Modifiers

Modifiers are applied with the `modifiers` prop, in array order. Put `background` before `paddingAll` so the padding sits inside the background rather than outside it.

```tsx ComposeModifiersExample.tsx
import { Column, Host, Text } from '@expo/ui/jetpack-compose';
import {
  background,
  border,
  fillMaxWidth,
  paddingAll,
  shadow,
} from '@expo/ui/jetpack-compose/modifiers';

export default function ComposeModifiersExample() {
  return (
    <Host style={{ flex: 1 }}>
      <Column
        verticalArrangement={{ spacedBy: 16 }}
        modifiers={[paddingAll(16)]}>
        <Text
          color="#FFFFFF"
          modifiers={[
            fillMaxWidth(),
            shadow(4),
            background('#6750A4'),
            paddingAll(16),
          ]}>
          Background, shadow and padding
        </Text>
        <Text
          color="#1D192B"
          modifiers={[
            fillMaxWidth(),
            background('#E8DEF8'),
            border(2, '#6750A4'),
            paddingAll(16),
          ]}>
          Background, border and padding
        </Text>
      </Column>
    </Host>
  );
}
```

### Settings screen

Combine `ListItem` slots with a `Switch` and an `Icon` to build a Material 3 settings screen.

```tsx ComposeSettingsScreenExample.tsx
import {
  Column,
  Host,
  Icon,
  ListItem,
  Switch,
  Text,
  useMaterialColors,
} from '@expo/ui/jetpack-compose';
import ChevronRight from '@expo/material-symbols/chevron_right.xml';
import Flight from '@expo/material-symbols/flight.xml';
import Wifi from '@expo/material-symbols/wifi.xml';
import { useState } from 'react';

export default function ComposeSettingsScreenExample() {
  const [airplaneMode, setAirplaneMode] = useState(true);
  const colors = useMaterialColors();

  return (
    <Host style={{ flex: 1 }}>
      <Column>
        <ListItem>
          <ListItem.LeadingContent>
            <Icon
              source={Flight}
              tint={colors.onSurfaceVariant}
              contentDescription="Airplane mode"
            />
          </ListItem.LeadingContent>
          <ListItem.HeadlineContent>
            <Text>Airplane mode</Text>
          </ListItem.HeadlineContent>
          <ListItem.TrailingContent>
            <Switch
              value={airplaneMode}
              onCheckedChange={setAirplaneMode}
            />
          </ListItem.TrailingContent>
        </ListItem>
        <ListItem>
          <ListItem.LeadingContent>
            <Icon
              source={Wifi}
              tint={colors.onSurfaceVariant}
              contentDescription="Wi-Fi"
            />
          </ListItem.LeadingContent>
          <ListItem.HeadlineContent>
            <Text>Wi-Fi</Text>
          </ListItem.HeadlineContent>
          <ListItem.SupportingContent>
            <Text>Expo Guest</Text>
          </ListItem.SupportingContent>
          <ListItem.TrailingContent>
            <Icon
              source={ChevronRight}
              tint={colors.onSurfaceVariant}
              contentDescription="Open"
            />
          </ListItem.TrailingContent>
        </ListItem>
      </Column>
    </Host>
  );
}
```

### Brightness row

A common pattern for brightness or volume controls is to flank a `Slider` with icons. Give the `Slider` a `weight` modifier so it takes the space left over by the icons.

```tsx ComposeBrightnessRowExample.tsx
import {
  Host,
  Icon,
  Row,
  Slider,
  useMaterialColors,
} from '@expo/ui/jetpack-compose';
import {
  paddingAll,
  weight,
} from '@expo/ui/jetpack-compose/modifiers';
import BacklightHigh from '@expo/material-symbols/backlight_high.xml';
import BacklightLow from '@expo/material-symbols/backlight_low.xml';
import { useState } from 'react';

export default function ComposeBrightnessRowExample() {
  const [brightness, setBrightness] = useState(0.5);
  const colors = useMaterialColors();

  return (
    <Host style={{ flex: 1 }}>
      <Row
        verticalAlignment="center"
        horizontalArrangement={{ spacedBy: 12 }}
        modifiers={[paddingAll(16)]}>
        <Icon
          source={BacklightLow}
          tint={colors.onSurfaceVariant}
          contentDescription="Dimmer"
        />
        <Slider
          value={brightness}
          onValueChange={setBrightness}
          modifiers={[weight(1)]}
        />
        <Icon
          source={BacklightHigh}
          tint={colors.onSurfaceVariant}
          contentDescription="Brighter"
        />
      </Row>
    </Host>
  );
}
```

### Secondary text

Use `ListItem.SupportingContent` for the second line, and `useMaterialColors` for a text color that follows the light and dark themes.

```tsx ComposeSecondaryTextExample.tsx
import {
  Column,
  Host,
  ListItem,
  Text,
  useMaterialColors,
} from '@expo/ui/jetpack-compose';

export default function ComposeSecondaryTextExample() {
  const colors = useMaterialColors();

  return (
    <Host style={{ flex: 1 }}>
      <Column>
        <ListItem>
          <ListItem.HeadlineContent>
            <Text>Chrome</Text>
          </ListItem.HeadlineContent>
          <ListItem.SupportingContent>
            <Text color={colors.onSurfaceVariant}>
              Last used: Today
            </Text>
          </ListItem.SupportingContent>
          <ListItem.TrailingContent>
            <Text color={colors.onSurfaceVariant}>1.57 GB</Text>
          </ListItem.TrailingContent>
        </ListItem>
      </Column>
    </Host>
  );
}
```
