## Step 1.5: Create Gateway Utils

**Purpose**: Convert Rucio API format to internal DTOs

<CodeBlock title="src/lib/infrastructure/gateway/subscription-gateway/subscription-gateway-utils.ts" language="typescript">

```typescript
export type TRucioSubscription = {
    id: string;
    name: string;
    account: string;
    state: string;
    filter: string;
    replication_rules: string;
    created_at: string;
    updated_at: string;
};

export function convertToSubscriptionDTO(
    data: TRucioSubscription,
    account: string
): SubscriptionDTO {
    return {
        status: 'success',
        id: data.id,
        name: data.name,
        account: account,
        state: parseSubscriptionState(data.state),
        filter: data.filter,
        replication_rules: parseReplicationRules(data.replication_rules),
        created_at: data.created_at,
        updated_at: data.updated_at,
    };
}
```

</CodeBlock>

---
**Key Points**:
- Define types for Rucio API response
- Convert to internal DTO format
- Parse enums and complex fields
