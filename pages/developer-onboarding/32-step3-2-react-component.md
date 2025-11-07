## Step 3.2: Create React Component

**Purpose**: Call API route and display data using React hooks

<CodeBlock title="src/component-library/pages/Subscriptions/list/ListSubscriptionTutorialExample.tsx" language="typescript">

```typescript
xport const ListSubscriptionTutorialExample = (props: ListSubscriptionTutorialExampleProps) => {
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

    // Get user account (non-streaming query)
    const {
        data: siteHeader,
        error: siteHeaderError,
        isFetching,
    } = useQuery({
        queryKey: ['subscription-account'],
        queryFn: async () => {
            const res = await fetch('/api/feature/get-site-header');
            return res.json();
        },
        retry: false,
    });

    if (isFetching) return <div>Loading...</div>;
    if (siteHeaderError) return <div>Error loading account</div>;

    const account = siteHeader.activeAccount.rucioAccount;

    return (
        <div className="flex flex-col space-y-3 w-full">
            <Heading text="Subscriptions" />
            <Heading size="sm" text={`for account ${account}`} />
            <ListSubscriptionTutorialTable
                streamingHook={streamingHook}
                onGridReady={onGridReady}
                account={account}
            />
        </div>
    );
};
```

</CodeBlock>
