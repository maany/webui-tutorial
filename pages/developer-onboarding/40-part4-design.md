## 🎨 PART 4: Design the Page

**Duration**: 3 minutes

### Tailwind CSS Patterns

<CodeBlock title="Common Tailwind patterns" language="typescript">

```typescript
// Layout container
<div className="flex flex-col space-y-3 w-full grow">

// Card/panel
<div className="bg-white dark:bg-gray-800 rounded-lg shadow p-4">

// Button
<button className="px-4 py-2 bg-blue-600 text-white rounded hover:bg-blue-700">
```

</CodeBlock>

### Component Library

**Reusable atoms** in `component-library/atoms/`:
- `<Heading>`: Page/section titles
- `<InfoField>`, `<WarningField>`, `<ErrorField>`: Messages

**Reusable features** in `component-library/features/`:
- `<StreamedTable>`: AG Grid wrapper for streaming
- `<RuleStateBadge>`: Status badges
- `<ClickableCell>`: Table cells with links
