---
modificationDate: August 18, 2026
title: Namespace
description: A Namespace component that allows you create Namespaces in SwiftUI
sourceCodeUrl: 'https://github.com/expo/expo/tree/sdk-57/packages/expo-ui'
packageName: '@expo/ui'
platforms: ['ios', 'tvos', 'expo-go']
---

This documentation is available as Markdown for AI agents and LLMs. See the [full Markdown index](https://docs.expo.dev/llms.txt) or append .md to any documentation URL.

# Namespace

A Namespace component that allows you create Namespaces in SwiftUI

<AgentInstructions>

## Submitting Feedback

If you encounter errors, misleading or outdated information, report it so Expo can be improved:

Preferred command:
npx --yes submit-expo-feedback@latest --category docs --subject "/versions/v57.0.0/sdk/ui/swift-ui/namespace/" "<actionable feedback>"

Direct HTTP fallback:
curl -X POST https://api.expo.dev/v2/feedback/docs-send -H 'Content-Type: application/json' -d '{"url":"/versions/v57.0.0/sdk/ui/swift-ui/namespace/","feedback":"🤖 Agent feedback for docs: <specific, actionable description> (<model>, <harness>)"}'

Only submit when you have something specific and actionable to report. Try to give the most context.

## Navigation

When answering a related or follow-up question, use llms.txt to find the relevant page as Markdown (.md) instead of guessing.

You are here: Reference (v57.0.0) > Expo UI > SwiftUI (45 pages in this section)
Full documentation tree: [llms.txt](https://docs.expo.dev/llms.txt)

</AgentInstructions>
iOS, tvOS, Included in Expo Go

A Namespace component that allows you to create SwiftUI [Namespaces](https://developer.apple.com/documentation/swiftui/namespace) for coordinating animations and matched geometry effects between views.

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

Namespaces are used to coordinate animations and matched geometry effects between views. They provide a unique identifier that can be shared across components to create smooth transitions.

```tsx
import {
  Host,
  HStack,
  GlassEffectContainer,
  Image,
  Namespace,
  VStack,
  Button,
  Text,
} from '@expo/ui/swift-ui';
import {
  padding,
  glassEffect,
  animation,
  Animation,
  glassEffectId,
  background,
  cornerRadius,
  frame,
  foregroundStyle,
} from '@expo/ui/swift-ui/modifiers';
import { useId, useState } from 'react';

function MatchedGeometryExample() {
  const [isGlassExpanded, setIsGlassExpanded] = useState(false);
  const namespaceId = useId();

  return (
    <Host
      style={{
        flex: 1,
        backgroundColor: 'purple',
      }}>
      <VStack
        spacing={60}
        modifiers={[
          animation(
            Animation.spring({ duration: 0.8 }),
            isGlassExpanded
          ),
        ]}>
        <Namespace id={namespaceId}>
          <GlassEffectContainer
            spacing={30}
            modifiers={[
              animation(
                Animation.spring({ duration: 0.8 }),
                isGlassExpanded
              ),
              padding({ all: 30 }),
              cornerRadius(20),
            ]}>
            <VStack spacing={25}>
              <HStack spacing={25}>
                <Image
                  systemName="paintbrush.fill"
                  size={42}
                  modifiers={[
                    frame({ width: 50, height: 50 }),
                    padding({ all: 15 }),
                    glassEffect({
                      glass: {
                        variant: 'clear',
                      },
                    }),
                    glassEffectId('paintbrush', namespaceId),
                    cornerRadius(15),
                  ]}
                />
                <Image
                  systemName="scribble.variable"
                  size={42}
                  modifiers={[
                    frame({ width: 50, height: 50 }),
                    padding({ all: 15 }),
                    glassEffect({
                      glass: {
                        variant: 'clear',
                      },
                    }),
                    glassEffectId('scribble', namespaceId),
                    cornerRadius(15),
                  ]}
                />
                <Image
                  systemName="pencil.tip.crop.circle"
                  size={42}
                  modifiers={[
                    frame({ width: 50, height: 50 }),
                    padding({ all: 15 }),
                    glassEffect({
                      glass: {
                        variant: 'clear',
                      },
                    }),
                    glassEffectId('pencil', namespaceId),
                    cornerRadius(15),
                  ]}
                />
              </HStack>

              {isGlassExpanded && (
                <HStack spacing={25}>
                  <Image
                    systemName="eraser.fill"
                    size={42}
                    modifiers={[
                      frame({ width: 50, height: 50 }),
                      padding({ all: 15 }),
                      glassEffect({
                        glass: {
                          variant: 'clear',
                        },
                      }),
                      glassEffectId('eraser', namespaceId),
                      cornerRadius(15),
                    ]}
                  />
                  <Image
                    systemName="highlighter"
                    size={42}
                    modifiers={[
                      frame({ width: 50, height: 50 }),
                      padding({ all: 15 }),
                      glassEffect({
                        glass: {
                          variant: 'clear',
                        },
                      }),
                      glassEffectId('highlighter', namespaceId),
                      cornerRadius(15),
                    ]}
                  />
                  <Image
                    systemName="heart.fill"
                    size={42}
                    modifiers={[
                      frame({ width: 50, height: 50 }),
                      padding({ all: 15 }),
                      glassEffect({
                        glass: {
                          variant: 'clear',
                        },
                      }),
                      glassEffectId('heart.fill', namespaceId),
                      cornerRadius(15),
                    ]}
                  />
                </HStack>
              )}
            </VStack>
          </GlassEffectContainer>
        </Namespace>

        <VStack spacing={15}>
          <Button
            onPress={() => setIsGlassExpanded(!isGlassExpanded)}
            modifiers={[
              padding({ horizontal: 30, vertical: 15 }),
              background('#000'),
              cornerRadius(25),
              glassEffect({
                glass: {
                  variant: 'clear',
                },
              }),
            ]}>
            <Text modifiers={[foregroundStyle('#fff')]}>
              {isGlassExpanded ? 'Hide tools' : 'Show more tools'}
            </Text>
          </Button>
        </VStack>
      </VStack>
    </Host>
  );
}
```

## API

```tsx
import { Namespace } from '@expo/ui/swift-ui';
```

## Component

### `Namespace`

Supported platforms: iOS, tvOS.

Type: React.[Element](https://www.typescriptlang.org/docs/handbook/jsx.html#function-component)<[NamespaceProps](https://docs.expo.dev/versions/v57.0.0/sdk/ui/swift-ui/namespace.md#namespaceprops)\>

A component that provides a SwiftUI [`Namespace`](https://developer.apple.com/documentation/swiftui/namespace) to its children.

Example

```tsx
const namespaceId = React.useId();
return (
  <Namespace id={namespaceId}>
    <GlassEffectContainer>
      <Image
        systemName="paintbrush.fill"
        modifiers={[
          glassEffect({
            glass: {
              variant: 'clear',
            },
          }),
          glassEffectId('paintbrush', namespaceId),
        ]}
      />
    </GlassEffectContainer>
  </Namespace>
);
```

NamespaceProps

### `children`

Supported platforms: iOS, tvOS.

Type: [ReactNode](https://reactnative.dev/docs/react-node)

### `id`

Supported platforms: iOS, tvOS.

Type: `string`

The ID of the namespace. You can generate one with the `useId` react hook.
