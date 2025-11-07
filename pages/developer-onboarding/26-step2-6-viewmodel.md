## Step 2.6: Create View Model

**Purpose**: Define data shape for UI consumption

<CodeBlock title="src/lib/infrastructure/data/view-model/subscriptions.ts" language="typescript">

```typescript
import { Subscription, SubscriptionState } from '@/lib/core/entity/rucio';
import { BaseViewModel } from '@/lib/sdk/view-models';

export interface SubscriptionViewModel extends BaseViewModel, Omit<Subscription, 'replication_rules'> {
    replication_rules: string; // Stringified for JSON serialization
}

export function getEmptySubscriptionViewModel(): SubscriptionViewModel {
    return {
        status: 'error',
        account: '',
        id: '',
        name: '',
        state: SubscriptionState.UNKNOWN,
        filter: '',
        replication_rules: '',
        created_at: '',
        updated_at: '',
    };
}
```

</CodeBlock>

---

**Key Points**:
- Extends `BaseViewModel` (includes `status`, `message`)
- May differ from domain model (e.g., stringified JSON)
- Helper function for empty/error view model
