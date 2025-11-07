## Step 2.7: Register Feature in IoC

**Purpose**: Wire UseCase, Controller, Presenter together via dependency injection

<CodeBlock title="src/lib/infrastructure/ioc/features/list-subscriptions-feature.ts" language="typescript">

```typescript
export default class ListSubscriptionsFeature extends BaseStreamableFeature {
    constructor(appContainer: Container) {
        const subscriptionGateway = appContainer.get(GATEWAYS.SUBSCRIPTION);

        const symbols = {
            CONTROLLER: CONTROLLERS.LIST_SUBSCRIPTIONS,
            USECASE_FACTORY: USECASE_FACTORY.LIST_SUBSCRIPTIONS,
            INPUT_PORT: INPUT_PORT.LIST_SUBSCRIPTIONS,
        };

        super(
            'ListSubscriptions',
            ListSubscriptionsController,
            ListSubscriptionsUseCase,
            [subscriptionGateway],
            ListSubscriptionsPresenter,
            false,
            symbols,
        );
    }
}
```

</CodeBlock>

---

**Then register**: Add to `container-config.ts`

<CodeBlock title="src/lib/infrastructure/ioc/container-config.ts" language="typescript">

```typescript
loadFeaturesSync(appContainer, [
    new ListSubscriptionsFeature(appContainer),
]);
```

</CodeBlock>
