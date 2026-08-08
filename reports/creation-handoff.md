# Qiaomu Meta Skill Creation Handoff

## Result

- Skill: `qiaomu-meta-skill` 2.9.0, Yat-mo fork
- Job: research, architect, evaluate, package, govern, and safely publish reusable skills through one self-contained workflow
- Status: progressive project-skill architecture and Codex adapter prepared on a feature branch; public 2.9.0 evidence remains `missing evidence` until the fork release workflow completes

## Reference skills studied

### `yaojingang/yao-meta-skill`

- Why shortlisted: direct meta-skill reference with full-lifecycle engineering, evaluation, governance, and portability concepts.
- Learned: Skill IR, evidence boundaries, release gates, output evaluation, review layers, and post-release iteration.
- Applied in: Qiaomu Skill OS layers, gate ladder, Skill IR export, output-eval method, and SkillOps references.

### `wshobson/agents@evaluation-methodology`

- Why shortlisted: complementary evaluation specialist found during prior-art research.
- Learned: separate evaluation dimensions, compare before/after behavior, preserve confidence and evidence limits.
- Applied in: trigger-first evaluation, output assertions, evidence labels, and the distinction between design and validated advantages.

### `joeseesun/qiaomu-skill-publisher`

- Why shortlisted: the user's explicit reference and the existing Qiaomu implementation of LICENSE, README, Profile, repository naming and `npx` installation.
- Learned: idempotent profile markers, strict YAML handling, repository/skill-name separation, public README scaffolding, discovery and temporary installation.
- Applied in: bundled `scripts/publish_skill.py`, `references/publishing.md`, profile assets, trigger cases and publisher regression tests.

### `WoJiSama/skill-based-architecture`

- Why shortlisted: user-specified MIT reference focused on project-rule routing, progressive disclosure, thin adapters, route reachability, and failure-driven maintenance.
- Learned: structure serves content, activation over storage, reusable structure without prefilled project content, principle-plus-check rules, task anchors, route rematching, and evidence-gated AAR.
- Applied in: `references/progressive-skill-architecture.md`, `SKILL.md` Compact Workflow, Codex adapter metadata, trigger cases, and owner-scoped publishing policy.

## Absorbed and rejected

- `keep`: platform-neutral intent, trigger/output evaluation, evidence-bound claims, proportional structure, activation paths, concrete checks, release gates and install verification.
- `adapt`: make routing manifests, thin shells, hooks and harness entries conditional; preserve the Qiaomu profile only for explicitly Qiaomu-owned packages.
- `reject`: mandatory full scaffolds, `primary: true` for Codex, imagined gotchas/rationalizations, mandatory subagents, popularity-only ranking, direct default-branch push, destructive replacement and unsupported completion claims.
- `invent`: owner-scoped profile injection, explicit Codex adapter validation, Python 3.9 catalog compatibility, and one compact architecture reference joined to Qiaomu's existing gate ladder.

## Advantages and highlights

- `design advantage`: prior-art discovery, synthesis, creation, validation, and handoff remain inside one canonical workflow, avoiding conflicting creator instructions. Evidence: `SKILL.md` Router Rules and Compact Workflow.
- `design advantage`: skills.sh installs and SkillsMP repository stars remain source-separated and cannot be combined into a fake score. Evidence: `references/prior-art-research.md`.
- `design advantage`: every created Production+ skill must expose design lineage and distinguish design advantages, validated advantages, and hypotheses. Evidence: `references/creation-handoff.md`.
- `design advantage`: catalog discovery now degrades explicitly under transient failures instead of losing the whole research run or hiding missing evidence. Evidence: `scripts/search_skillsmp.py` and `scripts/research_prior_art.py`.
- `design advantage`: local, PR, and published completion states are machine-checkable instead of prose-only. Evidence: `scripts/release_check.py`.
- `design advantage`: authoring and publishing now share one authority and one gate system; a separate publisher skill is no longer required. Evidence: `scripts/publish_skill.py` and `references/publishing.md`.
- `design advantage`: the integrated publisher cannot push directly to `main/master`, reuse a released version, silently ignore a failed push, or delete an installed skill without rollback.
- `design advantage`: project skills now grow through Single-file, Folder-light and Full tiers instead of inheriting a ceremonial directory tree. Evidence: `references/progressive-skill-architecture.md`.
- `design advantage`: OpenAI/Codex targets now require a dedicated `agents/openai.yaml` adapter while platform-neutral semantics stay canonical. Evidence: `agents/openai.yaml` and `scripts/validate_skill.py`.
- `design advantage`: generated packages require an explicit owner; Qiaomu profile injection is limited to Qiaomu-owned packages. Evidence: `scripts/publish_skill.py`.
- `validated advantage`: publisher unit tests cover URL parsing, profile idempotence, generated README quality, default-branch rejection, pending-check blocking, read-only dry-run and bundled assets.
- `hypothesis`: the richer handoff should improve user trust and adoption decisions, but a human comprehension or install-conversion study remains `missing evidence`.
- `design advantage`: the README now leads with the user outcome, a one-line installation command, a capability comparison, natural-language examples, and 28 evidence-backed practice cases instead of internal architecture.
- `validated advantage`: the Codex history catalog distinguishes 18 public repositories from 10 local/private cases and separates created/updated packages from researched prior art without publishing raw dialogue or local paths.

## Verification and limits

- Deterministic package validation: passed with 0 failures and 0 warnings.
- Trigger eval: passed 27/27, with 0 false positives and 0 false negatives.
- Unit tests: passed 38/38, including Python 3.9 catalog compatibility, Codex adapter, progressive architecture, explicit-owner, and owner-scoped profile regressions.
- Built-in prior-art smoke: passed 2/2 queries across skills.sh and SkillsMP, preserving 51 deduplicated candidate families with no missing catalog evidence.
- Self-contained publisher dry-run against this repository: passed, resolved `joeseesun/qiaomu-meta-skill`, planned no unwanted file changes, and reported default-branch push as forbidden.
- Independent `--prepare-only` fixture: passed; created MIT LICENSE, product README, three bundled Profile assets and an idempotent profile block, then passed the package validator with zero warnings.
- Integrated discovery verifier against the upstream published repository previously passed; public discovery and clean installation for Yat-mo Fork 2.9.0 remain `missing evidence` until release.
- Live dual-catalog smoke: passed in strict mode for `skill evaluation`; skills.sh and SkillsMP both completed, producing 9 merged candidate families with source metrics kept separate.
- Local release readiness: passed with 6 pass, 3 warn, and 0 block. Warnings accurately record the dirty worktree, unavailable clean-install proof before a remote revision exists, and missing provider/human output evidence.
- PR, merged default-branch, GitHub release, and public clean-install proof for 2.9.0: `missing evidence` until the current release workflow completes.
- Provider-backed head-to-head output evaluation: `missing evidence`.
- Human blind comparison of handoff persuasiveness: `missing evidence`.
