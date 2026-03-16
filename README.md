# Fidensa Certification Badges

**[Fidensa](https://fidensa.com)** is an independent AI certification authority. We verify that AI capabilities — MCP servers, Skills, plugins, and workflows — actually do what they claim, through behavioral testing, adversarial analysis, and supply chain verification. Every certification is a signed, portable artifact that anyone can verify against the evidence.

This repo documents how to embed Fidensa certification badges in your README, website, or manifest — and serves as a live demonstration.

---

## Live Badges

These badges are served live from the Fidensa attestation infrastructure. They reflect current certification status in real time.

| Capability | Badge | Tier | Score |
|---|---|---|---|
| fidensa-mcp-server | [![Fidensa Certified](https://fidensa.com/badges/fidensa-mcp-server.svg)](https://fidensa.com/v1/attestation/fidensa-mcp-server) | Certified | 96/A |
| mcp-server-everything | [![Fidensa Certified](https://fidensa.com/badges/mcp-server-everything.svg)](https://fidensa.com/v1/attestation/mcp-server-everything) | Certified | 91/A |
| mcp-server-filesystem | [![Fidensa Certified](https://fidensa.com/badges/mcp-server-filesystem.svg)](https://fidensa.com/v1/attestation/mcp-server-filesystem) | Certified | 90/A |
| docx-skill | [![Fidensa Certified](https://fidensa.com/badges/docx-skill.svg)](https://fidensa.com/v1/attestation/docx-skill) | Certified | 88/B |
| devin-cursorrules | [![Fidensa Verified](https://fidensa.com/badges/devin-cursorrules.svg)](https://fidensa.com/v1/attestation/devin-cursorrules) | Verified | 72/C |

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

## Certification Tiers

Fidensa assigns one of three tiers based on verification results. The tier determines the badge color and label.

| Tier | Meaning | Badge Color |
|---|---|---|
| **Certified** | Full pipeline passed. No unmitigated critical findings. No stage failures. | Green |
| **Verified** | Pipeline completed with findings. At least one stage produced data. All stages ran. | Blue |
| **Evaluated** | Partial coverage. One or more pipeline stages failed or were skipped. Honest about gaps. | Amber |

Every certification also includes a numeric trust score (0–100) and letter grade (A–F). These are computed from eight weighted signals covering functional testing, security analysis, adversarial resilience, SBOM supply chain health, and more. The per-signal breakdown is always published alongside the aggregate — we don't hide behind a single number.

---

## Attestation API

Every badge links to the JSON attestation endpoint. Consumers — human or AI — can verify certification status programmatically.

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
  "trust_score": 91,
  "grade": "A",
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

The certification pipeline runs six stages against every capability:

1. **Ingest** — Source acquisition, build, and capability enumeration
2. **SBOM & Supply Chain** — Software bill of materials generation, vulnerability scanning (syft, grype, osv-scanner)
3. **Security Analysis** — Static analysis, behavioral scanning, LLM-assisted review
4. **Functional Testing** — Automated test generation and execution against declared interfaces
5. **Adversarial Testing** — Structured attack library (6 categories, 40+ patterns) covering prompt injection, data exfiltration, resource abuse, and more
6. **Behavioral Fingerprint** — Per-tool timing profiles, error rates, resource consumption baselines

Every signed certification artifact includes the full evidence trail. Trust claims are verifiable, not asserted.

---

## Request Certification

If you maintain an MCP server, Skill, plugin, or workflow and want it independently certified, visit [fidensa.com](https://fidensa.com) or open an issue in this repo.

---

## License

This integration guide is released under the [MIT License](LICENSE). Fidensa certification artifacts, the Fidensa name, and the Fidensa badge design are property of Fidensa.
