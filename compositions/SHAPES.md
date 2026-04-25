# Composition Shapes

Stage 10 of the apprenticeship asks for one composition that uses your new construct. Most compositions land in one of four canonical shapes. Pick the one closest to what your construct does, study the exemplar, then author your variant.

These are not templates with placeholders — they are real compositions that survived review. Read them as patterns, not as fill-in-the-blanks.

## The four shapes

| Shape | One-line | Exemplar | Reach for it when… |
|---|---|---|---|
| **wayfinding-pair** | recommend → craft-gate | [`explore-ecosystem.yaml`](./explore-ecosystem.yaml) | your construct surfaces choices and a craft lens validates |
| **audit-pair** | primary → cross-reference | [`feel-audit.yaml`](https://github.com/0xHoneyJar/loa-constructs/blob/main/grimoires/compositions/feel-audit.yaml) | your construct emits a Verdict that benefits from a second-construct reality check |
| **eye-hand** | direction → execution (with iterate loop) | [`feel-image.yaml`](https://github.com/0xHoneyJar/loa-constructs/blob/main/grimoires/compositions/feel-image.yaml) | one construct distills *what* and another executes *how* |
| **full-stack** | multi-construct sequential pipeline | [`website-scaffold.yaml`](https://github.com/0xHoneyJar/loa-constructs/blob/main/grimoires/compositions/website-scaffold.yaml) | the operator's job spans 5+ stages with multiple iteration loops |

## Shape · wayfinding-pair

```
[primary: surfaces options + reasoning] → [craft-gate: validates against standard]
```

Two stages, both fresh-mode. Primary writes `Verdict` + `Signal`. Craft-gate refines the Verdict with severity tagging and caveats. Best for *recommendation* compositions — "what should I use to X?" with a built-in taste check before emission.

The pattern: synthesis register tolerates context dilution (CURATOR's lens is breadth-first); the craft-gate's narrow taste lens catches drift before the recommendation ships.

Exemplar: `explore-ecosystem.yaml` — `construct-network-tools/exploring-network` → `artisan/scoring-experience`.

## Shape · audit-pair

```
[primary: produces Verdict] → [cross-reference: enriches Verdict with second-construct context]
```

Two-or-three stages, primary-then-cross-reference. The primary owns the substantive analysis; the cross-reference construct lifts it from a single-surface Verdict into a multi-surface or longitudinal one. Pattern is symmetric: either side can lead, depending on which lens grounds the analysis.

The pattern: a single construct's Verdict is honest but parochial. Cross-referencing against a paired construct's context (friction map, behavior log, prior decisions) catches what one lens cannot see.

Exemplar: `feel-audit.yaml` — `artisan/decomposing-feel` + `artisan/scoring-experience` → `observer/analyzing-gaps`.

## Shape · eye-hand

```
[direction: distills creative brief from context] ↕ [execution: produces artifact from brief]
                                                    └─[craft-gate: selection test]
```

Three-or-four stages with an iterate loop between execution and selection. Direction is persistent (brief refines across iterations); execution is persistent (seed/ref history accumulates); selection is fresh (clean evaluation each pass). Output is artifact-shaped, not verdict-shaped.

The pattern: prompt engineers without direction produce plausible-but-uncanny output; creative directors without prompting technique produce beautiful briefs that never land. Naming both stages explicitly forces neither to be skipped.

Exemplar: `feel-image.yaml` — `artisan/directing-generation` ↔ `the-mint/prompting-images` → `the-mint/curate` → `the-mint/materialize`.

## Shape · full-stack

```
[research] → [exploration ↕ refinement] → [generation] → [system ↕ component] → [structure]
```

Five-to-seven stages, mix of fresh and persistent, multiple iterate loops. One construct per stage; persistent teammates accumulate register depth across their iteration partner.

The pattern: a single operator job (scaffolding a website, shipping a feature) spans research, design, build, and structure. Each phase wants a different expert. Compose them as one pipe with declared iteration boundaries; let the runner orchestrate.

Exemplar: `website-scaffold.yaml` — `k-hole` → `the-easel` ↔ `the-mint/mint` ↔ `the-easel` → `artisan/designing-systems` ↔ `artisan/distilling-components` → `the-arcade/mapping-topology`.

## When none of the shapes fit

Your construct may not chain at all. Two cases:

- **Read-only data exposure** (codex shape): your construct exposes a structured knowledge base via read-only skills (browse, query, cross-reference). It is consumed *by* other compositions, not authored as one. Reference: [`construct-mibera-codex`](https://github.com/0xHoneyJar/construct-mibera-codex) — three skills over a knowledge graph, no chain.
- **Single-skill construct**: one expert, one workflow, no orchestration needed. Authoring stage 10 in this case means writing a *minimal* composition that demonstrates the skill in context — one stage, one construct, full input/output declaration. Use it as the published invocation contract.

If your construct genuinely needs a new shape, document the shape here when it appears. Patterns earn their place by recurring; do not invent a shape for one composition.

## What to author at stage 10

1. Pick the shape closest to your construct's role in the chain
2. Study the exemplar — read `chain:`, `iterate:`, `outputs:`, `composes_symmetrically_with:`
3. Author `compositions/<your-demo>.yaml` declaring at minimum:
   - `schema_version: "1.0"`, `kind: workflow`, `name`, `description`, `intent`
   - `backend: headless-tmux` (until cycle-007 ships alternatives)
   - `inputs` with declared types (Artifact / Intent / Operator-Model / Signal / Verdict)
   - `chain` with at least one stage invoking your construct
   - `outputs` with destination paths (use `.run/compose/<run_id>/...`)
   - `compose_with`, `invocation_examples`, `when_to_use`, `known_limitations`
4. Run `compose-run <your-demo> --target ./test-canvas` (or with `LOA_STAGE_MOCK=1` for cheap iteration)

CURATOR refuses to advance past stage 10 without a concrete demonstrated use. The composition does not need to be production-ready; it needs to be *runnable* and *grounded in your construct's actual capabilities*.

## References

- Doctrine: `bonfire-construct-pipe-doctrine` v6 §15.2 (workflow-kind composition)
- Runner: `loa-constructs/.claude/scripts/compose-run.sh` (cycle-006 L-backend)
- Stream types: Signal · Verdict · Artifact · Intent · Operator-Model (cycle-007 adds Question)
