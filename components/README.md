# Slidev Components

This directory contains custom Vue components for the Slidev presentation.

## Architecture Diagram Components

### Option 1: Horizontal Flow (Default)
**Component**: `<ArchitectureDiagram />`

- Shows all layers flowing horizontally from left to right
- Includes color-coded layers and a legend at the bottom
- Best for wide screens
- May require horizontal scrolling on smaller displays

**Currently used in**: `pages/developer-onboarding/03-architecture-diagram.md`

### Option 2: Vertical Compact
**Component**: `<ArchitectureDiagramCompact />`

- Vertical flow with icons
- Includes key principles on the right side
- More compact, fits better on standard slides
- Combines diagram + principles in one view

**To use this instead**, edit `pages/developer-onboarding/03-architecture-diagram.md`:
```markdown
<ArchitectureDiagramCompact />
```

## Usage

Slidev automatically picks up components from the `/components` directory. Simply reference them in your markdown files:

```markdown
<ComponentName />
```

## Customization

You can customize the components by editing the `.vue` files:
- **Styling**: Modify the `<style scoped>` section
- **Content**: Update the `<template>` section
- **Colors**: Change the gradient colors in layer classes

## CodeBlock Component

**Component**: `<CodeBlock />`

Makes code blocks scrollable with a maximum height, preventing slide overflow.

### Usage

**Basic usage:**
```markdown
<CodeBlock>

\`\`\`typescript
// Your code here
\`\`\`

</CodeBlock>
```

**With file path and language:**
```markdown
<CodeBlock title="src/lib/core/port/secondary/subscription-gateway-output-port.ts" language="typescript">

\`\`\`typescript
export default interface SubscriptionGatewayOutputPort {
    list(rucioAuthToken: string, account: string): Promise<ListSubscriptionsDTO>;
}
\`\`\`

</CodeBlock>
```

### Props

- `title` (optional): File path or description shown in header
- `language` (optional): Programming language badge (e.g., "typescript", "javascript", "python")

### Features

- **Flexible height**: Adapts to available slide space (max 35vh or 300px, whichever is smaller)
- **No vertical overflow**: Automatically adjusts to prevent slides from overflowing
- **Scrollable**: Both vertical and horizontal for long code snippets
- **Styled scrollbars**: Custom dark theme scrollbars
- **File header**: Optional header with file icon and language badge
- **Copy button**: One-click copy to clipboard with visual feedback
- **Syntax highlighting**: Works with Slidev's built-in highlighting

## Creating New Components

1. Create a new `.vue` file in this directory
2. Use the Vue 3 Composition API or Options API
3. Reference the component in your slide markdown files
