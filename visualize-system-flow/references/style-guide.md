# Animated system-flow style guide

Use this guide to reproduce the visual language of the Rabbit-to-DB reference without copying its domain content.

## Composition

- Place scenario buttons and pause/resume in one compact row above the canvas.
- Put one live status sentence immediately below the controls.
- Let the topology fill the available width on a transparent, unframed surface.
- Use a subtle dotted grid inside the diagram.
- Prefer a wide and shallow desktop composition. Use a snake path when the flow has more than four major stages.
- At narrow widths, switch to a separate vertical composition rather than scaling desktop labels until unreadable.

## Nodes

- Draw nodes as SVG marks with a theme-aware surface, subtle neutral border, and restrained corner radius.
- Show a small numbered circle for every happy-path stage.
- Use one concise title, one divider, and at most three short metadata lines.
- Add compact badges only for decisive values such as batch size, prefetch, timeout, transaction mode, or concurrency.
- Place small circular ports where edges enter or leave.
- Use a low-opacity category fill and a slightly stronger border only for the active scenario.

## Edges and motion

- Use thin curved dashed connectors with arrowheads.
- Animate dash offset to suggest continuous flow.
- Move small packet dots along active paths to make sequencing obvious.
- Stagger packet timing across consecutive edges so the system reads as a pipeline.
- Use one stable visual category for normal flow, one for retry/recovery, and one for failure/reject.
- Dim inactive alternate paths without removing the surrounding topology.
- Stop both dash and packet animation when paused.
- Hide looping packet motion and stop dash animation under `prefers-reduced-motion`.

## Interaction

- Default to the happy path.
- Use scenario labels that describe an event, for example `Successful batch`, `DB error + split`, or `Invalid JSON`.
- On scenario change, update all of the following when relevant:
  - active edge and node emphasis;
  - packet paths;
  - transaction or ACK labels;
  - one-line status text.
- Keep the complete topology visible so the user can compare behavior without losing orientation.

## Information hierarchy

- Stage title: component or boundary, such as `RabbitMQ`, `Batch listener`, `persistBatch`, or `PostgreSQL`.
- Metadata: decisive operation, such as `chooseBest`, `@Transactional`, `UPSERT if newer`, or `basicAck(tag, false)`.
- Edge label: transition or guarantee, such as `COMMIT`, `ROLLBACK`, `retry half`, or `reject`.
- Status sentence: summarize the selected scenario in one causal chain.

## Accuracy rules

- Make durability boundaries explicit.
- Never place ACK before the database operation that makes the corresponding state durable.
- Distinguish batch ACK from per-message ACK visually and textually.
- Show a transaction boundary around all operations that commit or roll back together.
- Show whether retries repeat deduplication or reuse previously selected representatives.
- For recursive split, show both outcomes: successful subsets commit and acknowledge; the reproducibly failing singleton rejects to DLQ.

## Quality check

- Read every label at 736 px and at 320 px.
- Confirm there is no horizontal scrolling.
- Click every scenario and verify status and labels change consistently.
- Pause and resume the animation.
- Inspect light and dark themes.
- Verify the standalone HTML works without network access unless an approved static dependency is intentionally required.
