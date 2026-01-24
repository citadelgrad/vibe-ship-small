# Architecture Tools Reference

This guide covers alternative architecture documentation tools beyond the core concepts covered in [Visuals & Diagrams](./visuals-and-diagrams.md). These tools are for teams wanting to go deeper with diagrams-as-code, architecture decision records, and AI-powered diagram generation.

## Quick Reference

### High Priority Tools

| Tool | What It Does | Best For |
|------|--------------|----------|
| **LikeC4** | Modern C4 tooling with MCP server for AI agents | AI-assisted workflows |
| **D2** | Clean declarative diagramming language | Architecture diagrams |
| **Diagrams (Python)** | Programmatic cloud infrastructure diagrams | AWS/Azure/GCP/K8s |
| **ADR Tools + Log4brains** | Architecture Decision Records management | Documenting the "why" |
| **arc42** | 12-section documentation template | Comprehensive docs |
| **Eraser/Swark** | AI-powered diagram generation | Natural language to diagrams |

### Tools by C4 Level

| Level | Best Tools |
|-------|------------|
| Context | Mermaid, IcePanel, Structurizr |
| Container | D2, Diagrams (Python), Structurizr |
| Component | PlantUML, LikeC4 |
| Code | Auto-generate from source |

### Diagramming Tools Comparison Matrix

| Tool | Best For | C4 Support | Version Control | AI Friendly | Learning Curve |
|------|----------|------------|-----------------|-------------|----------------|
| Mermaid | GitHub/docs | Native | Excellent | High | Low |
| PlantUML | Complex UML | Via macros | Excellent | Medium | Medium |
| D2 | Architecture | Manual | Excellent | High | Low |
| Diagrams (Python) | Cloud infra | Manual | Excellent | Medium | Low |
| Structurizr DSL | Full C4 | Native | Excellent | Medium | Medium |
| LikeC4 | Modern C4 | Native | Excellent | High | Medium |
| IcePanel | Collaboration | Native | Limited | Low | Low |

---

## Detailed Tool Guides

### LikeC4

**What it does:** Modern toolchain for creating C4 architecture diagrams with TypeScript DSL and VSCode extension. Includes an MCP (Model Context Protocol) server for AI agent integration.

**Best for:** Teams working with AI coding assistants who want real-time architecture diagram updates as code evolves.

**C4 Levels:** Context, Container, Component

**Pros:**
- Native MCP server enables AI agents to query and update architecture diagrams
- TypeScript-based DSL with full IDE support (autocomplete, type checking)
- Live preview in VSCode
- Exports to multiple formats (PNG, SVG, JSON)
- Reactive - diagrams update automatically as DSL changes

**Cons:**
- Newer tool with smaller community than Structurizr
- Requires Node.js/TypeScript setup
- Learning curve for the DSL syntax

**Links:**
- Official site: https://likec4.dev/
- GitHub: https://github.com/likec4/likec4
- MCP Server: https://github.com/likec4/likec4/tree/main/packages/mcp-server

**Example:**
```typescript
specification {
  element system
  element container
  element component
}

model {
  customer = person 'Customer'

  system ecommerce 'E-commerce Platform' {
    container webapp 'Web App' {
      component orderCtrl 'Order Controller'
      component paymentSvc 'Payment Service'
    }
    container api 'API Service'
    container db 'Database'
  }

  customer -> webapp
  webapp -> api
  api -> db
}
```

**Installation:**
```bash
npm install -D @likec4/core @likec4/vscode
```

---

### D2 (Declarative Diagramming)

**What it does:** Modern alternative to Mermaid with clean syntax for creating technical diagrams. Focuses on readability and simplicity.

**Best for:** Architecture diagrams, system designs, and any technical documentation where you want human-readable source files.

**C4 Levels:** Container, Component (requires manual labeling for C4 methodology)

**Pros:**
- Extremely clean, minimal syntax
- Beautiful default styling
- Fast rendering
- Excellent for version control (diffs are readable)
- Supports themes and custom styling
- Multiple output formats (SVG, PNG, PDF)

**Cons:**
- No native C4 support (requires manual conventions)
- Smaller ecosystem than Mermaid
- Limited interactive features

**Links:**
- Official site: https://d2lang.com/
- Playground: https://play.d2lang.com/
- GitHub: https://github.com/terrastruct/d2

**Example:**
```d2
# Container Diagram
title: E-commerce Platform {
  shape: text
  near: top-center
}

customer: Customer {
  shape: person
}

platform: E-commerce Platform {
  web: Web App {
    shape: rectangle
  }
  api: API Service {
    shape: rectangle
  }
  db: Database {
    shape: cylinder
  }
}

customer -> platform.web: Uses HTTPS
platform.web -> platform.api: API calls
platform.api -> platform.db: SQL queries
```

**Installation:**
```bash
curl -fsSL https://d2lang.com/install.sh | sh -s --
```

---

### Diagrams (Python)

**What it does:** Python library for creating cloud infrastructure diagrams programmatically. Includes icons for AWS, Azure, GCP, Kubernetes, and more.

**Best for:** Documenting cloud architecture, infrastructure as code, DevOps workflows.

**C4 Levels:** Container level (shows infrastructure components)

**Pros:**
- Code-based (no manual drawing)
- Official provider icons (AWS, Azure, GCP, etc.)
- Great for auto-generating diagrams from infrastructure code
- Python integration enables dynamic diagrams
- Version control friendly

**Cons:**
- Requires Python environment
- Limited customization of visual appearance
- Not suitable for detailed component-level diagrams
- Layout can be tricky for complex architectures

**Links:**
- Official site: https://diagrams.mingrammer.com/
- GitHub: https://github.com/mingrammer/diagrams
- Icon reference: https://diagrams.mingrammer.com/docs/nodes/aws

**Example:**
```python
from diagrams import Diagram, Cluster
from diagrams.aws.compute import ECS
from diagrams.aws.database import RDS
from diagrams.aws.network import ELB

with Diagram("E-commerce Platform", show=False):
    lb = ELB("Load Balancer")

    with Cluster("ECS Cluster"):
        web = ECS("Web App")
        api = ECS("API Service")

    db = RDS("PostgreSQL")

    lb >> web >> api >> db
```

**Installation:**
```bash
pip install diagrams
```

---

### Structurizr

**What it does:** The gold standard C4 tooling created by Simon Brown (inventor of C4 Model). Provides a DSL for defining architecture and multiple rendering options.

**Best for:** Organizations committed to C4 methodology who want authoritative tooling.

**C4 Levels:** All four levels (Context, Container, Component, Code)

**Pros:**
- Official C4 implementation
- Workspace model separates architecture definition from visualization
- Multiple view types (diagrams, documentation, ADRs)
- Cloud service available (Structurizr Cloud)
- Export to PlantUML, Mermaid, WebSequenceDiagrams

**Cons:**
- DSL learning curve
- Cloud service requires paid subscription for teams
- Less AI-friendly than newer tools like LikeC4
- Java dependency for some tooling

**Links:**
- Official site: https://structurizr.com/
- DSL docs: https://docs.structurizr.com/dsl
- GitHub: https://github.com/structurizr/dsl
- Structurizr Lite (free): https://structurizr.com/help/lite

**Example:**
```structurizr
workspace {
    model {
        customer = person "Customer"

        ecommerce = softwareSystem "E-commerce Platform" {
            webapp = container "Web App" "React"
            api = container "API Service" "Node.js"
            database = container "Database" "PostgreSQL"
        }

        customer -> webapp "Uses"
        webapp -> api "API calls"
        api -> database "Reads/writes"
    }

    views {
        systemContext ecommerce {
            include *
            autolayout lr
        }

        container ecommerce {
            include *
            autolayout lr
        }
    }
}
```

---

### IcePanel

**What it does:** Visual-first collaborative C4 diagramming tool with real-time collaboration and landscape mapping.

**Best for:** Teams that prefer visual editing over code, distributed teams needing real-time collaboration.

**C4 Levels:** Context, Container, Component

**Pros:**
- Beautiful visual interface (no code required)
- Real-time collaboration (like Figma for architecture)
- Landscape view shows multiple systems
- Version history and branching
- Import from existing diagrams

**Cons:**
- Commercial product (paid plans required for teams)
- Less version control friendly than code-based tools
- Limited export options
- Not ideal for AI agent workflows

**Links:**
- Official site: https://icepanel.io/
- Documentation: https://docs.icepanel.io/
- Demo: https://icepanel.io/demo

**Use case:** Best for architecture workshops and stakeholder presentations where visual editing and collaboration trump version control integration.

---

### ADR Tools & Log4brains

**What they do:** Tools for managing Architecture Decision Records (ADRs) - documents that capture important architectural decisions and their context.

**Best for:** Documenting the "why" behind architectural choices, onboarding new team members, preventing decision flip-flopping.

**ADR Format:**
```markdown
# ADR-001: Use PostgreSQL for Primary Database

## Status
Accepted

## Context
Need to choose a database for our e-commerce platform. Requirements:
- ACID transactions for order processing
- Complex queries for reporting
- Strong consistency guarantees

## Decision
Use PostgreSQL as our primary database.

## Consequences
- Positive: Battle-tested ACID compliance, rich query capabilities
- Positive: Strong ecosystem and community support
- Negative: Higher operational complexity than managed NoSQL
- Negative: Scaling writes requires careful partitioning strategy
```

**ADR Tools:**
- GitHub: https://github.com/npryce/adr-tools
- Simple CLI for creating/managing ADRs
- Markdown-based, version controlled

**Installation:**
```bash
# macOS
brew install adr-tools

# Initialize in project
adr init docs/architecture/decisions

# Create new ADR
adr new "Use PostgreSQL for primary database"
```

**Log4brains:**
- GitHub: https://github.com/thomvaill/log4brains
- Modern ADR management with web UI
- Generates searchable static site from ADRs
- Better discoverability than plain markdown files

**Installation:**
```bash
npm install -g log4brains

# Initialize
log4brains init

# Create ADR
log4brains adr new

# Preview site
log4brains preview
```

**Pros:**
- Documents decision context (prevents "why did we do this?" questions)
- Immutable record (decisions marked as superseded, not deleted)
- Lightweight (just markdown files)
- Great for onboarding

**Cons:**
- Requires discipline to maintain
- Can become stale if not integrated into workflow
- Not a substitute for architecture diagrams

---

### arc42

**What it does:** A template for comprehensive software architecture documentation based on 12 predefined sections.

**Best for:** Organizations requiring thorough documentation for compliance, large teams, complex systems.

**Sections:**
1. Introduction and Goals
2. Constraints
3. Context and Scope
4. Solution Strategy
5. Building Block View
6. Runtime View
7. Deployment View
8. Cross-cutting Concepts
9. Architecture Decisions
10. Quality Requirements
11. Risks and Technical Debt
12. Glossary

**Pros:**
- Comprehensive framework covering all aspects
- Language/technology agnostic
- Free and open source
- Available in multiple formats (Markdown, AsciiDoc, Word)
- Widely adopted in European enterprises

**Cons:**
- Can be overkill for small projects
- Requires significant effort to complete fully
- May feel bureaucratic for agile teams

**Links:**
- Official site: https://arc42.org/
- Templates: https://arc42.org/download
- Examples: https://arc42.org/examples

**Usage:**
1. Download template in your preferred format
2. Customize sections based on project needs
3. Skip sections that don't apply (template is flexible)
4. Integrate with version control

**Best practice:** Start minimal (sections 1, 3, 4, 5) and expand over time. Don't let perfect documentation block shipping.

---

### AI-Powered Diagram Tools

#### Eraser DiagramGPT

**What it does:** Generate architecture diagrams from natural language descriptions using AI.

**Best for:** Rapid prototyping, brainstorming sessions, converting meeting notes to diagrams.

**Links:**
- Official site: https://www.eraser.io/diagramgpt
- App: https://app.eraser.io/

**Pros:**
- Instant diagram generation from text
- Supports multiple diagram types (flowcharts, sequence, entity-relationship)
- Editable results (not just static generation)
- Collaboration features

**Cons:**
- Commercial product (free tier limited)
- Generated diagrams may need manual refinement
- Less precise than code-based tools

**Example workflow:**
1. Describe your architecture: "An e-commerce platform with a React frontend, Node.js API, PostgreSQL database, and Redis cache. Include Stripe integration for payments."
2. DiagramGPT generates a diagram
3. Refine with natural language: "Add a background worker for order processing"
4. Export or continue editing visually

#### Swark

**What it does:** Open-source AI-powered diagram generator focusing on software architecture.

**Best for:** Teams wanting AI diagram generation without vendor lock-in.

**Links:**
- GitHub: https://github.com/swark-io/swark

**Pros:**
- Open source and self-hostable
- Multiple output formats
- Extensible

**Cons:**
- Younger project with smaller community
- Requires setup (not a SaaS product)
- May need fine-tuning for specific use cases

**Note:** The AI diagram space is evolving rapidly. Also explore:
- **Claude Code** (this tool!) can generate Mermaid/PlantUML directly
- **GitHub Copilot** with proper prompts
- **ChatGPT/Claude** for generating DSL code for Structurizr/LikeC4

---

## 2025 Industry Trends

Based on recent surveys and industry adoption:

### C4 Model Adoption

- **70%+ of architects** report being confident with the C4 model
- **Context (81%)** and **Container (79%)** are the most frequently used levels
- **Component level (45%)** used selectively for complex areas
- **Code level (<10%)** rarely maintained manually, mostly auto-generated

### Diagrams-as-Code Becoming Standard

- Version control integration is now considered essential
- Git-friendly formats (Mermaid, PlantUML, DSLs) preferred over binary formats
- CI/CD pipelines include diagram validation and rendering
- Diagrams treated as first-class artifacts, not afterthoughts

### AI Integration

- LLMs increasingly used for initial diagram generation
- Human architects focus on refinement and validation
- MCP servers (like LikeC4) bridge AI agents with architecture tools
- Natural language → diagram workflows becoming mainstream

### Shift from Documentation to Living Artifacts

- Architecture diagrams co-located with code
- Diagrams updated alongside code changes (not separately)
- ADRs integrated into PR workflows
- "Architecture as Code" mindset

---

## Choosing the Right Tool

### For Small Teams / Startups
- **Start with:** Mermaid (built into GitHub/GitLab)
- **Add:** ADR Tools for decision tracking
- **Consider:** D2 if you need prettier diagrams

### For AI-First Workflows
- **Start with:** LikeC4 (MCP server integration)
- **Add:** DiagramGPT for brainstorming
- **Generate with:** Claude Code, GitHub Copilot

### For Cloud-Heavy Projects
- **Start with:** Diagrams (Python) for infrastructure
- **Add:** Mermaid for application architecture
- **Consider:** Terraform → diagram generation

### For Enterprise / Compliance
- **Start with:** Structurizr (official C4)
- **Add:** arc42 template for comprehensive docs
- **Add:** Log4brains for ADR management

### For Distributed Teams
- **Start with:** IcePanel (real-time collaboration)
- **Add:** Structurizr for version-controlled diagrams
- **Hybrid:** Collaborative editing → export to DSL

---

## Integration with AI Coding Assistants

Modern architecture tools increasingly support AI workflows:

### LLM Prompts for Diagram Generation

**For Mermaid:**
```
Create a Mermaid C4 Container diagram showing:
- React frontend (Web App)
- Node.js backend (API Service)
- PostgreSQL database
- Redis cache
- Stripe payment integration
```

**For Structurizr DSL:**
```
Generate Structurizr DSL code for an e-commerce system with
3 containers: web app, API, database. Include external Stripe
dependency.
```

**For Diagrams (Python):**
```
Write Python code using the diagrams library to show an AWS
architecture with: ECS cluster (web + api), RDS database,
ElastiCache, and ALB.
```

### MCP Server Integration

If using tools with MCP servers (like LikeC4):

1. AI agent queries current architecture state
2. Agent suggests changes based on feature requirements
3. Updates diagrams programmatically via MCP
4. Human reviews and approves changes

**Example workflow:**
```
User: "Add a notification service that sends emails"

Agent: [Queries LikeC4 MCP server for current architecture]
Agent: [Generates new component definition]
Agent: [Updates diagram with new service + connections]
Agent: "I've updated the architecture diagram to include a
       new Notification Service component connected to the
       API Service and SendGrid. Ready to implement?"
```

This represents the future of architecture documentation: diagrams that evolve with code, maintained by both humans and AI.

---

## Summary

The architecture tooling landscape in 2025 offers something for every team:

- **Quick starts:** Mermaid (already in GitHub)
- **AI-first:** LikeC4 with MCP server
- **Cloud-heavy:** Diagrams (Python)
- **Enterprise:** Structurizr + arc42
- **Decision tracking:** ADR Tools or Log4brains
- **Rapid prototyping:** Eraser DiagramGPT

**Key principle:** Choose tools that integrate with your workflow, not ones that require separate maintenance effort. The best architecture documentation is the documentation that stays up to date.

For core concepts on C4 diagrams and task graphs, see [Visuals & Diagrams Guide](./visuals-and-diagrams.md).

---

## Further Reading

- **[C4 Model](https://c4model.com/)** - Official C4 methodology
- **[Diagrams as Code](https://diagrams.mingrammer.com/)** - Philosophy and tools
- **[ADR GitHub Organization](https://adr.github.io/)** - ADR tools and templates
- **[arc42 in Practice](https://arc42.org/examples)** - Real-world examples
- **[The Software Architect Elevator](https://www.amazon.com/dp/1492077542)** by Gregor Hohpe - Modern architecture practices