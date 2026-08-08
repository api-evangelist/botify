---
name: botify-audit-sitemaps-and-orphans
description: Audit a Botify analysis for sitemap problems, orphan URLs, robots.txt content and lost PageRank — the technical-SEO findings that live behind the analysis "features" endpoints.
api: Botify API
base_url: https://api.botify.com/v1
generated: '2026-08-08'
method: generated
source: openapi/botify-api-swagger.json + https://developers.botify.com/llms.txt
operations:
  - getProjectAnalyses
  - getSitemapsReport
  - getSitemapsSamplesOutOfConfig
  - getSitemapsSamplesSitemapsOnly
  - getVisitsOrphanURLs
  - getRobotsTxtIndexesView
  - getRobotsTxtFileView
  - getPageRankLost
  - getLinksPercentiles
  - getLinksTopDomains
  - getLinksTopSubdomains
  - getScoring
  - getUrlDetail
  - getUrlHTML
---

# Audit sitemaps, orphans and link structure in a Botify analysis

Everything here hangs off one completed analysis:
`/analyses/{username}/{project_slug}/{analysis_slug}/features/...`.
Get the `analysis_slug` from `getProjectAnalyses` first.

## Sitemaps

1. `getSitemapsReport` — `GET .../features/sitemaps/report` returns the global picture: sitemap indexes,
   sitemaps found, and invalid sitemap URLs. The `SitemapsReport` shape carries `sitemap_indexes[]`,
   `sitemaps[]` and `errors[]`, each a `SitemapsReportSitemap` with an optional nested `error`.
2. `getSitemapsSamplesOutOfConfig` — `GET .../features/sitemaps/samples/out_of_config` samples URLs found in
   the sitemaps but **outside the crawl perimeter** (domain/subdomain/protocol not allowed by project
   settings). These are usually a configuration bug, not a site bug.
3. `getSitemapsSamplesSitemapsOnly` — `GET .../features/sitemaps/samples/sitemap_only` samples URLs that are
   in the sitemaps, inside the allowed scope, and **were not found by the crawler** — i.e. unlinked.

## Orphan URLs

`getVisitsOrphanURLs` — `GET .../features/visits/orphan_urls/{medium}/{source}` lists URLs that generated
visits but were never crawled.

- `medium: organic` with `source` one of `all`, `aol`, `ask`, `baidu`, `bing`, `google`, `naver`, `yahoo`,
  `yandex`.
- `medium: social` with `source` one of `all`, `facebook`, `google+`, `linkedin`, `pinterest`, `reddit`,
  `tumblr`, `twitter`.
- `error_code` `1047` means orphans are not available for that combination.

**Do not use `getGanalyticsOrphanURLs`** (`.../features/ganalytics/orphan_urls/{medium}/{source}`) — Botify
labels it "Legacy" in its own published API index. It is *not* flagged `deprecated` in the Swagger, so nothing
in the contract will warn you; `getVisitsOrphanURLs` is the current operation.

## robots.txt

- `getRobotsTxtIndexesView` — `GET .../staticfiles/robots-txt-indexes` returns every robots.txt found across
  the project's domains. A `null` object means a virtual robots.txt.
- `getRobotsTxtFileView` — `GET .../staticfiles/robots-txt-indexes/{robots_txt}` returns one file's content.

## Link structure and scoring

- `getPageRankLost` — `GET .../features/pagerank/lost`
- `getLinksPercentiles` — `GET .../features/links/percentiles` (inlinks percentiles)
- `getLinksTopDomains` / `getLinksTopSubdomains` — `GET .../features/top_domains/domains` and `/subdomains`,
  each with `follow_samples[]` and `nofollow_samples[]`
- `getScoring` — `GET .../features/scoring/summary`

## Drilling into one URL

- `getUrlDetail` — `GET .../urls/{url}` for the crawled detail
- `getUrlHTML` — `GET .../urls/html/{url}` for the stored HTML
- `getUrlAI` — `GET .../urls/ai/{url}` for Botify's AI suggestions on that URL
- `error_code` `1017` means there is no result for that URL in this analysis.

## Feature gates

Several of these are plan- or project-gated and will fail with an *entitlement* error rather than a data
error: `1034` requested feature is disabled · `1035` comparison features disabled · `1036` Visits feature
disabled · `1046` Search Engines feature disabled. Treat these as "not purchased / not enabled", not as bugs.
Full code table: `errors/botify-problem-types.yml`.
