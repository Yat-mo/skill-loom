# Progressive Skill Architecture

Use this method when a skill must organize project rules, route several recurring jobs, support more than one agent harness, or retain hard-won lessons over time. It is an optional architecture gate, not the default shape of every skill.

Source inspiration: [WoJiSama/skill-based-architecture](https://github.com/WoJiSama/skill-based-architecture), reviewed at commit `7169668151505cc09fec1248127549540ff12a76` on 2026-08-08. MIT-licensed mechanisms are adopted semantically with attribution; prose and project-specific templates are not copied wholesale.

## Three laws

1. **Structure serves content.** Start with the smallest shape that makes the real job reliable.
   Check: can every directory be justified by a current route, deterministic action, evaluation, evidence need, or target-platform adapter?
2. **Activation beats storage.** A rule is useful only if the normal task path makes the agent encounter it before the decision it should change.
   Check: trace one real request from description to workflow to the rule; does reading it change the next action or check?
3. **Structure may be reusable; content must be earned.** Reuse manifests, validators, and empty protocol blocks, but do not prefill business rules, gotchas, or rationalizations.
   Check: would a Go service and a React site both accept the copied content unchanged? If not, replace it with an explicit fill decision or omit it.

## Choose a structural tier

### Single-file

Use when there are fewer than three coherent topics, no repeated multi-step workflow, and no target-specific adapter beyond normal discovery.

Expected shape:

```text
skill-name/
└── SKILL.md
```

### Folder-light

Use when one recurring procedure, one deterministic helper, or several independently useful references have appeared.

Add only the resource types that have a load or execution reason:

```text
skill-name/
├── SKILL.md
├── references/    # conditional judgment/background
├── workflows/     # ordered procedures, only when repeated
└── scripts/       # deterministic or repeatedly rewritten actions
```

### Full

Use when at least one of these pressures is proven:

- three or more distinct recurring task routes
- the same costly pitfall has recurred and needs route-time activation
- two or more harnesses need different discovery/entry adapters
- rules, workflows, and project facts change at different rates
- route drift or unreachable files have caused an observed failure

A full project skill may add `routing.yaml`, rules, gotchas, platform shells, and hooks. Each remains optional and must pass a reachability/usefulness check.

## Route after activation

The frontmatter `description` is a coarse activation boundary, not a workflow catalog. It should say what job the skill owns, natural user expressions, and important exclusions.

After activation:

1. Re-match the current request on every new task, including later tasks in the same session.
2. Select one route by intent; use an explicit `other` fallback.
3. Load the chosen workflow first.
4. Load rules, references, and gotchas only when they can change the next decision.
5. Do not treat keyword overlap as proof of route ownership.

If `routing.yaml` is introduced, keep exact route data there and generate summaries/adapters from it. Do not maintain several hand-edited copies.

## Principle plus check

Write important rules in this form:

```markdown
## Principle

Imperative behavior and why it matters.

Check: a command that can run, or one concrete question answerable from the artifact.
```

Prefer checks tied to user intent, changed files, output evidence, or route reachability. Avoid vague checks such as “does this look good?”

## Task anchor and native plan

For non-trivial work, establish:

- Goal: the result the current task must produce
- Boundaries: what must not change or expand
- Done When: observable evidence that proves completion

Use the harness-native plan as the runtime instance. Do not persist a planning file unless the user or workflow requires one. Re-anchor after interruption, compaction, or new evidence that invalidates the plan.

## Closure and learning

Pure Q&A and read-only advice do not need an AAR. After non-trivial mutation, scan:

1. Did a new reusable pattern appear?
2. Did a costly, non-obvious trap appear?
3. Was a missing rule responsible for wasted work?
4. Is an existing rule stale?

Record only when at least two of these are true: likely to recur, costly if missed, not obvious from the code or normal documentation. Generalize the lesson, put it in the lightest suitable file, and activate it from the owning task path.

Rationalization or “red flag” tables may contain only excuses observed in real failures or pressure tests. Never prefill imagined failure language.

## Adapter boundaries

- Codex/OpenAI: keep frontmatter compatible and generate `agents/openai.yaml`.
- Cursor: generate a registration entry only when Cursor is a declared target.
- Thin shells: keep them as routing/constraint adapters, not knowledge warehouses.
- Hooks: add only when the harness supports them and a deterministic re-injection or safety gate is worth the maintenance cost.
- Subagents: optional execution strategy, never a structural requirement; use only when the harness and user policy permit it.

## Validation

Apply only the gates earned by the chosen tier:

- every skill: frontmatter, links, root entrypoint, trigger boundaries
- routed skill: route schema, file existence, fallback, reachability, generated-adapter consistency
- self-maintaining skill: learning threshold, activation path, stale-rule removal
- cross-harness skill: adapter-specific validation without duplicating canonical content
- publishable skill: license, ownership, secrets, version, PR/release, discovery, clean install

Line counts are warnings that trigger judgment. Split only when the parts have independent load reasons; merge when real callers always co-load and co-change them.
