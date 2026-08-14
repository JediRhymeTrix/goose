# From Goose to the GDK

## Core story

> **We built Goose in the open as a general-purpose agent. Today there are many complete coding agents, but far fewer reusable components for building new agent experiences. The Goose Development Kit is Goose unbundled: providers, agent capabilities, local inference, context management, and related infrastructure offered as composable Rust crates and cross-language bindings.**

---

## 0:00–0:40 — Slide 1: From Goose to the GDK

### On the slide

**From Goose to the GDK**

*Unbundling an open-source agent into reusable components*

```text
Goose, the agent
       ↓ unbundled
GDK, the building blocks
       ↓ embedded
Your product
```

### Talking points

- We built Goose in the open as an agent for coding and non-technical work.
- In doing that, we built more than an application: providers, an agent loop, tool integration, context management, compaction, and local inference.
- Now we are making those pieces available independently as the Goose Development Kit.

**Key line:**

> “The GDK is Goose unbundled.”

---

## 0:40–1:20 — Slide 2: Goose in brief

### On the slide

**An open-source, general-purpose agent**

```text
Models ←→ Goose ←→ Tools and systems
```

Small labels beneath the diagram:

**Coding · Research · Knowledge · Workflows**

### Talking points

- Goose was built in the open during the early development of modern agents.
- It was used for both coding and non-technical tasks.
- Early adoption of MCP allowed it to connect to tools and systems through an open protocol.
- Building and operating a real agent gave us working implementations of the infrastructure underneath the user experience.

**Transition:**

> “Since then, the number of complete agent applications has exploded. What still feels scarce are the components underneath them.”

---

## 1:20–2:15 — Slide 3: The missing layer

### On the slide

**There are many agents. Where are the agent building blocks?**

```text
Today                         What is missing

┌───────────────────┐         ┌───────────────────┐
│ Complete agent A  │         │ Agent capabilities│
├───────────────────┤         ├───────────────────┤
│ Complete agent B  │         │ Providers         │
├───────────────────┤         ├───────────────────┤
│ Complete agent C  │         │ Context management│
└───────────────────┘         ├───────────────────┤
                              │ Local inference   │
                              └───────────────────┘
```

### Talking points

- There are now many coding agents and agent applications.
- Most are delivered as complete products with a particular interface and workflow.
- If you want to build a different kind of experience, you often have to:
  - adopt an entire framework;
  - call another process or service;
  - or rebuild the low-level machinery yourself.
- We think the ecosystem needs reusable, embeddable components—not only more complete agent applications.

**Key line:**

> “The opportunity isn’t another agent UI. It’s making proven agent infrastructure available below the application layer.”

---

## 2:15–3:55 — Slide 4: The GDK is Goose unbundled

### On the slide

**Use the whole stack—or only the pieces you need**

```text
┌─────────────────────────────────────┐
│ goose-sdk                           │
│ Unified API + UniFFI bindings       │
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

The crates currently published through the `goose-sdk` release flow are:

- **`goose-local-inference`** — running models locally;
- **`goose-providers`** — model-provider implementations;
- **`goose-agent`** — agent execution and tool use;
- **`goose-context-management`** — context accounting, management, and compaction;
- **`goose-sdk`** — the unified entry point and cross-language surface.

Emphasize:

- These are separate Rust crates, not merely internal modules.
- Developers can choose a single capability or use the complete SDK.
- They can bring their own interface, tools, policies, storage, and product assumptions.
- These are implementations exercised by Goose, not a parallel rewrite of Goose’s behavior.

**Key line:**

> “You can reuse the hard parts without adopting the Goose application.”

---

## 3:55–4:55 — Slide 5: Rust core, multiple ecosystems

### On the slide

**Composable in Rust, embeddable elsewhere**

```text
             ┌─ Rust crates / crates.io
GDK core ────┼─ Python package / PyPI
   Rust      └─ Kotlin/JVM / Maven
                  via UniFFI
```

### Talking points

- The components are offered as Rust crates with explicit boundaries.
- Rust gives us a portable and efficient in-process core, particularly valuable for local inference and desktop or mobile software.
- UniFFI exposes the SDK to other language ecosystems without reimplementing the underlying agent behavior.
- The current packaging supports:
  - Rust through crates.io;
  - Python bindings and wheels;
  - Kotlin/JVM bindings and Maven artifacts.
- The goal is to let products embed agent capabilities instead of wrapping a command-line application or operating another service.

Avoid implying that every internal Goose API is already stable or exposed through UniFFI. Describe this as the current and growing GDK surface.

---

## 4:55–5:40 — Slide 6: Open boundaries

### On the slide

**Building blocks inside; open protocols outside**

```text
Tools and systems
       │
      MCP
       │
   GDK / Goose
       │
      ACP
       │
Clients and interfaces
```

### Talking points

- The crates provide composability inside an application.
- MCP provides an open boundary between an agent and its tools and sources of context.
- ACP provides an open boundary between an agent and its clients.
- These standards keep the GDK from becoming another closed, vertically integrated stack.

**Key line:**

> “The GDK provides reusable internals; MCP and ACP provide interoperable boundaries.”

---

## 5:40–8:25 — Demo: A local personal-wiki CLI

The demo should prove one claim:

> **A developer can build a purpose-specific agent experience from Goose components without adopting the Goose application.**

### Demo framing

**A small CLI built with the GDK**

```text
Personal wiki
     ↓ application-specific tools
GDK agent capabilities
     ↓
Local model
```

The wiki is located at `~/development/lifewiki`. Use a known-safe topic and avoid displaying private content.

### 1. Establish what it is — 20 seconds

Briefly show:

- the CLI command;
- the small dependency or integration surface;
- that it uses Goose’s agent capabilities and local inference.

Do not tour the source code in detail.

### 2. Run one synthesis task — 90 seconds

Choose a prompt that:

- searches several notes;
- produces a concise answer;
- cites the source files;
- reliably completes with the local model.

For example:

> “Find the notes related to **[safe project or topic]**, summarize the key decisions, and cite the files you used.”

The audience should see:

1. the agent deciding what to inspect;
2. tool calls over the wiki;
3. local model inference;
4. a synthesized, cited answer.

### 3. Explain the composition — 45 seconds

- The CLI owns the user experience.
- The wiki operations are application-specific tools.
- The GDK supplies the agent execution.
- Local inference runs the model on the device.
- Context management keeps the interaction within the model’s context window.
- The tool does not embed or invoke the Goose application.

**Key line:**

> “This is not a customized Goose client. It is a new application assembled from the same underlying components.”

### Optional second prompt — 20 seconds

Only if the first command is consistently fast:

> “Turn that summary into a short weekly update.”

Otherwise, stop after the successful first result.

### Demo safety

Prepare:

- a warmed-up model;
- cached model artifacts;
- a sanitized wiki subset or known-safe topic;
- a pre-generated result in another terminal tab;
- a backup recording;
- enlarged terminal text;
- no network dependency.

Prefer a small, reliable model and constrained output over a more ambitious demonstration.

---

## 8:25–9:15 — Slide 7: Goose’s role going forward

### On the slide

**Goose remains—but its components stand alone**

```text
                    ┌─ Reference client
GDK capabilities ───┤
                    └─ ACP server

Other products ─────── GDK capabilities
```

### Talking points

- We will continue to ship the Goose application.
- Its primary roles are:
  - a reference client demonstrating how the components fit together;
  - a real application that exercises the GDK end to end;
  - an ACP server that makes Goose capabilities available to compatible clients.
- Goose remains useful in its own right, but it is no longer the only way to consume its underlying capabilities.
- Improvements can flow both ways: Goose validates the components, and the components make new applications possible.

**Key line:**

> “Goose becomes one important client of the GDK, rather than the container you must adopt to access it.”

---

## 9:15–10:00 — Slide 8: Where we’re going

### On the slide

**The Goose Development Kit**

```text
Proven in Goose · Composable as crates · Open at the boundaries
```

> **Build your agent, not the agent stack underneath it.**

### Talking points

- Continue separating Goose capabilities into focused crates.
- Make those crates useful independently as well as through the unified SDK.
- Expand and refine the cross-language surface.
- Keep local, private, and embedded inference first-class.
- Preserve interoperability through MCP and ACP.
- Continue using Goose as a reference implementation and ACP server.

### Suggested closing script

> “We built Goose in the open as a general-purpose agent for both coding and non-technical work. Today, there are many complete coding agents. What we think is still missing are the lower-level pieces you need to build something different.
>
> “The GDK is Goose unbundled: providers, agent capabilities, context management, compaction, local inference, and the supporting infrastructure, available as composable Rust crates and through cross-language bindings.
>
> “We’ll continue to ship Goose as a reference client and an ACP server. But you won’t need to adopt the Goose application to reuse what we learned building it. The goal is simple: build your agent, not the agent stack underneath it.”

End with the repository URL or a QR code.

---

## Timing summary

| Segment | Time |
|---|---:|
| Thesis | 0:40 |
| Goose in brief | 0:40 |
| The missing layer | 0:55 |
| GDK architecture | 1:40 |
| Rust and UniFFI | 1:00 |
| MCP and ACP | 0:45 |
| Demo | 2:45 |
| Goose’s ongoing role | 0:50 |
| Direction and close | 0:45 |
| **Total** | **10:00** |

---

## Presentation guidance

- Keep Goose history to one slide and less than a minute.
- Make the ecosystem gap the setup for the GDK—not a long history of agent standards.
- Treat the crate list as evidence that the unbundling is concrete, not as the whole story.
- Define MCP and ACP in one sentence each.
- Say **“building blocks”** or **“components”** more often than **“framework.”**
- Make clear that developers can consume individual crates, the unified SDK, or cross-language bindings.
- Use the demo to prove that the components support a new application rather than a customized Goose interface.
- Rehearse to roughly **9:00** so local-inference variance does not push the talk over time.
