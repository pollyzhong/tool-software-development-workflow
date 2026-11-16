---
name: tool-software-development-workflow
description: Plan and deliver cost-conscious tool software through requirements consolidation, platform and stack selection, data-model-first architecture, low-fidelity UI and interaction design, confirmation gates, batch implementation, testing, documentation, and deployment handoff. Use when creating, rebuilding, extending, or refactoring a web, desktop, mobile, 2D/3D, productivity, editor, or utility application; when requirements are arriving iteratively; or when reducing development time, rework, and token usage matters.
---

# Tool Software Development Workflow

Build tools in controlled batches. Optimize for a maintainable product, not the fastest first screenshot.

## Core Contract

1. Obey repository instructions such as `AGENTS.md` before this workflow.
2. Separate discussion from execution. Do not modify state while the user is exploring ideas.
3. Before any state-changing work, present the understood goal, proposed approach, affected files or services, important decisions, and validation plan. Wait for explicit confirmation.
4. Treat writing or running tests, building, previewing, deployment, installation, account creation, payment, and external publishing as separate approvals. Authorization to implement is not authorization to verify or release.
5. Keep new ideas out of an active implementation batch unless the user approves the revised scope. When asked for a text-only answer, do not record tasks or perform operations in that turn.

## Select The Work Mode

- **Question or brainstorming**: answer directly; do not create files.
- **New product**: run discovery, architecture, low-fidelity interaction design, and milestone planning before scaffolding.
- **Existing product**: inspect instructions, repository shape, current data model, tests, and dirty state before proposing changes.
- **Feature batch**: consolidate related requests into one bounded batch with acceptance criteria.
- **Bug fix**: reproduce first, identify the smallest ownership boundary, then propose a scoped fix.
- **Prototype rescue**: audit coupling, file size, state ownership, and missing tests before adding more features.

## Step 1: Consolidate The Product

Ask only high-impact questions that cannot be answered from the repository or prior context. Prefer one compact round over repeated interruptions.

Capture target users, required platforms, the smallest complete workflow, feature priorities, persisted/shared data, constraints, and explicit non-goals.
For a new product or a change to the foundation, actively ask the missing questions that would change the MVP or architecture:

1. Who will use it, and on which devices or platform must it run?
2. What is the one complete task the first usable version must let them finish?
3. What must not break or be lost, and which known future needs could affect today's design (for example, old saves, offline use, or sharing across devices)?

Use product language, not a questionnaire about libraries. Skip questions already answered; a small bug fix does not restart product intake.

Use [project-intake.md](references/project-intake.md) when the request is broad or ambiguous.

## Step 2: Choose The Cheapest Suitable Platform

Choose from product constraints, not novelty.
When a high-risk assumption could change the stack or architecture, propose the smallest check or disposable prototype that answers it before locking the choice. Get approval before building or running it; a prototype is not the production MVP.

- Prefer a browser-first stack for instant access, phone/tablet/desktop support, links, forms, uploads, collaboration, or simple deployment.
- Prefer Godot when native real-time 2D/3D interaction is the product core and installation is acceptable.
- Prefer Tauri when desktop OS integration, local files, small binaries, and a web-based UI are central.
- Prefer a native mobile stack when sensors, app-store distribution, background services, or platform-specific interaction dominate.
- Prefer an existing domain engine for established physics, parsing, layout, CAD, maps, charts, rich text, or 3D transform controls.

Record the decision and rejected alternatives. Read [architecture-template.md](references/architecture-template.md) before locking the stack.

## Step 3: Design Data Before Screens

Define one source of truth before implementing multiple views.

Specify stable IDs, schema version, domain ownership, canonical units, coordinates, derived values, constraints, migrations, undo boundaries, serialization, autosave, and sharing.

Do not let each view maintain a competing model. Do not make geometry, validation, or persistence depend on rendered DOM or canvas nodes.
Use compatible rules for saving and reopening the same data. Separate source values, edit rules, persistence, and rendering so additions can stay within one module. Do not scaffold speculative infrastructure or extension systems.

Give the user three concrete lists before implementation:

- **Decide now:** Hard-to-reverse contracts and the risks to check first, such as platform, the shared data model, units, identities, and compatibility with existing data.
- **MVP:** One useful journey through the real layers, including the save/reopen path when data is persisted. State what the user can do to accept it.
- **Add later:** Features that can extend a catalog or view without redefining saved data or edit rules. Flag proposed changes to those contracts as separate design and migration work, not routine feature additions.

For a 2D/3D editor, one room, a door, and one piece of furniture are enough to establish editing, shared 3D updates, and reopening. More assets and toolbar layouts can follow; the two views must already agree on what a dimension means.

## Step 4: Define Low-Fidelity UI And Interaction

Before coding, define the interface structure and interaction contract without polishing the visual style.

Capture:

- core screens, information hierarchy, and navigation;
- desktop, tablet, and mobile layout priorities;
- object selection, dragging, resizing, rotating, panning, zooming, and multi-select behavior;
- panel open, close, collapse, and focus behavior;
- destructive-action safeguards and undo expectations;
- empty, loading, invalid, failure, and read-only states;
- gesture ownership and conflicts, such as dragging an object versus panning a canvas, tapping versus opening an inspector, and pinching versus selecting.

Accept annotated screenshots, paper sketches, Photoshop or Illustrator compositions, Figma mockups, or plain wireframes. For a Photoshop or Illustrator handoff, request full-screen compositions, reusable component states, exported assets, fonts and colors, plus short interaction notes. A sprite sheet or isolated UI asset board does not define responsive composition or behavior by itself.

Freeze navigation, panel placement, responsive priorities, selection behavior, and core gestures before implementation. Present the low-fidelity flow for confirmation when interaction is central to the product.

Defer final colors, textures, icon polish, animation, illustration, and branding until the functional vertical slice works on target devices. Implement responsive structure and live text in code; use bitmap or vector assets only for visual elements that need them.

## Step 5: Establish Product Memory

For non-trivial projects, propose these files and create them only after confirmation:

- `PRODUCT.md`: users, workflows, scope, non-goals, and release boundaries;
- `ARCHITECTURE.md`: stack, data model, ownership, invariants, and decisions;
- `BACKLOG.md`: prioritized ideas and deferred requests;
- `ACCEPTANCE.md`: observable completion criteria and test matrix.

Adapt to existing repository conventions instead of creating duplicate documents. Use the templates in `references/` only when equivalent documents do not exist.

## Step 6: Present One Implementation Batch

Use two distinct confirmations. Discussed or logged items are pending, not approved. First ask which items to include ("确认把这些加入本批吗？"). An affirmative answer to inclusion does not authorize editing. Historical and deferred items do not join silently.

Before asking whether to start, show the complete batch, including confirmed items still unimplemented in it, not just the latest request. State:

1. what the batch will achieve and exclude;
2. data-model or API changes;
3. files and services expected to change;
4. risks and decisions that need the user;
5. acceptance criteria;
6. verification and deployment boundaries.

Ask explicitly whether to start that whole list. "确认", "可以", or "改吧" in direct response authorizes all listed items, unless the user narrows it. The user can explicitly approve inclusion and start together for a clear list. Acknowledgment of an explanation is neither approval. Freeze the started list; route additions to a later batch unless the user approves the revised list.

## Step 7: Implement A Vertical Slice

After confirmation:

1. Inspect existing patterns before editing.
2. Keep domain logic, rendering, UI state, persistence, and integrations in separate modules.
3. Use mature libraries for complex domain behavior instead of recreating them.
4. Implement the smallest end-to-end slice that produces user value.
5. Add, update, or run tests only within the separately authorized verification scope.
6. Preserve unrelated user changes and avoid opportunistic refactors.
7. Update project memory with decisions and newly discovered backlog items.

Prefer several cohesive modules over a single growing application file. Introduce abstractions only when they remove real coupling or match an existing pattern.

## Step 8: Verify At The Right Depth

Propose verification proportional to risk. Run only checks the user has authorized. When the user owns acceptance, give concise manual acceptance steps instead of compiling, launching, or testing on their behalf. Authorized verification may include:

- run syntax, type, lint, and unit checks for changed logic;
- exercise the complete affected workflow;
- verify persistence, reload, undo/redo, and serialization when state changes;
- test desktop, tablet, and mobile when the product targets them;
- inspect rendered screenshots when layout, canvas, 3D, or responsive behavior changes;
- check empty, loading, invalid, failure, and read-only states;
- confirm external assets and shared links in the deployment environment.

Use [acceptance-template.md](references/acceptance-template.md) to turn vague requests into observable checks.

## Step 9: Close The Batch

Report what changed, important code locations, tests and outcomes, limitations, deferred work, and whether changes are local, committed, pushed, previewed, or deployed.
Reconcile every item against the approved batch and report what is done, still waiting for user acceptance, or unfinished and why. Do not drop an item from the report or describe the whole batch as done while one remains unfinished.

Do not silently deploy or publish. Ask for the next required confirmation when external state will change.

## Token And Time Discipline

- Read project memory before replaying long conversation history.
- Consolidate related requests and search/read files in batches.
- Avoid regenerating unchanged plans and repeated explanations.
- Keep the active batch small enough to test completely.
- Freeze interaction structure before investing in visual polish; defer branding and decorative assets until the functional slice is stable.
- Record decisions once, then link to them.
- Move optional ideas to `BACKLOG.md` instead of interrupting implementation.
- Stop expanding a prototype when architecture work is cheaper than another patch.

Use [product-template.md](references/product-template.md), [backlog-template.md](references/backlog-template.md), and [acceptance-template.md](references/acceptance-template.md) only as needed.
