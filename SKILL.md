---
name: skill-loom
description: |
  Research, create, improve, migrate, evaluate, package, install-check, govern, and safely publish reusable agent skills from project rules, workflows, prompts, transcripts, docs, SOPs, runbooks, scripts, or notes. Use Skill Loom for new or existing skills, project skill architecture, progressive disclosure, routing and trigger boundaries, prior-art synthesis, trigger or output evals, Skill IR, release gates, GitHub repository and pull-request publication, versioned Releases, clean npx installation, team reuse, and create-and-publish flows. Formerly qiaomu-meta-skill; activate for legacy requests using that name. The publication path is self-contained and forbids direct default-branch pushes. Exclude one-off summaries, translations, ordinary docs, non-skill package publishing, and tasks that explicitly should not become a skill.
metadata:
  author: Yat-mo
  version: "3.0.1"
  upstream_inspiration: joeseesun/qiaomu-meta-skill; yaojingang/yao-meta-skill; joeseesun/qiaomu-skill-publisher; WoJiSama/skill-based-architecture
---

# Skill Loom

Turn repeatable work into reusable, evidence-backed agent skills—not long prompts.

## Router Rules

- Route by frontmatter `description` first.
- Once selected, `skill-loom` is the single authoring authority. Do not also invoke a generic `skill-creator` unless the user explicitly requests comparison or this skill is unavailable.
- Built-in prior-art discovery belongs to this skill. Do not install, load, or delegate to a separate discovery skill.
- Built-in GitHub publishing belongs to this skill. Do not require or invoke a separate publisher skill after this package is selected.
- Keep the package root `SKILL.md` to routing and the minimal workflow. Put judgment in `references/`, deterministic behavior in `scripts/`, regression cases in `evals/`, and evidence in `reports/`.
- A package has one discoverable root `SKILL.md`; embedded examples and fixtures use `SKILL.example.md` or `SKILL.fixture.md`.
- Do not turn one-off summaries, translations, explanations, or brainstorming into skills.
- Match the user's action: create/refactor/package requests may edit; audit/evaluate/diagnose-only requests remain read-only; publish only when explicitly requested.
- Prefer concise Chinese-first names with no more than three meaningful hyphen parts. Add a brand prefix only when the user explicitly wants it.
- Require an explicit owner for publishable skills. Never assign another creator's authorship, profile assets, or copyright to a package by default.
- For project-rule architecture, multi-workflow routing, cross-harness adapters, or self-maintenance, read [Progressive Skill Architecture](references/progressive-skill-architecture.md). Apply its mechanisms proportionally, not as a mandatory full scaffold.

## Modes

- `Scaffold`: exploratory or personal; minimum useful files.
- `Production`: team reuse; README, interface, trigger eval, output contract, and install evidence.
- `Library`: shared infrastructure; Production plus Skill IR, portability, trust, and review cadence.
- `Governed`: public or high-trust; Library plus permission, rollback, secret, release, and claim gates.

Choose proportionally with [Operating Modes](references/operating-modes.md), [Gate Selection](references/gate-selection.md), and [QA Ladder](references/qa-ladder.md).

## Built-In Prior-Art Discovery

Before a new skill or substantial redesign:

1. Derive 2–4 intent-shaped queries covering outcome, domain action, quality mechanism, and an adjacent synonym when useful.
2. Prefer the unified runner:

```bash
python3 scripts/research_prior_art.py "<query 1>" "<query 2>" --strict --summary --output reports/prior-art-candidates.json
```

Its underlying catalog calls remain:

```bash
npx --yes skills find "<query>"
python3 scripts/search_skillsmp.py "<query>" --limit 20 --sort stars
```

3. Keep metrics separate: skills.sh installs measure adoption; SkillsMP stars belong to the source repository; neither is a user rating or quality score.
4. Deduplicate by canonical GitHub repository and skill path. Collapse translations, mirrors, and obvious forks without adding metrics together.
5. Shortlist genuinely relevant popularity, trust, and complementary anchors. Inspect source `SKILL.md`, maintenance, license, permissions, security signals, and available rating evidence; never execute untrusted candidate code just to study it.
6. Synthesize `keep / adapt / reject / invent`. Map each adopted mechanism to the new package instead of collaging prose.
7. Preserve dated sources, metrics, failures, deduplication, lessons, rejections, and missing evidence in `reports/prior-art-research.md` for Production+ or materially researched work.

If a catalog fails, continue with the other sources, record `missing evidence`, and lower the claim. Full method: [Prior-Art Research](references/prior-art-research.md).

## Generalization Gate

Before promoting one failure into a core rule:

1. restate it as a domain-neutral behavior
2. classify it as core mechanism, optional adapter, or eval-only fixture
3. promote only safety/factual/permission invariants or behavior repeated across unrelated domains
4. keep one-off details in fixtures or specialist references
5. rerun the original and unrelated boundary cases

Prefer intent fidelity, source fidelity, and decision rules over an expanding topic encyclopedia.

## Skill Loom Pipeline

1. `Intent`: recurring job, users, inputs, output, exclusions, standards, references.
2. `Skill IR`: platform-neutral meaning and evidence boundary.
3. `Package`: lean root instructions, interface, README, and earned resources.
4. `Eval`: trigger boundaries first; output/runtime/human eval when risk justifies it.
5. `Review`: package, context, trust, install, README, and public claims.
6. `Operate`: explicit feedback, failures, drift, and next-iteration proposals without raw private content.

## Compact Workflow

1. Decide whether the request deserves a reusable skill; otherwise answer directly and create no package.
2. Capture job, finished output, target users, inputs, exclusions, permissions, standards, existing assets, platforms, and publication intent.
3. Pass prior-art discovery or record why it is not applicable or missing evidence.
4. Pass the generalization gate for sample-driven core changes.
5. Choose the lightest valid mode.
6. Write the `description` early; run `evals/trigger_cases.json` before expanding structure.
7. Choose the lightest structural tier that the content earns. Add routing manifests, workflows, thin shells, or hooks only when repeated tasks and target harnesses justify them.
8. Write important principles as behavior plus a concrete check. A statement without a post-execution check is guidance, not a gate.
9. Create only earned resources. Never create ceremonial directories or duplicate README/SKILL prose.
10. Export `reports/skill-ir.json` for Production+, public, or cross-platform packages.
11. Add output evals when correctness, safety, persuasion, or repeatability cannot be shown by trigger tests alone.
12. Keep mutations within the requested action boundary and preserve rollback for risky changes.
13. Validate package, unit tests, trigger behavior, route reachability when routing exists, context budget, secret/trust boundaries, and evidence claims.
14. Produce the creation handoff and clearly label missing evidence.
15. When publication is requested, read [Self-Contained Skill Publishing](references/publishing.md), then use the bundled publisher for feature branch → validation → PR → merge → release/install verification; never push directly to the default branch.

Core commands:

```bash
python3 scripts/validate_skill.py .
python3 scripts/export_skill_ir.py . --output reports/skill-ir.json
python3 scripts/trigger_eval.py . --cases evals/trigger_cases.json --output reports/trigger-eval.json
python3 scripts/release_check.py . --phase local --run-tests
python3 scripts/publish_skill.py /path/to/skill --dry-run
```

## Gate Ladder

- `Scaffold`: valid frontmatter, useful README hook, natural triggers, explicit exclusions.
- `Production`: Scaffold plus interface, trigger eval, output contract, troubleshooting, root isolation, and install verification.
- `Library`: Production plus Skill IR, portability, trust, review cadence, and evidence artifacts.
- `Governed`: Library plus permission/rollback boundary, secret scan, output or integrity-preserving human evidence, and public-claim guard.

Unavailable telemetry, provider runs, approval, install proof, or human review must remain `missing evidence`; planned work is not proof. See [Review And Release Gates](references/review-release-gates.md) and [Resource Boundary Spec](references/resource-boundaries.md).

## Output Contract

For package-producing requests, provide only what the selected mode earns:

1. working skill directory and trigger-aware root `SKILL.md`
2. aligned `agents/interface.yaml`, plus `agents/openai.yaml` when OpenAI/Codex is a target
3. human-facing README for shared/public skills
4. trigger cases and generated trigger report for Production+
5. Skill IR, prior-art report, and creation handoff for Production+
6. optional references, scripts, output evals, reports, and manifest when they improve judgment, repeatability, or evidence
7. publish artifacts only when publishing was requested

The final creation handoff must name the **reference skills studied**, give **candidate-specific lessons**, explain deliberate rejections and original contributions, and label each highlight as **design advantage**, **validated advantage**, or **hypothesis**. Never claim global superiority without a fair comparison. Use [Creation Handoff](references/creation-handoff.md).

## Publish Flow

1. Treat README as a product page: value, install, natural examples, prerequisites, outputs, configuration, risks, and troubleshooting.
2. Audit without mutation when useful: `python3 scripts/publish_skill.py /path/to/skill --dry-run`.
3. Only after an explicit publish request, run `python3 scripts/publish_skill.py /path/to/skill`.
4. The bundled publisher prepares MIT LICENSE and README; adds Qiaomu profile assets only for explicitly Qiaomu-owned packages; resolves skill/repository identity; blocks secrets and reused release versions; creates or reuses a GitHub repository; and publishes only through a feature branch and PR.
5. Merge is blocked by conflicts, failed/pending checks or requested changes. Successful publication creates `vX.Y.Z`, verifies `npx skills add --list`, performs an isolated install, and runs the published release gate.
6. Do not report publication complete until the remote default version, GitHub Release, discovery and clean installation are verified.

Detailed CLI and safety decisions: [Self-Contained Skill Publishing](references/publishing.md). README method: [GitHub README Playbook](references/github-readme-playbook.md). Operation method: [SkillOps Loop](references/skillops-loop.md).

## Skill Loom Defaults

- Prefer practical, concise, publishable Chinese output.
- Keep one creator authority and one root skill entrypoint.
- Preserve platform-neutral source plus minimal adapters.
- Re-match routing for every new task; do not reuse the previous task's route from memory.
- Public claims must match trigger, output, runtime, install, or human evidence actually present.
- Upstream ideas are adopted semantically with attribution, not mirrored wholesale.

## Reference Map

- Design: [Skill Engineering Method](references/skill-engineering-method.md), [Progressive Skill Architecture](references/progressive-skill-architecture.md), [Skill Archetypes](references/skill-archetypes.md), [Intent Dialogue](references/intent-dialogue.md), [Non-Skill Decision Tree](references/non-skill-decision-tree.md)
- Evidence: [Eval Playbook](references/eval-playbook.md), [Output Eval](references/output-eval-method.md), [Skill IR](references/skill-ir-method.md), [Governance](references/governance.md)
- Release: [Self-Contained Publishing](references/publishing.md), [Review And Release Gates](references/review-release-gates.md), [GitHub README](references/github-readme-playbook.md), [SkillOps](references/skillops-loop.md)
