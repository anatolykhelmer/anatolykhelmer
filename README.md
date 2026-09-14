Istanbul will report 100% on a test that still passes if the function returns a potato. I work on the other kind of coverage.

I am Anatoly Khelmer. I write TypeScript: test-quality tooling first, then local-first apps that keep data on the device.

## Line coverage is a vibes-based metric

```typescript
it('should create order', async () => {
  const result = await service.createOrder(mockInput);
  expect(result).toBeDefined();
});
```

Istanbul is green. The test still passes if `createOrder` returns `null`, `{}`, or a completely wrong order.

## DeepCover

[DeepCover](https://github.com/anatolykhelmer/deepcover) combines deterministic AST analysis with bounded LLM reasoning. It scores whether tests actually protect the code — assertion strength, domain states, mocks that replace the thing under test.

It does not replace Istanbul. It argues with it.

Same Istanbul number, different DeepCover score: [deepcover-demo-orders](https://github.com/anatolykhelmer/deepcover-demo-orders).

Read the [DeepCover README](https://github.com/anatolykhelmer/deepcover#readme).

## Also shipping

- [khesh](https://github.com/anatolykhelmer/khesh) — offline household ledger, double-entry, IndexedDB
- [food-tracker](https://github.com/anatolykhelmer/food-tracker) — nutrition tracker; browser only, no account
- [judo-scoreboard](https://github.com/anatolykhelmer/judo-scoreboard) / [judo-core](https://github.com/anatolykhelmer/judo-core) — contest UI and tournament engine, no server at contest time
- [skills](https://github.com/anatolykhelmer/skills) — agent skills as git-native tools, not a prompt folder
- [kaizen-backlog](https://github.com/anatolykhelmer/kaizen-backlog) — git-native backlog for how you work with Cursor and Claude

## Person

Based in Israel. I love judo.

TypeScript, Node, React, Jest/Vitest.

[LinkedIn](https://www.linkedin.com/in/anatoly-khelmer/)
