## 🔑 Key Concepts Summary

### 1. Streaming vs Non-Streaming

| Aspect | Streaming | Non-Streaming |
|--------|-----------|---------------|
| **Use Case Base** | `BaseSingleEndpointStreamingUseCase` | `BaseSingleEndpointUseCase` |
| **Endpoint Base** | `BaseStreamableEndpoint` | `BaseEndpoint` |
| **Presenter Base** | `BaseStreamingPresenter` | `BasePresenter` |
| **Response Format** | NDJSON (one JSON per line) | Single JSON |
| **API Route** | `isStreaming: true` | `isStreaming: false` |

### 2. Data Flow

```
Rucio API Response (TRucio*)
    ↓ (gateway-utils converter)
DTO (Core layer)
    ↓ (UseCase.processStreamedData)
Response Model (Core layer)
    ↓ (Presenter.streamResponseModelToViewModel)
View Model (Infrastructure)
    ↓ (API Route serialization)
React Component (UI)
```

### 3. Dependency Injection

- **@injectable()**: Mark classes for IoC
- **@inject(SYMBOL)**: Inject dependencies by symbol
- **appContainer.get(SYMBOL)**: Retrieve from container
- **Features**: Bundle UseCase + Controller + Presenter
