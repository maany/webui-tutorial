## Step 1.6: Write Gateway Tests

**Purpose**: Test gateway with mocked Rucio server

<CodeBlock title="test/gateway/subscription/subscription-gateway.test.ts" language="typescript">

```typescript
describe('SubscriptionGateway - list()', () => {
    beforeEach(() => {
        const subscriptionStream = Readable.from([
            JSON.stringify({ id: '1', name: 'Sub1' }),
            JSON.stringify({ id: '2', name: 'Sub2' }),
        ].join('\n'));

        MockRucioServerFactory.createMockRucioServer(true, [
            {
                url: `${MockRucioServerFactory.RUCIO_HOST}/subscriptions/ddmadmin`,
                method: 'GET',
                response: { status: 200, body: subscriptionStream },
            }
        ]);
    });

    it('should stream subscriptions', async () => {
        const gateway = appContainer.get(GATEWAYS.SUBSCRIPTION);
        const listDTO = await gateway.list(token, 'ddmadmin');

        expect(listDTO.status).toEqual('success');
        expect(listDTO.stream).toBeDefined();
    });
});
```

</CodeBlock>

---
**Key Points**:
- Use `MockRucioServerFactory` to mock endpoints
- Test stream handling
- Get gateway from IoC container
