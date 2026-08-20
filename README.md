<div align="center">

# 🐧 Penguin Technologies

### Open source, open models, and multi-cloud — easier to run, and secure by default.

We build the whole open stack: bare metal to Kubernetes, data to AI, network to endpoint.
Run it on your hardware, in any cloud, or across all of them — with the security already turned on.

[**penguintech.io**](https://penguintech.io) · [**PenguinCloud**](https://penguincloud.io)

</div>

---

## Why we exist

Modern infrastructure makes you pay twice: once in licensing, and again in the operational drag of gluing a dozen vendors together — each with its own control plane, its own identity model, its own lock-in. Open source was supposed to fix that. Too often it just moves the integration burden onto you.

So we build the whole stack in the open, designed to fit together and designed to be left alone.

| Our goal | What that actually means |
|---|---|
| **Open source** | What ships open source *stays* open source. No rug pulls, no bait-and-switch re-licensing. |
| **Open models** | AI that prefers open weights on hardware you control. Commercial providers are an option, never a dependency. |
| **Multi-cloud** | Deploy once; run on bare metal, AWS, Azure, GCP, or all of them at once. No vendor's proprietary control plane in your critical path. |
| **Secure by default** | Hardened defaults you have to deliberately opt *out* of — not a checklist you get around to after the incident. |

---

## The stack

Two things live in this org, and they are not the same kind of thing.

Most of it is one portfolio for **secure infrastructure and secure AI** — each product useful alone, with **PenguinCloud as the overlay** that makes the whole set portable across bare metal, any cloud, or all of them at once.

```
   ╭─────────────────────────────────────────────────────────────────────────────╮
   │  PenguinCloud              deploy once — any cloud, bare metal, air-gapped  │
   ╰─────────────────────────────────────────────────────────────────────────────╯
        overlays everything below
   ┌─────────────────────────────────────────────────────────────────────────────┐
   │  SECURE AI   WaddleAI      open models, on your own GPUs                    │
   │  GOVERNANCE  Elder         infrastructure + internal ticketing              │
   │              SkausWatch    prove it's safe                                  │
   │  ACCESS      Tobogganing   zero-trust network access                        │
   │              Squawk        authenticated DNS                                │
   │              Penguin       one hardened endpoint client                     │
   │  FOUNDATION  Gough         bare metal to Kubernetes                         │
   │              Nest          data, storage, databases                         │
   └─────────────────────────────────────────────────────────────────────────────┘

   ╭─────────────────────────────────────────────────────────────────────────────╮
   │  Waddles                   community and customer hub                       │
   │                            ← Current + Elder's customer-facing CRM          │
   ╰─────────────────────────────────────────────────────────────────────────────╯
```

### Common by design

Whatever you deploy, the foundations are the same. Nearly every product here is:

- **Multi-tenant from the ground up** — the tenant boundary is enforced at the query layer and checked before anything else, not bolted on as a filter someone has to remember.
- **OIDC scope-based for every role** — permissions resolve to OIDC scopes, never role names. Roles are just pre-bundled scope sets, so a new role never means new authorization code.
- **Short-lived JWTs by default** — one-hour tokens, refresh tokens that rotate on every use, and a reused refresh token treated as compromise that revokes the whole chain.

One identity model across the whole stack means access review is a single conversation instead of eleven of them.

---

### Foundation — metal, clusters, and data

| Project | What it does | Live |
|---|---|---|
| [**Gough**](https://github.com/penguintechinc/gough) | Hypervisor and bare-metal automation | [gough.app](https://gough.app) |
| [**Nest**](https://github.com/penguintechinc/nest) | Kubernetes-native and public cloud centralized data infrastructure  (Storage and DB as a Service| [nestdata.app](https://nestdata.app) |

**Gough** discovers a physical server over PXE and hands you a running Kubernetes cluster — then keeps going into AWS, Azure, GCP, Vultr, and LXD from the same control plane. Cosign-signed deployment templates, Vault PKI, SPIRE mTLS, and an append-only audit chain mean the provenance of every node is something you can prove, not just assert. Manage locally on your hardware, or in AWS, GCP, Vultr, and/or Azure!

**Nest** turns storage, databases, search, streaming, and analytics into Kubernetes custom resources. Declare a `DataResource` and get Ceph volumes, PostgreSQL with PITR, Valkey, Kafka, OpenSearch, or ClickHouse — provisioned on-cluster, pointed at a cloud provider, or adopted from what you already run, switchable per resource without re-architecting. Manage locally on your hardware, or in AWS, GCP, Vultr, and/or Azure!

### Access & network — zero trust, all the way to the endpoint

| Project | What it does | Live |
|---|---|---|
| [**Tobogganing**](https://github.com/penguintechinc/tobogganing) | SASE / Zero Trust Network Access on WireGuard | [tobogganing.app](https://tobogganing.app) |
| [**Squawk**](https://github.com/penguintechinc/squawk) | Authenticated DNS-over-HTTPS with per-domain access control | [squawkmgr.app](https://squawkmgr.app) |
| [**Penguin**](https://github.com/penguintechinc/penguin) | One modular client for desktop and mobile | |

**Tobogganing** is ZTNA without the enterprise VPN tax — WireGuard transport, dual X.509-certificate *and* SSO authentication, domain/IP/protocol/port firewalling, traffic mirroring to your IDS, and Suricata plus STIX/TAXII threat feeds. Self-hosted, no per-seat licensing, and no proprietary blobs in the data path.

**Squawk** puts authentication and per-user, per-domain policy in front of DNS itself, so resolution stops being the one unauthenticated hop in an otherwise zero-trust network.

**Penguin** is the single client your users install — Tobogganing, Squawk, and more as modules on one hardened core, across Windows, macOS, Linux, iOS, and Android. One agent to deploy and update, not one per product.

### Governance — know what you run, then prove it's safe

| Project | What it does | Live |
|---|---|---|
| [**Elder**](https://github.com/penguintechinc/elder) | Asset, entity, and relationship tracking | [elderrms.app](https://elderrms.app) |
| [**SkausWatch**](https://github.com/penguintechinc/skauswatch) | Cloud security, threat intel, and vulnerability management | [skauswatch.app](https://skauswatch.app) |

**Elder** maps what infrastructure you actually have and how it connects — resources, identities, dependencies, and organizational hierarchy — with identity sync across Okta, LDAP/AD, AWS, GCP, and Google Workspace, SBOM ingestion with vulnerability tracking, and PII/PHI/PCI metadata attached to the data stores that hold it. Audit-ready records instead of a spreadsheet nobody trusts. Elder also keeps ticketing — scoped to **internal company operations**. Customer-facing support and CRM move to Waddles; the dividing line is simply whether the person on the other end works for you.

**SkausWatch** scans S3 with ClamAV and YARA, enriches findings through VirusTotal and AlienVault OTX, runs Nuclei, ZAP, and OpenVAS against your infrastructure, and monitors hosts with an EDR agent that deploys as a read-only Kubernetes DaemonSet. Optional modules add envelope-encrypted secrets management with JIT access and a full X.509/SSH certificate authority.

### Platform & AI

| Project | What it does | Live |
|---|---|---|
| [**PenguinCloud**](https://github.com/penguintechinc/penguincloud) | Secure multi-cloud and hybrid deployment | [penguincloud.io](https://penguincloud.io) |
| [**WaddleAI**](https://github.com/penguintechinc/waddleai) | Self-hosted AI gateway and coding assistant | [waddleai.app](https://waddleai.app) |

**PenguinCloud** is the overlay that makes everything else portable — workload and storage deployment across multi-cloud and hybrid environments, including air-gapped, with self-testing and self-healing built into the images rather than bolted on afterward.

**WaddleAI** puts one OpenAI-compatible endpoint in front of Ollama, llama.cpp, OpenAI, Anthropic, Gemini, Bedrock, Azure, and Cohere — with prompt-injection detection, PII/PCI filtering, per-user and per-team budget quotas, and virtual API keys. It runs open models on your own GPUs, in your own cluster, air-gapped if you need it, and treats commercial providers as replaceable fallbacks. Ships with PenguinCode, a CLI and VS Code coding assistant that keeps your source on your machine.

---

## Waddles — a different animal

Everything above exists to run secure infrastructure and secure AI. Waddles doesn't, and that's deliberate.

| Project | What it does | Live |
|---|---|---|
| [**Waddles**](https://github.com/penguintechinc/waddlebot) | Community, customer, and relationship management | [waddles.app](https://waddles.app) |
| [**Current**](https://github.com/penguintechinc/current) | Link shortening and click analytics — consolidating into Waddles | [currenturl.app](https://currenturl.app) |

It started as a practical objection: we didn't want to pay for a community and customer management platform, so we built one on top of our waddlebot project. It runs communities across Twitch, Discord, Slack, YouTube, and Kick from a single multi-tenant deployment — AI-powered interactions, loyalty and reputation, minigames, giveaways, event calendars, and a visual workflow builder — with the same RBAC and audit logging discipline as the rest of the portfolio.

It is becoming **our community and customer hub**, and it is growing by consolidation rather than sprawl:

- **Current** brings branded short links, QR codes, and click analytics — campaign tracking where the campaigns already live. It remains usable standalone today.
- **Elder's customer-facing support and CRM** bring customer records, relationships, and support conversations. Elder keeps internal ticketing for your own staff; anything aimed at a customer lives here.

One place where communities, customers, and the links that reach them all live — instead of three products and an integration problem. PenguinCloud doesn't overlay it, and doesn't need to. Different job, same engineering standards.

*(The repo is still named `waddlebot` — the project outgrew the name.)*

---

## Penguin Libs — MIT, and yours to use

Everything above is built on [**penguin-libs**](https://github.com/penguintechinc/penguin-libs): the shared auth, data-access, licensing, and UI foundations our own products depend on. It's **MIT licensed and published to public registries** — no private scopes, no internal-only registry, no account required. Use it in your own projects, with or without anything else in this org.

| Language | Install from | What you get |
|---|---|---|
| **Python** | PyPI | `penguin-aaa` (OIDC, RBAC scopes, SPIFFE, tenant isolation) · `penguin-dal` (data access across SQL, cache, stream, and document backends) · `penguin-sal` (one API over multiple secrets backends) · `penguin-utils` (sanitized logging) · `penguin-limiter` · `penguin-email` · `penguin-licensing` |
| **TypeScript / React** | public npm | `@penguintechinc/react-aaa` (auth context, OIDC client, token manager, protected routes) · `@penguintechinc/react-libs` · `@penguintechinc/react-testutils` |
| **Go** | `go get github.com/penguintechinc/penguin-libs/packages/{name}` | `go-aaa` (OIDC RP with PKCE + SPIFFE) · `go-h3` (HTTP/3 interceptors) · `go-dal` · `go-logging` · `go-numa` (NUMA-aware buffer pools) · `go-xdp` (XDP/AF_XDP helpers) |
| **Rust · Flutter** | in the repo, publishing in progress | `penguin-h3-tower` and `penguin-rpc` (Connect RPC over HTTP/3) · `flutter_libs` (shared widgets, theming, login, sidebar) |

Packages are **MIT**, except the HTTP/3 RPC packages, which are Apache-2.0 — both permissive, both fine for commercial use.

Publishing to public registries under MIT isn't incidental. It's the same rule as the rest of the stack: the things we build to make our work easier should make yours easier too.

---

## Security isn't a feature here. It's the substrate.

Several of our engineers have spent 20+ years in security — application security, network security, cryptography, identity and access management, offensive security and red teaming, incident response, compliance and audit, and supply chain. Between us we've built and defended at Fortune 100, DoD, and big-tech scale.

That background shows up as engineering defaults, not marketing bullets:

| Practice | How it works in these repos |
|---|---|
| **Zero trust between services** | Every service is SPIFFE-ready and accepts mTLS/X.509-SVID identity. Every inter-service call carries a short-lived signed JWT — including internal gRPC. No long-lived shared secrets. |
| **Scope-based authorization** | Permission decisions run on OIDC scopes, never role names. Tenant isolation is a hard boundary enforced at the query layer, checked before anything else. |
| **Encrypted both directions** | TLS 1.2+ minimum in transit, at-rest encryption on every store holding sensitive data — database, object storage, and backups alike. Platform-managed keys are the baseline, not the upsell. |
| **PII tokenization** | One identity table per product. Everything else references UUIDs. No PII in logs, cache keys, or downstream tables. |
| **Validated in *and* out** | Inputs validated server-side, and every response scoped to an explicit schema — because an over-sharing endpoint fails silently and is far harder to notice than a crash. |
| **Rootless by default** | Rootless container runtime *and* non-root process, at both layers. Exceptions require a documented, approved reason. |
| **Default-deny networking** | Deny-by-default network policy in every namespace, egress filtered to known destinations, external access scoped to the port a pod actually serves. |
| **Supply chain discipline** | Every dependency pinned to an immutable, cryptographically verified reference — SHA256 digests for images, hashed requirements, full commit SHAs for CI actions. No `latest`, anywhere. |
| **Scanned before it ships** | SAST, DAST, dependency audit, container, IaC, and secrets scanning run in pre-commit and pre-push hooks — not just in CI where they're easy to ignore. |
| **90% coverage, enforced** | Lines, branches, functions, statements — every language. Builds fail below the threshold. Every bug reported gets a regression test before its issue closes. |

The reason to care: none of this is something you have to configure, buy as an add-on tier, or remember to turn on. It's how the software is built, so the secure path is the default path — and the paranoid can read every line of it.

---

## What this means for you

**If you run the infrastructure** — fewer pagers. Everything self-tests, health-checks, and scales horizontally; provisioning, data services, and access control speak the same identity model instead of four different ones.

**If you write the code** — stop caring whether you're on bare metal or which cloud. Deploy once, run anywhere, and pull MIT-licensed libraries off public registries instead of rebuilding auth and data access for the fourth time.

**If you sign the checks** — less risk and less complexity at the same time, without per-seat licensing on the core. The security work is already done and auditable, which is considerably cheaper than doing it after an incident.

---

## Guiding principles

- We make software that is secure, performant, and scalable.
- **What we deploy as open source features stays open source.** Always.
- We preserve as much freedom as we can for individual users outside of corporations.
- No shortcuts on safety, stability, or feature-completeness — no partial features with TODOs standing in for error handling.

## Free, Professional, Enterprise

The split is consistent across the portfolio, and the core is never the thing we hold back.

| Tier | Who it's for | What it adds |
|---|---|---|
| **Free / Community** | Individuals, non-commercial use, and small startups still finding their footing | The complete core product — not a trial, not a crippled demo |
| **Professional** | Established organizations, typically 50–150 people | Whitelabelling and Google OAuth2 SSO |
| **Enterprise** | Larger established companies, government, and regulated industries | SAML 2.0 / OIDC SSO, audit logging and compliance tooling, external KMS, advanced analytics, and WaddleAI |

Paid tiers gate advanced organizational capabilities — the kind you only need once you have a compliance team. They never gate the product itself.

## Licensing

Most products are **AGPL-3.0 with a contributor and commercial-use exception**. In plain terms: use them, run them internally, modify them, and build on them freely — we only want to make sure nobody repackages and resells our work. Organizations that employ official contributors receive community-edition access under limited GPL-2.0 terms. The exception is **penguin-libs**, which is MIT and published to PyPI, npm, and Go module registries for anyone to use, commercially or otherwise.

Organizations employing official contributors get community-edition access under GPL-2.0 terms. See each repository's `LICENSE` for specifics.

Non-profits can reach out for a free self-hosted professional level license!

## Contributing

We'd genuinely like the help. Before you open a PR:

- Code follows the project's style and format guidelines
- Security and build scanners and tests all pass
- Contributions are offered without strings, by someone with the authority to do so

Check the employer GPL-2.0 notice in our licenses for recognized contributors.

## Current status

Building toward large-enterprise scale, and rebuilding selected pieces on what we learned the first time. Expect active development, frequent releases, and honest changelogs.

<div align="center">

**Found something broken? Open an issue.**
**Found something insecure? We run responsible disclosure — please report it privately rather than in a public issue.**

</div>
