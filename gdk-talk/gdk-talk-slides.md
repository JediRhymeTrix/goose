---
marp: true
theme: default
paginate: true
size: 16:9
header: "**goose development kit**"
footer: "github.com/aaif-goose/goose"
style: |
  :root {
    --pink: #ff00ff;
    --blue: #0000ff;
    --dark-blue: #100f51;
    --white: #ffffff;
    --ink: var(--dark-blue);
    --paper: var(--white);
    --accent: var(--pink);
    --secondary: var(--blue);
    --muted: #55548a;
  }
  section {
    background: var(--paper);
    color: var(--ink);
    font-family: Inter, Avenir Next, Avenir, Helvetica, Arial, sans-serif;
    font-size: 30px;
    padding: 68px 78px;
  }
  h1 {
    font-size: 60px;
    line-height: 1.06;
    letter-spacing: -2px;
    margin: 0 0 0;
  }
  h2 {
    font-size: 42px;
    letter-spacing: -1px;
  }
  strong { color: var(--blue); }
  code {
    background: #f2f2ff;
    color: var(--ink);
  }
  pre {
    background: var(--ink);
    border-left: 10px solid var(--accent);
    border-radius: 8px;
    color: white;
    font-size: 22px;
    padding: 22px 28px;
  }
  blockquote {
    border-left: 8px solid var(--accent);
    color: var(--ink);
    font-size: 34px;
    font-weight: 650;
    margin: 28px 0;
    padding: 8px 0 8px 28px;
  }
  header, footer {
    color: var(--muted);
    font-size: 15px;
  }
  section::after {
    color: var(--muted);
    font-size: 15px;
  }
  section.title {
    background: var(--ink);
    color: white;
  }
  section.title h1 {
    color: white;
    font-size: 72px;
  }
  section.title strong { color: var(--accent); }
  section.title header, section.title footer, section.title::after {
    display: none;
  }
  section.demo {
    background: var(--accent);
  }
  section.demo h1, section.demo strong { color: var(--dark-blue); }
  .demo-video {
    background: var(--dark-blue);
    border-radius: 10px;
    display: block;
    margin: 24px auto 0;
    max-height: 500px;
    width: 88%;
  }
  .eyebrow {
    color: var(--accent);
    font-size: 22px;
    font-weight: 750;
    letter-spacing: 2px;
    text-transform: uppercase;
  }
  .subtitle {
    color: #d9d9ff;
    font-size: 32px;
    max-width: 830px;
  }
  .small { color: var(--muted); font-size: 20px; }
  .center { text-align: center; }
  .columns {
    display: grid;
    gap: 30px;
    grid-template-columns: 1fr 1fr;
  }
  .three-columns {
    display: grid;
    gap: 22px;
    grid-template-columns: repeat(3, 1fr);
  }
  .card {
    background: white;
    border: 2px solid #d9d9ff;
    border-radius: 14px;
    padding: 22px 25px;
    margin-bottom: 4px;
  }
  .card h2, .card h3 { margin-top: 0; }
  .pink-card {
    background: var(--accent);
    border-color: var(--accent);
    color: var(--dark-blue);
  }
  .pink-card strong { color: var(--dark-blue); }
  .blue-card {
    background: var(--secondary);
    border-color: var(--secondary);
    color: var(--white);
  }
  .blue-card .small, .blue-card strong { color: var(--white); }
  .stack {
    display: grid;
    gap: 9px;
    margin: 20px auto 0;
    max-width: 940px;
  }
  .layer {
    background: white;
    border: 2px solid #d9d9ff;
    border-radius: 10px;
    font-size: 23px;
    padding: 12px 22px;
  }
  .layer.primary {
    background: var(--accent);
    border-color: var(--accent);
  }
  .flow {
    align-items: center;
    display: flex;
    gap: 18px;
    justify-content: center;
    margin-top: 55px;
  }
  .node {
    background: white;
    border: 2px solid #d9d9ff;
    border-radius: 14px;
    font-size: 27px;
    font-weight: 700;
    min-width: 195px;
    padding: 25px 18px;
    text-align: center;
  }
  .node.primary {
    background: var(--accent);
    border-color: var(--accent);
  }
  .compact-flow {
    gap: 14px;
    margin-top: 20px;
  }
  .compact-flow .node {
    padding: 11px 18px;
  }
  .compact-flow > div:last-child .node + .node {
    margin-top: 8px;
  }
  .compact-caption {
    margin-top: 10px;
  }
  .arrow {
    color: var(--blue);
    font-size: 46px;
    font-weight: 800;
  }
  .tag {
    background: #eeeeff;
    border-radius: 999px;
    display: inline-block;
    font-size: 20px;
    margin: 5px;
    padding: 7px 15px;
  }
---

<!-- _class: title -->

<div class="eyebrow">The goose development kit</div>

# From **goose** to the **GDK**

<div class="subtitle">Unbundling an open-source agent into reusable components</div>



<!--
Intro to:
 - me
 - goose
 - this talk
-->

---

# We built an agent in the open

<div class="flow" style="margin-top:22px; transform:scale(.8)">
  <div class="node">Models</div>
  <div class="arrow">↔</div>
  <div class="node primary">goose</div>
  <div class="arrow">↔</div>
  <div class="node">Tools & systems</div>
</div>

<div class="columns" style="margin-top:12px">
  <div>
    <ul>
      <li>Used across Block</li>
      <li>Forked by several large companies</li>
      <li>Donated to the Agentic AI Foundation</li>
    </ul>
  </div>
</div>

---

# Many agents. A missing layer.

<div class="columns">
  <div class="card">
    <h2>What we have</h2>
    <p>Complete coding agents</p>
    <p>Opinionated interfaces</p>
    <p>Vertically integrated stacks</p>
  </div>
  <div class="card pink-card">
    <h2>What builders need</h2>
    <p>Agent capabilities</p>
    <p>Embeddable local inference</p>
    <p>Open standards support</p>
  </div>
</div>

> The opportunity is below the application layer.

---

# The GDK is **goose unbundled**

<div class="stack">
  <div class="layer primary"><strong>goose-sdk</strong> · unified API + UniFFI bindings</div>
  <div class="layer"><strong>goose-agent</strong> · execution and tool use</div>
  <div class="columns" style="gap:9px">
    <div class="layer"><strong>goose-providers</strong></div>
    <div class="layer"><strong>goose-context-management</strong></div>
  </div>
  <div class="layer"><strong>goose-local-inference</strong> · local model execution</div>
  <div class="layer"><strong>goose-sdk-types</strong> · shared SDK types</div>
</div>

---

# Composable in Rust. Embeddable elsewhere.

<div class="flow compact-flow">
  <div class="node primary">GDK core<br><span class="small">Rust</span></div>
  <div class="arrow">→</div>
  <div>
    <div class="node">Rust crates<br><span class="small">crates.io</span></div>
    <div class="node">Python<br><span class="small">PyPI</span></div>
    <div class="node">Kotlin/JVM<br><span class="small">Maven</span></div>
  </div>
</div>

<div class="center small compact-caption">Cross-language bindings generated with <strong>UniFFI</strong></div>

---

# Building on open protocols

<div><br></div>

<div class="columns" style="margin-top:38px">
  <div class="card"><strong>MCP</strong>
      <br>
      <span class="small">Agent ↔ capabilities</span>
  </div>
  <div class="card"><strong>ACP</strong>
      <br>
      <span class="small">Client ↔ agent</span>
  </div>
</div>

<div class="columns" style="margin-top:38px">
  <div class="card"><strong>Agents.md</strong>
      <br>
      <span class="small"></span>
  </div>
  <div class="card"><strong>Skills</strong>
      <br>
      <span class="small"></span>
  </div>
</div>

---

<!-- _class: demo -->

# Demo: a local personal-wiki agent

<video class="demo-video" src="./assets/demo.mov" controls playsinline preload="metadata"></video>

---

# goose remains—and its components stand alone

<div class="columns">
  <div class="card pink-card">
    <h2>goose app</h2>
    <p>Reference client</p>
    <p>Power tool</p>
    <p>ACP server</p>
  </div>
  <div class="card">
    <h2>Your product</h2>
    <p>Your interface</p>
    <p>Your tools & policies</p>
    <p>GDK components</p>
  </div>
</div>

> goose is one important client of the GDK—not the container required to access it.


---

<!-- _class: title -->

<div class="eyebrow">The goose development kit</div>

# Build your agent—not the stack underneath it.

<div class="three-columns" style="margin-top:55px; color:#100f51">
  <div class="card pink-card"><strong style="color:#100f51">Proven</strong><br></div>
  <div class="card blue-card"><strong style="color:#100f51">Composable</strong><br></div>
  <div class="card"><strong>Open</strong><br></div>
</div>

<div class="center" style="margin-top:65px; color:#b9b9e8">github.com/aaif-goose/goose</div>
