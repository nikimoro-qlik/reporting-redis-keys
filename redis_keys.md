# `reporting-service` Redis keys

## Task Queues
| Key Name | Type | Description | Can be sharded by... | Contains PII? | Used by LUA scripts? |
|---------|---------|---------|---------|---------|---------|
| `reporting:ReportRequests` | List | Circular list of tenants in the queue, to implement Round Robin between shards | queue name | No | **Yes** (getMaxScript, getBatchScript, storeAndConsumeScript, removeFromQueueScript, lenScript, moveScript, parkScript, parkOrRequeueScript, moveParkedItemsToQueueScript, moveParkedItemsToQueueReturnFieldValuesScript) |
| `reporting:ReportRequests:deficit` | Hash | Keeps shard's deficit, to implement fairness | queue name | No | **Yes** (getMaxScript, getBatchScript, removeFromQueueScript, getDeficitsScript) |
| `reporting:ReportRequests:blacklist:<SHARD_ID>` | String | Used to flag a shard as blacklisted, no items will be dequeued for it | queue name | No | **Yes** (getMaxScript, getBatchScript, appendShardsToBlackListScript, getBlackListValuesByShardName, getBlackListedShardsListWithValues) |
| `reporting:ReportRequests:producecheck` | String | ??? | queue name | No | **Yes** (produceWidthIDScript) |
| `reporting:ReportRequests_<SHARD_ID>` | SortedSet | Used to store enqueued items for every shard | queue name | **Consumer driven** | **Yes** (getMaxScript, getBatchScript, storeAndConsumeScript, removeFromQueueScript, requeueItemsScript, lenScript, moveScript, parkScript, removeByFieldValueScript, removeByFieldPrefixScript, parkOrRequeueScript, moveParkedItemsToQueueScript, moveParkedItemsToQueueReturnFieldValuesScript, appendShardsToBlackListScript, getBlackListValuesByShardName, getBlackListedShardsListWithValues, produceWidthIDScript, restoreScript) |
| `reporting:ReportCallbackRequests` | List | Circular list of tenants in the queue, to implement Round Robin between shards | queue name | No | **Yes** (see above) |
| `reporting:ReportCallbackRequests:deficit` | Hash | Keeps shard's deficit, to implement fairness | queue name | No | **Yes** (see above) |
| `reporting:ReportCallbackRequests:blacklist:<SHARD_ID>` | String | Used to flag a shard as blacklisted, no items will be dequeued for it | queue name | No | **Yes** (see above) |
| `reporting:ReportCallbackRequests:producecheck` | String | ??? | queue name | No | **Yes** (see above) |
| `reporting:ReportCallbackRequests_<SHARD_ID>` | SortedSet | Used to store enqueued items for every shard | queue name | **Consumer driven** | **Yes** (see above) |
| `reporting:TaskRequests` | List | Circular list of tenants in the queue, to implement Round Robin between shards | queue name | No | **Yes** (see above) |
| `reporting:TaskRequests:deficit` | Hash | Keeps shard's deficit, to implement fairness | queue name | No | **Yes** (see above) |
| `reporting:TaskRequests:blacklist:<SHARD_ID>` | String | Used to flag a shard as blacklisted, no items will be dequeued for it | queue name | No | **Yes** (see above) |
| `reporting:TaskRequests:producecheck` | String | ??? | queue name | No | **Yes** (see above) |
| `reporting:TaskRequests_<SHARD_ID>` | SortedSet | Used to store enqueued items for every shard | queue name | **Consumer driven** | **Yes** (see above) |
| `reporting:TaskRwrRequests` | List | Circular list of tenants in the queue, to implement Round Robin between shards | queue name | No | **Yes** (see above) |
| `reporting:TaskRwrRequests:deficit` | Hash | Keeps shard's deficit, to implement fairness | queue name | No | **Yes** (see above) |
| `reporting:TaskRwrRequests:blacklist:<SHARD_ID>` | String | Used to flag a shard as blacklisted, no items will be dequeued for it | queue name | No | **Yes** (see above) |
| `reporting:TaskRwrRequests:producecheck` | String | ??? | queue name | No | **Yes** (see above) |
| `reporting:TaskRwrRequests_<SHARD_ID>` | SortedSet | Used to store enqueued items for every shard | queue name | **Consumer driven** | **Yes** (see above) |
| `reporting:TaskRetries` | List | Circular list of tenants in the queue, to implement Round Robin between shards | queue name | No | **Yes** (see above) |
| `reporting:TaskRetries:deficit` | Hash | Keeps shard's deficit, to implement fairness | queue name | No | **Yes** (see above) |
| `reporting:TaskRetries:blacklist:<SHARD_ID>` | String | Used to flag a shard as blacklisted, no items will be dequeued for it | queue name | No | **Yes** (see above) |
| `reporting:TaskRetries:producecheck` | String | ??? | queue name | No | **Yes** (see above) |
| `reporting:TaskRetries_<SHARD_ID>` | SortedSet | Used to store enqueued items for every shard | queue name | **Consumer driven** | **Yes** (see above) |
| `reporting:TaskCleanup` | List | Circular list of tenants in the queue, to implement Round Robin between shards | queue name | No | **Yes** (see above) |
| `reporting:TaskCleanup:deficit` | Hash | Keeps shard's deficit, to implement fairness | queue name | No | **Yes** (see above) |
| `reporting:TaskCleanup:blacklist:<SHARD_ID>` | String | Used to flag a shard as blacklisted, no items will be dequeued for it | queue name | No | **Yes** (see above) |
| `reporting:TaskCleanup:producecheck` | String | ??? | queue name | No | **Yes** (see above) |
| `reporting:TaskCleanup_<SHARD_ID>` | SortedSet | Used to store enqueued items for every shard | queue name | **Consumer driven** | **Yes** (see above) |
| `reporting:GeneratorRequests` | List | Circular list of tenants in the queue, to implement Round Robin between shards | queue name | No | **Yes** (see above) |
| `reporting:GeneratorRequests:deficit` | Hash | Keeps shard's deficit, to implement fairness | queue name | No | **Yes** (see above) |
| `reporting:GeneratorRequests:blacklist:<SHARD_ID>` | String | Used to flag a shard as blacklisted, no items will be dequeued for it | queue name | No | **Yes** (see above) |
| `reporting:GeneratorRequests:producecheck` | String | ??? | queue name | No | **Yes** (see above) |
| `reporting:GeneratorRequests_<SHARD_ID>` | SortedSet | Used to store enqueued items for every shard | queue name | **Consumer driven** | **Yes** (see above) |
| `reporting:GeneratorResponses` | List | Circular list of tenants in the queue, to implement Round Robin between shards | queue name | No | **Yes** (see above) |
| `reporting:GeneratorResponses:deficit` | Hash | Keeps shard's deficit, to implement fairness | queue name | No | **Yes** (see above) |
| `reporting:GeneratorResponses:blacklist:<SHARD_ID>` | String | Used to flag a shard as blacklisted, no items will be dequeued for it | queue name | No | **Yes** (see above) |
| `reporting:GeneratorResponses:producecheck` | String | ??? | queue name | No | **Yes** (see above) |
| `reporting:GeneratorResponses_<SHARD_ID>` | SortedSet | Used to store enqueued items for every shard | queue name | **Consumer driven** | **Yes** (see above) |
| `<ITEM_UUID>`: | String | Keepalive key for an item in the queue | queue name | No | **Yes** (see above) |
| `reporting:parkhashes:<TENANT_ID>:<CONN_TYPE>:<APP_ID>:<USER_ID>:<SELECTION_HASH>` | Hash ||| **Consumer driven** | **Yes** (parkOrRequeueScript, moveParkedItemsToQueueScript, moveParkedItemsToQueueReturnFieldValuesScript) |
| `reporting:parkhashes:rdr-<SESSION_ID>` | Hash ||| **Consumer driven** | **Yes** (parkOrRequeueScript, moveParkedItemsToQueueScript, moveParkedItemsToQueueReturnFieldValuesScript) |

## Encryption Plain Key Cache
| Key Name | Type | Description | Can be sharded by... | Contains PII? | Used by LUA scripts? |
|---------|---------|---------|---------|---------|---------|
| `repsvc_file_info:` |||| No | No |

## Session Manager

`WORKLOAD_TYPE` can be `reporting-analytic` or `reporting-batch`

| Key Name | Type | Description | Can be sharded by... | Contains PII? | Used by LUA scripts? |
|---------|---------|---------|---------|---------|---------|
| `repsvc:qix.session:` ||||  **Yes** (JWT)  | No |
| `repsvc:<WORKLOAD_TYPE>:workload_session_count` | String ||| No | **Yes** (getSessionScript, removeSessionScript) |
| `repsvc:<WORKLOAD_TYPE>:workload_session_scan_start` | String ||| No | **Yes** (getSessionScript) |
| `repsvc:<WORKLOAD_TYPE>:session_count` | String ||| No | **Yes** (releaseSessionScript, setSessionActiveScript, getSessionScript, removeSessionScript) |
| `repsvc:<WORKLOAD_TYPE>:session_name` | String ||| No | **Yes** (setSessionActiveScript, getSessionScript, removeSessionScript) |
| `repsvc:<WORKLOAD_TYPE>:session_map` | SortedSet ||| ??? | **Yes** (releaseSessionScript, getSessionScript, removeSessionScript) |
| `repsvc:<WORKLOAD_TYPE>:session_queue_map` | SortedSet ||| ??? | **Yes** (scavangeForIdleParkedSessionsScript, releaseSessionScript, getSessionScript, cleanUpSessionScript) |
| `repsvc:<WORKLOAD_TYPE>:session_queue_count` | String ||| No | **Yes** (scavangeForIdleParkedSessionsScript, releaseSessionScript, getSessionScript, cleanUpSessionScript) |
| `repsvc:<WORKLOAD_TYPE>:session_queue_scavange_check` | String ||| No | **Yes** (scavangeForIdleParkedSessionsScript) |
| `repsvc:<WORKLOAD_TYPE>:session_queue_alive` | String ||| No | **Yes** (scavangeForIdleParkedSessionsScript, releaseSessionScript, getSessionScript) |
| `repsvc:<WORKLOAD_TYPE>:max_workload_sessions` | String ||| No | **Yes** (getSessionScript) |
| `repsvc:<WORKLOAD_TYPE>:max_sessions` | String ||| No | **Yes** (getSessionScript) |
| `repsvc:<WORKLOAD_TYPE>:parked_session_key` | String ||| ??? | **Yes** (scavangeForIdleParkedSessionsScript, getSessionScript, cleanUpSessionScript) |
| `repsvc:<WORKLOAD_TYPE>:parked_info_key` | Hash ||| ??? | **Yes** (scavangeForIdleParkedSessionsScript, releaseSessionScript, getSessionScript, cleanUpSessionScript) |
| `reporting:parkedsessions:<SESSION_ID>` | Hash ||| ??? | **Yes** (scavangeForIdleParkedSessionsScript, releaseSessionScript, getSessionScript, cleanUpSessionScript) |

## Permission Cache / Rate Limiter Cache
| Key Name | Type | Description | Can be sharded by... | Contains PII? | Used by LUA scripts? |
|---------|---------|---------|---------|---------|---------|
| `repsvc:cache:` || *[UNUSED]* This is a default value for key prefix into `RedisCache` || No | No |
| `repsvc:basic.consumer:<TENANT_ID>:<RESOURCE_TYPE>:<APP_ID>:<USER_ID>:<SUBJECT>` | String | Cache used by Access Control middleware || ??? | No |
| `repsvc:limiter:http` | String | Cache used by rate limiter on http calls || ??? | No |
| `repsvc:limiter:report` | String | Cache used by rate limiter on report generation || ??? | No |

## Report Processing
| Key Name | Type | Description | Can be sharded by... | Contains PII? | Used by LUA scripts? |
|---------|---------|---------|---------|---------|---------|
| `repsvc_save_request_status_lock:<REQUEST_ID>` | String | Ensures synchronous access when saving Request Status || No | **Yes** (exclusiveScript) |
| `repsvc_report_hash:<REPORT_ID>` | Hash ||| **Yes** (cycleSelections) | **Yes** (calculateFinalRequestStatusScript, abortRunningReportsScript, ScanHashScript) |
| `repsvc_request_hash:<REQUEST_ID>` | Hash ||| **Yes** (reportRequest) | **Yes** (calculateFinalRequestStatusScript) |
| `repsvc_report_status_callback_count:<REPORT_ID>` | String ||| No | No |
| `repsvc_report_status_failures_count:<REPORT_ID>` | String ||| No | No |
| `repsvc_report_request:<REQUEST_ID>:running_reports` | Set ||| No | **Yes** (abortRunningReportsScript, addRequestRunningReportsScript, removeRequestRunningReportsScript) |
| `repsvc_selection_errors:<SESSION_ID>` | String ||| **Yes** (selection missing values) | No |
| `repsvc_report_export_errors:<TASK_ID>` | List ||| ??? | No |
| `repsvc_report_jwt:<REQUEST_ID>` | String ||| **Yes** (JWT) | No |
| `repsvc_report:<REPORT_ID>:session` | String ||| ??? | No |
| `repsvc_report:<REPORT_ID>:tasks` | SortedSet ||| No | **Yes** (scriptRegisterNewTaskAndItems, saveReportTaskStatusScript, abortReportTasksScript) |
| `repsvc:dist_res:resolved` | PubSub | PubSub channel name for "resolved" events in distributed resolver || No | **Yes** (setResolvedValuesScript) |
| `repsvc:dist_res:session:<SESSION_ID>` | Hash | Keeps lookup info used after session resolution by CQ || **Yes** (JWT) | **Yes** (getAndRemoveSessionInfoScript, setSessionInfoScript) |
| `repsvc:dist_res:value:<SESSION_ID>` | Hash | Keeps info returned by CQ when a session is made available || No | **Yes** (setResolvedValuesScript) |
| `repsvc_app_last_reload:<REQUEST_ID>` | Hash ||| No | No |
| `repsvc_app_reload_check:<REQUEST_ID>` | Hash ||| No | No |
| `repsvc_app_reload_complete:<REQUEST_ID>` | String ||| No | No |

## Template Tree / Content Tree
| Key Name | Type | Description | Can be sharded by... | Contains PII? | Used by LUA scripts? |
|---------|---------|---------|---------|---------|---------|
| `repsvc_report_ctree:1` | String ||| **Yes** | No |
| `repsvc_report_image_count:<REPORT_ID>` | String ||| No | No |
| `repsvc_report_object_count:<REPORT_ID>` | String ||| No | No |
| `repsvc_report_resource_cnode_data:<TASK_ID>` | String ||| **Yes** | No |
| `repsvc_report_resource_cnode:<TASK_ID>` | String ||| **Yes** | No |
| `repsvc_report_resource_completed_count:<REPORT_ID>` | String ||| No | No |
| `repsvc_report_resource_ctile:<TASK_ID>` | String ||| **Yes** | No |
| `repsvc_report_resource_status:<REPORT_ID>` | String ||| No | No |
| `repsvc_report_resource_tnode:<TASK_ID>` | String ||| **Yes** | **Yes** (scriptRegisterNewTaskAndItems) |

## Data Engineering
| Key Name | Type | Description | Can be sharded by... | Contains PII? | Used by LUA scripts? |
|---------|---------|---------|---------|---------|---------|
| `repsvc_report_de:<REPORT_ID>` | Hash| Contains info regarding Data Engineering || No | **Yes** (scriptUpdateDEStatCharge, scriptIncFailedDEStatCharge, scriptDESetMax, scriptDESetMin) |

## Bookmarks Management
| Key Name | Type | Description | Can be sharded by... | Contains PII? | Used by LUA scripts? |
|---------|---------|---------|---------|---------|---------|
| `repsvc_bookmark_ts:<BOOKMARK_ID>` | String ||| No | **Yes** (getBookmarkTsScript) |
| `repsvc_reset_bookmarks` | SortedSet ||| No | No |
| `repsvc_reset_bookmarks_destroy_lock:<APP_ID>` | String ||| No | **Yes** (exclusiveScript) |
| `repsvc_reset_bookmarks_requests:<BUCKET_ID>` | Set ||| No | No |
| `repsvc_temporary_reset_bookmark_expirations` | SortedSet||| No | **Yes** (rollExpiredKeysScript) |
| `repsvc_temporary_reset_bookmark_info:<BUCKET_ID>` | Hash ||| **Yes** (JWT) | No |
