# Composing Constructs

Compositions are not prescribed shapes. They emerge when you name what the workflow should *provide* — for the operator running it, and for the end user consuming its output — then chain the right experts to deliver.

This doc is not a menu of templates. It surfaces patterns observed in shipped compositions because naming them helps new authors orient. Read each entry as "this is what happened when X needed to be delivered" — not "this is how X must look."

The philosophy is the constant. The shape is what's left over once the philosophy is named.

## What composing provides

- **A way to name expertise as orchestration.** A construct is a named expert. A composition is what those experts collaborate on, with declared streams and iteration boundaries.
- **Inheritance of feedback mechanisms.** When you compose with `artisan`, you inherit the single-stamp discipline, the shelf test, the craft-gate. You don't re-author the rails — they come with the pack.
- **An invocation contract.** A composition's `inputs` + `outputs` + `chain` is the public surface. Operators don't need to know which skills run; they hand inputs and receive declared streams.
- **A philosophical rail in non-deterministic territory.** Skills give structure to "how and why" you approach problems; scripts give deterministic outputs. Compositions are where that structure compounds across multiple experts.

## Patterns observed in the wild

For each pattern below: lead with what the workflow *provides*, then point at an exemplar.

### wayfinding-pair

**Provides**: a recommendation that's been craft-gated. Operator gets a defensible answer to "what should I use to X"; downstream consumers get reasoning chains they can audit.

**In the wild**: [`find-construct.yaml`](./discovery/find-construct.yaml) — `construct-network-tools/exploring-network` → `artisan/scoring-experience`.

**Reach for it when**: your construct surfaces choices and you want a built-in taste check before emission.

### audit-pair

**Provides**: a Verdict raised from single-surface to multi-surface context. Operator gets cross-referenced findings; downstream consumers (PR reviewers, team members) get evidence chains anchored in two constructs' lenses, not one.

**In the wild**: [`audit-feel.yaml`](https://github.com/0xHoneyJar/loa-constructs/blob/main/grimoires/compositions/discovery/audit-feel.yaml) — `artisan/decomposing-feel` + `artisan/scoring-experience` → `observer/analyzing-gaps`.

**Reach for it when**: your construct emits a Verdict that benefits from cross-reference (friction map, behavior log, prior decisions).

### eye-hand

**Provides**: an artifact produced from a brief, with selection discipline built in. Operator gets output that landed inside the canon; the end user (whoever sees the asset) gets work that feels like it belongs.

**In the wild**: [`direct-render.yaml`](https://github.com/0xHoneyJar/loa-constructs/blob/main/grimoires/compositions/delivery/direct-render.yaml) — `artisan/directing-generation` ↔ `the-mint/prompting-images` → `the-mint/curate` → `the-mint/materialize`.

**Reach for it when**: one construct distills *what should exist* and another produces it.

### full-stack

**Provides**: an end-to-end deliverable across research → design → build → structure. Operator gets a compounded outcome no single expert could deliver alone; the end user (visitor, dashboard user) gets coherence across phases that usually drift.

**In the wild**: [`research-scaffold.yaml`](https://github.com/0xHoneyJar/loa-constructs/blob/main/grimoires/compositions/delivery/research-scaffold.yaml) — `k-hole` → `the-easel` ↔ `the-mint/mint` ↔ `the-easel` → `artisan/designing-systems` ↔ `artisan/distilling-components` → `the-arcade/mapping-topology`.

**Reach for it when**: the operator's job spans 5+ stages and benefits from a different expert per phase.

### construct-emitter

**Provides**: a publishable construct repo as the composition's terminal output. Operator gets a packaged result they can ship as a new pack; the end user (anyone who installs it) gets a queryable, composable expertise surface.

**In the wild**: [`mint-codex.yaml`](https://github.com/0xHoneyJar/loa-constructs/blob/main/grimoires/compositions/experimentation/mint-codex.yaml) — `artisan/synthesizing-taste` → `artisan/distilling-components` ↔ `the-mint/mint` ↔ `the-mint/curate` → `artisan/recording-taste` → `the-mint/materialize`.

**Reach for it when**: you're building tools that scaffold publishable constructs as users iterate (gen-art collection preview tools, lore authoring surfaces, character pipelines).

## When your construct doesn't chain

Compositions express orchestration. Some constructs don't orchestrate — they expose. If your construct is a codex (read-only data over a structured schema), other compositions consume it; it doesn't author one of its own. Reference: [`construct-mibera-codex`](https://github.com/0xHoneyJar/construct-mibera-codex) — three skills over a knowledge graph, no chain.

If your construct has a single skill, your stage-10 composition is that skill in invocation form — one stage, full input/output declaration. The philosophy still lands; the orchestration is degenerate.

## What to author at stage 10

1. Name what the workflow *provides* — for the operator running it, and for the end user consuming the output. Not "what stages does this run" but "what value does this deliver."
2. Look at the patterns above. If one names something close to your value, study its exemplar.
3. If none fit, your composition may be a new pattern. Author it — patterns earn their place by recurring, not by design.
4. Author `compositions/<your-demo>.yaml` declaring at minimum:
   - `schema_version: "1.0"`, `kind: workflow`, `name`, `description`, `intent`
   - `backend: headless-tmux` (until cycle-007 ships alternatives)
   - `inputs` with declared types
   - `chain` with at least one stage invoking your construct
   - `outputs` with destination paths
   - `compose_with`, `invocation_examples`, `when_to_use`, `known_limitations`
5. Run `compose-run <your-demo> --target ./test-canvas` (or `LOA_STAGE_MOCK=1` for cheap iteration).

CURATOR refuses to advance past stage 10 without a concrete demonstrated use *and* a clear statement of what the workflow provides. The composition doesn't need to be production-ready; it needs to be *runnable*, *grounded in your construct's actual capabilities*, and *honest about what it delivers*.

## References

- Doctrine: `bonfire-construct-pipe-doctrine` v6 §15.2 (workflow-kind composition)
- Runner: `loa-constructs/.claude/scripts/compose-run.sh`
- Stream types: Signal · Verdict · Artifact · Intent · Operator-Model (cycle-007 adds Question)
