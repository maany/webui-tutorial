## Step 3.2: Create React Component

**Purpose**: Call API route and display data using React hooks

<CodeBlock title="src/component-library/pages/Subscriptions/list/ListSubscription.tsx" language="typescript">

```typescript
export const ListSubscription = (props: ListSubscriptionProps) => {
    // Hook for streaming table data
    const { gridApi, onGridReady, streamingHook, startStreaming } =
        useTableStreaming<SubscriptionViewModel>(props.initialData);

    const [startedStreaming, setStartedStreaming] = useState(false);

    // Start streaming when table is ready
    useEffect(() => {
        if (!props.initialData && gridApi !== null && !startedStreaming) {
            startStreaming('/api/feature/list-subscription');
            setStartedStreaming(true);
        }
    }, [gridApi, startStreaming, startedStreaming]);

    return (
        <div className="flex flex-col space-y-3 w-full">
            <Heading text="Subscriptions" />
            <ListSubscriptionTable
                streamingHook={streamingHook}
                onGridReady={onGridReady}
            />
        </div>
    );
};
```

</CodeBlock>
