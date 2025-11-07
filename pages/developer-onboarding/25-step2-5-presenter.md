## Step 2.5: Create the Presenter

**Purpose**: Transform response/error models to view models for UI

<CodeBlock title="src/lib/infrastructure/presenter/list-subscriptions-presenter.ts" language="typescript">

```typescript
export default class ListSubscriptionsPresenter extends BaseStreamingPresenter<
    ListSubscriptionsResponse,
    ListSubscriptionsError,
    SubscriptionViewModel
> {
    streamResponseModelToViewModel(responseModel: ListSubscriptionsResponse): SubscriptionViewModel {
        // Convert response model to view model (for UI)
        const viewModel: SubscriptionViewModel = {
            ...responseModel,
            replication_rules: JSON.stringify(responseModel.replication_rules),
        };
        return viewModel;
    }

    convertErrorModelToViewModel(errorModel: ListSubscriptionsError) {
        const viewModel = getEmptySubscriptionViewModel();
        if (errorModel.error === 'INVALID_ACCOUNT') {
            viewModel.message = errorModel.message;
            return { status: 400, viewModel };
        }
        return { status: 500, viewModel };
    }
}
```

</CodeBlock>

---

**Key Points**:
- Extends `BaseStreamingPresenter`
- Transform response/error to view model
- Map errors to HTTP status codes
