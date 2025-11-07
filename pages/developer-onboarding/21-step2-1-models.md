## Step 2.1: Define UseCase Models

**Purpose**: Define request, response, and error models for business logic

<CodeBlock title="src/lib/core/usecase-models/list-subscriptions-usecase-models.ts" language="typescript">

```typescript
import { BaseErrorResponseModel, BaseResponseModel } from '@/lib/sdk/usecase-models';
import { Subscription } from '../entity/rucio';

export interface ListSubscriptionsRequest {
    account: string;
}

export interface ListSubscriptionsResponse extends Subscription, BaseResponseModel {}

export interface ListSubscriptionsError extends BaseErrorResponseModel {
    error: 'INVALID_ACCOUNT' | string;
}
```

</CodeBlock>

---

**Key Points**:
- `Request`: input to use case
- `Response`: successful output
- `Error`: error cases
- Extend base models for consistency
- Located in `core/usecase-models`
