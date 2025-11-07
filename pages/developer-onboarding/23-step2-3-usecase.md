## Step 2.3: Create the UseCase

**Purpose**: Orchestrate business logic - validate, call gateway, process results

<CodeBlock title="src/lib/core/usecase/list-subscriptions-usecase.ts" language="typescript">

```typescript
@injectable()
class ListSubscriptionsUseCase extends BaseSingleEndpointStreamingUseCase {
    validateRequestModel(request) {
        if (!request.account) {
            return { status: 'error', error: 'INVALID_ACCOUNT' };
        }
    }

    async makeGatewayRequest(request) {
        return await this.subscriptionGateway.list(
            request.rucioAuthToken,
            request.account
        );
    }

    processStreamedData(dto: SubscriptionDTO) {
        const responseModel: ListSubscriptionsResponse = {
            ...dto,
            status: 'success',
        };
        return { status: 'success', data: responseModel };
    }
}
```

</CodeBlock>

---

**Key Points**:
- Extends `BaseSingleEndpointStreamingUseCase` for streaming
- Inject presenter and gateway
- Implement lifecycle methods
