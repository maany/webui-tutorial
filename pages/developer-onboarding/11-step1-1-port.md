## Step 1.1: Define the Secondary Output Port

**Purpose**: Define what operations the gateway must support

<CodeBlock title="src/lib/core/port/secondary/subscription-gateway-output-port.ts" language="typescript">

```typescript
import { BaseStreamableDTO } from '@/lib/sdk/dto';
import { ListSubscriptionsDTO, SubscriptionDTO } from '../../dto/subscription-dto';

export default interface SubscriptionGatewayOutputPort {
    /**
     * Lists all subscriptions for a given account in an NDJSON stream
     * @param rucioAuthToken A valid rucio auth token
     * @param account The rucio account name for which subscriptions should be listed
     */
    list(rucioAuthToken: string, account: string): Promise<ListSubscriptionsDTO>;
}
```

</CodeBlock>

---

**Key Points**:
- Interface only (no implementation)
- Clear JSDoc comments
- Returns DTO (Data Transfer Object)
- Located in `core/port/secondary` (part of business logic layer)
