# Patent Intelligence Plugin

An AI-powered productivity plugin for IP law teams, designed for [Cowork](https://claude.com/product/cowork). Automates patentability assessments, prior art searches, and invention feature mapping — all configurable to your organization's specific workflows and preferences.

> **Disclaimer:** This plugin assists with patent workflows but does not provide legal advice. All analysis should be reviewed by a registered patent attorney or agent before being relied upon. AI-generated analysis should not be used as a substitute for professional legal judgment.

## Target Personas

- **Patent Counsel** — Patentability evaluations, prior art landscape analysis, prosecution support
- **Patent Agents** — Prior art search execution, feature mapping, report preparation
- **Inventors & R&D Teams** — Invention disclosure submission, preliminary patentability feedback
- **IP Portfolio Managers** — Portfolio gap analysis, technology landscape monitoring

## Installation

```
claude plugins add FluidityIQ/patent-intelligence-plugin
```

## Quick Start

### 1. Install the plugin

```
claude plugins add FluidityIQ/patent-intelligence-plugin
```

### 2. Configure your Patent Search MCP

The plugin requires a patent search MCP server that provides semantic search and patent details retrieval. Configure the connection in `.mcp.json` at the plugin root. Authentication is handled automatically via OAuth (auto-discovery); for org-wide or CI deployments using an API key instead, see [CONNECTORS.md](CONNECTORS.md) for the API key configuration.

### 3. Configure your settings (optional)

Create a local settings file to define your organization's preferences. In your project's `.claude/` directory, create a `patent-intelligence.local.md` file:

```markdown
# FluidityIQ Patent Intelligence Plugin Settings

## Report Branding
- Organization: [Your Organization Name]
- Matter numbering convention: [e.g., PAT-2026-001]
- Default privilege marking: PRIVILEGED AND CONFIDENTIAL — ATTORNEY WORK PRODUCT

## Search Preferences
- Default jurisdiction focus: US, EP, WO, CN, JP, KR
- Minimum search rounds: 3
- Result threshold: 20-30 results per round

## Review Workflow
- Reports route to: [Patent Counsel Name/Email]
- Required sign-off: [Senior Counsel / IP Committee]
- Escalation path: [For anticipatory references or complex combinations]

## Technology Focus Areas
- Priority fields: [e.g., semiconductor, biologics, wireless]
- Internal portfolio: [Reference to internal patent database or tracking system]
- Competitive landscape: [Key competitors to monitor]
```

### 4. Connect your tools

The plugin requires the patent search MCP (FluidityIQ Patents MCP). See [CONNECTORS.md](CONNECTORS.md) for configuration.

## Commands

### `/patent-intelligence:assess-patentability` — Patentability Assessment

Conduct a full patentability assessment for an invention or idea. Gathers invention details, searches patent prior art via semantic search, maps features against references, and produces a structured report.

```
/patent-intelligence:assess-patentability
```

Accepts: invention description, Invention Disclosure Form, pasted text, or file upload. The command walks through a structured workflow:

1. **Intake** — Gather invention details and identify the point of novelty
2. **Search** — Multi-round semantic patent search with terminology refinement
3. **Classify** — Categorize references as Anticipatory (RED), Combinable (YELLOW), or Background (GREEN)
4. **Map** — Build feature coverage matrix with specific citations
5. **Analyze** — Evaluate novelty and non-obviousness
6. **Report** — Generate the structured Patentability Assessment Report
7. **Recommend** — Suggest next steps based on findings

## Skills

| Skill | Description |
|-------|-------------|
| `patentability` | Semantic patent search, prior art classification, feature coverage mapping, novelty and non-obviousness analysis, structured report generation |

## Example Workflows

### Patentability Assessment for a New Invention

1. Inventor describes their idea or uploads an Invention Disclosure Form
2. Run `/patent-intelligence:assess-patentability`
3. Provide context: technology field, known prior art, key features believed to be novel
4. The skill runs 3-4 rounds of semantic patent search, harvesting terminology along the way
5. References are classified (Anticipatory / Combinable / Background) and mapped against invention features
6. Receive a structured report with feature coverage matrix, novelty analysis, and non-obviousness assessment
7. Route the report to patent counsel for review and filing decision

### Quick Prior Art Check for an Idea

1. Describe the idea in a few sentences
2. Run `/patent-intelligence:assess-patentability`
3. The skill identifies the point of novelty and runs a focused search
4. Get a rapid assessment of whether similar patents exist and what features overlap
5. Decide whether to invest in a full invention disclosure

### Portfolio Gap Analysis

1. Describe a technology area your team is working in
2. Run `/patent-intelligence:assess-patentability` for each inventive concept
3. Compare feature coverage matrices across assessments
4. Identify unprotected innovations and prioritize filing

## MCP Integration

> If you see unfamiliar placeholders or need to check which tools are connected, see [CONNECTORS.md](CONNECTORS.md).

The plugin connects to tools through MCP (Model Context Protocol) servers. The patent search MCP (FluidityIQ Patents MCP) is **required**:

| Category | Purpose |
|----------|---------|
| Patent search | Semantic prior art search, patent document retrieval |

## Customization

### Local Settings

Your settings file (`patent-intelligence.local.md`) controls:

- **Report branding**: Organization name, matter numbering, privilege markings
- **Search preferences**: Jurisdiction focus, search depth, result thresholds
- **Review workflow**: Routing, sign-offs, escalation paths
- **Technology focus**: Priority fields, competitive landscape, internal portfolio references

### Report Output

The Patentability Assessment Report follows a structured template:

1. **Executive Summary** — Key findings in 2-3 sentences
2. **Feature Coverage Matrix** — Visual mapping of features vs. references
3. **Invention Summary** — Technical field, problem, solution, key features
4. **Prior Art References** — Categorized reference table with detailed descriptions
5. **Novelty Analysis** — Anticipation assessment per reference
6. **Non-Obviousness Analysis** — Combination analysis with motivation assessment
7. **Search Methodology** — Search strategy, rounds executed, tools used
8. **Limitations** — Patent-only scope, 18-month window, semantic search constraints

### Reference Classification

References follow a three-tier classification:

| Category | Threat Level | Action |
|----------|-------------|--------|
| **Anticipatory** (RED) | Discloses all key features — threatens novelty | Detailed mapping, immediate flag, design-around analysis |
| **Combinable** (YELLOW) | Discloses some features — may threaten non-obviousness | Feature gap analysis, combination assessment |
| **Background** (GREEN) | Provides context, no direct threat | Landscape awareness |

## File Structure

```
patent-intelligence-plugin/
├── .claude-plugin/plugin.json
├── .mcp.json
├── README.md
├── CONNECTORS.md
├── LICENSE
├── commands/
│   └── assess-patentability.md
└── skills/
    └── patentability/
        └── SKILL.md
```

## Roadmap

Future skills planned for the Patent Intelligence Plugin:

| Skill | Description | Status |
|-------|-------------|--------|
| `patentability` | Patent prior art search and assessment | Available |
| `npl-search` | Non-patent literature search (journals, conferences, standards) | Planned |
| `fto-search` | Freedom-to-operate / right-to-practice analysis | Planned |
| `invalidity-search` | Patent invalidity and inter partes review support | Planned |
| `portfolio-analysis` | Patent portfolio gap analysis and landscaping | Planned |
| `claim-drafting` | Claim drafting assistance from invention disclosures | Planned |

## Support

- **GitHub Issues:** [Report bugs or request features](https://github.com/FluidityIQ/patent-intelligence-plugin/issues)
- **Email:** support@fluidityiq.com

## Privacy

This plugin sends invention descriptions and semantic search queries to the Patent Search MCP (FluidityIQ Patents MCP at `https://patents.fluidityiq.ai/mcp`) for prior art search and patent retrieval. No other conversation data is transmitted. For full details on data collection, use, and retention, see the [FluidityIQ Privacy Policy](https://www.fluidityiq.com/privacy-policy).

## Terms of Service

For more details, see the [FluidityIQ Terms of Service](https://www.fluidityiq.com/terms-of-service).

## License

MIT — see [LICENSE](LICENSE) for details.
