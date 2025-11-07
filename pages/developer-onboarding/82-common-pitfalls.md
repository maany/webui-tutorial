## 🚨 Common Pitfalls

1. **Forgetting `'reflect-metadata'`** in API routes → Inversify fails

2. **Not setting `isStreaming: true`** for streaming endpoints → Response not chunked

3. **Missing `@injectable()`** decorator → IoC can't instantiate

4. **Wrong DTO type in endpoint** → `BaseStreamableEndpoint<DTO, StreamData>` types

5. **Not handling errors in streams** → Errors appear as data items

6. **Forgetting to register feature** in `container-config.ts` → 404 errors

7. **Not calling `super(true)`** in streaming endpoint constructor → No stream parsing

8. **Mixing sync/async** in UseCase lifecycle methods → Unexpected behavior
