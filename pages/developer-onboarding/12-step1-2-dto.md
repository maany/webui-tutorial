## Step 1.2: Define DTOs

**Purpose**: Define data structures passed between layers

<CodeBlock title="src/lib/core/dto/subscription-dto.ts" language="typescript">

```typescript
import { BaseDTO, BaseStreamableDTO } from '@/lib/sdk/dto';
import { Subscription } from '../entity/rucio';

export interface SubscriptionDTO extends Subscription, BaseDTO {}

export interface ListSubscriptionsDTO extends BaseStreamableDTO {
    // Inherits: status, stream, error fields
}
```

</CodeBlock>

---
**Key Points**:
- DTOs extend `BaseDTO` or `BaseStreamableDTO`
- Streaming DTOs include a `stream` field or error info
- Located in `core/dto` (domain layer)
