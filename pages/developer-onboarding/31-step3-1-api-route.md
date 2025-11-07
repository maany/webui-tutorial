## Step 3.1: Create API Route

**Purpose**: Expose controller as HTTP endpoint

<CodeBlock title="src/app/api/feature/list-subscription/route.ts" language="typescript">

```typescript
import 'reflect-metadata'; // Required for Inversify

export async function GET(request: NextRequest) {
    // 1. Get session user
    const sessionUser = await getSessionUser();
    if (!sessionUser) {
        return NextResponse.json({ error: 'Unauthorized' }, { status: 401 });
    }

    // 2. Get controller from IoC container
    const controller = appContainer.get(CONTROLLERS.LIST_SUBSCRIPTIONS);

    // 3. Execute controller
    return executeAuthenticatedController(
        controller,
        { sessionAccount: sessionUser.rucioAccount },
        true // isStreaming = true for NDJSON response
    );
}
```

</CodeBlock>

---
**Key Points**:
- Import `'reflect-metadata'` at the top
- Validate session
- Get controller from IoC
- Set `isStreaming: true` for NDJSON
