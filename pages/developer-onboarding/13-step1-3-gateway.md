## Step 1.3: Implement the Gateway

**Purpose**: Implement the port interface by delegating to endpoints

<CodeBlock title="src/lib/infrastructure/gateway/subscription-gateway/subscription-gateway.ts" language="typescript">

```typescript
import { ListSubscriptionsDTO } from '@/lib/core/dto/subscription-dto';
import SubscriptionGatewayOutputPort from '@/lib/core/port/secondary/subscription-gateway-output-port';
import { injectable } from 'inversify';
import ListSubscriptionsEndpoint from './endpoints/list-subscriptions-endpoint';

@injectable()
export default class SubscriptionGateway implements SubscriptionGatewayOutputPort {
    async list(rucioAuthToken: string, account: string): Promise<ListSubscriptionsDTO> {
        try {
            const endpoint: ListSubscriptionsEndpoint = new ListSubscriptionsEndpoint(
                rucioAuthToken,
                account
            );
            const errorDTO: ListSubscriptionsDTO | undefined = await endpoint.fetch();

            // If no error, wrap the stream in success DTO
            if (!errorDTO) {
                return {
                    status: 'success',
                    stream: endpoint,
                };
            }
            return errorDTO;
        } catch (error) {
            const errorDTO: ListSubscriptionsDTO = {
                status: 'error',
                errorName: 'Exception occurred while fetching subscriptions',
                errorType: 'gateway_endpoint_error',
                errorMessage: error?.toString(),
            };
            return Promise.resolve(errorDTO);
        }
    }
}
```

</CodeBlock>
