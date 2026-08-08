---
name: botify-export-seo-data
description: Export a large Botify result set by wrapping a BQL query in an export job, poll it to completion, and collect the file — without accidentally spending export credits twice.
api: Botify API
base_url: https://api.botify.com/v1
generated: '2026-08-08'
method: generated
source: openapi/botify-api-swagger.json + https://developers.botify.com/docs/export-seo-data
operations:
  - createJob
  - getJobs
  - getJob
  - createUrlsExport
  - getUrlsExports
  - getUrlsExportStatus
---

# Export Botify data

Use this when the result set is larger than the 2,000 rows an interactive BQL call returns, or when the data
should land in your own warehouse rather than in a response body.

## Before you start

- Auth header: `Authorization: Token <YOUR_TOKEN>`.
- **Exports cost credits**, metered per web property: 1 credit per exported row, 0.1 credit per row linked to
  the links graph. There is no dry-run that avoids the charge.
- Separate hard limits apply: **50 CSV exports per day** and **100,000 URLs per CSV export**, and those
  counters are **shared with the Botify web application** — exports a colleague launches in URL Explorer come
  out of the same 50.

## Steps — generic export job

1. **Get a BQL query working first** with `projectQuery` (see `botify-query-seo-data`). Only promote a query
   to an export once it returns what you expect.

2. **Create the job.** `createJob` — `POST /jobs`. The job wraps the BQL query with metadata: the `job_type`,
   the output format, the destination backend, and the row count.
   - Formats: `csv`, `json`, `xml`, `sitemap`.
   - Backends: direct download (Botify stores the file and hands you a link), AWS S3, AWS Redshift,
     Google Cloud Storage, Google BigQuery.
   - The response carries the job id that manages the task.

3. **Poll.** `getJob` — `GET /jobs/{job_id}`. `getJobs` (`GET /jobs`, filterable by `job_type`, `project`,
   `analysis`) lists what is running. Poll on a back-off; there is no webhook, no callback and no event
   stream — Botify publishes no async notification surface at all.

4. **Collect.** For the direct-download backend, take the link from the completed job. For S3 / Redshift /
   GCS / BigQuery, the data lands in your own destination.

## Steps — analysis URL CSV export (the older, narrower path)

1. `createUrlsExport` — `POST /analyses/{username}/{project_slug}/{analysis_slug}/urls/export`.
   Returns the model id managing the task.
2. `getUrlsExportStatus` — `GET .../urls/export/{url_export_id}` for the status.
3. `getUrlsExports` — `GET .../urls/export` lists the export requests and their current status.

## The retry trap — read this

**There is no idempotency key anywhere in the Botify API.** `POST /jobs` and `POST .../urls/export` create a
new job on every call. If a request times out and you retry it blindly, you start a **second** export and
spend the credits twice.

Do this instead:
- Before retrying, call `getJobs` (or `getUrlsExports`) and check whether your job already exists.
- Treat error `1052` ("A CSV export is already running") and `1058` ("An advanced export is already running")
  as *your previous request succeeded* — poll, do not re-POST.
- Cap retries and never retry a create on a network timeout without listing first.

## Errors

Proprietary envelope, not RFC 9457: `{"error": {"error_code": "...", "message": "...", "error_detail": {...}}}`.
Relevant codes: `1006` Url export was not found · `1027` more than 10 fields requested · `1028` more than 1
multiple field requested · `1037` The requested task failed · `1052` / `1058` already running · `1059`
Advanced export was not found · `1060` The export failed · `1053` Too many requests (HTTP 429).
Full table: `errors/botify-problem-types.yml`.
