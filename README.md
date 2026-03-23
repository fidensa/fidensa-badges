# Fidensa Certification Badges

**[Fidensa](https://fidensa.com)** is an independent AI certification authority. We verify that AI capabilities -- MCP servers, skills, agent rules files, hooks, sub-agents, and plugins -- actually do what they claim, through behavioral testing, adversarial analysis, and supply chain verification. Every certification is a signed, portable artifact that anyone can verify against the evidence.

This repo documents how to embed Fidensa certification badges in your README, website, or manifest -- and serves as a live demonstration.

---

## Live Badges

These badges are served live from the Fidensa attestation infrastructure. They reflect current certification status in real time.

| Capability | Badge | Tier | Score | Type |
|---|---|---|---|---|
| fidensa-mcp-server | [![Fidensa Certified](https://fidensa.com/badges/fidensa-mcp-server.svg)](https://fidensa.com/v1/attestation/fidensa-mcp-server) | Certified | 96/A | MCP Server |
| docx-skill | [![Fidensa Certified](https://fidensa.com/badges/docx-skill.svg)](https://fidensa.com/v1/attestation/docx-skill) | Certified | 90/A | Skill |
| mcp-server-git | [![Fidensa Verified](https://fidensa.com/badges/mcp-server-git.svg)](https://fidensa.com/v1/attestation/mcp-server-git) | Verified | 79/C | MCP Server |
| claude-guardrails | [![Fidensa Verified](https://fidensa.com/badges/claude-guardrails.svg)](https://fidensa.com/v1/attestation/claude-guardrails) | Verified | 75/C | Hook |

These are a representative sample. **[Browse all 18 certifications](https://fidensa.com/certifications)** spanning MCP servers, skills, rules files, hooks, sub-agents, and plugins.

If a certification is suspended, revoked, or expired, the badge updates automatically.

---

## Embed a Badge

### Markdown (GitHub README)

```markdown
[![Fidensa Certified](https://fidensa.com/badges/YOUR-CAPABILITY-ID.svg)](https://fidensa.com/v1/attestation/YOUR-CAPABILITY-ID)
```

**Example with a real capability:**

```markdown
[![Fidensa Certified](https://fidensa.com/badges/mcp-server-everything.svg)](https://fidensa.com/v1/attestation/mcp-server-everything)
```

### HTML (website, docs, app listing)

```html
<a href="https://fidensa.com/v1/attestation/YOUR-CAPABILITY-ID">
  <img
    src="https://fidensa.com/badges/YOUR-CAPABILITY-ID.svg"
    alt="Fidensa Certified"
  />
</a>
```

### Version-pinned badge

To link to a specific certified version rather than the latest:

```markdown
[![Fidensa Certified](https://fidensa.com/badges/mcp-server-everything/2.0.0.svg)](https://fidensa.com/v1/attestation/mcp-server-everything/2.0.0)
```

---

## Badge Styles

Fidensa badges support the same style conventions as [shields.io](https://shields.io).

| Style | URL | Preview |
|---|---|---|
| Flat (default) | `?style=flat` | [![](https://fidensa.com/badges/mcp-server-everything.svg?style=flat)](https://fidensa.com/v1/attestation/mcp-server-everything) |
| Flat Square | `?style=flat-square` | [![](https://fidensa.com/badges/mcp-server-everything.svg?style=flat-square)](https://fidensa.com/v1/attestation/mcp-server-everything) |
| For the Badge | `?style=for-the-badge` | [![](https://fidensa.com/badges/mcp-server-everything.svg?style=for-the-badge)](https://fidensa.com/v1/attestation/mcp-server-everything) |
| Compact | `?compact=true` | [![](https://fidensa.com/badges/mcp-server-everything.svg?compact=true)](https://fidensa.com/v1/attestation/mcp-server-everything) |

---

## Maturity Indicator

Badges include a maturity indicator shown as dots (through). This reflects how much real-world validation a certification has received beyond the initial pipeline evaluation.

| Level | Dots | Meaning |
|---|---|---|
| **Initial** | one filled, three empty | Pipeline-tested only. No consumer reports or monitoring data yet. |
| **Emerging** | two filled, two empty | 10 or more consumer reports or 30 or more days of uptime monitoring. |
| **Established** | three filled, one empty | 50 or more reports from 10 or more consumers and 90 or more days monitoring. |
| **Proven** | four filled | 200 or more reports from 25 or more consumers and 180 or more days monitoring. |

Maturity is computed dynamically -- as consumer experience reports accumulate and uptime monitoring data grows, the dots fill in automatically. The badge always reflects the current maturity level.

---

## Certification Tiers

Fidensa assigns one of three tiers based on verification results. The tier determines the badge color and label.

| Tier | Meaning | Badge Color |
|---|---|---|
| **Certified** | Full pipeline passed. No unmitigated critical findings. No stage failures. | Green |
| **Verified** | Pipeline completed with findings. At least one stage produced data. All stages ran. | Blue |
| **Evaluated** | Partial coverage. One or more pipeline stages failed or were skipped. Honest about gaps. | Amber |

Every certification also includes a numeric trust score (0-100) and letter grade (A-F). These are computed from eight weighted signals covering functional testing, security analysis, adversarial resilience, SBOM supply chain health, and more. The per-signal breakdown is always published alongside the aggregate -- we don't hide behind a single number.

---

## Attestation API

Every badge links to the JSON attestation endpoint. Consumers -- human or AI -- can verify certification status programmatically.

**Endpoints:**

```
GET https://fidensa.com/v1/attestation/{capabilityId}
GET https://fidensa.com/v1/attestation/{capabilityId}/{version}
GET https://fidensa.com/v1/attestation/by-hash/{contentHash}
```

**Example response:**

```json
{
  "schema_version": "1.0",
  "capability_id": "mcp-server-everything",
  "version": "1.0.0",
  "status": "valid",
  "tier": "certified",
  "trust_score": 84,
  "grade": "B",
  "maturity": "Initial",
  "supply_chain_status": "clean",
  "certified_at": "2026-03-14T...",
  "expires_at": "2027-03-14T...",
  "badge_url": "https://fidensa.com/badges/mcp-server-everything.svg"
}
```

**Platform public key** for signature verification is published at:

```
GET https://fidensa.com/.well-known/certification-keys.json
```

---

## JSON Reference Block

For `package.json`, MCP server manifests, plugin manifests, or any machine-readable context:

```json
{
  "certification": {
    "authority": "fidensa.com",
    "capability_id": "mcp-server-everything",
    "version": "2.0.0",
    "status_url": "https://fidensa.com/v1/attestation/mcp-server-everything/2.0.0",
    "badge_url": "https://fidensa.com/badges/mcp-server-everything/2.0.0.svg"
  }
}
```

An AI agent or tooling that encounters this block can immediately fetch the attestation status and verify the certification before using the capability.

---

## What Fidensa Verifies

The certification pipeline runs seven stages against every capability:

1. **Ingest** -- Source acquisition, build, capability enumeration, provenance metadata gathering
2. **SBOM and Supply Chain** -- Software bill of materials generation, vulnerability scanning (syft, grype, osv-scanner, cdxgen)
3. **Security Analysis** -- Static analysis, behavioral scanning, LLM-assisted review
4. **Functional Testing** -- Automated test generation and execution against declared interfaces
5. **Adversarial Testing** -- Structured attack library (6 categories, 55 patterns) covering prompt injection, data exfiltration, resource abuse, and more, with impact-based finding classification (Block/Warn/Review/Info)
6. **Behavioral Fingerprint** -- Per-tool timing profiles, error rates, resource consumption baselines
7. **Certification** -- Contract assembly with OWASP MCP Top 10 coverage mapping, provenance verification, trust score computation from eight weighted signals, ES256 cryptographic signing

Every signed certification artifact includes the full evidence trail. Trust claims are verifiable, not asserted.

---

## Request Certification

If you maintain an MCP server, skill, agent rules file, hook, sub-agent, or plugin and want it independently certified, visit [fidensa.com](https://fidensa.com) or open an issue in this repo.

---

## License

This integration guide is released under the [MIT License](LICENSE). Fidensa certification artifacts, the Fidensa name, and the Fidensa badge design are property of Fidensa.
