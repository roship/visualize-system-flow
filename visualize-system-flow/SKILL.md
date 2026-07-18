---
name: visualize-system-flow
description: Create animated, interactive system-flow visualizations for software architecture, event pipelines, message queues, batch processing, persistence paths, transactions, retries, ACK/reject behavior, and error handling. Use when the user asks to visualize how a system or algorithm works, especially in the established Rabbit-to-DB style with a dotted topology canvas, connected nodes and ports, moving messages, scenario controls, responsive layout, and downloadable standalone HTML.
---

# Visualize System Flow

Build an inspectable interactive explainer rather than a decorative architecture diagram. Preserve the visual language of the established Rabbit-to-DB visualization while adapting the topology and content to the actual system.

Use the `visualize` skill for its current HTML contract, theme tokens, accessibility rules, validation workflow, inline directive, and standalone rendering support. Read [references/style-guide.md](references/style-guide.md) before designing the flow.

## Workflow

1. Establish the source of truth.
   - Inspect relevant code, configuration, tests, documentation, traces, or recordings before drawing.
   - Derive components, order, transaction boundaries, batching, ownership, retries, and terminal states from evidence.
   - Do not invent queue sizes, timeouts, protocols, or database behavior. Mark an uncertain relationship as an inference or omit it.

2. Model the flow.
   - Identify the happy path from entry to terminal state.
   - Identify meaningful alternate paths such as parse failure, validation failure, rollback, retry, recursive split, reject, DLQ, or fallback.
   - Show where state becomes durable and only then show acknowledgement.
   - When deduplication or aggregation exists, show what survives and which original messages or identifiers it owns.

3. Design the interaction.
   - Default to one compact scenario control row, one live status sentence, and one dominant topology canvas.
   - Provide two to four scenario buttons only when they reveal materially different behavior.
   - Add a pause/resume control when motion loops.
   - Update edge emphasis, packet motion, labels, and the status sentence when the scenario changes; avoid fade-only switching.

4. Draw the topology.
   - Use a wide, shallow dotted canvas for desktop and a readable stacked layout for narrow screens.
   - Number the main stages.
   - Use rounded nodes with component name, key operation, and only decisive configuration values.
   - Use small ports, curved dashed connectors, directional arrows, and moving packet dots.
   - Keep normal, retry, and error meanings visually stable and pair color with labels or line styles.
   - Prefer a snake layout over shrinking text when the complete path does not fit in one row.

5. Implement and verify.
   - Create the interactive fragment through the `visualize` skill.
   - Use theme-aware variables only; support light and dark themes.
   - Honor `prefers-reduced-motion` and make every control keyboard accessible.
   - Support widths from 736 px down to 320 px without horizontal overflow or unreadable scaled text. Use a separate mobile composition when necessary.
   - Render a standalone HTML version, open it in a browser, inspect a screenshot, and exercise every scenario and pause/resume control.
   - Fix clipped labels, overlapping edges, inactive buttons, stale status text, and misleading visual emphasis before delivery.

6. Deliver both forms by default.
   - Show the interactive version inline using the exact directive required by the `visualize` skill.
   - Provide a clickable standalone `.html` file that preserves animation and controls across independent browser sessions.
   - If the user also requests PNG, GIF, or video, export it as an additional view and state that static/video formats do not preserve button interaction.

## Content Density

- Prefer operation names and short behavioral labels over prose.
- Put explanation outside the canvas unless the text is required to interpret a node or edge.
- Include concrete configuration values only when they explain behavior or performance.
- Avoid legends when paths are directly labeled.
- Do not add dashboards, KPI cards, search, filters, zoom controls, or decorative panels unless requested.

## Example Invocations

- `$visualize-system-flow Visualize the order lifecycle from Kafka through validation and payment to PostgreSQL, including retries and DLQ.`
- `$visualize-system-flow Show the current batch persistence algorithm from RabbitMQ to the database and contrast success with rollback and split.`
- `$visualize-system-flow Inspect this codebase and create an animated end-to-end request flow with timeout and circuit-breaker scenarios.`
