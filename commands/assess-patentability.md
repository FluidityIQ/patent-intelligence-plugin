---
description: Conduct a patentability assessment — gather invention details, search patent prior art, map features, and generate a structured report
---

# /assess-patentability -- Assess Patentability

> If you see unfamiliar placeholders or need to check which tools are connected, see [CONNECTORS.md](../CONNECTORS.md).

Conduct a patentability assessment for an invention or idea. Searches patent prior art via semantic search, maps invention features against references, and produces a structured assessment report.

**Important**: This command assists with patent workflows but does not provide legal advice. All analysis should be reviewed by a registered patent attorney or agent before being relied upon.

## Invocation

```
/patent-intelligence:assess-patentability
```

Accepts: invention description, Invention Disclosure Form (IDF), pasted text, or file upload. Will ask clarifying questions to gather required details before searching.

## Workflow

### Step 1: Load Settings

Check for organization-specific settings in `patent-intelligence.local.md`. Settings may define:
- Report branding (organization name, matter numbering)
- Privilege markings and confidentiality handling
- Search preferences (jurisdiction focus, minimum rounds)
- Review workflow (who receives reports, sign-off requirements)

If no settings file exists, proceed with defaults and note this in the report.

### Step 2: Invention Intake

Gather invention details (description, key features, known prior art) and any context the user can provide. Use the patentability skill for required fields and follow-up questions.

### Step 3: Identify Point of Novelty

Explicitly identify and document the **point of novelty** — the aspect that distinguishes this invention from what exists. Confirm with the user.

### Step 4: Craft Semantic Queries

Transform the disclosure into one or more semantic search queries (primary + sub-queries if needed). Use the patentability skill for query quality and structure.

### Step 5: Execute Search

Run the iterative search protocol (primary search, sub-query expansion, terminology harvesting, gap-filling) using the `~~patent search` MCP tools. Stop when results saturate, coverage is sufficient, or an anticipatory reference is found.

### Step 6: Classify References

Categorize each relevant reference as Anticipatory, Combinable, or Background. For Anticipatory and strong Combinable references, retrieve full patent text for detailed analysis.

### Step 7: Build Feature Coverage Matrix

Map the invention's key features against the top references with specific citations (paragraph numbers, figure references, claim numbers).

### Step 8: Analyze Patentability

Assess novelty (all-elements rule), non-obviousness (motivation to combine), and utility. Use the patentability skill for the analytical frameworks.

### Step 9: Generate Report

Produce the structured Patentability Assessment Report per the skill's report template. Mark as CONFIDENTIAL; include privilege markings if prepared under attorney direction.

### Step 10: Recommend Next Steps

Based on the assessment results:

| Finding | Recommendation |
|---------|----------------|
| **No anticipatory references** | Potentially novel; consider filing strategy and non-obviousness strengthening |
| **Anticipatory reference found** | Design around the reference or narrow the scope of the inventive concept |
| **Strong combinations exist** | Identify features that resist combination; consider narrowing claims to uncovered aspects |
| **Sparse prior art** | Positive signal, but note that additional searching (non-patent literature, expanded jurisdictions) is recommended |

Always recommend:
- Attorney review of the assessment
- Non-patent literature search (separate skill) for completeness
- Monitoring for newly published applications (18-month secrecy window)
- Freedom-to-operate analysis if the invention uses features described in prior art

## Notes

- If the user provides an Invention Disclosure Form, extract the relevant fields automatically rather than re-asking
- For complex inventions spanning multiple domains, consider running separate assessments for each inventive concept
- Queries submitted to the Patent Search MCP contain invention details — remind the user if confidentiality is critical
- This command searches patent documents only; non-patent literature is handled by a separate skill
