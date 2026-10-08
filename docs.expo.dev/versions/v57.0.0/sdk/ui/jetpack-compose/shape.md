---
modificationDate: August 18, 2026
title: Shape
description: A Jetpack Compose Shape component for drawing geometric shapes.
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['android', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# Shape

A Jetpack Compose Shape component for drawing geometric shapes.

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/jetpack-compose/shape/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/jetpack-compose/shape/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > Jetpack Compose (51 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
Android, Included in Expo Go

Expo UI Shape matches the official Jetpack Compose [Shapes](https://developer.android.com/develop/ui/compose/graphics/draw/shapes) API and provides a set of sub-components for drawing geometric shapes such as stars, circles, rectangles, pills, and polygons.

Image: Four geometric shapes: hexagon, circle, rounded rectangle, and pill

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

### Basic shapes

Render common shapes using the `Shape` sub-components.

```tsx BasicShapesExample.tsx
import { Host, Shape, Row } from '@expo/ui/jetpack-compose';
import { size } from '@expo/ui/jetpack-compose/modifiers';

export default function BasicShapesExample() {
  return (
    <Host
      matchContents={{ vertical: true }}
      style={{ width: '100%' }}>
      <Row
        horizontalArrangement={{ spacedBy: 16 }}
        verticalAlignment="center">
        <Shape.Star
          radius={1}
          innerRadius={0.5}
          color="#FFD700"
          modifiers={[size(80, 80)]}
        />
        <Shape.Circle
          radius={1}
          color="#4285F4"
          modifiers={[size(80, 80)]}
        />
        <Shape.Rectangle
          color="#34A853"
          modifiers={[size(80, 80)]}
        />
        <Shape.Pill color="#EA4335" modifiers={[size(100, 50)]} />
      </Row>
    </Host>
  );
}
```

### Shapes with rounded corners

Use `cornerRounding` and `smoothing` to customize the appearance of shapes.

```tsx RoundedShapesExample.tsx
import { Host, Shape, Row } from '@expo/ui/jetpack-compose';
import { size } from '@expo/ui/jetpack-compose/modifiers';

export default function RoundedShapesExample() {
  return (
    <Host
      matchContents={{ vertical: true }}
      style={{ width: '100%' }}>
      <Row
        horizontalArrangement={{ spacedBy: 16 }}
        verticalAlignment="center">
        <Shape.Rectangle
          cornerRounding={0.2}
          smoothing={0.5}
          color="#9C27B0"
          modifiers={[size(100, 80)]}
        />
        <Shape.RoundedCorner
          cornerRadii={{
            topStart: 20,
            topEnd: 20,
            bottomStart: 0,
            bottomEnd: 0,
          }}
          color="#FF5722"
          modifiers={[size(100, 80)]}
        />
      </Row>
    </Host>
  );
}
```

### Polygon and star variants

Use `verticesCount` and `innerRadius` to control the shape geometry.

```tsx PolygonShapesExample.tsx
import { Host, Shape, Row } from '@expo/ui/jetpack-compose';
import { size } from '@expo/ui/jetpack-compose/modifiers';

export default function PolygonShapesExample() {
  return (
    <Host
      matchContents={{ vertical: true }}
      style={{ width: '100%' }}>
      <Row
        horizontalArrangement={{ spacedBy: 16 }}
        verticalAlignment="center">
        <Shape.Polygon
          verticesCount={6}
          cornerRounding={0.05}
          color="#00BCD4"
          modifiers={[size(80, 80)]}
        />
        <Shape.Star
          verticesCount={8}
          radius={1}
          innerRadius={0.4}
          cornerRounding={0.025}
          color="#FF9800"
          modifiers={[size(80, 80)]}
        />
        <Shape.PillStar
          verticesCount={6}
          innerRadius={0.5}
          color="#E91E63"
          modifiers={[size(80, 80)]}
        />
      </Row>
    </Host>
  );
}
```

## API

```tsx
import { Shape } from '@expo/ui/jetpack-compose';
```

## Constants

### `Shape.Shape`

Supported platforms: Android.

Type: { Circle: (props: [Pick](https://www.typescriptlang.org/docs/handbook/utility-types.html#picktype-keys)<ShapeProps, 'radius' | 'verticesCount' | 'color' | 'modifiers'\>) => [ShapeJSXElement](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/shape.md#shapejsxelement), Pill: (props: [Pick](https://www.typescriptlang.org/docs/handbook/utility-types.html#picktype-keys)<ShapeProps, 'smoothing' | 'color' | 'modifiers'\>) => [ShapeJSXElement](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/shape.md#shapejsxelement), PillStar: (props: ShapeProps) => [ShapeJSXElement](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/shape.md#shapejsxelement), Polygon: (props: [Pick](https://www.typescriptlang.org/docs/handbook/utility-types.html#picktype-keys)<ShapeProps, 'smoothing' | 'cornerRounding' | 'verticesCount' | 'color' | 'modifiers'\>) => [ShapeJSXElement](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/shape.md#shapejsxelement), Rectangle: (props: [Pick](https://www.typescriptlang.org/docs/handbook/utility-types.html#picktype-keys)<ShapeProps, 'smoothing' | 'cornerRounding' | 'color' | 'modifiers'\>) => [ShapeJSXElement](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/shape.md#shapejsxelement), RoundedCorner: (props: [Pick](https://www.typescriptlang.org/docs/handbook/utility-types.html#picktype-keys)<ShapeProps, 'cornerRadii' | 'color' | 'modifiers'\>) => [ShapeJSXElement](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/shape.md#shapejsxelement), Star: (props: ShapeProps) => [ShapeJSXElement](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/shape.md#shapejsxelement) }

## Props

### `color`

Supported platforms: Android.

Optional • Type: [ColorValue](https://reactnative.dev/docs/colors)

Color of the shape

### `cornerRadii`

Supported platforms: Android.

Optional • Type: [CornerRadii](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/shape.md#cornerradii)

Corner radii for RoundedCorner shape. Values are in dp.

### `cornerRounding`

Supported platforms: Android.

Optional • Type: `number` • Default: `0.0`

Corner rounding percentage. Multiplied by the shorter dimension of the view to produce pixel values.

### `innerRadius`

Supported platforms: Android.

Optional • Type: `number` • Default: `1.0`

Inner radius of star-related shapes (`'STAR'` and `'PILL_STAR'`). Multiplied by the shorter dimension of the view to produce pixel values.

### `modifiers`

Supported platforms: Android.

Optional • Type: `ModifierConfig[]`

Modifiers for the component.

### `radius`

Supported platforms: Android.

Optional • Type: `number` • Default: `1.0`

Radius of the circular shape. Multiplied by the shorter dimension of the view to produce pixel values.

### `smoothing`

Supported platforms: Android.

Optional • Type: `number` • Default: `0.0`

Number between `0.0` and `1.0` that determines how much each line between vertices is "smoothed".

### `verticesCount`

Supported platforms: Android.

Optional • Type: `number` • Default: `6.0`

Number of vertices. For `'POLYGON'` it must be at least `3.0`. For `'STAR'` and `'PILL_STAR'` it is a number of vertices for each of two radii (A 5-pointed star has 10 vertices.)

## Methods

### `Shape.parseJSXShape(shape)`

Supported platforms: Android.

Overload #1

| Parameter | Type |
| --- | --- |
| `shape` | [ShapeJSXElement](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/shape.md#shapejsxelement) |

  

Returns: `ShapeRecordProps`

### `Shape.parseJSXShape(shape)`

Supported platforms: Android.

Overload #2

| Parameter | Type |
| --- | --- |
| `shape`(optional) | [ShapeJSXElement](https://docs.expo.dev/versions/v57.0.0/sdk/ui/jetpack-compose/shape.md#shapejsxelement) |

  

Returns: `ShapeRecordProps | undefined`

## Types

### `CornerRadii`

Supported platforms: Android.

Corner radii for RoundedCorner shape.

| Property | Type | Description |
| --- | --- | --- |
| bottomEnd(optional) | `number` | Bottom-end corner radius in dp. |
| bottomStart(optional) | `number` | Bottom-start corner radius in dp. |
| topEnd(optional) | `number` | Top-end corner radius in dp. |
| topStart(optional) | `number` | Top-start corner radius in dp. |

### `ShapeJSXElement`

Supported platforms: Android.

Type: `React.ReactElement<NativeShapeProps>` extended by:

| Property | Type | Description |
| --- | --- | --- |
| __expo_shape_jsx_element_marker | `true` | - |
