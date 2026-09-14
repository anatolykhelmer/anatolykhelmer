# GitHub Profile Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Publish an editorial GitHub profile for `anatolykhelmer`: README column, account bio/location/LinkedIn, and six pinned repos.

**Architecture:** A new public special repo `anatolykhelmer/anatolykhelmer` (not a branch of `deepcover`) whose `README.md` is the profile column. Account card fields are set via `gh api`. Pins are applied in the GitHub UI because the public GraphQL API does not expose a pin mutation; the plan verifies pins by querying `pinnedItems`.

**Tech Stack:** Markdown, Git, GitHub CLI (`gh`), GitHub REST/GraphQL for read/update of user fields, browser for pin UI and live verification.

## Global Constraints

- Working directory is `/Users/anatoly/MyProjects/anatolykhelmer`. Never add files to `/Users/anatoly/MyProjects/deep-cover` or `anatolykhelmer/deepcover`.
- Language: English. Voice: dry humor; jokes land on coverage theater and empty assertions, not on the reader or employers.
- No GitHub stats, snake, typing GIF, visitor counters, trophy cards, or badge walls.
- No bilingual README. No email, company, role, or “open to work”.
- No copy-paste `npx` one-liner. Call to action is a link to the DeepCover README.
- Markdown only: no HTML layout tricks, no centered `<div>` forests, no visitor pixels.
- Potato line and tooling-then-local-first order are required. Exhibit heading is exactly `Line coverage is a vibes-based metric`.
- Pinned repos, in this order: `deepcover`, `food-tracker`, `judo-core`, `kaizen-backlog`, `khesh`, `skills`.
- LinkedIn: `https://www.linkedin.com/in/anatoly-khelmer/`. Location: Israel.
- Account bio, verbatim, ≤160 characters: `Istanbul reports 100% on tests that would still pass if the function returned a potato. DeepCover, TypeScript, local-first.`
- Do not invent pinned-repo descriptions; keep existing GitHub descriptions.
- Target README length: one desktop screen, at most one and a half.

## File map

| Path | Responsibility |
|---|---|
| `/Users/anatoly/MyProjects/anatolykhelmer/README.md` | Profile column rendered at `https://github.com/anatolykhelmer` |
| `/Users/anatoly/MyProjects/anatolykhelmer/.gitignore` | Ignore `.DS_Store` |
| `/Users/anatoly/MyProjects/anatolykhelmer/docs/superpowers/specs/2026-09-14-github-profile-design.md` | Already exists; keep, do not rewrite |
| `/Users/anatoly/MyProjects/anatolykhelmer/docs/superpowers/plans/2026-09-14-github-profile.md` | This plan |

No app code, no CI, no verify script committed to the repo. Verification is shell `grep` / `gh api` / browser, run during tasks.

---

### Task 1: Local git repo and profile README

**Files:**
- Create: `/Users/anatoly/MyProjects/anatolykhelmer/.gitignore`
- Create: `/Users/anatoly/MyProjects/anatolykhelmer/README.md`
- Existing: `/Users/anatoly/MyProjects/anatolykhelmer/docs/superpowers/specs/2026-09-14-github-profile-design.md`

**Interfaces:**
- Consumes: design spec copy rules (lede, exhibit, DeepCover, Also shipping, Person)
- Produces: `README.md` at repo root; git repository on `main`

- [ ] **Step 1: Confirm we are not inside deepcover**

Run:

```bash
pwd
ls /Users/anatoly/MyProjects/anatolykhelmer/docs/superpowers/specs/2026-09-14-github-profile-design.md
```

Expected: cwd may still be `deep-cover`; the spec path exists. All later commands in this task use `working_directory` `/Users/anatoly/MyProjects/anatolykhelmer`.

- [ ] **Step 2: Write the failing content checks (no README yet)**

Run from `/Users/anatoly/MyProjects/anatolykhelmer`:

```bash
test -f README.md && echo HAS_README || echo NO_README
```

Expected: `NO_README`

- [ ] **Step 3: Init git if needed, add .gitignore**

Run from `/Users/anatoly/MyProjects/anatolykhelmer`:

```bash
git init -b main
```

Write `.gitignore`:

```
.DS_Store
```

- [ ] **Step 4: Write README.md with this exact content**

````markdown
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

Based in Israel. I train judo.

TypeScript, Node, React, Jest/Vitest.

[LinkedIn](https://www.linkedin.com/in/anatoly-khelmer/)
````

Do not add an H1 name banner, a closer (“feel free to reach out”), email, or widgets.

- [ ] **Step 5: Run required-content checks**

Run from `/Users/anatoly/MyProjects/anatolykhelmer`:

```bash
python3 - <<'PY'
from pathlib import Path
text = Path("README.md").read_text()
required = [
    "Istanbul will report 100% on a test that still passes if the function returns a potato.",
    "test-quality tooling first, then local-first",
    "## Line coverage is a vibes-based metric",
    "expect(result).toBeDefined()",
    "https://github.com/anatolykhelmer/deepcover",
    "https://github.com/anatolykhelmer/deepcover-demo-orders",
    "https://github.com/anatolykhelmer/deepcover#readme",
    "https://github.com/anatolykhelmer/khesh",
    "https://github.com/anatolykhelmer/food-tracker",
    "https://github.com/anatolykhelmer/judo-scoreboard",
    "https://github.com/anatolykhelmer/judo-core",
    "https://github.com/anatolykhelmer/skills",
    "https://github.com/anatolykhelmer/kaizen-backlog",
    "Based in Israel",
    "I train judo",
    "TypeScript, Node, React, Jest/Vitest",
    "https://www.linkedin.com/in/anatoly-khelmer/",
]
forbidden = [
    "👋",
    "anatoly.khelmer@gmail.com",
    "open to work",
    "open to work".title(),
    "github-readme-stats",
    "snake",
    "visitor",
    "npx @anatolykhelmer",
    "feel free",
    "passionate",
    "ninja",
    "<div",
    "<img",
]
missing = [s for s in required if s not in text]
present = [s for s in forbidden if s.lower() in text.lower()]
if missing or present:
    raise SystemExit(f"missing={missing!r} forbidden_present={present!r}")
print("README checks passed")
PY
```

Expected: `README checks passed`

- [ ] **Step 6: Commit**

```bash
git add .gitignore README.md docs/superpowers/specs/2026-09-14-github-profile-design.md docs/superpowers/plans/2026-09-14-github-profile.md
git commit -m "$(cat <<'EOF'
Add editorial GitHub profile README.

EOF
)"
```

---

### Task 2: Create public special repo and push

**Files:**
- Remote: `https://github.com/anatolykhelmer/anatolykhelmer` (does not exist yet)

**Interfaces:**
- Consumes: local `main` from Task 1
- Produces: public GitHub repo named exactly `anatolykhelmer` under user `anatolykhelmer`

- [ ] **Step 1: Confirm the special repo is missing**

```bash
gh repo view anatolykhelmer/anatolykhelmer --json name 2>&1
```

Expected: error that the repository could not be resolved.

- [ ] **Step 2: Create and push**

From `/Users/anatoly/MyProjects/anatolykhelmer`:

```bash
gh repo create anatolykhelmer/anatolykhelmer --public --source=. --remote=origin --push
```

Expected: repo created, `main` pushed. GitHub will render `README.md` on `https://github.com/anatolykhelmer`.

- [ ] **Step 3: Verify remote README contains the potato line**

```bash
gh api repos/anatolykhelmer/anatolykhelmer/contents/README.md --jq .content | base64 -d | grep -F "returns a potato"
```

Expected: a line containing `returns a potato`.

---

### Task 3: Account card — bio, location, LinkedIn

**Files:**
- GitHub user settings for `anatolykhelmer` (no local files)

**Interfaces:**
- Consumes: bio string, location `Israel`, LinkedIn URL from spec
- Produces: public profile card fields

- [ ] **Step 1: Measure bio length (must be ≤160)**

```bash
python3 - <<'PY'
bio = "Istanbul reports 100% on tests that would still pass if the function returned a potato. DeepCover, TypeScript, local-first."
print(len(bio))
assert len(bio) <= 160
PY
```

Expected: a number ≤ 160, no assertion error.

- [ ] **Step 2: Patch bio and location**

```bash
gh api --method PATCH /user \
  -f bio='Istanbul reports 100% on tests that would still pass if the function returned a potato. DeepCover, TypeScript, local-first.' \
  -f location='Israel'
```

Expected: JSON user object with those `bio` and `location` values.

- [ ] **Step 3: Add LinkedIn social account**

```bash
gh api --method POST /user/social_accounts \
  --input - <<'EOF'
{"account_urls":["https://www.linkedin.com/in/anatoly-khelmer/"]}
EOF
```

If GitHub returns that the account already exists, that is success. If the endpoint 404s, set LinkedIn only via the README link (already present) and note it in the task report; do not invent a different API.

- [ ] **Step 4: Read back the card**

```bash
gh api user --jq '{bio,location,blog}'
gh api user/social_accounts
```

Expected: `bio` matches the spec string, `location` is `Israel`, `blog` empty or unchanged. Social accounts include LinkedIn if Step 3 succeeded.

---

### Task 4: Pin six repositories

**Files:**
- GitHub profile pins for `anatolykhelmer` (no local files)

**Interfaces:**
- Consumes: repo names `deepcover`, `food-tracker`, `judo-core`, `kaizen-backlog`, `khesh`, `skills`
- Produces: those six pinned, in that order

Public GraphQL does not expose a pin mutation (`updateItemsPinnedByViewer` / `updatePinnedItems` are not on `Mutation`). Do not spend time hunting undocumented mutations. Pin in the GitHub UI, then verify with GraphQL.

- [ ] **Step 1: Snapshot current pins and confirm descriptions exist**

```bash
gh api graphql -f query='
query {
  user(login: "anatolykhelmer") {
    pinnedItems(first: 6, types: REPOSITORY) {
      nodes { ... on Repository { name } }
    }
  }
}'

for repo in deepcover food-tracker judo-core kaizen-backlog khesh skills; do
  gh repo view "anatolykhelmer/$repo" --json name,description
done
```

Expected: each description is non-empty. Do not PATCH descriptions.

- [ ] **Step 2: Pin in the GitHub UI**

Open `https://github.com/anatolykhelmer`. Click **Customize your pins**. Uncheck everything that is not in the list. Check exactly:

1. `deepcover`
2. `food-tracker`
3. `judo-core`
4. `kaizen-backlog`
5. `khesh`
6. `skills`

Drag until that visual order matches. Save.

If browser automation cannot complete the pin dialog, stop and ask the user to do this one UI action. Do not skip verification.

- [ ] **Step 3: Verify pin names and order**

```bash
gh api graphql -f query='
query {
  user(login: "anatolykhelmer") {
    pinnedItems(first: 6, types: REPOSITORY) {
      nodes { ... on Repository { name } }
    }
  }
}'
```

Expected `nodes` names, in order:

```
deepcover
food-tracker
judo-core
kaizen-backlog
khesh
skills
```

`deepcover-demo-orders`, `woledger`, `judo-scoreboard`, and `train-ticket-graph` must not appear.

---

### Task 5: Live profile verification

**Files:**
- None. Target URL: `https://github.com/anatolykhelmer`

**Interfaces:**
- Consumes: Tasks 1–4 published
- Produces: evidence that the public page matches the spec

- [ ] **Step 1: Open the public profile**

Navigate to `https://github.com/anatolykhelmer` (logged-out or a fresh load, not the repo page `.../anatolykhelmer/anatolykhelmer` alone). Snapshot the page.

- [ ] **Step 2: Check README column**

Confirm, in order: potato lede → exhibit heading `Line coverage is a vibes-based metric` → `toBeDefined()` snippet → DeepCover + demo link + README link → Also shipping four lines → Person (Israel, judo, stack, LinkedIn). Confirm there are no stats widgets, snake, GIFs, visitor counters, or email.

- [ ] **Step 3: Check account card**

Confirm bio matches the spec string, location shows Israel, LinkedIn is visible on the card and/or in the Person block.

- [ ] **Step 4: Check pins**

Confirm the six repos in spec order, with their existing descriptions.

- [ ] **Step 5: Images-disabled sanity**

Re-read the README via:

```bash
gh api repos/anatolykhelmer/anatolykhelmer/readme --jq .content | base64 -d
```

Expected: the column still makes sense as plain markdown. No image URLs, no HTML.

If any check fails, fix the corresponding surface (README commit + push, `gh api` patch, or pin UI) and re-run this task. Do not declare done on a local file that is not live.
