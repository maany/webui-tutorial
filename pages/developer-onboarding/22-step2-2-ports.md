## Step 2.2: Define Input/Output Ports

**Purpose**: Define interfaces for use case execution

<CodeBlock title="src/lib/core/port/primary/list-subscriptions-port.ts" language="typescript">

```typescript
import { AuthenticatedRequestModel } from '@/lib/sdk/usecase-models';
import { ListSubscriptionsRequest, ListSubscriptionsResponse, ListSubscriptionsError } from '../../usecase-models/list-subscriptions-usecase-models';
import { SubscriptionViewModel } from '@/lib/infrastructure/data/view-model/subscriptions';

export interface ListSubscriptionsInputPort {
    execute(request: AuthenticatedRequestModel<ListSubscriptionsRequest>): Promise<void>;
}

export interface ListSubscriptionsOutputPort {
    presentSuccess(response: ListSubscriptionsResponse): SubscriptionViewModel;
    presentError(error: ListSubscriptionsError): SubscriptionViewModel;
}
```

</CodeBlock>

---

**Key Points**:
- `InputPort`: how to call the use case
- `OutputPort`: how to present results (implemented by presenter)
- Located in `core/port/primary`
