# Botify

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Botify is an enterprise organic-search and AI-search visibility platform that crawls a brand's website, ingests its server logs, and joins that with Google Search Console, analytics and third-party data to produce thousands of SEO metrics across its SiteCrawler, LogAnalyzer, RealKeywords, ActionBoard, AlertPanel, SpeedWorkers, PageWorkers and EngagementAnalytics products. All of that data is reachable programmatically through the Botify REST API at api.botify.com/v1, which is documented with Swagger/OpenAPI and driven by BQL (Botify Query Language), a JSON DSL used both for interactive queries (up to 2,000 rows per call) and for large export jobs delivered to direct download, AWS S3, AWS Redshift, Google Cloud Storage or Google BigQuery. Botify also operates a hosted, OAuth-protected MCP server ("Botify Agents MCP") at mcp.botify.com so agents can work with Botify data alongside the company's own AI agents.

**Areas:** SEO · Organic search · Web Crawling · Log Analysis · Search Console · Marketing Analytics · AI Search · Data Export · MCP · Agent-Native

## Botify on APIs.io

Everything profiled for Botify is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/botify/](https://apis.io/providers/botify/)** — or go straight to one of the APIs or properties below.

### APIs (9)

- [Botify Agents MCP](https://apis.io/apis/botify/botify-agents-mcp/) — Hosted Model Context Protocol server at mcp.botify.com, advertised via RFC 9728 protected-resource metadata as "Botify Agents MCP" with the single scope…
- [Botify Analysis API](https://apis.io/apis/botify/botify-analysis-api/) — The Analysis API from Botify — 30 operation(s) for analysis.
- [Botify Collections API](https://apis.io/apis/botify/botify-collections-api/) — The Collections API from Botify — 2 operation(s) for collections.
- [Botify Job API](https://apis.io/apis/botify/botify-job-api/) — The Job API from Botify — 2 operation(s) for job.
- [Botify Keywords Groups API](https://apis.io/apis/botify/botify-keywordsgroups-api/) — The KeywordsGroups API from Botify — 1 operation(s) for keywordsgroups.
- [Botify Project API](https://apis.io/apis/botify/botify-project-api/) — The Project API from Botify — 9 operation(s) for project.
- [Botify Project Query API](https://apis.io/apis/botify/botify-projectquery-api/) — The ProjectQuery API from Botify — 1 operation(s) for projectquery.
- [Botify User API](https://apis.io/apis/botify/botify-user-api/) — The User API from Botify — 1 operation(s) for user.
- [Botify Data Source API](https://apis.io/apis/botify/botify-data-source-api/) — The Data Source API from Botify — 1 operation(s) for data source.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [Botify Agents MCP](https://apis.io/servers/botify/botify-agents-mcp/)

#### Collections (8)

Postman and Open Collection request collections.

- [Botify Analysis API](https://apis.io/collections/botify/open-botify-analysis-api/)
- [Botify Collections API](https://apis.io/collections/botify/open-botify-collections-api/)
- [Botify Datasource API](https://apis.io/collections/botify/open-botify-datasource-api/)
- [Botify Job API](https://apis.io/collections/botify/open-botify-job-api/)
- [Botify Keywords Groups API](https://apis.io/collections/botify/open-botify-keywordsgroups-api/)
- [Botify Project API](https://apis.io/collections/botify/open-botify-project-api/)
- [Botify Project Query API](https://apis.io/collections/botify/open-botify-projectquery-api/)
- [Botify User API](https://apis.io/collections/botify/open-botify-user-api/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Botify Api Swagger Overlay](https://apis.io/overlays/botify/botify-api-swagger-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Botify Authentication](https://apis.io/security/botify/botify-authentication/)
- [Botify Domain Security](https://apis.io/security/botify/botify-domain-security/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Botify Scopes](https://apis.io/scopes/botify/botify-scopes/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.botify.com/)
- [Documentation](https://developers.botify.com/docs/introduction)
- [Getting started](https://developers.botify.com/docs/getting-started)
- [API reference](https://developers.botify.com/reference/getalluserprojects-1)
- [Pricing](https://www.botify.com/pricing)
- [Sign up](https://app.botify.com/)
- [Support](https://support.botify.com/)
- [Changelog](https://developers.botify.com/changelog)
- [Blog](https://www.botify.com/blog)
- [Terms of service](https://www.botify.com/privacy-and-terms)
- [Privacy policy](https://www.botify.com/privacy-and-terms)
- [GitHub](https://github.com/botify-labs)
- [Status](https://status.botify.com/)

## API Evangelist rating

**Kin Score 45.3** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 71.7 |
| Contract quality | 45.3 |
| Contract governance | 18.2 |
| Operational transparency | 26.3 |
| Developer ergonomics | 51.8 |
| Access clarity | 39.5 |

**Agent readiness 44.6** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | documented (partial credit) |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | paginated |
| Operation Distinctiveness | distinct |

**Regulatory alignment 39.2** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/botify/](https://apis.io/providers/botify/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Botify: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/botify/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
