## Step 3.3: Create Table Component

**Purpose**: Display streamed data in AG Grid table

<CodeBlock title="src/component-library/pages/Subscriptions/list/ListSubscriptionTable.tsx" language="typescript">

```typescript
export const ListSubscriptionTable = (props: ListSubscriptionTableProps) => {
    const tableRef = useRef<AgGridReact<SubscriptionViewModel>>(null);

    const [columnDefs] = useState([
        {
            headerName: 'Name',
            field: 'name',
            flex: 5,
            cellRenderer: ClickableName,
            filter: true,
        },
        {
            headerName: 'State',
            field: 'state',
            flex: 2,
        },
        {
            headerName: 'Created',
            field: 'created_at',
            flex: 3,
        },
    ]);

    return (
        <StreamedTable
            columnDefs={columnDefs}
            tableRef={tableRef}
            {...props}
        />
    );
};
```

</CodeBlock>

---

**Key Points**:
- Use `StreamedTable` component
- Define `columnDefs` for AG Grid
- Use custom cell renderers
