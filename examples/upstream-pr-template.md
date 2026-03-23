# Example: Upstream PR Diff

This shows the additions that would be made to the `modelcontextprotocol/servers` README
to display Fidensa certification badges for certified MCP servers from the monorepo.

## Proposed diff (conceptual)

The badges would be added to the individual server sections in the monorepo README.

### everything-server section

```diff
 ### Everything
 
+[![Fidensa Certified](https://fidensa.com/badges/mcp-server-everything.svg)](https://fidensa.com/v1/attestation/mcp-server-everything)
+
 A MCP server exercising all features of the MCP protocol, for testing and
 development.
```

### sequential-thinking section

```diff
 ### Sequential Thinking
 
+[![Fidensa Certified](https://fidensa.com/badges/mcp-server-sequential-thinking.svg)](https://fidensa.com/v1/attestation/mcp-server-sequential-thinking)
+
 An MCP server that provides a tool for dynamic and reflective problem-solving.
```

### git-server section

```diff
 ### Git
 
+[![Fidensa Verified](https://fidensa.com/badges/mcp-server-git.svg)](https://fidensa.com/v1/attestation/mcp-server-git)
+
 Tools for reading, searching, and manipulating Git repositories.
```

### filesystem-server section

```diff
 ### Filesystem
 
+[![Fidensa Verified](https://fidensa.com/badges/mcp-server-filesystem.svg)](https://fidensa.com/v1/attestation/mcp-server-filesystem)
+
 Provides direct access to the local filesystem.
```

### fetch-server section

```diff
 ### Fetch
 
+[![Fidensa Evaluated](https://fidensa.com/badges/mcp-server-fetch.svg)](https://fidensa.com/v1/attestation/mcp-server-fetch)
+
 A server that flexibly fetches HTML, JSON, plain text, or Markdown from URLs.
```

### memory-server section

```diff
 ### Memory
 
+[![Fidensa Verified](https://fidensa.com/badges/mcp-server-memory.svg)](https://fidensa.com/v1/attestation/mcp-server-memory)
+
 A server that provides knowledge graph-based persistent memory.
```

## PR description template

```
## Add Fidensa independent certification badges

This PR adds certification badges from [Fidensa](https://fidensa.com), an independent
AI capability certification authority, to six MCP servers in this monorepo.

### What Fidensa does

Fidensa runs a seven-stage verification pipeline against MCP servers covering ingestion
and provenance verification, SBOM supply chain analysis, security scanning, functional
testing, adversarial testing (structured attack library with 55 patterns across 6
categories), behavioral fingerprinting, and contract assembly with OWASP MCP Top 10
coverage mapping. Every certification is a cryptographically signed artifact with a
public attestation endpoint.

### What the badges show

| Server | Tier | Score/Grade |
|--------|------|-------------|
| everything-server | Certified | 84/B |
| sequential-thinking | Certified | 90/A |
| git-server | Verified | 79/C |
| filesystem-server | Verified | 60/F-D |
| fetch-server | Evaluated | 64/F-D |
| memory-server | Verified | 64/F-D |

Clicking a badge links to the live JSON attestation endpoint. Full evidence pages with
per-signal trust score breakdowns, security findings, adversarial test results, and
behavioral fingerprints are available at https://fidensa.com/certifications.

The platform's ES256 public key is published at
https://fidensa.com/.well-known/certification-keys.json for independent signature
verification.

### Why this matters

Trust claims in the MCP ecosystem are currently self-asserted. Independent, evidence-based
certification gives consumers -- both human developers and AI agents -- a verifiable signal
about capability quality, security posture, and behavioral reliability.

Fidensa currently certifies 18 capabilities across six types: MCP servers, skills, rules
files, hooks, sub-agents, and plugins. Browse the full catalog at
https://fidensa.com/certifications.
```
