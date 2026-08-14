# From Goose to the GDK

## Core story

> **Goose emerged during the first wave of open-source AI agents, with strong coding capabilities. Inside Block, it quickly became an “everything agent” used by technical and non-technical people alike. Early adoption of MCP connected it to Block’s internal systems. Now we’re extracting the infrastructure behind that experience into the Goose Development Kit: composable agent building blocks developers can embed in their own products.**

A useful line to repeat throughout the talk:

> **Goose proved that a general-purpose agent becomes valuable through connections; the GDK makes the machinery behind that agent reusable.**

Aim for six slides plus the demo. Keep the history brief and spend most of the time on the transition from application to SDK.

---

## 0:00–0:45 — Slide 1: From Goose to the GDK

### On the slide

**From an “everything agent” to agent building blocks**

*Unbundling Goose into a reusable development kit*

```text
Goose, the application
          ↓
GDK, the building blocks
          ↓
Your agents and products
```

### Talking points

- Goose emerged during the first wave of open-source AI agents.
- Coding was an important early use case, but Goose did not remain narrowly a coding agent.
- Inside Block, people began applying it to many kinds of work.
- That experience showed us that the valuable core wasn’t a particular interface or use case—it was a reusable set of agent capabilities.

**Transition:**

> “Goose started with a strong technical audience, but what happened next changed how we thought about the project.”

---

## 0:45–1:45 — Slide 2: Goose became an “everything agent”

### On the slide

**Inside Block, Goose expanded beyond code**

```text
                  ┌─ Engineering
                  ├─ Knowledge discovery
Goose + MCP ──────┼─ Internal workflows
                  ├─ Data and operations
                  └─ Everyday questions
```

Consider using anonymized examples of internal systems or workflows if permitted.

### Talking points

- Goose quickly spread beyond engineers and coding tasks.
- Many users were non-technical.
- They were not asking for a general-purpose coding environment. They wanted an agent that could help them do their actual work.
- Early adoption of MCP let Goose connect to Block’s internal tools, data, and systems.
- That transformed Goose from an application with built-in abilities into an interface over a growing ecosystem of organizational capabilities.

**Key line:**

> “The agent loop gave Goose intelligence; MCP gave it reach.”

---

## 1:45–2:45 — Slide 3: MCP enabled breadth; ACP enables choice

### On the slide

**Open standards create interchangeable parts**

```text
Tools and systems
       │
      MCP
       │
     Agent
       │
      ACP
       │
Clients and interfaces
```

### Talking points

- **MCP** lets an agent discover and use tools and sources of context.
- At Block, that meant Goose could connect to internal systems without every integration becoming bespoke agent code.
- Once those capabilities were available, technical and non-technical users found their own use cases.
- **ACP** applies the same interoperability principle to the other side: communication between an agent and its clients.
- Together, they create clean seams around the agent:
  - MCP between agents and capabilities;
  - ACP between agents and user experiences.

**Key lines:**

> “MCP helped Goose become an everything agent. ACP helps that agent appear in more than one application.”

> “Open standards unbundle the ecosystem around Goose. The GDK unbundles the machinery within Goose.”

---

## 2:45–4:15 — Slide 4: The GDK architecture

### On the slide

**One application revealed a general-purpose stack**

```text
┌─────────────────────────────────────┐
│ goose-sdk                           │
│ Rust API + UniFFI language bindings │
├─────────────────────────────────────┤
│ goose-agent                         │
│ Agent execution and tool use        │
├──────────────────┬──────────────────┤
│ goose-providers  │ goose-context-   │
│                  │ management       │
├──────────────────┼──────────────────┤
│ goose-local-     │ goose-download-  │
│ inference        │ manager          │
├─────────────────────────────────────┤
│ goose-sdk-types · goose-provider-   │
│ types                               │
└─────────────────────────────────────┘
```

### Talking points

Supporting many users and workflows exposed a common set of difficult problems:

- working across model providers;
- reliably executing tool-use loops;
- managing long and growing contexts;
- compacting conversations without losing important state;
- supporting cloud and local inference;
- connecting through open protocols.

None of these problems belongs exclusively to coding. Until now, much of the implementation lived inside the Goose application.

The crates currently published through the `goose-sdk` release flow are:

- **`goose-provider-types`** — shared provider interfaces and data types;
- **`goose-sdk-types`** — shared SDK-facing types;
- **`goose-download-manager`** — model and artifact downloading;
- **`goose-local-inference`** — running models locally;
- **`goose-providers`** — model-provider implementations;
- **`goose-agent`** — agent behavior and execution;
- **`goose-context-management`** — context accounting, compaction, and management;
- **`goose-sdk`** — the unified entry point and cross-language surface.

Emphasize:

- These are separate Rust crates, not merely modules hidden inside Goose.
- A developer can adopt one layer or use the higher-level SDK.
- The application becomes one consumer of the same capabilities available to others.

**Key lines:**

> “Goose proved the stack in a real organization. The GDK makes that stack available without requiring the Goose application.”

> “We’re not asking everyone to build another Goose. We’re making it possible to build something that Goose’s monolith was never designed to be.”

---

## 4:15–5:15 — Slide 5: Rust core, language-native access

### On the slide

**One Rust implementation, multiple ecosystems**

```text
             ┌─ Rust crates / crates.io
GDK core ────┼─ Python package / PyPI
   Rust      └─ Kotlin/JVM / Maven
                  via UniFFI
```

### Talking points

- Rust gives us a portable, efficient core and strong interfaces between components.
- **UniFFI** exposes that implementation to other languages without reimplementing agent behavior.
- The current packaging supports:
  - native Rust crates;
  - Python bindings and wheels;
  - Kotlin/JVM bindings and Maven artifacts.
- This matters especially for:
  - desktop and mobile applications;
  - local inference;
  - products that need in-process agent capabilities;
  - teams whose application code is not written in Rust.

Say “the current surface supports” rather than implying every internal Goose API is already stable and exposed.

---

## 5:15–5:45 — Slide 6: What this enables

### On the slide

**Agents should be a capability, not a destination**

- an IDE feature;
- a personal knowledge assistant;
- an enterprise workflow;
- a mobile app;
- an embedded or offline tool;
- a specialized agent with a custom interface.

> **Choose the provider. Choose the tools. Choose where inference runs.**

### Talking points

- Not every agent should look like a coding assistant or chat application.
- With reusable pieces, developers can own the product experience while reusing the difficult infrastructure.
- Local inference makes privacy, offline operation, predictable cost, and low-latency workflows possible.

**Transition to demo:**

> “Inside Block, MCP allowed people to bring their organizational context and systems to Goose. For this demo, I’ll show the smaller, personal version of that idea: a CLI that combines Goose’s agent loop and local inference with my own wiki.”

---

## 5:45–8:45 — Demo: A local personal-wiki agent

The demo should prove one clear claim:

> **Goose’s agent loop and local inference are reusable outside Goose and outside coding.**

### Setup slide or terminal title

**A small CLI built with the GDK**

```text
Personal wiki
     ↓ tools
GDK agent loop
     ↓
Local model
```

The wiki is located at `~/development/lifewiki`, but avoid lingering on private content.

### 1. Show the tool’s shape — 20 seconds

Briefly display:

- the CLI command;
- the small amount of integration code or its dependencies;
- that it uses `goose-agent` and `goose-local-inference`.

Do not tour the source in detail.

### 2. Ask a question requiring synthesis — 90 seconds

Choose a prompt that:

- requires searching several notes;
- has a concise answer;
- does not expose sensitive information;
- reliably completes with the local model.

For example:

> “Find the notes related to **[safe project or topic]**, summarize the key decisions, and cite the files you used.”

The audience should see:

1. the agent deciding what to inspect;
2. tool calls over the wiki;
3. local model inference;
4. a synthesized, cited answer.

### 3. Explain what happened — 40 seconds

- The CLI owns the experience.
- The filesystem and wiki operations are the application-specific tools.
- `goose-agent` handles the tool-use loop.
- `goose-local-inference` runs the model.
- Context management keeps the interaction within the available context window.
- No Goose desktop or CLI application was required.

**Key line:**

> “This isn’t a coding workflow, and it isn’t the Goose application. It is a purpose-built experience composed from the same underlying machinery.”

### 4. Optional second command — 30 seconds

Only if the first command is consistently fast:

> “Turn that summary into a short weekly update.”

This demonstrates reuse of gathered context. Otherwise, stop after the successful first result.

### Demo safety

Have all of these ready:

- a warmed-up model;
- a sanitized wiki subset or known-safe topic;
- a pre-run backup recording;
- cached model artifacts;
- a pre-generated result in another terminal tab;
- enlarged terminal text;
- no network dependency.

A local-inference demo may spend most of its allotted time producing tokens. Prefer a small, reliable model and a constrained answer over an ambitious task.

---

## 8:45–9:35 — Final slide: Where we’re going

### On the slide

**The Goose Development Kit**

```text
Open protocols   Composable crates   Cross-language APIs
      MCP/ACP          Rust             UniFFI
```

> **Build an agent, not an agent stack.**

### Talking points

- Continue separating proven Goose capabilities into focused crates.
- Make the boundaries stable and useful independently.
- Expand and refine the cross-language surface.
- Preserve interoperability through MCP and ACP.
- Make local, private, embedded agents first-class—not an afterthought.
- Let Goose continue to be both a product and the integration test for the kit.

Avoid giving a rigid roadmap unless dates and commitments are settled.

---

## 9:35–10:00 — Close

### Suggested closing script

> “Goose emerged during the first wave of open-source agents, with coding as an important early capability. But inside Block, it quickly became something broader: an ‘everything agent’ used by technical and non-technical people. Early adoption of MCP let Goose connect to the systems where their work actually happened.
>
> “That taught us that the lasting value wasn’t one application or one category of task. It was the underlying stack: providers, agent execution, tools, context management, compaction, and local inference.
>
> “MCP and ACP provide open boundaries around that stack. The GDK turns what is inside Goose into reusable Rust crates and cross-language APIs. The goal is to let developers build the agent their users need—without rebuilding all of the infrastructure that made Goose useful.”

End with the repository URL or a QR code.

---

## Timing summary

| Segment | Time |
|---|---:|
| Thesis | 0:45 |
| Goose inside Block | 1:00 |
| MCP and ACP | 1:00 |
| GDK architecture | 1:30 |
| UniFFI and distribution | 1:00 |
| What it enables | 0:30 |
| Demo | 3:00 |
| Direction and close | 1:15 |
| **Total** | **10:00** |

---

## Presentation guidance

- Use **one diagram per concept**, not crate names on every slide.
- Treat the crate list as evidence that unbundling is real, not as the main story.
- Keep the history to two or three points; the audience needs more time to understand the GDK.
- Define MCP and ACP in one sentence each.
- Say **“building blocks”** more often than **“framework.”**
- Make the demo domain clearly non-coding; that is what proves the thesis.
- Rehearse to **8:45–9:00** so live inference variance does not push the talk over time.
