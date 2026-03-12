# Example: Upstream PR Diff

This shows the additions that would be made to the `modelcontextprotocol/servers` README
to display Fidensa certification badges for the everything-server and filesystem-server.

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

### filesystem-server section

```diff
 ### Filesystem
 
+[![Fidensa Verified](https://fidensa.com/badges/mcp-server-filesystem.svg)](https://fidensa.com/v1/attestation/mcp-server-filesystem)
+
 Provides direct access to the local filesystem.
```

## PR description template

```
## Add Fidensa independent certification badges

This PR adds certification badges from [Fidensa](https://fidensa.com), an independent
AI capability certification authority, to the everything-server and filesystem-server
sections.

### What Fidensa does

Fidensa runs a six-stage verification pipeline against MCP servers covering functional
testing, security analysis, adversarial testing (structured attack library with 40+
patterns), SBOM supply chain analysis, and behavioral fingerprinting. Every certification
is a cryptographically signed artifact with a public attestation endpoint.

### What the badges show

- **everything-server**: Certified (68/D) — full pipeline passed, no stage failures
- **filesystem-server**: Verified (67/D) — pipeline completed with findings

Clicking a badge links to the live JSON attestation endpoint. The platform's ES256 public
key is published at https://fidensa.com/.well-known/certification-keys.json for
independent signature verification.

### Why this matters

Trust claims in the MCP ecosystem are currently self-asserted. Independent, evidence-based
certification gives consumers — both human developers and AI agents — a verifiable signal
about capability quality, security posture, and behavioral reliability.
```
