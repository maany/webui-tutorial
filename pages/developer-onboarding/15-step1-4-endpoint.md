## Step 1.4: Create the Endpoint

**Purpose**: Make HTTP requests to Rucio server and transform data

<CodeBlock title="src/lib/infrastructure/gateway/subscription-gateway/endpoints/list-subscriptions-endpoint.ts" language="typescript">

```typescript
export default class ListSubscriptionsEndpoint extends BaseStreamableEndpoint<
    ListSubscriptionsDTO, SubscriptionDTO> {

    constructor(
        private readonly rucioAuthToken: string,
        private readonly account: string
    ) {
        super(true); // streamAsNDJSON = true
    }

    async initialize(): Promise<void> {
        const rucioHost = await this.envConfigGateway.rucioHost();
        const request: HTTPRequest = {
            method: 'GET',
            url: `${rucioHost}/subscriptions/${this.account}`,
            headers: {
                'X-Rucio-Auth-Token': this.rucioAuthToken,
                'Content-Type': 'application/x-json-stream',
            }
        };
        this.request = request;
    }

    createDTO(response: Buffer): SubscriptionDTO {
        const data = JSON.parse(response.toString());
        return convertToSubscriptionDTO(data, this.account);
    }
}
```

</CodeBlock>
---

**Key Points**:
- Extends `BaseStreamableEndpoint<TDTO, TStreamData>`
- `initialize()`: builds the HTTP request
- `createDTO()`: transforms each streamed line to DTO
