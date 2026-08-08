---
name: botify-query-seo-data
description: Run an interactive BQL query against a Botify project and read back up to 2,000 rows of SEO data, after discovering which collections and fields that project actually has.
api: Botify API
base_url: https://api.botify.com/v1
generated: '2026-08-08'
method: generated
source: openapi/botify-api-swagger.json + https://developers.botify.com/docs/querying-seo-data
operations:
  - getAllUserProjects
  - getProjectAnalyses
  - getProjectCollections
  - getCollectionDetail
  - getUrlsDatamodel
  - projectQuery
  - getProjectUrlsAggs
---

# Query Botify SEO data with BQL

Use this when you need SEO metrics out of Botify **now**, in a single call, for a bounded result set.
For anything larger than 2,000 rows, use `botify-export-seo-data` instead.

## Before you start

- Auth: every request carries `Authorization: Token <YOUR_TOKEN>` and `Content-Type: application/json`.
  The token is unscoped and long-lived (`authentication/botify-authentication.yml`).
- Rate limit: **5 requests/second** on project endpoints. There is no `Retry-After` header — self-throttle.
  Exceeding it returns HTTP 429 with `error_code` `1053`.

## Steps

1. **Find the project.** `getAllUserProjects` (`GET /users/{username}/projects`) or
   `getUserProjects` (`GET /projects/{username}`) — paginated with `page` + `size`, response envelope is
   `{count, page, size, next, previous, results}`. Take the `slug`; that is `project_slug`.

2. **Find the analysis you want to query.** `getProjectAnalyses`
   (`GET /analyses/{username}/{project_slug}`) or the cheaper `getProjectAnalysesLight`.
   The `slug` of an analysis is a crawl date in `YYYYMMDD` form — that same string is the BQL collection name
   (`crawl.20210205`).

3. **Discover what the project actually holds — do not assume fields.** Field availability is per-project.
   - `getProjectCollections` (`GET /projects/{username}/{project_slug}/collections`) lists the collections.
   - `getCollectionDetail` (`GET /projects/{username}/{project_slug}/collections/{collection}`) lists that
     collection's fields.
   - `getUrlsDatamodel` (`GET /analyses/{username}/{project_slug}/{analysis_slug}/urls/datamodel`) gives the
     analysis datamodel; pass `deprecated_fields` only if you deliberately want fields Botify has deprecated.

4. **Run the query.** `projectQuery` — `POST /projects/{username}/{project_slug}/query`, optional
   `?page=&size=` (size defaults to 500). Body is BQL:

   ```json
   {
     "collections": ["crawl.20210205"],
     "query": {
       "dimensions": ["url", "crawl.20210205.depth", "crawl.20210205.http_code"],
       "metrics": [],
       "sort": [1]
     }
   }
   ```

5. **Aggregate instead of listing, when you only need counts.** `getProjectUrlsAggs`
   (`POST /projects/{username}/{project_slug}/urls/aggs`) accepts multiple queries executed across every
   completed analysis in the project; `getUrlsAggs` does the same scoped to one analysis.

6. **Page through the result.** Follow `next` until it is null, respecting the 5 QPS ceiling.

## Ceilings that will bite you

- **2,000 rows per interactive call.** Past that, switch to an export job.
- Error `1043` "The query is too big to execute it" and `1044` "Query can not be executed" mean narrow the
  query — fewer dimensions, tighter filters — or export.
- Error `1029` "Field does not exist" means you skipped step 3.
- Error `1034` / `1035` / `1036` / `1046` mean the feature is not enabled on that project's plan, not that
  your query is wrong.

## Errors

Botify does **not** use RFC 9457. A failure returns
`{"error": {"error_code": "1029", "message": "...", "error_detail": {...}}}` with HTTP 4xx. The numeric
`error_code` is the useful signal — the full 60-code table is in `errors/botify-problem-types.yml`.
