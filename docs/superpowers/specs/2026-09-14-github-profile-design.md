# GitHub profile — design

Date: 2026-09-14
Owner: Anatoly Khelmer (`anatolykhelmer`)

## Goal

A GitHub profile that a visiting developer reads as a short column, not a widget dump. Primary audience is other developers and OSS; recruiters and personal character are present but secondary. Language is English. Voice is dry humor: serious on substance, slightly sarcastic in form.

After five seconds the visitor should remember: this person cares whether tests protect code, not whether Istanbul is green.

## Non-goals

- GitHub stats, snake, typing GIF, visitor counters, trophy cards, or badge walls
- A bilingual README
- Email, company, role, or “open to work”
- Putting this work in the `deepcover` product repository
- A copy-paste `npx` one-liner that cannot succeed without a target module (that would be a broken exhibit)

## Artifacts

The profile is three GitHub surfaces, not one file.

1. **Special repo** `anatolykhelmer/anatolykhelmer`, public, default branch `main`, single meaningful file: `README.md`. Optional: this spec under `docs/`. No app code, no CI required.
2. **Account card**
   - Name: Anatoly Khelmer (already set)
   - Bio (≤160 characters): `Istanbul reports 100% on tests that would still pass if the function returned a potato. DeepCover, TypeScript, local-first.`
   - Location: Israel
   - Social: LinkedIn `https://www.linkedin.com/in/anatoly-khelmer/`
   - Website: empty unless a personal site exists later
3. **Pinned repos**, exactly these six, in this order:
   1. `deepcover`
   2. `food-tracker`
   3. `judo-core`
   4. `kaizen-backlog`
   5. `khesh`
   6. `skills`

`deepcover-demo-orders` and `judo-scoreboard` are linked from the README, not pinned. `woledger` and `train-ticket-graph` stay unpinned.

Pinned repo descriptions (set on GitHub if currently empty or weak; do not invent features):

| Repo | Description to use |
|---|---|
| `deepcover` | Keep existing: agentic coverage beyond line coverage / meaningful coverage. |
| `food-tracker` | Keep existing privacy-first nutrition tracker description. |
| `judo-core` | Keep existing tournament engine description. |
| `kaizen-backlog` | Keep existing git-native continual-improvement backlog description. |
| `khesh` | Keep existing offline-first household ledger description. |
| `skills` | Keep existing reusable agent skills description. |

## README structure

Target length: one desktop screen, at most one and a half. Readable with images disabled. Markdown only; no HTML layout tricks, no centered `<div>` forests, no visitor pixels.

### 1. Lede

No `Hi 👋`, no H1 name banner. Open on the thesis, then one sentence of who/what:

> Istanbul will report 100% on a test that still passes if the function returns a potato. I work on the other kind of coverage.
>
> I am Anatoly Khelmer. I write TypeScript: test-quality tooling first, then local-first apps that keep data on the device.

Wording may be edited for rhythm in implementation, but the potato line and the tooling-then-local-first order are required.

### 2. Exhibit

Heading, exactly: `Line coverage is a vibes-based metric`.

Use the weak-test snippet already used in the DeepCover README:

```typescript
it('should create order', async () => {
  const result = await service.createOrder(mockInput);
  expect(result).toBeDefined();
});
```

Caption, one or two sentences: Istanbul is green; the test still passes if `createOrder` returns `null`, `{}`, or a wrong order.

### 3. Featured: DeepCover

Link `https://github.com/anatolykhelmer/deepcover`. Three to four sentences, not a tutorial:

- Combines deterministic AST analysis with bounded LLM reasoning
- Scores whether tests protect code (assertion strength, domain states, mocks that replace the thing under test)
- Does not replace Istanbul; it argues with it
- Companion exhibit: `https://github.com/anatolykhelmer/deepcover-demo-orders` (identical Istanbul, different DeepCover)

Call to action: a link to the DeepCover README, not a non-working `npx` command.

### 4. Also shipping

A short list, one line each. Judo is one field with two repos; `judo-scoreboard` stays in this list even though it is not pinned.

- [khesh](https://github.com/anatolykhelmer/khesh) — offline household ledger, double-entry, IndexedDB
- [food-tracker](https://github.com/anatolykhelmer/food-tracker) — nutrition tracker; browser only, no account
- [judo-scoreboard](https://github.com/anatolykhelmer/judo-scoreboard) / [judo-core](https://github.com/anatolykhelmer/judo-core) — contest UI and tournament engine, no server at contest time
- [skills](https://github.com/anatolykhelmer/skills) — agent skills as git-native tools, not a prompt folder
- [kaizen-backlog](https://github.com/anatolykhelmer/kaizen-backlog) — git-native backlog for how you work with Cursor and Claude

No extra repos in this list.

### 5. Person

Quiet block after the work. Required facts only:

- Based in Israel
- Judo: the README sentence is `I love judo.` — no rank, no club, no emoji. Humor stays in the lede/exhibit; do not force a joke here.
- Stack, one line: TypeScript, Node, React, Jest/Vitest
- [LinkedIn](https://www.linkedin.com/in/anatoly-khelmer/)

Forbidden here: email, company, “open to work”, pronouns unless later requested.

## Voice rules

- Dry, specific, slightly sarcastic. No hype (“passionate”, “ninja”, “full-stack wizard”).
- Jokes land on coverage theater and empty assertions, not on the reader or on employers.
- Prefer short sentences. Cut any paragraph that restates the previous one.
- Do not add a “feel free to reach out” closer.

## Implementation notes

- Create the public repo via `gh repo create anatolykhelmer/anatolykhelmer --public --source .` from a directory that is not inside `deepcover`.
- Set account metadata with `gh api` (bio, location, linkedin). Pinning uses GitHub’s GraphQL `updateItemsPinnedByViewer` (or the UI if the API shape changes).
- Do not commit this profile into `anatolykhelmer/deepcover`.
- Verification: open `https://github.com/anatolykhelmer` in a browser, confirm README order, potato line, six pins in the specified order, location Israel, LinkedIn visible, no widgets.

## Success criteria

A developer who already knows Istanbul should smile at the exhibit and click DeepCover. A recruiter who scrolls once should see TypeScript, Israel, and LinkedIn without being pitched. The page still makes sense if GitHub’s extra profile chrome is ignored.
