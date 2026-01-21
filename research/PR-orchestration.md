# Managing AI-Driven PRs: The 10k Line Problem

This guide transforms chaotic "vibe coding" into a structured **Architectural Orchestration** workflow. By front-loading technical rigor, you reduce cognitive load on human reviewers and prevent the 10,000-line PR bottleneck.

---

## Phase 1: The Planning Layer (Alignment)

*Stop "vibe-ing" in the IDE; start defining the boundaries.*

- [ ] **GRASPS Meta-Prompting:** Define Goal, Role, Audience, Situation, Product, and Standards before generating code.
- [ ] **Constraint Setting:** Use the "Situation" and "Standards" sections of GRASPS to prevent "hallucinated scope" (e.g., unnecessary tech stack rewrites).
- [ ] **Recursive PRD Discovery:** Use an AI workflow to interrogate the team for clarifying questions before drafting requirements.
- [ ] **Define Non-functional Requirements:** Establish latency and security goals early so agents can use them to grade their own output.

---

## Phase 2: The Architectural Layer (Visualization)

*Make the architecture "diffable" so you can review logic instead of lines.*

- [ ] **C4 Diagrams-as-Code:** Generate Mermaid.js code for system architecture. Reviewing 20 lines of Mermaid is faster than reviewing 5,000 lines of Go.
- [ ] **Task Graphs (DAGs):** Map out execution logic with nodes (actions) and edges (logic) before prompting the agent.
- [ ] **Logic Flow Review:** Verify logic (e.g., "Do we auto-cancel VIPs?") at the graph level before code is written.

---

## Phase 3: The Coordination Layer (Inter-Agent Protocols)

*Prevent "vibe coders" from overwriting each other.*

- [ ] **File Reservations:** Implement "Advisory Leases" where agents must claim a file with a Time-to-Live (TTL) before editing.
- [ ] **Modular Workflows:** Force agents into sequential tasks to break massive changes into smaller, manageable units.
- [ ] **Shared Memory (MCP):** Use a shared-memory-mcp server to provide 100-token summaries instead of full project context, increasing token efficiency.
- [ ] **Context Deduplication:** Maintain a "reference by key" system for specific project sections to reduce the "coordination tax."

---

## Adoption Roadmap

| Week | Focus | Action Item |
|------|-------|-------------|
| Week 1 | Specs | Stop one-sentence prompts; adopt GRASPS |
| Week 2 | Visuals | Every feature branch must include a Mermaid C4 diagram |
| Week 3 | Agents | Deploy MCP-based file reservations to stop PR conflicts |
| Week 4 | Memory | Use Shared Memory (Byterover/Cipher) for team-wide context |
