---
title: "API Version History"
source_url: https://docs.rundeck.com/docs/api/rundeck-api-versions.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# API Version History \| Current Version 58

This page documents changes to the Rundeck API through-out the versions. For usage references please see the [API Reference](https://docs.rundeck.com/docs/api/) page.

## API Version Number

| Current | Minimum | Deprecation |
|---------|---------|-------------|
| `58`    | `14`    | `17`        |

Current  
The current version number.

Minimum  
Minimum supported version.

Deprecation  
Future minimum version.

## Incubating Endpoints

These endpoints are in "Incubating" status, and are subject to change in future releases.

- (none)

## API Changes

Changes introduced by API Version number:

> **Deprecation Notice**
>
> API versions below `17` are *deprecated*. Clients using earlier versions should upgrade to use `17` as the minimum version before release `6.0.0` to avoid errors.

### Version 58

- Updated Endpoints:
  - [`GET /api/V/project/[PROJECT]/jobs/browse`](https://docs.rundeck.com/docs/api/#project-job-group-browse) - Optional query parameter `metaExclude`: comma-separated job metadata component names to omit after resolving `meta`. When `meta` includes `*`, the server expands `*` to the union of all registered job metadata component names, then removes excluded names (the literal `*` is not treated as a component name). For an explicit comma-separated `meta` list, excluded names are removed from that list. The parameter is ignored if the request URL uses an API version below 58.
  - [`GET /api/V/job/[ID]/meta`](https://docs.rundeck.com/docs/api/#get-job-ui-metadata) - Same optional `metaExclude` query parameter and resolution rules (API version 58+ only).

### Version 57

- Updated Endpoints:
  - [`GET /api/V/plugin/list`](https://docs.rundeck.com/docs/api/#list-installed-plugins) - Plugin list response `providerMetadata` now includes `groupBy` and `groupIconUrl` fields for plugin UI grouping
  - [`GET /api/V/plugin/detail/[SERVICE]/[PROVIDER]`](https://docs.rundeck.com/docs/api/#get-plugin-detail) - Plugin detail response `providerMetadata` now includes `groupBy` and `groupIconUrl` fields for plugin UI grouping
  - [`GET /api/V/executions/metrics`](https://docs.rundeck.com/docs/api/#execution-query-metrics)
    - Added `useStats` parameter: if `true`, use snapshot-based metrics from `SCHEDULED_EXECUTION_STATS` table. If `false` or not provided, use execution table query.
    - Added `groupByJob` parameter: if `true` with `useStats=true`, returns metrics for all jobs in the project (batch mode). Requires `project` parameter.
    - Added `begin` and `end` parameters for date range filtering when using `useStats=true`.
  - [`GET /api/V/project/[PROJECT]/executions/metrics`](https://docs.rundeck.com/docs/api/#execution-query-metrics)
    - Added `useStats` parameter: if `true`, use snapshot-based metrics from `SCHEDULED_EXECUTION_STATS` table. If `false` or not provided, use execution table query.
    - Added `groupByJob` parameter: if `true` with `useStats=true`, returns metrics for all jobs in the project (batch mode).
    - Added `begin` and `end` parameters for date range filtering when using `useStats=true`.

### Version 56

- Updated Endpoints:

  - [`GET /api/V/project/[PROJECT]/jobs`](https://docs.rundeck.com/docs/api/#listing-jobs) - Job listing responses now include audit tracking fields: `createdBy` (job creator username), `lastModifiedBy` (last modifier username), `created` (creation timestamp), and `lastModified` (last modification timestamp)
  - [`GET /api/18/job/[ID]/info`](https://docs.rundeck.com/docs/api/#get-job-metadata) - Job metadata response now includes audit tracking fields
  - Job Export endpoints now include audit tracking fields in exported job definitions

- Job Import Behavior:

  - Audit tracking fields (`user`, `createdBy`, `lastModifiedBy`, `created`, `lastModified`) are now protected during job import operations and will not be overwritten. These fields are managed by the system to maintain accurate audit history.

### Version 55

- New Endpoints:

  - [`POST /api/V/runnerManagement/runner/[RUNNERID]/replicas`](https://docs.rundeck.com/docs/api/#create-manual-runner-replica-at-project-level) - Create a new Runner Replica
  - [`POST /api/V/project/[PROJECT]/runnerManagement/runner/[RUNNERID]/replicas`](https://docs.rundeck.com/docs/api/#create-manual-runner-replica-at-project-level) - Create a new Runner Replica at Project Level
  - [`GET /api/V/runnerManagement/runner/[RUNNERID]/replicas`](https://docs.rundeck.com/docs/api/#list-runner-replicas) - List Runner Replicas
  - [`GET /api/V/project/[PROJECT]/runnerManagement/runner/[RUNNERID]/replicas`](https://docs.rundeck.com/docs/api/#list-runner-replicas-at-project-level) - List Runner Replicas at Project Level
  - [`DELETE /api/V/runnerManagement/runner/[RUNNERID]/replica/[REPLICAID]`](https://docs.rundeck.com/docs/api/#delete-manual-runner-replica) - Delete a Runner Replica
  - [`DELETE /api/V/project/[PROJECT]/runnerManagement/runner/[RUNNERID]/replica/[REPLICAID]`](https://docs.rundeck.com/docs/api/#delete-manual-runner-replica-at-project-level) - Delete a Runner Replica at Project Level

- Updated Endpoints:

  - [`POST /api/V/runnerManagement/runners`](https://docs.rundeck.com/docs/api/#create-a-new-runner) - Update the endpoint to create a new runner to include the optionals fields: `installationType` and `replicaType`. `InstallantionType` should have values of `linux`, `windows`, `docker` or `kubernetes` and `replicaType` should have values of `manual` or `ephemeral`. If not provided, they will default to `linux` and `manual` respectively.

### Version 52

- New Endpoints:
  - \[`GET /api/V/project/[PROJECT]/nodes/tags`\]\[GET GET /api/V/project/\[PROJECT\]/nodes/tags\] - Get tags for project nodes

### Version 51

- Updated Endpoints:
  - [`GET /api/V/plugin/list`](https://docs.rundeck.com/docs/api/#list-installed-plugins) - Plugin detail includes `isHighlighted` and `highlightedOrder`

### Version 50

- Updated Endpoints:
  - [`GET /api/V/job/[ID]/executions`](https://docs.rundeck.com/docs/api/#getting-executions-for-a-job) - Now supports `includeJobRef` parameter to include executions from job reference in the response

### Version 49

- New Endpoints:
  - [`GET /api/V/plugin/detail/[SERVICE]/[PROVIDER]`](https://docs.rundeck.com/docs/api/#get-plugin-detail) - Get Plugin Detail for a specific provider name

### Version 48

- Updated Endpoints:
  - [`GET /api/V/job/[ID]/forecast`](https://docs.rundeck.com/docs/api/#get-job-forecast) - Forecast now includes average duration, and information if the project has executions and scheduling disabled

### Version 46

- New Endpoints
  - [`GET /api/46/project/[PROJECT]/jobTags/query`](https://docs.rundeck.com/docs/api/#query-project-job-tags-enterprise) - Query Project Job Tags (Commercial)
  - [`GET /api/46/job/[ID]/tags`](https://docs.rundeck.com/docs/api/#get-job-tags-enterprise) - Get Job Tags (Commercial)
  - [`GET /api/46/project/[PROJECT]/meta`](https://docs.rundeck.com/docs/api/#get-project-ui-metadata) - Get Project UI Metadata
  - [`GET /api/46/project/[PROJECT]/jobs/browse`](https://docs.rundeck.com/docs/api/#project-job-group-browse) - Project Job Group browse
  - [`GET /api/46/job/[ID]/meta`](https://docs.rundeck.com/docs/api/#get-job-ui-metadata) - Get Job UI Metadata
  - [`POST /api/46/project/[PROJECT]/scm/toggle`](https://docs.rundeck.com/docs/api/#toggle-scm-for-a-project) - Toggle SCM for a Project

### Version 45

- [Delete Project API](https://docs.rundeck.com/api/#project-deletion) runs in deferred mode if v45+ is used. Specify `?deferred=false` to run in synchronous mode.
  - [`DELETE /api/45/project/[PROJECT]`](https://docs.rundeck.com/docs/api/#project-deletion) - Project Deletion

### Version 44

- JSON format added to Job Export and Import APIs. Specify `Accept: application/json` or `?format=json` when exporting, and `Content-Type: application/json` or `?format=json` when importing.
  - [`POST /api/14/project/[PROJECT]/jobs/import`](https://docs.rundeck.com/docs/api/#importing-jobs) - Job Import
  - [`GET /api/44/job/[ID]`](https://docs.rundeck.com/docs/api/#getting-a-job-definition) - Single Job Export
  - [`GET /api/44/project/[PROJECT]/jobs/export`](https://docs.rundeck.com/docs/api/#exporting-jobs) - Project Jobs Export

### Version 43

- Execution log and state ouput returns extended metadata if API v43+ is used.
  - [`GET /api/43/execution/[ID]/output/state`](https://docs.rundeck.com/docs/api/#execution-output-with-state) - Execution output with state
  - [`GET /api/43/execution/[ID]/output`](https://docs.rundeck.com/docs/api/#execution-output) - Get Execution log output

### Version 42

- Endpoints promoted out of incubating status. These endpoints no longer contain `incubating/` in the endpoint URL, and now require API version 42 minimum.
  - [`GET /api/42/feature/[FEATURE]`](https://docs.rundeck.com/docs/api/#get-a-system-feature-status) - Query system feature status for a feature.
  - [`GET /api/42/feature/`](https://docs.rundeck.com/docs/api/#get-all-system-feature-status) - Get all system feature statuses.
- New Endpoints:
  - [`GET /api/V/runnerManagement/checkPing/\[TOKEN\]`](https://docs.rundeck.com/docs/api/#check-a-ping-response) - Check a ping response
  - [`POST /api/V/runnerManagement/runner/\[ID\]/regenerateCreds`](https://docs.rundeck.com/docs/api/#regenerate-credentials-for-the-runner) - Regenerate credentials for the Runner
  - [`GET /api/V/runnerManagement/runner/\[ID\]/tags`](https://docs.rundeck.com/docs/api/#list-tags-for-the-runner) - List tags for the Runner
  - [`POST /api/V/runnerManagement/runners`](https://docs.rundeck.com/docs/api/#create-a-new-runner) - Create a new Runner
  - [`GET /api/V/runnerManagement/tags`](https://docs.rundeck.com/docs/api/#list-all-known-tags) - List all known tags
  - [`GET /api/V/runnerManagement/ui`](https://docs.rundeck.com/docs/api/#get-ui-info-for-runner-management) - Get UI info for runner management
  - [`GET /api/V/runnerTag/searchTags`](https://docs.rundeck.com/docs/api/#list-tags-for-the-runner) - List tags for the Runner

### Version 41

- Endpoints promoted out of incubating status. These endpoints no longer contain `incubating/` in the endpoint URL, and now require API version 41 minimum.
  - [`GET /api/V/enterprise/license`](https://docs.rundeck.com/docs/api/#view-license) - Get Enterprise license
  - [`POST /api/V/enterprise/license`](https://docs.rundeck.com/docs/api/#set-license-key) - Store Enterprise license
  - [`GET /api/V/project/[PROJECT]/calendars`](https://docs.rundeck.com/docs/api/#list-project-calendars) - Get Project Calendars (Enterprise only)
  - [`POST /api/V/project/[PROJECT]/calendars`](https://docs.rundeck.com/docs/api/#create-update-project-calendar) - Create/Update Project Calendars (Enterprise only)
  - [`DELETE /api/V/project/[PROJECT]/calendars/[ID]`](https://docs.rundeck.com/docs/api/#delete-project-calendar) - Delete a Project Calendar (Enterprise only)
  - [`GET /api/V/system/calendars`](https://docs.rundeck.com/docs/api/#list-system-calendars) - Get System Calendars (Enterprise only)
  - [`POST /api/V/system/calendars`](https://docs.rundeck.com/docs/api/#create-update-system-calendar) - Create/Update System Calendars (Enterprise only)
  - [`DELETE /api/V/system/calendars/[ID]`](https://docs.rundeck.com/docs/api/#delete-system-calendar) - Delete a System Calendar (Enterprise only)
- New Endpoints:
  - [`POST /api/V/enterprise/cluster/executions/enable`](https://docs.rundeck.com/docs/api/#set-active-mode-for-a-cluster-member-enterprise) - Set Active execution Mode for a cluster member
  - [`POST /api/V/enterprise/cluster/executions/disable`](https://docs.rundeck.com/docs/api/#set-passive-mode-for-a-cluster-member-enterprise) - Set Passive execution Mode for a cluster member
  - [`GET /api/V/runnerManagement/download/\[TOKEN\]`](https://docs.rundeck.com/docs/api/#download-runner-jar) - Download runner Jar
  - [`POST /api/V/runnerManagement/runner/\[ID\]/ping`](https://docs.rundeck.com/docs/api/#ping-the-runner) - Ping the runner
  - [`GET /api/V/runnerManagement/runner/\[RUNNERID\]`](https://docs.rundeck.com/docs/api/#get-runner-information) - Get runner information
  - [`POST /api/V/runnerManagement/runner/\[RUNNERID\]`](https://docs.rundeck.com/docs/api/#update-the-runner) - Update the runner
  - [`DELETE /api/V/runnerManagement/runner/\[RUNNERID\]`](https://docs.rundeck.com/docs/api/#delete-the-specified-runner) - Delete the specified runner
  - [`GET /api/V/runnerManagement/runners`](https://docs.rundeck.com/docs/api/#list-available-runners) - List available runners

### Version 40

- Updated Endpoints:
  - [`GET /api/V/plugin/list`](https://docs.rundeck.com/docs/api/#list-installed-plugins) - Plugin detail includes `iconUrl` and `providerMetadata`

### Version 39

- Removed support for previously deprecated API v10 and below. The minimum API version is now v11.

- XML Responses no longer support the request header of `X-Rundeck-API-XML-Response-Wrapper: true`. A `<result>` element will now only be returned in some endpoints where explicitly documented.

- When returning an error response, JSON will be sent by default if no `Accept:` header is specified, instead of XML.

- Removed Endpoints:

  - `/api/1/executions/running` replacement: [`/api/14/project/[PROJECT*]/executions/running`](https://docs.rundeck.com/docs/api/#listing-running-executions)
  - `/api/1/executions` replacement: [`/api/14/project/[PROJECT]/executions`](https://docs.rundeck.com/docs/api/#execution-query)
  - `/api/1/history` replacement: [`/api/14/project/[PROJECT]/history`](https://docs.rundeck.com/docs/api/#listing-history)
  - `/api/1/jobs/export` replacement: [`/api/14/project/[PROJECT]/jobs/export`](https://docs.rundeck.com/docs/api/#exporting-jobs)
  - `/api/1/jobs/import` replacement: [`/api/14/project/[PROJECT]/jobs/import`](https://docs.rundeck.com/docs/api/#importing-jobs)
  - `/api/1/jobs` replacement: [`/api/14/project/[PROJECT]/jobs`](https://docs.rundeck.com/docs/api/#listing-jobs)
  - `/api/1/resource/[NAME]` replacement: [`/api/14/project/[PROJECT]/resource/[NAME]`](https://docs.rundeck.com/docs/api/#getting-resource-info)
  - `/api/1/resources(/*)` replacement: [`/api/14/project/[PROJECT]/resources`](https://docs.rundeck.com/docs/api/#listing-resources)
  - `/api/1/run/command` replacement: [`/api/14/project/[PROJECT]/run/command`](https://docs.rundeck.com/docs/api/#running-adhoc-commands)
  - `/api/1/run/script` replacement: [`/api/14/project/[PROJECT]/run/script`](https://docs.rundeck.com/docs/api/#running-adhoc-scripts)
  - `/api/1/run/url` replacement: [`/api/14/project/[PROJECT]/run/url`](https://docs.rundeck.com/docs/api/#running-adhoc-script-urls)

  **Replacement endpoints above require v14**

### Version 38

- Updated Endpoint:
  - [`PUT /api/V/project/[PROJECT]/import`](https://docs.rundeck.com/docs/api/#project-archive-import) - Added `importNodesSources` parameter to define if Node Resources Source will be imported

### Version 36

- Updated Response:
  - [`GET /api/V/system/executions/status`](https://docs.rundeck.com/docs/api/#get-current-execution-mode) - If Rundeck is in passive mode, the call will now return a 503 error code.

### Version 35

- Updated Response:
  - [`PUT /api/V/project/[PROJECT]/import`](https://docs.rundeck.com/docs/api/#project-archive-import) - More validation and error message results added.

### Version 34

- New Endpoints:
  - [`GET /api/V/job/[ID]/workflow`](https://docs.rundeck.com/docs/api/#get-job-workflow) - Get the job workflow tree

### Version 33

- New Endpoints:

  - [`POST /api/V/webhook/[AUTH_TOKEN]`](https://docs.rundeck.com/docs/api/#send-webhook-event) - Trigger a webhook with the payload as the body of the post
  - [`GET /api/V/project/[PROJECT]/webhooks`](https://docs.rundeck.com/docs/api/#list-project-webhooks) - Lists the webhooks configured for the project
  - [`GET /api/V/project/[PROJECT]/webhook/[ID]`](https://docs.rundeck.com/docs/api/#list-project-webhooks) - Get the webhook identified by ID
  - [`POST /api/V/project/[PROJECT]/webhook/[ID]`](https://docs.rundeck.com/docs/api/#list-project-webhooks) - Create or update the webhook identified by ID. When creating a new webhook ID is not provided.
  - [`DELETE /api/V/project/[PROJECT]/webhook/[ID]`](https://docs.rundeck.com/docs/api/#list-project-webhooks) - Delete the webhook identified by ID
  - [`GET /api/V/plugin/list`](https://docs.rundeck.com/docs/api/#list-installed-plugins) - List the installed plugins.

- Updated Endpoints:

  - [`GET /api/V/projects`](https://docs.rundeck.com/docs/api/#listing-projects) - project creation date to response.

### Version 32

- New Endpoint:

  - [`GET /api/V/system/executions/status`](https://docs.rundeck.com/docs/api/#get-current-execution-mode) - Gets the current execution mode.

- Updated Endpoints:

  - [`GET /api/V/project/[PROJECT]/executions/running`](https://docs.rundeck.com/docs/api/#listing-running-executions) - Added `jobIdFilter` parameter to return running executions for a specific job.
  - [`GET /api/V/job/[ID]/forecast`](https://docs.rundeck.com/docs/api/#get-job-forecast) - Added `past` parameter to return inverse forecast.
  - [`PUT /api/V/scheduler/takeover`](https://docs.rundeck.com/docs/api/#takeover-schedule-in-cluster-mode) - Added capability to specify multiple job ids.

### Version 31

- New Endpoint:
  - [`GET /api/V/job/[ID]/forecast`](https://docs.rundeck.com/docs/api/#get-job-forecast) - Get a forecast for a specific amount of days of the job by ID.

### Version 30

- Updated Endpoints:
  - [`GET /api/V/user/roles`](https://docs.rundeck.com/docs/api/#list-roles) - List the roles of the authenticated user

### Version 29

- New Endpoints:
  - [`GET /api/V/executions/metrics`](https://docs.rundeck.com/docs/api/#execution-query-metrics) - Get metrics over a system-wide execution query.
  - [`GET /api/V/project/[PROJECT]/executions/metrics`](https://docs.rundeck.com/docs/api/#execution-query-metrics) - Get metrics over a project-wide execution query.

### Version 28

- Updated Endpoints:
  - [`GET /api/V/project/[PROJECT]/export`](https://docs.rundeck.com/docs/api/#project-archive-export) - exportScm parameter.
  - [`PUT /api/V/project/[PROJECT]/import`](https://docs.rundeck.com/docs/api/#project-archive-import) - importScm parameter.

### Version 27

- Updated Endpoints:
  - [`GET /api/V/user/list`](https://docs.rundeck.com/docs/api/#list-users) - More info from the user.

### Version 26

- Updated Endpoints:
  - [`GET /api/V/projects`](https://docs.rundeck.com/docs/api/#listing-projects) - label to projects response.

### Version 25

- New Endpoints.

  - [`GET /api/V/metrics`](https://docs.rundeck.com/docs/api/#list-metrics) - List enabled Metrics endpoints
  - [`GET /api/V/metrics/metrics`](https://docs.rundeck.com/docs/api/#metrics-data) - Get Metrics Data
  - [`GET /api/V/metrics/threads`](https://docs.rundeck.com/docs/api/#metrics-threads) - Get Metrics Threads
  - [`GET /api/V/metrics/healthcheck`](https://docs.rundeck.com/docs/api/#metrics-healthcheck) - Get Metrics Healthcheck
  - [`GET /api/V/metrics/ping`](https://docs.rundeck.com/docs/api/#metrics-ping) - Get Metrics Ping

- Updated Endpoints:

  - [`GET /api/V/system/info`](https://docs.rundeck.com/docs/api/#system-info) - `metrics` links now point to correct API endpoints.

### Version 24

- New Endpoints.
  - [`POST /api/V/job/[ID]/retry/[EXECID]`](https://docs.rundeck.com/docs/api/#retry-a-job-based-on-execution) - Retry a Job based on execution

### Version 23

- New Endpoints. (replacing removed `POST /api/2/project/[PROJECT]/resources` endpoint)
  - [`GET /api/V/project/[PROJECT]/sources`](https://docs.rundeck.com/docs/api/#list-resource-model-sources-for-a-project) - List project resource model sources
  - [`GET /api/V/project/[PROJECT]/source/[INDEX]`](https://docs.rundeck.com/docs/api/#get-a-resource-model-source-for-a-project) - Get a specific project resource model source by index
  - [`GET /api/V/project/[PROJECT]/source/[INDEX]/resources`](https://docs.rundeck.com/docs/api/#list-resources-of-a-resource-model-source) - Get Nodes content from a specific resource model source by index
  - [`POST /api/V/project/[PROJECT]/source/[INDEX]/resources`](https://docs.rundeck.com/docs/api/#update-resources-of-a-resource-model-source) - Update Nodes content for a specific Writeable resource model source by index
- Updated Endpoints.
  - [`GET /api/V/project/[PROJECT]/resources`](https://docs.rundeck.com/docs/api/#listing-resources) - Default response format is `application/json` for API v23 and later
  - [`GET /api/V/project/[PROJECT]/resource/[NAME]`](https://docs.rundeck.com/docs/api/#getting-resource-info) - Default response format is `application/json` for API v23 and later

### Version 22

- Updated Endpoints.
  - [`GET /api/V/project/[PROJECT]/scm/[INTEGRATION]/action/[ACTION_ID]/input`](https://docs.rundeck.com/docs/api/#get-project-scm-action-input-fields) - Include Job `status`, and `deleted` whether the job file was deleted for Import integration
  - [`POST /api/V/project/[PROJECT]/scm/[INTEGRATION]/action/[ACTION_ID]`](https://docs.rundeck.com/docs/api/#perform-project-scm-action) - Can include `deletedJobs` to delete jobs for Import integration.

### Version 21

- Removed Endpoints.
  - `POST /api/2/project/[PROJECT]/resources`
  - `POST /api/2/project/[PROJECT]/resources/refresh`
- Updated Endpoints.
  - [`/api/21/execution/[ID]/output`](https://docs.rundeck.com/docs/api/#execution-output) - Execution output, supports `compacted=true` query parameter for less verbose xml/json results
- New Endpoints.
  - [`GET /api/21/user/list`](https://docs.rundeck.com/docs/api/#list-users) - List user profiles

  - [`GET /api/21/user/info`](https://docs.rundeck.com/docs/api/#get-user-profile) - Get current user profile

  - [`POST /api/21/user/info`](https://docs.rundeck.com/docs/api/#modify-user-profile) - Modify current user profile

  - [`GET /api/21/user/info/[USER]`](https://docs.rundeck.com/docs/api/#get-another-user-profile) - Get another user's profile

  - [`POST /api/21/user/info/[USER]`](https://docs.rundeck.com/docs/api/#modify-another-user-profile) - Modify another user's profile

### Version 20

- Updated Endpoints.
  - [`GET /api/20/project/[PROJECT]/executions`](https://docs.rundeck.com/docs/api/#execution-query) - Executions query, add `executionTypeFilter`

### Version 19

- New Endpoints.

  - [`POST /api/19/job/[ID]/input/file`](https://docs.rundeck.com/docs/api/#upload-a-file-for-a-job-option) - Upload file(s) to use for job option values
  - [`GET /api/19/job/[ID]/input/files`](https://docs.rundeck.com/docs/api/#list-files-uploaded-for-a-job) - List uploaded files for a job
  - [`GET /api/19/execution/[ID]/input/files`](https://docs.rundeck.com/docs/api/#list-input-files-for-an-execution) - List input files used for an execution
  - [`GET /api/19/jobs/file/[ID]`](https://docs.rundeck.com/docs/api/#get-info-about-an-uploaded-file) - Get info for an uploaded file
  - [`GET /api/19/project/[PROJECT]/export/async`](https://docs.rundeck.com/docs/api/#project-archive-export-async) - Async project archive export
  - [`GET /api/19/project/[PROJECT]/export/status/[TOKEN]`](https://docs.rundeck.com/docs/api/#project-archive-export-async-status) - Async project archive export status
  - [`GET /api/19/project/[PROJECT]/export/download/[TOKEN]`](https://docs.rundeck.com/docs/api/#project-archive-export-async-download) - Async project archive export download

- Updated Endpoints.

  - [`POST /api/19/tokens/[USER]`](https://docs.rundeck.com/docs/api/#create-a-token) - Specify token roles and expiration
  - [`GET /api/19/tokens/[USER]`](https://docs.rundeck.com/docs/api/#list-tokens) - List tokens for users
  - [`GET /api/19/token/[ID]`](https://docs.rundeck.com/docs/api/#get-a-token) - Get Token string for Token ID
  - [`GET /api/19/project/[PROJECT]/export`](https://docs.rundeck.com/docs/api/#project-archive-export) - Additional parameters to select archive contents.

### Version 18

- New Endpoints.
  - [`GET /api/18/job/[ID]/info`](https://docs.rundeck.com/docs/api/#get-job-metadata) - Get metadata about a Job: Project name and scheduling info.
- Updated Endpoints:
  - [`/api/18/job/[ID]/run`](https://docs.rundeck.com/docs/api/#running-a-job)
    - new `runAtTime` parameter to run once at a certain time.
    - Job options can now be specified separately outside of the `argString`. Use `option.NAME=value` parameters, or specify `options` entry in JSON body.
- Updated responses for Executions
  - Executions results include custom status strings.
  - Documented `timedout`,`failed-with-retry`, and `scheduled` status values.
  - See [Listing Running Executions](https://docs.rundeck.com/docs/api/#listing-running-executions)

### Version 17

- New Endpoints.

  - [`/api/17/scheduler/server/[UUID]/jobs`](https://docs.rundeck.com/docs/api/#list-scheduled-jobs-for-a-cluster-server) - List scheduled jobs owned by the server with given UUID.
  - [`/api/17/scheduler/jobs`](https://docs.rundeck.com/docs/api/#list-scheduled-jobs-for-this-cluster-server) - List scheduled jobs owned by the target server.
  - [`/api/17/system/logstorage`](https://docs.rundeck.com/docs/api/#log-storage-info) - Get stats about the Log File storage system.
  - [`/api/17/system/logstorage/incomplete`](https://docs.rundeck.com/docs/api/#list-executions-with-incomplete-log-storage) - List all executions with incomplete logstorage.
  - [`/api/17/system/logstorage/incomplete/resume`](https://docs.rundeck.com/docs/api/#resume-incomplete-log-storage) - Resume incomplete log storage processing.

- Updated Endpoints.

  - [`/api/17/project/[PROJECT]/jobs`](https://docs.rundeck.com/docs/api/#listing-jobs)
    - Response now includes whether a job is enabled, scheduled, schedule is enabled, and in Cluster mode includes the cluster mode server UUID of the schedule owner, and whether that is the current server or not.
    - add `?scheduledFilter=true/false` returns scheduled/unscheduled jobs only
    - and `?serverNodeUUIDFilter=[uuid]` returns scheduled jobs owned by the given cluster member
  - [`/api/17/scheduler/takeover`](https://docs.rundeck.com/docs/api/#takeover-schedule-in-cluster-mode)
    - Response now includes previous scheduler owner UUID for jobs.
  - [`/api/17/scheduler/takeover`](https://docs.rundeck.com/docs/api/#takeover-schedule-in-cluster-mode) - Can specify a single job ID to takeover.

### Version 16

- New Endpoints.
  - [`/api/16/jobs/execution/enable`](https://docs.rundeck.com/docs/api/#bulk-toggle-job-execution) - Enable execution for multiple jobs
  - [`/api/16/jobs/execution/disable`](https://docs.rundeck.com/docs/api/#bulk-toggle-job-execution) - Disable execution for multiple jobs
  - [`/api/16/jobs/schedule/enable`](https://docs.rundeck.com/docs/api/#bulk-toggle-job-schedules) - Enable schedule for multiple jobs
  - [`/api/16/jobs/schedule/disable`](https://docs.rundeck.com/docs/api/#bulk-toggle-job-schedules) - Disable schedule for multiple jobs

### Version 15

- New Endpoints.
  - [`/api/15/project/[PROJECT]/scm/[INTEGRATION]/plugins`](https://docs.rundeck.com/docs/api/#list-scm-plugins) - List SCM plugins for a project.

  - [`/api/15/project/[PROJECT]/scm/[INTEGRATION]/plugin/[TYPE]/input`](https://docs.rundeck.com/docs/api/#get-scm-plugin-input-fields) - Get SCM plugin setup input fields.

  - [`/api/15/project/[PROJECT]/scm/[INTEGRATION]/plugin/[TYPE]/setup`](https://docs.rundeck.com/docs/api/#setup-scm-plugin-for-a-project) - Setup SCM for a project.

  - [`/api/15/project/[PROJECT]/scm/[INTEGRATION]/plugin/[TYPE]/enable`](https://docs.rundeck.com/docs/api/#enable-scm-plugin-for-a-project) - Enable SCM for a project.

  - [`/api/15/project/[PROJECT]/scm/[INTEGRATION]/plugin/[TYPE]/disable`](https://docs.rundeck.com/docs/api/#disable-scm-plugin-for-a-project) - Disable SCM for a project.

  - [`/api/15/project/[PROJECT]/scm/[INTEGRATION]/status`](https://docs.rundeck.com/docs/api/#get-project-scm-status) - Get SCM status for a project.

  - [`/api/15/project/[PROJECT]/scm/[INTEGRATION]/config`](https://docs.rundeck.com/docs/api/#get-project-scm-config) - Get SCM config for a project.

  - [`/api/15/project/[PROJECT]/scm/[INTEGRATION]/action/[ACTION_ID]/input`](https://docs.rundeck.com/docs/api/#get-project-scm-action-input-fields) - Get Project SCM Action Input Fields.

  - [`/api/15/project/[PROJECT]/scm/[INTEGRATION]/action/[ACTION_ID]`](https://docs.rundeck.com/docs/api/#perform-project-scm-action) - Perform SCM action for a project.

  - [`/api/15/job/[ID]/scm/[INTEGRATION]/status`](https://docs.rundeck.com/docs/api/#get-job-scm-status) - Get SCM status for a Job.

  - [`/api/15/job/[ID]/scm/[INTEGRATION]/action/[ACTION_ID]`](https://docs.rundeck.com/docs/api/#perform-job-scm-action) - Perform SCM action for a Job.

  - [`/api/15/job/[ID]/scm/[INTEGRATION]/action/[ACTION_ID]/input`](https://docs.rundeck.com/docs/api/#get-job-scm-action-input-fields) - Get Job SCM Action Input Fields

### Version 14

**Note**: this document now has an [Index](https://docs.rundeck.com/docs/api/#index) listing API paths.

- Deprecated Endpoints with no replacement
  - `/api/2/project/[PROJECT]/resources/refresh`
- New Endpoints
  - [`/api/14/system/executions/enable`](https://docs.rundeck.com/docs/api/#set-active-mode) - Enable executions (ACTIVE mode)
  - [`/api/14/system/executions/disable`](https://docs.rundeck.com/docs/api/#set-passive-mode) - Disable executions (PASSIVE mode)
  - [`/api/14/system/acl/*`](https://docs.rundeck.com/docs/api/#acls) - Manage system ACLs
  - [`/api/14/project/[PROJECT]/acl/*`](https://docs.rundeck.com/docs/api/#project-acls) - Manage project ACLs
  - [`/api/14/job/[ID]/execution/enable`](https://docs.rundeck.com/docs/api/#enable-executions-for-a-job) - Enable executions for a job
  - [`/api/14/job/[ID]/execution/disable`](https://docs.rundeck.com/docs/api/#disable-executions-for-a-job) - Disable executions for a job
  - [`/api/14/job/[ID]/schedule/enable`](https://docs.rundeck.com/docs/api/#enable-scheduling-for-a-job) - Enable scheduling for a job
  - [`/api/14/job/[ID]/schedule/disable`](https://docs.rundeck.com/docs/api/#disable-scheduling-for-a-job) - Disable scheduling for a job
- New Endpoints, replacing deprecated versions:
  - [`/api/14/project/[PROJECT*]/executions/running`](https://docs.rundeck.com/docs/api/#listing-running-executions)
  - [`/api/14/project/[PROJECT]/executions`](https://docs.rundeck.com/docs/api/#execution-query)
  - [`/api/14/project/[PROJECT]/history`](https://docs.rundeck.com/docs/api/#listing-history)
  - [`/api/14/project/[PROJECT]/jobs/export`](https://docs.rundeck.com/docs/api/#exporting-jobs)
  - [`/api/14/project/[PROJECT]/jobs/import`](https://docs.rundeck.com/docs/api/#importing-jobs)
  - [`/api/14/project/[PROJECT]/resource/[NAME]`](https://docs.rundeck.com/docs/api/#getting-resource-info)
  - `/api/14/project/[PROJECT]/resources(/*)`
  - [`/api/14/project/[PROJECT]/run/command`](https://docs.rundeck.com/docs/api/#running-adhoc-commands)
  - [`/api/14/project/[PROJECT]/run/script`](https://docs.rundeck.com/docs/api/#running-adhoc-scripts)
  - [`/api/14/project/[PROJECT]/run/url`](https://docs.rundeck.com/docs/api/#running-adhoc-script-urls)
- Added JSON support for endpoints, when using API v14:
  - [`/api/14/execution/[ID]/abort`](https://docs.rundeck.com/docs/api/#aborting-executions)
  - [`/api/14/execution/[ID]`](https://docs.rundeck.com/docs/api/#execution-info)
  - [`/api/14/job/[ID]/executions`](https://docs.rundeck.com/docs/api/#getting-executions-for-a-job)
  - [`/api/14/job/[ID]/run`](https://docs.rundeck.com/docs/api/#running-a-job) and [`POST /api/14/job/[ID]/executions`](https://docs.rundeck.com/docs/api/#running-a-job)
  - [`/api/14/jobs/delete`](https://docs.rundeck.com/docs/api/#bulk-job-delete)
  - [`/api/14/project/[PROJECT]/executions/running`](https://docs.rundeck.com/docs/api/#listing-running-executions)
  - [`/api/14/project/[PROJECT]/executions`](https://docs.rundeck.com/docs/api/#execution-query)
  - [`/api/14/project/[PROJECT]/history`](https://docs.rundeck.com/docs/api/#listing-history)
  - [`/api/14/project/[PROJECT]/jobs/import`](https://docs.rundeck.com/docs/api/#importing-jobs)
  - [`/api/14/project/[PROJECT]/jobs`](https://docs.rundeck.com/docs/api/#listing-jobs)
  - [`/api/14/project/[PROJECT]/resource/[NAME]`](https://docs.rundeck.com/docs/api/#getting-resource-info)
  - [`/api/14/project/[PROJECT]/resources`](https://docs.rundeck.com/docs/api/#listing-resources)
  - [`/api/14/project/[PROJECT]/run/command`](https://docs.rundeck.com/docs/api/#running-adhoc-commands)
  - [`/api/14/project/[PROJECT]/run/script`](https://docs.rundeck.com/docs/api/#running-adhoc-scripts)
  - [`/api/14/project/[PROJECT]/run/url`](https://docs.rundeck.com/docs/api/#running-adhoc-script-urls)
  - [`/api/14/system/info`](https://docs.rundeck.com/docs/api/#system-info)
- TODO json support:
  - [`/api/14/project/[PROJECT]/jobs/export`](https://docs.rundeck.com/docs/api/#exporting-jobs)
- Updated endpoints:
  - [`/api/14/job/[ID]/run`](https://docs.rundeck.com/docs/api/#running-a-job) action `GET` is no longer allowed (v14+), `POST` is required. For POST, this endpoint is now equivalent to `/api/14/job/[ID]/executions`. JSON request content is now supported.
  - [`/api/14/project/[PROJECT]/jobs/import`](https://docs.rundeck.com/docs/api/#importing-jobs)
    - Both XML and YAML job definitions can now be posted directly using the appropriate MIME type
    - Add API `href` and GUI `permalink` values into XML response
    - JSON response support
  - [`/api/14/project/[PROJECT]/jobs`](https://docs.rundeck.com/docs/api/#listing-jobs) - added API/GUI href/permalink to XML responses.
  - [`/api/14/execution/[ID]/abort`](https://docs.rundeck.com/docs/api/#aborting-executions) - added API/GUI href/permalink to XML responses.
  - [`/api/14/project/[PROJECT]/history`](https://docs.rundeck.com/docs/api/#listing-history) - added API/GUI href/permalink to XML responses.
  - `/api/14/project/[PROJECT]/run/*` - added API/GUI href/permalink to XML responses for adhoc command/script/url.
  - [`/api/14/system/info`](https://docs.rundeck.com/docs/api/#system-info) - added information about Rundeck Execution Mode
  - [`/api/14/project/[PROJECT]/import`](https://docs.rundeck.com/docs/api/#project-archive-import) - Added parameters for importing Configuration and ACL Policies from the archive.
- Endpoints promoted out of "incubator" status:
  - [`/api/14/scheduler/takeover`](https://docs.rundeck.com/docs/api/#takeover-schedule-in-cluster-mode) - Can specify `all` servers, or jobs within a specific `project`. Added API/GUI href/permalink to XML responses for adhoc command/script/url. Note: `href` was modified as mentioned below.
- Modified `href` meaning for XML responses:
  - Some endpoints that included a `href` value in XML responses used the link that was appropriate for an end user to use in a web browser, essentially the permalink to the GUI view for the linked object. When using API v14, these URLs now point to the API, and a new attribute `permalink` will be included to link to the GUI view for the object.
  - Using an API version 13 or earlier will retain the old behavior of `href` in XML responses.

Corrections:

- The response for [DELETE /api/V/job/\[ID\]](https://docs.rundeck.com/docs/api/#deleting-a-job-definition) incorrectly stated it would return XML response, when the actual response is `204 No Content`.

### Version 13

- New endpoints
  - `/api/13/project/[PROJECT]/readme.md` and `/api/13/project/[PROJECT]/motd.md`
    - [Project Readme File](https://docs.rundeck.com/docs/api/#project-readme-file) (`GET`, `PUT`, `DELETE`)

### Version 12

- New endpoints
  - `POST /api/12/executions/delete`
    - [Bulk delete executions](https://docs.rundeck.com/docs/api/#bulk-delete-executions)
- Updated endpoints
  - `DELETE /api/12/execution/[ID]`
    - [Delete an execution](https://docs.rundeck.com/docs/api/#delete-an-execution)
  - `DELETE /api/12/job/[ID]/executions`
    - [Delete all executions for a job](https://docs.rundeck.com/docs/api/#delete-all-executions-for-a-job)
  - `POST /api/12/job/[ID]/executions`
    - [Run a Job](https://docs.rundeck.com/docs/api/#running-a-job)

### Version 11

**Update**: The URL path for Token access was corrected.

In this version, all new and updated endpoints support XML or JSON request and response content where appropriate.

**Modified XML Response format**:

- For endpoints requiring API version 11 *only*, the default for XML responses is to *no longer* include a `<result>` element around the data.
- For API clients that expect to see the `<result>` element, a request header of `X-Rundeck-API-XML-Response-Wrapper: true` will restore it.
- For endpoint requests for API version 10 and earlier, the `<result>` element will be sent as it has been (described in \[Response Format\]\[\])

<!-- -->

- New endpoints
  - `/api/11/project/[PROJECT]/config`
    - PUT and GET for [Project Configuration](https://docs.rundeck.com/docs/api/#project-configuration)
  - `/api/11/project/[PROJECT]/config/[KEY]`
    - PUT, GET, DELETE for [Project Configuration Keys](https://docs.rundeck.com/docs/api/#project-configuration-keys)
  - `/api/11/project/[PROJECT]/export`
    - GET to retrieve archive of a project - [Project Archive Export](https://docs.rundeck.com/docs/api/#project-archive-export)
  - `/api/11/project/[PROJECT]/import`
    - PUT to import an archive to a project - [Project Archive Import](https://docs.rundeck.com/docs/api/#project-archive-import)
  - `/api/11/storage/keys/[PATH]`
    - GET, POST, PUT, DELETE: manage stored keys - [Key Storage](https://docs.rundeck.com/docs/api/#key-storage)
  - `/api/11/tokens`
    - GET: List all auth tokens - [List Tokens](https://docs.rundeck.com/docs/api/#list-tokens)
    - POST: Generate a token for a user - [Create a Token](https://docs.rundeck.com/docs/api/#create-a-token)
  - `/api/11/tokens/[user]`
    - GET: List auth tokens defined for a user - [List Tokens](https://docs.rundeck.com/docs/api/#list-tokens)
    - POST: Generate a token for a user - [Create a Token](https://docs.rundeck.com/docs/api/#create-a-token)
  - `/api/11/token/[tokenID]`
    - GET: get a token - [Get a token](https://docs.rundeck.com/docs/api/#get-a-tokens)
    - DELETE: delete a token - [Delete a Token](https://docs.rundeck.com/docs/api/#delete-a-token)
- Updated endpoints
  - `/api/11/project/[PROJECT]`
    - DELETE method can delete a project - [Project Deletion](https://docs.rundeck.com/docs/api/#project-deletion)
    - GET method response updated - [Getting Project Info](https://docs.rundeck.com/docs/api/#getting-project-info)
  - `/api/11/projects`
    - POST method can be used to create a new project - [Project creation](https://docs.rundeck.com/docs/api/#project-creation)

### Version 10

- New endpoints
  - `/api/10/execution/[ID]/state` - [Execution State](https://docs.rundeck.com/docs/api/#execution-state)
    - Retrieve workflow step and node state information
  - `/api/10/execution/[ID]/output/state` - [Execution Output with State](https://docs.rundeck.com/docs/api/#execution-output-with-state)
    - Retrieve log output with state change information
  - `/api/10/execution/[ID]/output/node/[NODENAME]` and `/api/10/execution/[ID]/output/step/[STEPCTX]` - [Execution Output](https://docs.rundeck.com/docs/api/#execution-output)
    - Retrieve log output for a particular node or step
    - Can combine both node and step context
- Updated endpoints
  - `/api/10/execution/[ID]` - [Execution Info](https://docs.rundeck.com/docs/api/#execution-info)
    - added `successfulNodes` and `failedNodes` detail.
    - added `job/options` data

### Version 9

- Updated endpoints
  - `/api/9/executions/running` - [Listing Running Executions](https://docs.rundeck.com/docs/api/#listing-running-executions)
    - Allow `project=*` to list running executions across all projects
    - Result data now includes `project` attribute for each `<execution>`.
  - `/api/9/jobs/import` - [Importing Jobs](https://docs.rundeck.com/docs/api/#importing-jobs)
    - Add `uuidOption` parameter to allow removing imported UUIDs to avoid creation conflicts.

### Version 8

- Updated endpoints
  - `/api/8/run/script` and `/api/8/run/url` - [Running Adhoc Scripts](https://docs.rundeck.com/docs/api/#running-adhoc-scripts) and [Running Adhoc Script URLs](https://docs.rundeck.com/docs/api/#running-adhoc-script-urls)
    - Added two optional parameters for `scriptInterpreter` and `interpreterArgsQuoted`
  - `/api/8/jobs/import` - [Importing Jobs](https://docs.rundeck.com/docs/api/#importing-jobs)
    - Added an optional parameter `project` which will override any project defined in the Job definition contexts. If used, the job definitions do not need a `project` value in them.
- Removed endpoints
  - `/api/1/report/create`
    - Removed due to History no longer supporting arbitrary event reports.

### Version 7

- Add **Incubator** endpoint
  - PUT `/api/7/incubator/jobs/takeoverSchedule` - [Takeover Schedule in Cluster Mode](https://docs.rundeck.com/docs/api/#takeover-schedule-in-cluster-mode)
    - incubating feature for cluster mode schedule takeover

### Version 6

- Updated endpoints
  - `/api/6/execution/[ID]/output` - [Execution Output](https://docs.rundeck.com/docs/api/#execution-output)
    - XML format has changed for API v6: entry log content is now specified as a `log` attribute value
    - The old XML format will still be used for queries using `/api/5`
    - Fixed invalid XML when no format was specified and XML was used by default
    - **documentation typo fixed**: the JSON format incorrectly specified the log text key as 'mesg', corrected to 'log'

### Version 5

Added in Rundeck 1.4.6, 1.5.1:

- New feature for some endpoints:

  - new `asUser` parameter can record an action (run or abort) as having been performed by another user
  - Affected endpoints
    - [Running a Job](https://docs.rundeck.com/docs/api/#running-a-job)
    - [Running Adhoc Commands](https://docs.rundeck.com/docs/api/#running-adhoc-commands)
    - [Running Adhoc Scripts](https://docs.rundeck.com/docs/api/#running-adhoc-scripts)
    - [Running Adhoc Script URLs](https://docs.rundeck.com/docs/api/#running-adhoc-script-urls)
    - [Aborting Executions](https://docs.rundeck.com/docs/api/#aborting-executions)

- New endpoint

  - `/api/5/jobs/delete` - [Bulk Job Delete](https://docs.rundeck.com/docs/api/#bulk-job-delete)

- New endpoint

  - `/api/5/execution/[ID]/output` - [Execution Output](https://docs.rundeck.com/docs/api/#execution-output)

- New endpoint

  - `/api/5/executions` - [Execution Query](https://docs.rundeck.com/docs/api/#execution-query)

- Updated endpoints

  - `/api/1/history` - [Listing History](https://docs.rundeck.com/docs/api/#listing-history)
    - new filter parameters added for including or excluding reports for exact job group/name values: `jobListFilter` and `excludeJobListFilter`

### Version 4

- New endpoint
  - `/api/4/run/url` - [Running Adhoc Script URLs](https://docs.rundeck.com/docs/api/#running-adhoc-script-urls)

### Version 3

- Updated endpoints
  - `/api/1/resources` - [Listing Resources](https://docs.rundeck.com/docs/api/#listing-resources)
    - `format` parameter can now use any supported Resource Format Parser format name.
  - `/api/2/project/[PROJECT]/resources` - [Updating and Listing Resources for a Project](https://docs.rundeck.com/docs/api/#updating-and-listing-resources-for-a-project)
    - `POST` request Content-Type can be any MIME type supported by a Resource Format Parser plugin.

### Version 2

- New endpoints
  - `/api/2/project/[PROJECT]/jobs` - [Listing Jobs for a Project](https://docs.rundeck.com/docs/api/#listing-jobs-for-a-project)
  - `/api/2/project/[PROJECT]/resources` - [Updating and Listing Resources for a Project](https://docs.rundeck.com/docs/api/#updating-and-listing-resources-for-a-project)
  - `/api/2/project/[PROJECT]/resources/refresh` - [Refreshing Resources for a Project](https://docs.rundeck.com/docs/api/#refreshing-resources-for-a-project)
- Updated endpoints
  - `/api/1/jobs` - [Listing Jobs](https://docs.rundeck.com/docs/api/#listing-jobs)
    - Additional parameters added
