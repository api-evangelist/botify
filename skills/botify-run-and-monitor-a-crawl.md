---
name: botify-run-and-monitor-a-crawl
description: Launch a Botify analysis (crawl) for a project, watch it live through crawl statistics, pause or resume it, and read the finished summary.
api: Botify API
base_url: https://api.botify.com/v1
generated: '2026-08-08'
method: generated
source: openapi/botify-api-swagger.json + https://developers.botify.com/docs/getting-started
operations:
  - getAllUserProjects
  - launchAnalysisCreate
  - getProjectAnalyses
  - getAnalysisSummary
  - getCrawlStatistics
  - getCrawlStatisticsByFrequency
  - getCrawlStatisticsUrls
  - pauseAnalysis
  - resumeAnalysis
  - getAnalysisSegments
---

# Run and monitor a Botify crawl

## Before you start

- Auth header: `Authorization: Token <YOUR_TOKEN>`.
- 5 requests/second on project endpoints; HTTP 429 + `error_code` `1053` when exceeded, with no `Retry-After`.

## Steps

1. **Pick the project.** `getAllUserProjects` (`GET /users/{username}/projects`) — take `username` and the
   project `slug`.

2. **Launch the analysis.** `launchAnalysisCreate` —
   `POST /analyses/{username}/{project_slug}/create/launch`. Returns `201` with an
   `AnalysisCreateAndLaunch` payload.

   **This call is not idempotent.** There is no idempotency key on any Botify endpoint. If it times out, call
   `getProjectAnalyses` and check for a newly-created analysis before you POST again — a blind retry starts a
   second crawl.

3. **Watch it run.**
   - `getCrawlStatistics` — `GET /analyses/{username}/{project_slug}/{analysis_slug}/crawl_statistics`
     returns global statistics for the analysis.
   - `getCrawlStatisticsByFrequency` — `.../crawl_statistics/time?frequency=` groups the statistics by time
     bucket (1 min, 5 min or 60 min). Invalid values return `error_code` `1026`; a missing `frequency`
     returns `1025`.
   - `getCrawlStatisticsUrls` — `.../crawl_statistics/urls/{list_type}` returns the 1,000 most recently
     crawled URLs, either all of them or only those with HTTP errors.
   - `error_code` `1011` means crawl-statistics data is not available yet — back off and re-poll.

4. **Pause / resume if you need to.** `pauseAnalysis` (`POST .../pause`) and `resumeAnalysis`
   (`POST .../resume`).

5. **Read the finished crawl.** `getAnalysisSummary` — `GET /analyses/{username}/{project_slug}/{analysis_slug}`
   for the `AnalysisDetail`. `getAnalysisSegments` (`GET .../segments`) returns the segments feature's public
   metadata.

6. **Then query or export the data.** The analysis `slug` (a `YYYYMMDD` date) is the BQL collection name —
   hand it to `botify-query-seo-data` or `botify-export-seo-data`.

## Polling, because there are no events

Botify publishes **no webhooks, no event stream and no AsyncAPI**. Crawl progress and completion are only
observable by polling `getCrawlStatistics` / `getAnalysisSummary`. Budget your poll interval against the
5 QPS ceiling that is shared with everything else you are doing on the project.

## Errors

`1004` Analysis was not found · `1010` Project was not found · `1011` Crawl Statistics Data is currently not
available · `1025` / `1026` frequency problems · `1038` Cannot delete an already-launched planified crawl ·
`1002` Permission denied · `1053` Too many requests. Full table: `errors/botify-problem-types.yml`.
