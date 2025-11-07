## Step 2.4: Create the Controller

**Purpose**: Map HTTP request parameters to UseCase request model

<CodeBlock title="src/lib/infrastructure/controller/list-subscriptions-controller.ts" language="typescript">

```typescript
export type ListSubscriptionsControllerParameters = TAuthenticatedControllerParameters & {
    sessionAccount: string;
};

@injectable()
class ListSubscriptionsController extends BaseController<
    ListSubscriptionsControllerParameters,
    AuthenticatedRequestModel<ListSubscriptionsRequest>
> {
    constructor(
        @inject(USECASE_FACTORY.LIST_SUBSCRIPTIONS)
        listSubscriptionsUseCaseFactory: (response: Signal) => ListSubscriptionsInputPort
    ) {
        super(listSubscriptionsUseCaseFactory);
    }

    prepareRequestModel(parameters: ListSubscriptionsControllerParameters) {
        return {
            rucioAuthToken: parameters.rucioAuthToken,
            account: parameters.sessionAccount,
        };
    }
}
```

</CodeBlock>

---

**Key Points**:
- Extends `BaseController<Parameters, RequestModel>`
- Inject use case factory from IoC
- Implement `prepareRequestModel()` to map parameters
