## Step 1.3: Key Points

- `@injectable()` decorator for dependency injection
- Creates endpoint instance and calls `fetch()`
- For streaming: returns `{ status: 'success', stream: endpoint }`
- Handles errors consistently
- Located in `infrastructure/gateway`
