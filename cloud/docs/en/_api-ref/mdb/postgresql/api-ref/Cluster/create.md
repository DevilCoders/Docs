---
editable: false
---

# Method create
Creates a PostgreSQL cluster in the specified folder.
 

 
## HTTP request {#https-request}
```
POST https://mdb.{{ api-host }}/managed-postgresql/v1/clusters
```
 
## Body parameters {#body_params}
 
```json 
{
  "folderId": "string",
  "name": "string",
  "description": "string",
  "labels": "object",
  "environment": "string",
  "configSpec": {
    "version": "string",
    "poolerConfig": {
      "poolingMode": "string",
      "poolDiscard": true
    },
    "resources": {
      "resourcePresetId": "string",
      "diskSize": "string",
      "diskTypeId": "string"
    },
    "autofailover": true,
    "backupWindowStart": {
      "hours": "integer",
      "minutes": "integer",
      "seconds": "integer",
      "nanos": "integer"
    },
    "backupRetainPeriodDays": "integer",
    "access": {
      "dataLens": true,
      "webSql": true,
      "serverless": true,
      "dataTransfer": true
    },
    "performanceDiagnostics": {
      "enabled": true,
      "sessionsSamplingInterval": "string",
      "statementsSamplingInterval": "string"
    },

    // `configSpec` includes only one of the fields `postgresqlConfig_9_6`, `postgresqlConfig_10_1C`, `postgresqlConfig_10`, `postgresqlConfig_11`, `postgresqlConfig_11_1C`, `postgresqlConfig_12`, `postgresqlConfig_12_1C`, `postgresqlConfig_13`, `postgresqlConfig_14`
    "postgresqlConfig_9_6": {
      "maxConnections": "integer",
      "sharedBuffers": "integer",
      "tempBuffers": "integer",
      "maxPreparedTransactions": "integer",
      "workMem": "integer",
      "maintenanceWorkMem": "integer",
      "replacementSortTuples": "integer",
      "autovacuumWorkMem": "integer",
      "tempFileLimit": "integer",
      "vacuumCostDelay": "integer",
      "vacuumCostPageHit": "integer",
      "vacuumCostPageMiss": "integer",
      "vacuumCostPageDirty": "integer",
      "vacuumCostLimit": "integer",
      "bgwriterDelay": "integer",
      "bgwriterLruMaxpages": "integer",
      "bgwriterLruMultiplier": "number",
      "bgwriterFlushAfter": "integer",
      "backendFlushAfter": "integer",
      "oldSnapshotThreshold": "integer",
      "walLevel": "string",
      "synchronousCommit": "string",
      "checkpointTimeout": "integer",
      "checkpointCompletionTarget": "number",
      "checkpointFlushAfter": "integer",
      "maxWalSize": "integer",
      "minWalSize": "integer",
      "maxStandbyStreamingDelay": "integer",
      "defaultStatisticsTarget": "integer",
      "constraintExclusion": "string",
      "cursorTupleFraction": "number",
      "fromCollapseLimit": "integer",
      "joinCollapseLimit": "integer",
      "forceParallelMode": "string",
      "clientMinMessages": "string",
      "logMinMessages": "string",
      "logMinErrorStatement": "string",
      "logMinDurationStatement": "integer",
      "logCheckpoints": true,
      "logConnections": true,
      "logDisconnections": true,
      "logDuration": true,
      "logErrorVerbosity": "string",
      "logLockWaits": true,
      "logStatement": "string",
      "logTempFiles": "integer",
      "searchPath": "string",
      "rowSecurity": true,
      "defaultTransactionIsolation": "string",
      "statementTimeout": "integer",
      "lockTimeout": "integer",
      "idleInTransactionSessionTimeout": "integer",
      "byteaOutput": "string",
      "xmlbinary": "string",
      "xmloption": "string",
      "ginPendingListLimit": "integer",
      "deadlockTimeout": "integer",
      "maxLocksPerTransaction": "integer",
      "maxPredLocksPerTransaction": "integer",
      "arrayNulls": true,
      "backslashQuote": "string",
      "defaultWithOids": true,
      "escapeStringWarning": true,
      "loCompatPrivileges": true,
      "operatorPrecedenceWarning": true,
      "quoteAllIdentifiers": true,
      "standardConformingStrings": true,
      "synchronizeSeqscans": true,
      "transformNullEquals": true,
      "exitOnError": true,
      "seqPageCost": "number",
      "randomPageCost": "number",
      "sqlInheritance": true,
      "autovacuumMaxWorkers": "integer",
      "autovacuumVacuumCostDelay": "integer",
      "autovacuumVacuumCostLimit": "integer",
      "autovacuumNaptime": "integer",
      "archiveTimeout": "integer",
      "trackActivityQuerySize": "integer",
      "effectiveIoConcurrency": "integer",
      "effectiveCacheSize": "integer"
    },
    "postgresqlConfig_10_1C": {
      "maxConnections": "integer",
      "sharedBuffers": "integer",
      "tempBuffers": "integer",
      "maxPreparedTransactions": "integer",
      "workMem": "integer",
      "maintenanceWorkMem": "integer",
      "replacementSortTuples": "integer",
      "autovacuumWorkMem": "integer",
      "tempFileLimit": "integer",
      "vacuumCostDelay": "integer",
      "vacuumCostPageHit": "integer",
      "vacuumCostPageMiss": "integer",
      "vacuumCostPageDirty": "integer",
      "vacuumCostLimit": "integer",
      "bgwriterDelay": "integer",
      "bgwriterLruMaxpages": "integer",
      "bgwriterLruMultiplier": "number",
      "bgwriterFlushAfter": "integer",
      "backendFlushAfter": "integer",
      "oldSnapshotThreshold": "integer",
      "walLevel": "string",
      "synchronousCommit": "string",
      "checkpointTimeout": "integer",
      "checkpointCompletionTarget": "number",
      "checkpointFlushAfter": "integer",
      "maxWalSize": "integer",
      "minWalSize": "integer",
      "maxStandbyStreamingDelay": "integer",
      "defaultStatisticsTarget": "integer",
      "constraintExclusion": "string",
      "cursorTupleFraction": "number",
      "fromCollapseLimit": "integer",
      "joinCollapseLimit": "integer",
      "forceParallelMode": "string",
      "clientMinMessages": "string",
      "logMinMessages": "string",
      "logMinErrorStatement": "string",
      "logMinDurationStatement": "integer",
      "logCheckpoints": true,
      "logConnections": true,
      "logDisconnections": true,
      "logDuration": true,
      "logErrorVerbosity": "string",
      "logLockWaits": true,
      "logStatement": "string",
      "logTempFiles": "integer",
      "searchPath": "string",
      "rowSecurity": true,
      "defaultTransactionIsolation": "string",
      "statementTimeout": "integer",
      "lockTimeout": "integer",
      "idleInTransactionSessionTimeout": "integer",
      "byteaOutput": "string",
      "xmlbinary": "string",
      "xmloption": "string",
      "ginPendingListLimit": "integer",
      "deadlockTimeout": "integer",
      "maxLocksPerTransaction": "integer",
      "maxPredLocksPerTransaction": "integer",
      "arrayNulls": true,
      "backslashQuote": "string",
      "defaultWithOids": true,
      "escapeStringWarning": true,
      "loCompatPrivileges": true,
      "operatorPrecedenceWarning": true,
      "quoteAllIdentifiers": true,
      "standardConformingStrings": true,
      "synchronizeSeqscans": true,
      "transformNullEquals": true,
      "exitOnError": true,
      "seqPageCost": "number",
      "randomPageCost": "number",
      "autovacuumMaxWorkers": "integer",
      "autovacuumVacuumCostDelay": "integer",
      "autovacuumVacuumCostLimit": "integer",
      "autovacuumNaptime": "integer",
      "archiveTimeout": "integer",
      "trackActivityQuerySize": "integer",
      "enableBitmapscan": true,
      "enableHashagg": true,
      "enableHashjoin": true,
      "enableIndexscan": true,
      "enableIndexonlyscan": true,
      "enableMaterial": true,
      "enableMergejoin": true,
      "enableNestloop": true,
      "enableSeqscan": true,
      "enableSort": true,
      "enableTidscan": true,
      "maxWorkerProcesses": "integer",
      "maxParallelWorkers": "integer",
      "maxParallelWorkersPerGather": "integer",
      "autovacuumVacuumScaleFactor": "number",
      "autovacuumAnalyzeScaleFactor": "number",
      "defaultTransactionReadOnly": true,
      "timezone": "string",
      "effectiveIoConcurrency": "integer",
      "effectiveCacheSize": "integer",
      "sharedPreloadLibraries": [
        "string"
      ],
      "autoExplainLogMinDuration": "integer",
      "autoExplainLogAnalyze": true,
      "autoExplainLogBuffers": true,
      "autoExplainLogTiming": true,
      "autoExplainLogTriggers": true,
      "autoExplainLogVerbose": true,
      "autoExplainLogNestedStatements": true,
      "autoExplainSampleRate": "number",
      "pgHintPlanEnableHint": true,
      "pgHintPlanEnableHintTable": true,
      "pgHintPlanDebugPrint": "string",
      "pgHintPlanMessageLevel": "string",
      "onlineAnalyzeEnable": true,
      "plantunerFixEmptyTable": true,
      "pgQualstatsEnabled": true,
      "pgQualstatsTrackConstants": true,
      "pgQualstatsMax": "integer",
      "pgQualstatsResolveOids": true,
      "pgQualstatsSampleRate": "number"
    },
    "postgresqlConfig_10": {
      "maxConnections": "integer",
      "sharedBuffers": "integer",
      "tempBuffers": "integer",
      "maxPreparedTransactions": "integer",
      "workMem": "integer",
      "maintenanceWorkMem": "integer",
      "replacementSortTuples": "integer",
      "autovacuumWorkMem": "integer",
      "tempFileLimit": "integer",
      "vacuumCostDelay": "integer",
      "vacuumCostPageHit": "integer",
      "vacuumCostPageMiss": "integer",
      "vacuumCostPageDirty": "integer",
      "vacuumCostLimit": "integer",
      "bgwriterDelay": "integer",
      "bgwriterLruMaxpages": "integer",
      "bgwriterLruMultiplier": "number",
      "bgwriterFlushAfter": "integer",
      "backendFlushAfter": "integer",
      "oldSnapshotThreshold": "integer",
      "walLevel": "string",
      "synchronousCommit": "string",
      "checkpointTimeout": "integer",
      "checkpointCompletionTarget": "number",
      "checkpointFlushAfter": "integer",
      "maxWalSize": "integer",
      "minWalSize": "integer",
      "maxStandbyStreamingDelay": "integer",
      "defaultStatisticsTarget": "integer",
      "constraintExclusion": "string",
      "cursorTupleFraction": "number",
      "fromCollapseLimit": "integer",
      "joinCollapseLimit": "integer",
      "forceParallelMode": "string",
      "clientMinMessages": "string",
      "logMinMessages": "string",
      "logMinErrorStatement": "string",
      "logMinDurationStatement": "integer",
      "logCheckpoints": true,
      "logConnections": true,
      "logDisconnections": true,
      "logDuration": true,
      "logErrorVerbosity": "string",
      "logLockWaits": true,
      "logStatement": "string",
      "logTempFiles": "integer",
      "searchPath": "string",
      "rowSecurity": true,
      "defaultTransactionIsolation": "string",
      "statementTimeout": "integer",
      "lockTimeout": "integer",
      "idleInTransactionSessionTimeout": "integer",
      "byteaOutput": "string",
      "xmlbinary": "string",
      "xmloption": "string",
      "ginPendingListLimit": "integer",
      "deadlockTimeout": "integer",
      "maxLocksPerTransaction": "integer",
      "maxPredLocksPerTransaction": "integer",
      "arrayNulls": true,
      "backslashQuote": "string",
      "defaultWithOids": true,
      "escapeStringWarning": true,
      "loCompatPrivileges": true,
      "operatorPrecedenceWarning": true,
      "quoteAllIdentifiers": true,
      "standardConformingStrings": true,
      "synchronizeSeqscans": true,
      "transformNullEquals": true,
      "exitOnError": true,
      "seqPageCost": "number",
      "randomPageCost": "number",
      "autovacuumMaxWorkers": "integer",
      "autovacuumVacuumCostDelay": "integer",
      "autovacuumVacuumCostLimit": "integer",
      "autovacuumNaptime": "integer",
      "archiveTimeout": "integer",
      "trackActivityQuerySize": "integer",
      "enableBitmapscan": true,
      "enableHashagg": true,
      "enableHashjoin": true,
      "enableIndexscan": true,
      "enableIndexonlyscan": true,
      "enableMaterial": true,
      "enableMergejoin": true,
      "enableNestloop": true,
      "enableSeqscan": true,
      "enableSort": true,
      "enableTidscan": true,
      "maxWorkerProcesses": "integer",
      "maxParallelWorkers": "integer",
      "maxParallelWorkersPerGather": "integer",
      "autovacuumVacuumScaleFactor": "number",
      "autovacuumAnalyzeScaleFactor": "number",
      "defaultTransactionReadOnly": true,
      "timezone": "string",
      "effectiveIoConcurrency": "integer",
      "effectiveCacheSize": "integer",
      "sharedPreloadLibraries": [
        "string"
      ],
      "autoExplainLogMinDuration": "integer",
      "autoExplainLogAnalyze": true,
      "autoExplainLogBuffers": true,
      "autoExplainLogTiming": true,
      "autoExplainLogTriggers": true,
      "autoExplainLogVerbose": true,
      "autoExplainLogNestedStatements": true,
      "autoExplainSampleRate": "number",
      "pgHintPlanEnableHint": true,
      "pgHintPlanEnableHintTable": true,
      "pgHintPlanDebugPrint": "string",
      "pgHintPlanMessageLevel": "string",
      "pgQualstatsEnabled": true,
      "pgQualstatsTrackConstants": true,
      "pgQualstatsMax": "integer",
      "pgQualstatsResolveOids": true,
      "pgQualstatsSampleRate": "number"
    },
    "postgresqlConfig_11": {
      "maxConnections": "integer",
      "sharedBuffers": "integer",
      "tempBuffers": "integer",
      "maxPreparedTransactions": "integer",
      "workMem": "integer",
      "maintenanceWorkMem": "integer",
      "autovacuumWorkMem": "integer",
      "tempFileLimit": "integer",
      "vacuumCostDelay": "integer",
      "vacuumCostPageHit": "integer",
      "vacuumCostPageMiss": "integer",
      "vacuumCostPageDirty": "integer",
      "vacuumCostLimit": "integer",
      "bgwriterDelay": "integer",
      "bgwriterLruMaxpages": "integer",
      "bgwriterLruMultiplier": "number",
      "bgwriterFlushAfter": "integer",
      "backendFlushAfter": "integer",
      "oldSnapshotThreshold": "integer",
      "walLevel": "string",
      "synchronousCommit": "string",
      "checkpointTimeout": "integer",
      "checkpointCompletionTarget": "number",
      "checkpointFlushAfter": "integer",
      "maxWalSize": "integer",
      "minWalSize": "integer",
      "maxStandbyStreamingDelay": "integer",
      "defaultStatisticsTarget": "integer",
      "constraintExclusion": "string",
      "cursorTupleFraction": "number",
      "fromCollapseLimit": "integer",
      "joinCollapseLimit": "integer",
      "forceParallelMode": "string",
      "clientMinMessages": "string",
      "logMinMessages": "string",
      "logMinErrorStatement": "string",
      "logMinDurationStatement": "integer",
      "logCheckpoints": true,
      "logConnections": true,
      "logDisconnections": true,
      "logDuration": true,
      "logErrorVerbosity": "string",
      "logLockWaits": true,
      "logStatement": "string",
      "logTempFiles": "integer",
      "searchPath": "string",
      "rowSecurity": true,
      "defaultTransactionIsolation": "string",
      "statementTimeout": "integer",
      "lockTimeout": "integer",
      "idleInTransactionSessionTimeout": "integer",
      "byteaOutput": "string",
      "xmlbinary": "string",
      "xmloption": "string",
      "ginPendingListLimit": "integer",
      "deadlockTimeout": "integer",
      "maxLocksPerTransaction": "integer",
      "maxPredLocksPerTransaction": "integer",
      "arrayNulls": true,
      "backslashQuote": "string",
      "defaultWithOids": true,
      "escapeStringWarning": true,
      "loCompatPrivileges": true,
      "operatorPrecedenceWarning": true,
      "quoteAllIdentifiers": true,
      "standardConformingStrings": true,
      "synchronizeSeqscans": true,
      "transformNullEquals": true,
      "exitOnError": true,
      "seqPageCost": "number",
      "randomPageCost": "number",
      "autovacuumMaxWorkers": "integer",
      "autovacuumVacuumCostDelay": "integer",
      "autovacuumVacuumCostLimit": "integer",
      "autovacuumNaptime": "integer",
      "archiveTimeout": "integer",
      "trackActivityQuerySize": "integer",
      "enableBitmapscan": true,
      "enableHashagg": true,
      "enableHashjoin": true,
      "enableIndexscan": true,
      "enableIndexonlyscan": true,
      "enableMaterial": true,
      "enableMergejoin": true,
      "enableNestloop": true,
      "enableSeqscan": true,
      "enableSort": true,
      "enableTidscan": true,
      "maxWorkerProcesses": "integer",
      "maxParallelWorkers": "integer",
      "maxParallelWorkersPerGather": "integer",
      "autovacuumVacuumScaleFactor": "number",
      "autovacuumAnalyzeScaleFactor": "number",
      "defaultTransactionReadOnly": true,
      "timezone": "string",
      "enableParallelAppend": true,
      "enableParallelHash": true,
      "enablePartitionPruning": true,
      "enablePartitionwiseAggregate": true,
      "enablePartitionwiseJoin": true,
      "jit": true,
      "maxParallelMaintenanceWorkers": "integer",
      "parallelLeaderParticipation": true,
      "vacuumCleanupIndexScaleFactor": "number",
      "effectiveIoConcurrency": "integer",
      "effectiveCacheSize": "integer",
      "sharedPreloadLibraries": [
        "string"
      ],
      "autoExplainLogMinDuration": "integer",
      "autoExplainLogAnalyze": true,
      "autoExplainLogBuffers": true,
      "autoExplainLogTiming": true,
      "autoExplainLogTriggers": true,
      "autoExplainLogVerbose": true,
      "autoExplainLogNestedStatements": true,
      "autoExplainSampleRate": "number",
      "pgHintPlanEnableHint": true,
      "pgHintPlanEnableHintTable": true,
      "pgHintPlanDebugPrint": "string",
      "pgHintPlanMessageLevel": "string",
      "pgQualstatsEnabled": true,
      "pgQualstatsTrackConstants": true,
      "pgQualstatsMax": "integer",
      "pgQualstatsResolveOids": true,
      "pgQualstatsSampleRate": "number"
    },
    "postgresqlConfig_11_1C": {
      "maxConnections": "integer",
      "sharedBuffers": "integer",
      "tempBuffers": "integer",
      "maxPreparedTransactions": "integer",
      "workMem": "integer",
      "maintenanceWorkMem": "integer",
      "autovacuumWorkMem": "integer",
      "tempFileLimit": "integer",
      "vacuumCostDelay": "integer",
      "vacuumCostPageHit": "integer",
      "vacuumCostPageMiss": "integer",
      "vacuumCostPageDirty": "integer",
      "vacuumCostLimit": "integer",
      "bgwriterDelay": "integer",
      "bgwriterLruMaxpages": "integer",
      "bgwriterLruMultiplier": "number",
      "bgwriterFlushAfter": "integer",
      "backendFlushAfter": "integer",
      "oldSnapshotThreshold": "integer",
      "walLevel": "string",
      "synchronousCommit": "string",
      "checkpointTimeout": "integer",
      "checkpointCompletionTarget": "number",
      "checkpointFlushAfter": "integer",
      "maxWalSize": "integer",
      "minWalSize": "integer",
      "maxStandbyStreamingDelay": "integer",
      "defaultStatisticsTarget": "integer",
      "constraintExclusion": "string",
      "cursorTupleFraction": "number",
      "fromCollapseLimit": "integer",
      "joinCollapseLimit": "integer",
      "forceParallelMode": "string",
      "clientMinMessages": "string",
      "logMinMessages": "string",
      "logMinErrorStatement": "string",
      "logMinDurationStatement": "integer",
      "logCheckpoints": true,
      "logConnections": true,
      "logDisconnections": true,
      "logDuration": true,
      "logErrorVerbosity": "string",
      "logLockWaits": true,
      "logStatement": "string",
      "logTempFiles": "integer",
      "searchPath": "string",
      "rowSecurity": true,
      "defaultTransactionIsolation": "string",
      "statementTimeout": "integer",
      "lockTimeout": "integer",
      "idleInTransactionSessionTimeout": "integer",
      "byteaOutput": "string",
      "xmlbinary": "string",
      "xmloption": "string",
      "ginPendingListLimit": "integer",
      "deadlockTimeout": "integer",
      "maxLocksPerTransaction": "integer",
      "maxPredLocksPerTransaction": "integer",
      "arrayNulls": true,
      "backslashQuote": "string",
      "defaultWithOids": true,
      "escapeStringWarning": true,
      "loCompatPrivileges": true,
      "operatorPrecedenceWarning": true,
      "quoteAllIdentifiers": true,
      "standardConformingStrings": true,
      "synchronizeSeqscans": true,
      "transformNullEquals": true,
      "exitOnError": true,
      "seqPageCost": "number",
      "randomPageCost": "number",
      "autovacuumMaxWorkers": "integer",
      "autovacuumVacuumCostDelay": "integer",
      "autovacuumVacuumCostLimit": "integer",
      "autovacuumNaptime": "integer",
      "archiveTimeout": "integer",
      "trackActivityQuerySize": "integer",
      "enableBitmapscan": true,
      "enableHashagg": true,
      "enableHashjoin": true,
      "enableIndexscan": true,
      "enableIndexonlyscan": true,
      "enableMaterial": true,
      "enableMergejoin": true,
      "enableNestloop": true,
      "enableSeqscan": true,
      "enableSort": true,
      "enableTidscan": true,
      "maxWorkerProcesses": "integer",
      "maxParallelWorkers": "integer",
      "maxParallelWorkersPerGather": "integer",
      "autovacuumVacuumScaleFactor": "number",
      "autovacuumAnalyzeScaleFactor": "number",
      "defaultTransactionReadOnly": true,
      "timezone": "string",
      "enableParallelAppend": true,
      "enableParallelHash": true,
      "enablePartitionPruning": true,
      "enablePartitionwiseAggregate": true,
      "enablePartitionwiseJoin": true,
      "jit": true,
      "maxParallelMaintenanceWorkers": "integer",
      "parallelLeaderParticipation": true,
      "vacuumCleanupIndexScaleFactor": "number",
      "effectiveIoConcurrency": "integer",
      "effectiveCacheSize": "integer",
      "sharedPreloadLibraries": [
        "string"
      ],
      "autoExplainLogMinDuration": "integer",
      "autoExplainLogAnalyze": true,
      "autoExplainLogBuffers": true,
      "autoExplainLogTiming": true,
      "autoExplainLogTriggers": true,
      "autoExplainLogVerbose": true,
      "autoExplainLogNestedStatements": true,
      "autoExplainSampleRate": "number",
      "pgHintPlanEnableHint": true,
      "pgHintPlanEnableHintTable": true,
      "pgHintPlanDebugPrint": "string",
      "pgHintPlanMessageLevel": "string",
      "pgQualstatsEnabled": true,
      "pgQualstatsTrackConstants": true,
      "pgQualstatsMax": "integer",
      "pgQualstatsResolveOids": true,
      "pgQualstatsSampleRate": "number"
    },
    "postgresqlConfig_12": {
      "maxConnections": "integer",
      "sharedBuffers": "integer",
      "tempBuffers": "integer",
      "maxPreparedTransactions": "integer",
      "workMem": "integer",
      "maintenanceWorkMem": "integer",
      "autovacuumWorkMem": "integer",
      "tempFileLimit": "integer",
      "vacuumCostDelay": "integer",
      "vacuumCostPageHit": "integer",
      "vacuumCostPageMiss": "integer",
      "vacuumCostPageDirty": "integer",
      "vacuumCostLimit": "integer",
      "bgwriterDelay": "integer",
      "bgwriterLruMaxpages": "integer",
      "bgwriterLruMultiplier": "number",
      "bgwriterFlushAfter": "integer",
      "backendFlushAfter": "integer",
      "oldSnapshotThreshold": "integer",
      "walLevel": "string",
      "synchronousCommit": "string",
      "checkpointTimeout": "integer",
      "checkpointCompletionTarget": "number",
      "checkpointFlushAfter": "integer",
      "maxWalSize": "integer",
      "minWalSize": "integer",
      "maxStandbyStreamingDelay": "integer",
      "defaultStatisticsTarget": "integer",
      "constraintExclusion": "string",
      "cursorTupleFraction": "number",
      "fromCollapseLimit": "integer",
      "joinCollapseLimit": "integer",
      "forceParallelMode": "string",
      "clientMinMessages": "string",
      "logMinMessages": "string",
      "logMinErrorStatement": "string",
      "logMinDurationStatement": "integer",
      "logCheckpoints": true,
      "logConnections": true,
      "logDisconnections": true,
      "logDuration": true,
      "logErrorVerbosity": "string",
      "logLockWaits": true,
      "logStatement": "string",
      "logTempFiles": "integer",
      "searchPath": "string",
      "rowSecurity": true,
      "defaultTransactionIsolation": "string",
      "statementTimeout": "integer",
      "lockTimeout": "integer",
      "idleInTransactionSessionTimeout": "integer",
      "byteaOutput": "string",
      "xmlbinary": "string",
      "xmloption": "string",
      "ginPendingListLimit": "integer",
      "deadlockTimeout": "integer",
      "maxLocksPerTransaction": "integer",
      "maxPredLocksPerTransaction": "integer",
      "arrayNulls": true,
      "backslashQuote": "string",
      "defaultWithOids": true,
      "escapeStringWarning": true,
      "loCompatPrivileges": true,
      "operatorPrecedenceWarning": true,
      "quoteAllIdentifiers": true,
      "standardConformingStrings": true,
      "synchronizeSeqscans": true,
      "transformNullEquals": true,
      "exitOnError": true,
      "seqPageCost": "number",
      "randomPageCost": "number",
      "autovacuumMaxWorkers": "integer",
      "autovacuumVacuumCostDelay": "integer",
      "autovacuumVacuumCostLimit": "integer",
      "autovacuumNaptime": "integer",
      "archiveTimeout": "integer",
      "trackActivityQuerySize": "integer",
      "enableBitmapscan": true,
      "enableHashagg": true,
      "enableHashjoin": true,
      "enableIndexscan": true,
      "enableIndexonlyscan": true,
      "enableMaterial": true,
      "enableMergejoin": true,
      "enableNestloop": true,
      "enableSeqscan": true,
      "enableSort": true,
      "enableTidscan": true,
      "maxWorkerProcesses": "integer",
      "maxParallelWorkers": "integer",
      "maxParallelWorkersPerGather": "integer",
      "autovacuumVacuumScaleFactor": "number",
      "autovacuumAnalyzeScaleFactor": "number",
      "defaultTransactionReadOnly": true,
      "timezone": "string",
      "enableParallelAppend": true,
      "enableParallelHash": true,
      "enablePartitionPruning": true,
      "enablePartitionwiseAggregate": true,
      "enablePartitionwiseJoin": true,
      "jit": true,
      "maxParallelMaintenanceWorkers": "integer",
      "parallelLeaderParticipation": true,
      "vacuumCleanupIndexScaleFactor": "number",
      "logTransactionSampleRate": "number",
      "planCacheMode": "string",
      "effectiveIoConcurrency": "integer",
      "effectiveCacheSize": "integer",
      "sharedPreloadLibraries": [
        "string"
      ],
      "autoExplainLogMinDuration": "integer",
      "autoExplainLogAnalyze": true,
      "autoExplainLogBuffers": true,
      "autoExplainLogTiming": true,
      "autoExplainLogTriggers": true,
      "autoExplainLogVerbose": true,
      "autoExplainLogNestedStatements": true,
      "autoExplainSampleRate": "number",
      "pgHintPlanEnableHint": true,
      "pgHintPlanEnableHintTable": true,
      "pgHintPlanDebugPrint": "string",
      "pgHintPlanMessageLevel": "string",
      "pgQualstatsEnabled": true,
      "pgQualstatsTrackConstants": true,
      "pgQualstatsMax": "integer",
      "pgQualstatsResolveOids": true,
      "pgQualstatsSampleRate": "number"
    },
    "postgresqlConfig_12_1C": {
      "maxConnections": "integer",
      "sharedBuffers": "integer",
      "tempBuffers": "integer",
      "maxPreparedTransactions": "integer",
      "workMem": "integer",
      "maintenanceWorkMem": "integer",
      "autovacuumWorkMem": "integer",
      "tempFileLimit": "integer",
      "vacuumCostDelay": "integer",
      "vacuumCostPageHit": "integer",
      "vacuumCostPageMiss": "integer",
      "vacuumCostPageDirty": "integer",
      "vacuumCostLimit": "integer",
      "bgwriterDelay": "integer",
      "bgwriterLruMaxpages": "integer",
      "bgwriterLruMultiplier": "number",
      "bgwriterFlushAfter": "integer",
      "backendFlushAfter": "integer",
      "oldSnapshotThreshold": "integer",
      "walLevel": "string",
      "synchronousCommit": "string",
      "checkpointTimeout": "integer",
      "checkpointCompletionTarget": "number",
      "checkpointFlushAfter": "integer",
      "maxWalSize": "integer",
      "minWalSize": "integer",
      "maxStandbyStreamingDelay": "integer",
      "defaultStatisticsTarget": "integer",
      "constraintExclusion": "string",
      "cursorTupleFraction": "number",
      "fromCollapseLimit": "integer",
      "joinCollapseLimit": "integer",
      "forceParallelMode": "string",
      "clientMinMessages": "string",
      "logMinMessages": "string",
      "logMinErrorStatement": "string",
      "logMinDurationStatement": "integer",
      "logCheckpoints": true,
      "logConnections": true,
      "logDisconnections": true,
      "logDuration": true,
      "logErrorVerbosity": "string",
      "logLockWaits": true,
      "logStatement": "string",
      "logTempFiles": "integer",
      "searchPath": "string",
      "rowSecurity": true,
      "defaultTransactionIsolation": "string",
      "statementTimeout": "integer",
      "lockTimeout": "integer",
      "idleInTransactionSessionTimeout": "integer",
      "byteaOutput": "string",
      "xmlbinary": "string",
      "xmloption": "string",
      "ginPendingListLimit": "integer",
      "deadlockTimeout": "integer",
      "maxLocksPerTransaction": "integer",
      "maxPredLocksPerTransaction": "integer",
      "arrayNulls": true,
      "backslashQuote": "string",
      "defaultWithOids": true,
      "escapeStringWarning": true,
      "loCompatPrivileges": true,
      "operatorPrecedenceWarning": true,
      "quoteAllIdentifiers": true,
      "standardConformingStrings": true,
      "synchronizeSeqscans": true,
      "transformNullEquals": true,
      "exitOnError": true,
      "seqPageCost": "number",
      "randomPageCost": "number",
      "autovacuumMaxWorkers": "integer",
      "autovacuumVacuumCostDelay": "integer",
      "autovacuumVacuumCostLimit": "integer",
      "autovacuumNaptime": "integer",
      "archiveTimeout": "integer",
      "trackActivityQuerySize": "integer",
      "enableBitmapscan": true,
      "enableHashagg": true,
      "enableHashjoin": true,
      "enableIndexscan": true,
      "enableIndexonlyscan": true,
      "enableMaterial": true,
      "enableMergejoin": true,
      "enableNestloop": true,
      "enableSeqscan": true,
      "enableSort": true,
      "enableTidscan": true,
      "maxWorkerProcesses": "integer",
      "maxParallelWorkers": "integer",
      "maxParallelWorkersPerGather": "integer",
      "autovacuumVacuumScaleFactor": "number",
      "autovacuumAnalyzeScaleFactor": "number",
      "defaultTransactionReadOnly": true,
      "timezone": "string",
      "enableParallelAppend": true,
      "enableParallelHash": true,
      "enablePartitionPruning": true,
      "enablePartitionwiseAggregate": true,
      "enablePartitionwiseJoin": true,
      "jit": true,
      "maxParallelMaintenanceWorkers": "integer",
      "parallelLeaderParticipation": true,
      "vacuumCleanupIndexScaleFactor": "number",
      "logTransactionSampleRate": "number",
      "planCacheMode": "string",
      "effectiveIoConcurrency": "integer",
      "effectiveCacheSize": "integer",
      "sharedPreloadLibraries": [
        "string"
      ],
      "autoExplainLogMinDuration": "integer",
      "autoExplainLogAnalyze": true,
      "autoExplainLogBuffers": true,
      "autoExplainLogTiming": true,
      "autoExplainLogTriggers": true,
      "autoExplainLogVerbose": true,
      "autoExplainLogNestedStatements": true,
      "autoExplainSampleRate": "number",
      "pgHintPlanEnableHint": true,
      "pgHintPlanEnableHintTable": true,
      "pgHintPlanDebugPrint": "string",
      "pgHintPlanMessageLevel": "string",
      "pgQualstatsEnabled": true,
      "pgQualstatsTrackConstants": true,
      "pgQualstatsMax": "integer",
      "pgQualstatsResolveOids": true,
      "pgQualstatsSampleRate": "number"
    },
    "postgresqlConfig_13": {
      "maxConnections": "integer",
      "sharedBuffers": "integer",
      "tempBuffers": "integer",
      "maxPreparedTransactions": "integer",
      "workMem": "integer",
      "maintenanceWorkMem": "integer",
      "autovacuumWorkMem": "integer",
      "tempFileLimit": "integer",
      "vacuumCostDelay": "integer",
      "vacuumCostPageHit": "integer",
      "vacuumCostPageMiss": "integer",
      "vacuumCostPageDirty": "integer",
      "vacuumCostLimit": "integer",
      "bgwriterDelay": "integer",
      "bgwriterLruMaxpages": "integer",
      "bgwriterLruMultiplier": "number",
      "bgwriterFlushAfter": "integer",
      "backendFlushAfter": "integer",
      "oldSnapshotThreshold": "integer",
      "walLevel": "string",
      "synchronousCommit": "string",
      "checkpointTimeout": "integer",
      "checkpointCompletionTarget": "number",
      "checkpointFlushAfter": "integer",
      "maxWalSize": "integer",
      "minWalSize": "integer",
      "maxStandbyStreamingDelay": "integer",
      "defaultStatisticsTarget": "integer",
      "constraintExclusion": "string",
      "cursorTupleFraction": "number",
      "fromCollapseLimit": "integer",
      "joinCollapseLimit": "integer",
      "forceParallelMode": "string",
      "clientMinMessages": "string",
      "logMinMessages": "string",
      "logMinErrorStatement": "string",
      "logMinDurationStatement": "integer",
      "logCheckpoints": true,
      "logConnections": true,
      "logDisconnections": true,
      "logDuration": true,
      "logErrorVerbosity": "string",
      "logLockWaits": true,
      "logStatement": "string",
      "logTempFiles": "integer",
      "searchPath": "string",
      "rowSecurity": true,
      "defaultTransactionIsolation": "string",
      "statementTimeout": "integer",
      "lockTimeout": "integer",
      "idleInTransactionSessionTimeout": "integer",
      "byteaOutput": "string",
      "xmlbinary": "string",
      "xmloption": "string",
      "ginPendingListLimit": "integer",
      "deadlockTimeout": "integer",
      "maxLocksPerTransaction": "integer",
      "maxPredLocksPerTransaction": "integer",
      "arrayNulls": true,
      "backslashQuote": "string",
      "defaultWithOids": true,
      "escapeStringWarning": true,
      "loCompatPrivileges": true,
      "operatorPrecedenceWarning": true,
      "quoteAllIdentifiers": true,
      "standardConformingStrings": true,
      "synchronizeSeqscans": true,
      "transformNullEquals": true,
      "exitOnError": true,
      "seqPageCost": "number",
      "randomPageCost": "number",
      "autovacuumMaxWorkers": "integer",
      "autovacuumVacuumCostDelay": "integer",
      "autovacuumVacuumCostLimit": "integer",
      "autovacuumNaptime": "integer",
      "archiveTimeout": "integer",
      "trackActivityQuerySize": "integer",
      "enableBitmapscan": true,
      "enableHashagg": true,
      "enableHashjoin": true,
      "enableIndexscan": true,
      "enableIndexonlyscan": true,
      "enableMaterial": true,
      "enableMergejoin": true,
      "enableNestloop": true,
      "enableSeqscan": true,
      "enableSort": true,
      "enableTidscan": true,
      "maxWorkerProcesses": "integer",
      "maxParallelWorkers": "integer",
      "maxParallelWorkersPerGather": "integer",
      "autovacuumVacuumScaleFactor": "number",
      "autovacuumAnalyzeScaleFactor": "number",
      "defaultTransactionReadOnly": true,
      "timezone": "string",
      "enableParallelAppend": true,
      "enableParallelHash": true,
      "enablePartitionPruning": true,
      "enablePartitionwiseAggregate": true,
      "enablePartitionwiseJoin": true,
      "jit": true,
      "maxParallelMaintenanceWorkers": "integer",
      "parallelLeaderParticipation": true,
      "vacuumCleanupIndexScaleFactor": "number",
      "logTransactionSampleRate": "number",
      "planCacheMode": "string",
      "effectiveIoConcurrency": "integer",
      "effectiveCacheSize": "integer",
      "sharedPreloadLibraries": [
        "string"
      ],
      "autoExplainLogMinDuration": "integer",
      "autoExplainLogAnalyze": true,
      "autoExplainLogBuffers": true,
      "autoExplainLogTiming": true,
      "autoExplainLogTriggers": true,
      "autoExplainLogVerbose": true,
      "autoExplainLogNestedStatements": true,
      "autoExplainSampleRate": "number",
      "pgHintPlanEnableHint": true,
      "pgHintPlanEnableHintTable": true,
      "pgHintPlanDebugPrint": "string",
      "pgHintPlanMessageLevel": "string",
      "hashMemMultiplier": "number",
      "logicalDecodingWorkMem": "integer",
      "maintenanceIoConcurrency": "integer",
      "maxSlotWalKeepSize": "integer",
      "walKeepSize": "integer",
      "enableIncrementalSort": true,
      "autovacuumVacuumInsertThreshold": "integer",
      "autovacuumVacuumInsertScaleFactor": "number",
      "logMinDurationSample": "integer",
      "logStatementSampleRate": "number",
      "logParameterMaxLength": "integer",
      "logParameterMaxLengthOnError": "integer",
      "pgQualstatsEnabled": true,
      "pgQualstatsTrackConstants": true,
      "pgQualstatsMax": "integer",
      "pgQualstatsResolveOids": true,
      "pgQualstatsSampleRate": "number"
    },
    "postgresqlConfig_14": {
      "maxConnections": "integer",
      "sharedBuffers": "integer",
      "tempBuffers": "integer",
      "maxPreparedTransactions": "integer",
      "workMem": "integer",
      "maintenanceWorkMem": "integer",
      "autovacuumWorkMem": "integer",
      "tempFileLimit": "integer",
      "vacuumCostDelay": "integer",
      "vacuumCostPageHit": "integer",
      "vacuumCostPageMiss": "integer",
      "vacuumCostPageDirty": "integer",
      "vacuumCostLimit": "integer",
      "bgwriterDelay": "integer",
      "bgwriterLruMaxpages": "integer",
      "bgwriterLruMultiplier": "number",
      "bgwriterFlushAfter": "integer",
      "backendFlushAfter": "integer",
      "oldSnapshotThreshold": "integer",
      "walLevel": "string",
      "synchronousCommit": "string",
      "checkpointTimeout": "integer",
      "checkpointCompletionTarget": "number",
      "checkpointFlushAfter": "integer",
      "maxWalSize": "integer",
      "minWalSize": "integer",
      "maxStandbyStreamingDelay": "integer",
      "defaultStatisticsTarget": "integer",
      "constraintExclusion": "string",
      "cursorTupleFraction": "number",
      "fromCollapseLimit": "integer",
      "joinCollapseLimit": "integer",
      "forceParallelMode": "string",
      "clientMinMessages": "string",
      "logMinMessages": "string",
      "logMinErrorStatement": "string",
      "logMinDurationStatement": "integer",
      "logCheckpoints": true,
      "logConnections": true,
      "logDisconnections": true,
      "logDuration": true,
      "logErrorVerbosity": "string",
      "logLockWaits": true,
      "logStatement": "string",
      "logTempFiles": "integer",
      "searchPath": "string",
      "rowSecurity": true,
      "defaultTransactionIsolation": "string",
      "statementTimeout": "integer",
      "lockTimeout": "integer",
      "idleInTransactionSessionTimeout": "integer",
      "byteaOutput": "string",
      "xmlbinary": "string",
      "xmloption": "string",
      "ginPendingListLimit": "integer",
      "deadlockTimeout": "integer",
      "maxLocksPerTransaction": "integer",
      "maxPredLocksPerTransaction": "integer",
      "arrayNulls": true,
      "backslashQuote": "string",
      "defaultWithOids": true,
      "escapeStringWarning": true,
      "loCompatPrivileges": true,
      "quoteAllIdentifiers": true,
      "standardConformingStrings": true,
      "synchronizeSeqscans": true,
      "transformNullEquals": true,
      "exitOnError": true,
      "seqPageCost": "number",
      "randomPageCost": "number",
      "autovacuumMaxWorkers": "integer",
      "autovacuumVacuumCostDelay": "integer",
      "autovacuumVacuumCostLimit": "integer",
      "autovacuumNaptime": "integer",
      "archiveTimeout": "integer",
      "trackActivityQuerySize": "integer",
      "enableBitmapscan": true,
      "enableHashagg": true,
      "enableHashjoin": true,
      "enableIndexscan": true,
      "enableIndexonlyscan": true,
      "enableMaterial": true,
      "enableMergejoin": true,
      "enableNestloop": true,
      "enableSeqscan": true,
      "enableSort": true,
      "enableTidscan": true,
      "maxWorkerProcesses": "integer",
      "maxParallelWorkers": "integer",
      "maxParallelWorkersPerGather": "integer",
      "autovacuumVacuumScaleFactor": "number",
      "autovacuumAnalyzeScaleFactor": "number",
      "defaultTransactionReadOnly": true,
      "timezone": "string",
      "enableParallelAppend": true,
      "enableParallelHash": true,
      "enablePartitionPruning": true,
      "enablePartitionwiseAggregate": true,
      "enablePartitionwiseJoin": true,
      "jit": true,
      "maxParallelMaintenanceWorkers": "integer",
      "parallelLeaderParticipation": true,
      "logTransactionSampleRate": "number",
      "planCacheMode": "string",
      "effectiveIoConcurrency": "integer",
      "effectiveCacheSize": "integer",
      "sharedPreloadLibraries": [
        "string"
      ],
      "autoExplainLogMinDuration": "integer",
      "autoExplainLogAnalyze": true,
      "autoExplainLogBuffers": true,
      "autoExplainLogTiming": true,
      "autoExplainLogTriggers": true,
      "autoExplainLogVerbose": true,
      "autoExplainLogNestedStatements": true,
      "autoExplainSampleRate": "number",
      "pgHintPlanEnableHint": true,
      "pgHintPlanEnableHintTable": true,
      "pgHintPlanDebugPrint": "string",
      "pgHintPlanMessageLevel": "string",
      "hashMemMultiplier": "number",
      "logicalDecodingWorkMem": "integer",
      "maintenanceIoConcurrency": "integer",
      "maxSlotWalKeepSize": "integer",
      "walKeepSize": "integer",
      "enableIncrementalSort": true,
      "autovacuumVacuumInsertThreshold": "integer",
      "autovacuumVacuumInsertScaleFactor": "number",
      "logMinDurationSample": "integer",
      "logStatementSampleRate": "number",
      "logParameterMaxLength": "integer",
      "logParameterMaxLengthOnError": "integer",
      "clientConnectionCheckInterval": "integer",
      "enableAsyncAppend": true,
      "enableGathermerge": true,
      "enableMemoize": true,
      "logRecoveryConflictWaits": true,
      "vacuumFailsafeAge": "integer",
      "vacuumMultixactFailsafeAge": "integer",
      "pgQualstatsEnabled": true,
      "pgQualstatsTrackConstants": true,
      "pgQualstatsMax": "integer",
      "pgQualstatsResolveOids": true,
      "pgQualstatsSampleRate": "number"
    },
    // end of the list of possible fields`configSpec`

  },
  "databaseSpecs": [
    {
      "name": "string",
      "owner": "string",
      "lcCollate": "string",
      "lcCtype": "string",
      "extensions": [
        {
          "name": "string",
          "version": "string"
        }
      ],
      "templateDb": "string"
    }
  ],
  "userSpecs": [
    {
      "name": "string",
      "password": "string",
      "permissions": [
        {
          "databaseName": "string"
        }
      ],
      "connLimit": "integer",
      "settings": {
        "defaultTransactionIsolation": "string",
        "lockTimeout": "integer",
        "logMinDurationStatement": "integer",
        "synchronousCommit": "string",
        "tempFileLimit": "integer",
        "logStatement": "string"
      },
      "login": true,
      "grants": [
        "string"
      ]
    }
  ],
  "hostSpecs": [
    {
      "zoneId": "string",
      "subnetId": "string",
      "assignPublicIp": true,
      "replicationSource": "string",
      "priority": "integer",
      "configSpec": {

        // `hostSpecs[].configSpec` includes only one of the fields `postgresqlConfig_9_6`, `postgresqlConfig_10_1C`, `postgresqlConfig_10`, `postgresqlConfig_11`, `postgresqlConfig_11_1C`, `postgresqlConfig_12`, `postgresqlConfig_12_1C`, `postgresqlConfig_13`, `postgresqlConfig_14`
        "postgresqlConfig_9_6": {
          "recoveryMinApplyDelay": "integer",
          "sharedBuffers": "integer",
          "tempBuffers": "integer",
          "workMem": "integer",
          "replacementSortTuples": "integer",
          "tempFileLimit": "integer",
          "backendFlushAfter": "integer",
          "oldSnapshotThreshold": "integer",
          "maxStandbyStreamingDelay": "integer",
          "constraintExclusion": "string",
          "cursorTupleFraction": "number",
          "fromCollapseLimit": "integer",
          "joinCollapseLimit": "integer",
          "forceParallelMode": "string",
          "clientMinMessages": "string",
          "logMinMessages": "string",
          "logMinErrorStatement": "string",
          "logMinDurationStatement": "integer",
          "logCheckpoints": true,
          "logConnections": true,
          "logDisconnections": true,
          "logDuration": true,
          "logErrorVerbosity": "string",
          "logLockWaits": true,
          "logStatement": "string",
          "logTempFiles": "integer",
          "searchPath": "string",
          "rowSecurity": true,
          "defaultTransactionIsolation": "string",
          "statementTimeout": "integer",
          "lockTimeout": "integer",
          "idleInTransactionSessionTimeout": "integer",
          "byteaOutput": "string",
          "xmlbinary": "string",
          "xmloption": "string",
          "ginPendingListLimit": "integer",
          "deadlockTimeout": "integer",
          "maxLocksPerTransaction": "integer",
          "maxPredLocksPerTransaction": "integer",
          "arrayNulls": true,
          "backslashQuote": "string",
          "defaultWithOids": true,
          "escapeStringWarning": true,
          "loCompatPrivileges": true,
          "operatorPrecedenceWarning": true,
          "quoteAllIdentifiers": true,
          "standardConformingStrings": true,
          "synchronizeSeqscans": true,
          "transformNullEquals": true,
          "exitOnError": true,
          "seqPageCost": "number",
          "randomPageCost": "number",
          "sqlInheritance": true,
          "effectiveIoConcurrency": "integer",
          "effectiveCacheSize": "integer"
        },
        "postgresqlConfig_10_1C": {
          "recoveryMinApplyDelay": "integer",
          "sharedBuffers": "integer",
          "tempBuffers": "integer",
          "workMem": "integer",
          "replacementSortTuples": "integer",
          "tempFileLimit": "integer",
          "backendFlushAfter": "integer",
          "oldSnapshotThreshold": "integer",
          "maxStandbyStreamingDelay": "integer",
          "constraintExclusion": "string",
          "cursorTupleFraction": "number",
          "fromCollapseLimit": "integer",
          "joinCollapseLimit": "integer",
          "forceParallelMode": "string",
          "clientMinMessages": "string",
          "logMinMessages": "string",
          "logMinErrorStatement": "string",
          "logMinDurationStatement": "integer",
          "logCheckpoints": true,
          "logConnections": true,
          "logDisconnections": true,
          "logDuration": true,
          "logErrorVerbosity": "string",
          "logLockWaits": true,
          "logStatement": "string",
          "logTempFiles": "integer",
          "searchPath": "string",
          "rowSecurity": true,
          "defaultTransactionIsolation": "string",
          "statementTimeout": "integer",
          "lockTimeout": "integer",
          "idleInTransactionSessionTimeout": "integer",
          "byteaOutput": "string",
          "xmlbinary": "string",
          "xmloption": "string",
          "ginPendingListLimit": "integer",
          "deadlockTimeout": "integer",
          "maxLocksPerTransaction": "integer",
          "maxPredLocksPerTransaction": "integer",
          "arrayNulls": true,
          "backslashQuote": "string",
          "defaultWithOids": true,
          "escapeStringWarning": true,
          "loCompatPrivileges": true,
          "operatorPrecedenceWarning": true,
          "quoteAllIdentifiers": true,
          "standardConformingStrings": true,
          "synchronizeSeqscans": true,
          "transformNullEquals": true,
          "exitOnError": true,
          "seqPageCost": "number",
          "randomPageCost": "number",
          "enableBitmapscan": true,
          "enableHashagg": true,
          "enableHashjoin": true,
          "enableIndexscan": true,
          "enableIndexonlyscan": true,
          "enableMaterial": true,
          "enableMergejoin": true,
          "enableNestloop": true,
          "enableSeqscan": true,
          "enableSort": true,
          "enableTidscan": true,
          "maxParallelWorkers": "integer",
          "maxParallelWorkersPerGather": "integer",
          "timezone": "string",
          "effectiveIoConcurrency": "integer",
          "effectiveCacheSize": "integer"
        },
        "postgresqlConfig_10": {
          "recoveryMinApplyDelay": "integer",
          "sharedBuffers": "integer",
          "tempBuffers": "integer",
          "workMem": "integer",
          "replacementSortTuples": "integer",
          "tempFileLimit": "integer",
          "backendFlushAfter": "integer",
          "oldSnapshotThreshold": "integer",
          "maxStandbyStreamingDelay": "integer",
          "constraintExclusion": "string",
          "cursorTupleFraction": "number",
          "fromCollapseLimit": "integer",
          "joinCollapseLimit": "integer",
          "forceParallelMode": "string",
          "clientMinMessages": "string",
          "logMinMessages": "string",
          "logMinErrorStatement": "string",
          "logMinDurationStatement": "integer",
          "logCheckpoints": true,
          "logConnections": true,
          "logDisconnections": true,
          "logDuration": true,
          "logErrorVerbosity": "string",
          "logLockWaits": true,
          "logStatement": "string",
          "logTempFiles": "integer",
          "searchPath": "string",
          "rowSecurity": true,
          "defaultTransactionIsolation": "string",
          "statementTimeout": "integer",
          "lockTimeout": "integer",
          "idleInTransactionSessionTimeout": "integer",
          "byteaOutput": "string",
          "xmlbinary": "string",
          "xmloption": "string",
          "ginPendingListLimit": "integer",
          "deadlockTimeout": "integer",
          "maxLocksPerTransaction": "integer",
          "maxPredLocksPerTransaction": "integer",
          "arrayNulls": true,
          "backslashQuote": "string",
          "defaultWithOids": true,
          "escapeStringWarning": true,
          "loCompatPrivileges": true,
          "operatorPrecedenceWarning": true,
          "quoteAllIdentifiers": true,
          "standardConformingStrings": true,
          "synchronizeSeqscans": true,
          "transformNullEquals": true,
          "exitOnError": true,
          "seqPageCost": "number",
          "randomPageCost": "number",
          "enableBitmapscan": true,
          "enableHashagg": true,
          "enableHashjoin": true,
          "enableIndexscan": true,
          "enableIndexonlyscan": true,
          "enableMaterial": true,
          "enableMergejoin": true,
          "enableNestloop": true,
          "enableSeqscan": true,
          "enableSort": true,
          "enableTidscan": true,
          "maxParallelWorkers": "integer",
          "maxParallelWorkersPerGather": "integer",
          "timezone": "string",
          "effectiveIoConcurrency": "integer",
          "effectiveCacheSize": "integer"
        },
        "postgresqlConfig_11": {
          "recoveryMinApplyDelay": "integer",
          "sharedBuffers": "integer",
          "tempBuffers": "integer",
          "workMem": "integer",
          "tempFileLimit": "integer",
          "backendFlushAfter": "integer",
          "oldSnapshotThreshold": "integer",
          "maxStandbyStreamingDelay": "integer",
          "constraintExclusion": "string",
          "cursorTupleFraction": "number",
          "fromCollapseLimit": "integer",
          "joinCollapseLimit": "integer",
          "forceParallelMode": "string",
          "clientMinMessages": "string",
          "logMinMessages": "string",
          "logMinErrorStatement": "string",
          "logMinDurationStatement": "integer",
          "logCheckpoints": true,
          "logConnections": true,
          "logDisconnections": true,
          "logDuration": true,
          "logErrorVerbosity": "string",
          "logLockWaits": true,
          "logStatement": "string",
          "logTempFiles": "integer",
          "searchPath": "string",
          "rowSecurity": true,
          "defaultTransactionIsolation": "string",
          "statementTimeout": "integer",
          "lockTimeout": "integer",
          "idleInTransactionSessionTimeout": "integer",
          "byteaOutput": "string",
          "xmlbinary": "string",
          "xmloption": "string",
          "ginPendingListLimit": "integer",
          "deadlockTimeout": "integer",
          "maxLocksPerTransaction": "integer",
          "maxPredLocksPerTransaction": "integer",
          "arrayNulls": true,
          "backslashQuote": "string",
          "defaultWithOids": true,
          "escapeStringWarning": true,
          "loCompatPrivileges": true,
          "operatorPrecedenceWarning": true,
          "quoteAllIdentifiers": true,
          "standardConformingStrings": true,
          "synchronizeSeqscans": true,
          "transformNullEquals": true,
          "exitOnError": true,
          "seqPageCost": "number",
          "randomPageCost": "number",
          "enableBitmapscan": true,
          "enableHashagg": true,
          "enableHashjoin": true,
          "enableIndexscan": true,
          "enableIndexonlyscan": true,
          "enableMaterial": true,
          "enableMergejoin": true,
          "enableNestloop": true,
          "enableSeqscan": true,
          "enableSort": true,
          "enableTidscan": true,
          "maxParallelWorkers": "integer",
          "maxParallelWorkersPerGather": "integer",
          "timezone": "string",
          "effectiveIoConcurrency": "integer",
          "effectiveCacheSize": "integer"
        },
        "postgresqlConfig_11_1C": {
          "recoveryMinApplyDelay": "integer",
          "sharedBuffers": "integer",
          "tempBuffers": "integer",
          "workMem": "integer",
          "tempFileLimit": "integer",
          "backendFlushAfter": "integer",
          "oldSnapshotThreshold": "integer",
          "maxStandbyStreamingDelay": "integer",
          "constraintExclusion": "string",
          "cursorTupleFraction": "number",
          "fromCollapseLimit": "integer",
          "joinCollapseLimit": "integer",
          "forceParallelMode": "string",
          "clientMinMessages": "string",
          "logMinMessages": "string",
          "logMinErrorStatement": "string",
          "logMinDurationStatement": "integer",
          "logCheckpoints": true,
          "logConnections": true,
          "logDisconnections": true,
          "logDuration": true,
          "logErrorVerbosity": "string",
          "logLockWaits": true,
          "logStatement": "string",
          "logTempFiles": "integer",
          "searchPath": "string",
          "rowSecurity": true,
          "defaultTransactionIsolation": "string",
          "statementTimeout": "integer",
          "lockTimeout": "integer",
          "idleInTransactionSessionTimeout": "integer",
          "byteaOutput": "string",
          "xmlbinary": "string",
          "xmloption": "string",
          "ginPendingListLimit": "integer",
          "deadlockTimeout": "integer",
          "maxLocksPerTransaction": "integer",
          "maxPredLocksPerTransaction": "integer",
          "arrayNulls": true,
          "backslashQuote": "string",
          "defaultWithOids": true,
          "escapeStringWarning": true,
          "loCompatPrivileges": true,
          "operatorPrecedenceWarning": true,
          "quoteAllIdentifiers": true,
          "standardConformingStrings": true,
          "synchronizeSeqscans": true,
          "transformNullEquals": true,
          "exitOnError": true,
          "seqPageCost": "number",
          "randomPageCost": "number",
          "enableBitmapscan": true,
          "enableHashagg": true,
          "enableHashjoin": true,
          "enableIndexscan": true,
          "enableIndexonlyscan": true,
          "enableMaterial": true,
          "enableMergejoin": true,
          "enableNestloop": true,
          "enableSeqscan": true,
          "enableSort": true,
          "enableTidscan": true,
          "maxParallelWorkers": "integer",
          "maxParallelWorkersPerGather": "integer",
          "timezone": "string",
          "effectiveIoConcurrency": "integer",
          "effectiveCacheSize": "integer"
        },
        "postgresqlConfig_12": {
          "recoveryMinApplyDelay": "integer",
          "sharedBuffers": "integer",
          "tempBuffers": "integer",
          "workMem": "integer",
          "tempFileLimit": "integer",
          "backendFlushAfter": "integer",
          "oldSnapshotThreshold": "integer",
          "maxStandbyStreamingDelay": "integer",
          "constraintExclusion": "string",
          "cursorTupleFraction": "number",
          "fromCollapseLimit": "integer",
          "joinCollapseLimit": "integer",
          "forceParallelMode": "string",
          "clientMinMessages": "string",
          "logMinMessages": "string",
          "logMinErrorStatement": "string",
          "logMinDurationStatement": "integer",
          "logCheckpoints": true,
          "logConnections": true,
          "logDisconnections": true,
          "logDuration": true,
          "logErrorVerbosity": "string",
          "logLockWaits": true,
          "logStatement": "string",
          "logTempFiles": "integer",
          "searchPath": "string",
          "rowSecurity": true,
          "defaultTransactionIsolation": "string",
          "statementTimeout": "integer",
          "lockTimeout": "integer",
          "idleInTransactionSessionTimeout": "integer",
          "byteaOutput": "string",
          "xmlbinary": "string",
          "xmloption": "string",
          "ginPendingListLimit": "integer",
          "deadlockTimeout": "integer",
          "maxLocksPerTransaction": "integer",
          "maxPredLocksPerTransaction": "integer",
          "arrayNulls": true,
          "backslashQuote": "string",
          "defaultWithOids": true,
          "escapeStringWarning": true,
          "loCompatPrivileges": true,
          "operatorPrecedenceWarning": true,
          "quoteAllIdentifiers": true,
          "standardConformingStrings": true,
          "synchronizeSeqscans": true,
          "transformNullEquals": true,
          "exitOnError": true,
          "seqPageCost": "number",
          "randomPageCost": "number",
          "enableBitmapscan": true,
          "enableHashagg": true,
          "enableHashjoin": true,
          "enableIndexscan": true,
          "enableIndexonlyscan": true,
          "enableMaterial": true,
          "enableMergejoin": true,
          "enableNestloop": true,
          "enableSeqscan": true,
          "enableSort": true,
          "enableTidscan": true,
          "maxParallelWorkers": "integer",
          "maxParallelWorkersPerGather": "integer",
          "timezone": "string",
          "effectiveIoConcurrency": "integer",
          "effectiveCacheSize": "integer"
        },
        "postgresqlConfig_12_1C": {
          "recoveryMinApplyDelay": "integer",
          "sharedBuffers": "integer",
          "tempBuffers": "integer",
          "workMem": "integer",
          "tempFileLimit": "integer",
          "backendFlushAfter": "integer",
          "oldSnapshotThreshold": "integer",
          "maxStandbyStreamingDelay": "integer",
          "constraintExclusion": "string",
          "cursorTupleFraction": "number",
          "fromCollapseLimit": "integer",
          "joinCollapseLimit": "integer",
          "forceParallelMode": "string",
          "clientMinMessages": "string",
          "logMinMessages": "string",
          "logMinErrorStatement": "string",
          "logMinDurationStatement": "integer",
          "logCheckpoints": true,
          "logConnections": true,
          "logDisconnections": true,
          "logDuration": true,
          "logErrorVerbosity": "string",
          "logLockWaits": true,
          "logStatement": "string",
          "logTempFiles": "integer",
          "searchPath": "string",
          "rowSecurity": true,
          "defaultTransactionIsolation": "string",
          "statementTimeout": "integer",
          "lockTimeout": "integer",
          "idleInTransactionSessionTimeout": "integer",
          "byteaOutput": "string",
          "xmlbinary": "string",
          "xmloption": "string",
          "ginPendingListLimit": "integer",
          "deadlockTimeout": "integer",
          "maxLocksPerTransaction": "integer",
          "maxPredLocksPerTransaction": "integer",
          "arrayNulls": true,
          "backslashQuote": "string",
          "defaultWithOids": true,
          "escapeStringWarning": true,
          "loCompatPrivileges": true,
          "operatorPrecedenceWarning": true,
          "quoteAllIdentifiers": true,
          "standardConformingStrings": true,
          "synchronizeSeqscans": true,
          "transformNullEquals": true,
          "exitOnError": true,
          "seqPageCost": "number",
          "randomPageCost": "number",
          "enableBitmapscan": true,
          "enableHashagg": true,
          "enableHashjoin": true,
          "enableIndexscan": true,
          "enableIndexonlyscan": true,
          "enableMaterial": true,
          "enableMergejoin": true,
          "enableNestloop": true,
          "enableSeqscan": true,
          "enableSort": true,
          "enableTidscan": true,
          "maxParallelWorkers": "integer",
          "maxParallelWorkersPerGather": "integer",
          "timezone": "string",
          "effectiveIoConcurrency": "integer",
          "effectiveCacheSize": "integer"
        },
        "postgresqlConfig_13": {
          "recoveryMinApplyDelay": "integer",
          "sharedBuffers": "integer",
          "tempBuffers": "integer",
          "workMem": "integer",
          "tempFileLimit": "integer",
          "backendFlushAfter": "integer",
          "oldSnapshotThreshold": "integer",
          "maxStandbyStreamingDelay": "integer",
          "constraintExclusion": "string",
          "cursorTupleFraction": "number",
          "fromCollapseLimit": "integer",
          "joinCollapseLimit": "integer",
          "forceParallelMode": "string",
          "clientMinMessages": "string",
          "logMinMessages": "string",
          "logMinErrorStatement": "string",
          "logMinDurationStatement": "integer",
          "logCheckpoints": true,
          "logConnections": true,
          "logDisconnections": true,
          "logDuration": true,
          "logErrorVerbosity": "string",
          "logLockWaits": true,
          "logStatement": "string",
          "logTempFiles": "integer",
          "searchPath": "string",
          "rowSecurity": true,
          "defaultTransactionIsolation": "string",
          "statementTimeout": "integer",
          "lockTimeout": "integer",
          "idleInTransactionSessionTimeout": "integer",
          "byteaOutput": "string",
          "xmlbinary": "string",
          "xmloption": "string",
          "ginPendingListLimit": "integer",
          "deadlockTimeout": "integer",
          "maxLocksPerTransaction": "integer",
          "maxPredLocksPerTransaction": "integer",
          "arrayNulls": true,
          "backslashQuote": "string",
          "defaultWithOids": true,
          "escapeStringWarning": true,
          "loCompatPrivileges": true,
          "operatorPrecedenceWarning": true,
          "quoteAllIdentifiers": true,
          "standardConformingStrings": true,
          "synchronizeSeqscans": true,
          "transformNullEquals": true,
          "exitOnError": true,
          "seqPageCost": "number",
          "randomPageCost": "number",
          "enableBitmapscan": true,
          "enableHashagg": true,
          "enableHashjoin": true,
          "enableIndexscan": true,
          "enableIndexonlyscan": true,
          "enableMaterial": true,
          "enableMergejoin": true,
          "enableNestloop": true,
          "enableSeqscan": true,
          "enableSort": true,
          "enableTidscan": true,
          "maxParallelWorkers": "integer",
          "maxParallelWorkersPerGather": "integer",
          "timezone": "string",
          "effectiveIoConcurrency": "integer",
          "effectiveCacheSize": "integer"
        },
        "postgresqlConfig_14": {
          "recoveryMinApplyDelay": "integer",
          "sharedBuffers": "integer",
          "tempBuffers": "integer",
          "workMem": "integer",
          "tempFileLimit": "integer",
          "backendFlushAfter": "integer",
          "oldSnapshotThreshold": "integer",
          "maxStandbyStreamingDelay": "integer",
          "constraintExclusion": "string",
          "cursorTupleFraction": "number",
          "fromCollapseLimit": "integer",
          "joinCollapseLimit": "integer",
          "forceParallelMode": "string",
          "clientMinMessages": "string",
          "logMinMessages": "string",
          "logMinErrorStatement": "string",
          "logMinDurationStatement": "integer",
          "logCheckpoints": true,
          "logConnections": true,
          "logDisconnections": true,
          "logDuration": true,
          "logErrorVerbosity": "string",
          "logLockWaits": true,
          "logStatement": "string",
          "logTempFiles": "integer",
          "searchPath": "string",
          "rowSecurity": true,
          "defaultTransactionIsolation": "string",
          "statementTimeout": "integer",
          "lockTimeout": "integer",
          "idleInTransactionSessionTimeout": "integer",
          "byteaOutput": "string",
          "xmlbinary": "string",
          "xmloption": "string",
          "ginPendingListLimit": "integer",
          "deadlockTimeout": "integer",
          "maxLocksPerTransaction": "integer",
          "maxPredLocksPerTransaction": "integer",
          "arrayNulls": true,
          "backslashQuote": "string",
          "defaultWithOids": true,
          "escapeStringWarning": true,
          "loCompatPrivileges": true,
          "quoteAllIdentifiers": true,
          "standardConformingStrings": true,
          "synchronizeSeqscans": true,
          "transformNullEquals": true,
          "exitOnError": true,
          "seqPageCost": "number",
          "randomPageCost": "number",
          "enableBitmapscan": true,
          "enableHashagg": true,
          "enableHashjoin": true,
          "enableIndexscan": true,
          "enableIndexonlyscan": true,
          "enableMaterial": true,
          "enableMergejoin": true,
          "enableNestloop": true,
          "enableSeqscan": true,
          "enableSort": true,
          "enableTidscan": true,
          "maxParallelWorkers": "integer",
          "maxParallelWorkersPerGather": "integer",
          "timezone": "string",
          "effectiveIoConcurrency": "integer",
          "effectiveCacheSize": "integer"
        },
        // end of the list of possible fields`hostSpecs[].configSpec`

      }
    }
  ],
  "networkId": "string",
  "securityGroupIds": [
    "string"
  ],
  "deletionProtection": true,
  "hostGroupIds": [
    "string"
  ]
}
```

 
Field | Description
--- | ---
folderId | **string**<br><p>Required. ID of the folder to create the PostgreSQL cluster in.</p> <p>The maximum string length in characters is 50.</p> 
name | **string**<br><p>Required. Name of the PostgreSQL cluster. The name must be unique within the folder.</p> <p>The maximum string length in characters is 63. Value must match the regular expression ``[a-zA-Z0-9_-]*``.</p> 
description | **string**<br><p>Description of the PostgreSQL cluster.</p> <p>The maximum string length in characters is 256.</p> 
labels | **object**<br><p>Custom labels for the PostgreSQL cluster as ``key:value`` pairs. Maximum 64 per resource. For example, "project": "mvp" or "source": "dictionary".</p> <p>No more than 64 per resource. The maximum string length in characters for each key is 63. Each key must match the regular expression ``[a-z][-_0-9a-z]*``. The maximum string length in characters for each value is 63. Each value must match the regular expression ``[-_0-9a-z]*``.</p> 
environment | **string**<br><p>Required. Deployment environment of the PostgreSQL cluster.</p> <ul> <li>PRODUCTION: Stable environment with a conservative update policy: only hotfixes are applied during regular maintenance.</li> <li>PRESTABLE: Environment with more aggressive update policy: new versions are rolled out irrespective of backward compatibility.</li> </ul> 
configSpec | **object**<br><p>Required. Configuration and resources for hosts that should be created for the PostgreSQL cluster.</p> 
configSpec.<br>version | **string**<br><p>Version of PostgreSQL used in the cluster. Possible values: ``9.6``, ``10``, ``10_1c``, ``11``, ``12``, ``13``.</p> 
configSpec.<br>poolerConfig | **object**<br>Configuration of the connection pooler.
configSpec.<br>poolerConfig.<br>poolingMode | **string**<br><p>Mode that the connection pooler is working in. See descriptions of all modes in the <a href="https://pgbouncer.github.io/usage">documentation for PgBouncer</a>.</p> <ul> <li>SESSION: Session pooling mode.</li> <li>TRANSACTION: Transaction pooling mode.</li> <li>STATEMENT: Statement pooling mode.</li> </ul> 
configSpec.<br>poolerConfig.<br>poolDiscard | **boolean** (boolean)<br><p>Setting ``server_reset_query_always`` parameter in PgBouncer.</p> 
configSpec.<br>resources | **object**<br>Resources allocated to PostgreSQL hosts.
configSpec.<br>resources.<br>resourcePresetId | **string**<br><p>ID of the preset for computational resources available to a host (CPU, memory etc.). All available presets are listed in the <a href="/docs/managed-postgresql/concepts/instance-types">documentation</a>.</p> 
configSpec.<br>resources.<br>diskSize | **string** (int64)<br><p>Volume of the storage available to a host, in bytes.</p> 
configSpec.<br>resources.<br>diskTypeId | **string**<br><p>Type of the storage environment for the host. Possible values:</p> <ul> <li>network-hdd - network HDD drive,</li> <li>network-ssd - network SSD drive,</li> <li>local-ssd - local SSD storage.</li> </ul> 
configSpec.<br>autofailover | **boolean** (boolean)<br><p>Configuration setting which enables/disables autofailover in cluster.</p> 
configSpec.<br>backupWindowStart | **object**<br>Time to start the daily backup, in the UTC timezone.
configSpec.<br>backupWindowStart.<br>hours | **integer** (int32)<br><p>Hours of day in 24 hour format. Should be from 0 to 23. An API may choose to allow the value "24:00:00" for scenarios like business closing time.</p> 
configSpec.<br>backupWindowStart.<br>minutes | **integer** (int32)<br><p>Minutes of hour of day. Must be from 0 to 59.</p> 
configSpec.<br>backupWindowStart.<br>seconds | **integer** (int32)<br><p>Seconds of minutes of the time. Must normally be from 0 to 59. An API may allow the value 60 if it allows leap-seconds.</p> 
configSpec.<br>backupWindowStart.<br>nanos | **integer** (int32)<br><p>Fractions of seconds in nanoseconds. Must be from 0 to 999,999,999.</p> 
configSpec.<br>backupRetainPeriodDays | **integer** (int64)<br><p>Retention policy of automated backups.</p> <p>Acceptable values are 7 to 60, inclusive.</p> 
configSpec.<br>access | **object**<br>Access policy to DB
configSpec.<br>access.<br>dataLens | **boolean** (boolean)<br><p>Allow access for DataLens</p> 
configSpec.<br>access.<br>webSql | **boolean** (boolean)<br><p>Allow SQL queries to the cluster databases from the management console.</p> <p>See <a href="/docs/managed-postgresql/operations/web-sql-query">SQL queries in the management console</a> for more details.</p> 
configSpec.<br>access.<br>serverless | **boolean** (boolean)<br><p>Allow access for Serverless</p> 
configSpec.<br>access.<br>dataTransfer | **boolean** (boolean)<br><p>Allow access for DataTransfer.</p> 
configSpec.<br>performanceDiagnostics | **object**<br>Configuration of the performance diagnostics service.
configSpec.<br>performanceDiagnostics.<br>enabled | **boolean** (boolean)<br><p>Configuration setting which enables/disables performance diagnostics service in cluster.</p> 
configSpec.<br>performanceDiagnostics.<br>sessionsSamplingInterval | **string** (int64)<br><p>Interval (in seconds) for pg_stat_activity sampling</p> <p>Acceptable values are 1 to 86400, inclusive.</p> 
configSpec.<br>performanceDiagnostics.<br>statementsSamplingInterval | **string** (int64)<br><p>Interval (in seconds) for pg_stat_statements sampling</p> <p>Acceptable values are 1 to 86400, inclusive.</p> 
configSpec.<br>postgresqlConfig_9_6 | **object**<br>Configuration for a PostgreSQL 9.6 cluster. <br>`configSpec` includes only one of the fields `postgresqlConfig_9_6`, `postgresqlConfig_10_1C`, `postgresqlConfig_10`, `postgresqlConfig_11`, `postgresqlConfig_11_1C`, `postgresqlConfig_12`, `postgresqlConfig_12_1C`, `postgresqlConfig_13`, `postgresqlConfig_14`<br>
configSpec.<br>postgresqlConfig_9_6.<br>maxConnections | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>sharedBuffers | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>tempBuffers | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>maxPreparedTransactions | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>workMem | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>maintenanceWorkMem | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>replacementSortTuples | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>autovacuumWorkMem | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>tempFileLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>vacuumCostDelay | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>vacuumCostPageHit | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>vacuumCostPageMiss | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>vacuumCostPageDirty | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>vacuumCostLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>bgwriterDelay | **integer** (int64)<br><p>Acceptable values are 10 to 10000, inclusive.</p> 
configSpec.<br>postgresqlConfig_9_6.<br>bgwriterLruMaxpages | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>bgwriterLruMultiplier | **number** (double)
configSpec.<br>postgresqlConfig_9_6.<br>bgwriterFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_9_6.<br>backendFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_9_6.<br>oldSnapshotThreshold | **integer** (int64)<br><p>Acceptable values are -1 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_9_6.<br>walLevel | **string**
configSpec.<br>postgresqlConfig_9_6.<br>synchronousCommit | **string**
configSpec.<br>postgresqlConfig_9_6.<br>checkpointTimeout | **integer** (int64)<br><p>Acceptable values are 30000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_9_6.<br>checkpointCompletionTarget | **number** (double)
configSpec.<br>postgresqlConfig_9_6.<br>checkpointFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_9_6.<br>maxWalSize | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>minWalSize | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>maxStandbyStreamingDelay | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>defaultStatisticsTarget | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>constraintExclusion | **string**
configSpec.<br>postgresqlConfig_9_6.<br>cursorTupleFraction | **number** (double)
configSpec.<br>postgresqlConfig_9_6.<br>fromCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_9_6.<br>joinCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_9_6.<br>forceParallelMode | **string**
configSpec.<br>postgresqlConfig_9_6.<br>clientMinMessages | **string**
configSpec.<br>postgresqlConfig_9_6.<br>logMinMessages | **string**
configSpec.<br>postgresqlConfig_9_6.<br>logMinErrorStatement | **string**
configSpec.<br>postgresqlConfig_9_6.<br>logMinDurationStatement | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>logCheckpoints | **boolean** (boolean)
configSpec.<br>postgresqlConfig_9_6.<br>logConnections | **boolean** (boolean)
configSpec.<br>postgresqlConfig_9_6.<br>logDisconnections | **boolean** (boolean)
configSpec.<br>postgresqlConfig_9_6.<br>logDuration | **boolean** (boolean)
configSpec.<br>postgresqlConfig_9_6.<br>logErrorVerbosity | **string**
configSpec.<br>postgresqlConfig_9_6.<br>logLockWaits | **boolean** (boolean)
configSpec.<br>postgresqlConfig_9_6.<br>logStatement | **string**
configSpec.<br>postgresqlConfig_9_6.<br>logTempFiles | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>searchPath | **string**
configSpec.<br>postgresqlConfig_9_6.<br>rowSecurity | **boolean** (boolean)
configSpec.<br>postgresqlConfig_9_6.<br>defaultTransactionIsolation | **string**
configSpec.<br>postgresqlConfig_9_6.<br>statementTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>lockTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>idleInTransactionSessionTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>byteaOutput | **string**
configSpec.<br>postgresqlConfig_9_6.<br>xmlbinary | **string**
configSpec.<br>postgresqlConfig_9_6.<br>xmloption | **string**
configSpec.<br>postgresqlConfig_9_6.<br>ginPendingListLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>deadlockTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>maxLocksPerTransaction | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>maxPredLocksPerTransaction | **integer** (int64)
configSpec.<br>postgresqlConfig_9_6.<br>arrayNulls | **boolean** (boolean)
configSpec.<br>postgresqlConfig_9_6.<br>backslashQuote | **string**
configSpec.<br>postgresqlConfig_9_6.<br>defaultWithOids | **boolean** (boolean)
configSpec.<br>postgresqlConfig_9_6.<br>escapeStringWarning | **boolean** (boolean)
configSpec.<br>postgresqlConfig_9_6.<br>loCompatPrivileges | **boolean** (boolean)
configSpec.<br>postgresqlConfig_9_6.<br>operatorPrecedenceWarning | **boolean** (boolean)
configSpec.<br>postgresqlConfig_9_6.<br>quoteAllIdentifiers | **boolean** (boolean)
configSpec.<br>postgresqlConfig_9_6.<br>standardConformingStrings | **boolean** (boolean)
configSpec.<br>postgresqlConfig_9_6.<br>synchronizeSeqscans | **boolean** (boolean)
configSpec.<br>postgresqlConfig_9_6.<br>transformNullEquals | **boolean** (boolean)
configSpec.<br>postgresqlConfig_9_6.<br>exitOnError | **boolean** (boolean)
configSpec.<br>postgresqlConfig_9_6.<br>seqPageCost | **number** (double)
configSpec.<br>postgresqlConfig_9_6.<br>randomPageCost | **number** (double)
configSpec.<br>postgresqlConfig_9_6.<br>sqlInheritance | **boolean** (boolean)<br><p>This option has been removed in PostgreSQL 10.</p> 
configSpec.<br>postgresqlConfig_9_6.<br>autovacuumMaxWorkers | **integer** (int64)<br><p>Acceptable values are 1 to 32, inclusive.</p> 
configSpec.<br>postgresqlConfig_9_6.<br>autovacuumVacuumCostDelay | **integer** (int64)<br><p>Acceptable values are -1 to 100, inclusive.</p> 
configSpec.<br>postgresqlConfig_9_6.<br>autovacuumVacuumCostLimit | **integer** (int64)<br><p>Acceptable values are -1 to 10000, inclusive.</p> 
configSpec.<br>postgresqlConfig_9_6.<br>autovacuumNaptime | **integer** (int64)<br><p>Acceptable values are 1000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_9_6.<br>archiveTimeout | **integer** (int64)<br><p>Acceptable values are 10000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_9_6.<br>trackActivityQuerySize | **integer** (int64)<br><p>Acceptable values are 100 to 102400, inclusive.</p> 
configSpec.<br>postgresqlConfig_9_6.<br>effectiveIoConcurrency | **integer** (int64)<br><p>Acceptable values are 0 to 1000, inclusive.</p> 
configSpec.<br>postgresqlConfig_9_6.<br>effectiveCacheSize | **integer** (int64)<br><p>Acceptable values are 0 to 549755813888, inclusive.</p> 
configSpec.<br>postgresqlConfig_10_1C | **object**<br>Configuration for a PostgreSQL 10 1C cluster. <br>`configSpec` includes only one of the fields `postgresqlConfig_9_6`, `postgresqlConfig_10_1C`, `postgresqlConfig_10`, `postgresqlConfig_11`, `postgresqlConfig_11_1C`, `postgresqlConfig_12`, `postgresqlConfig_12_1C`, `postgresqlConfig_13`, `postgresqlConfig_14`<br>
configSpec.<br>postgresqlConfig_10_1C.<br>maxConnections | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>sharedBuffers | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>tempBuffers | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>maxPreparedTransactions | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>workMem | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>maintenanceWorkMem | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>replacementSortTuples | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>autovacuumWorkMem | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>tempFileLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>vacuumCostDelay | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>vacuumCostPageHit | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>vacuumCostPageMiss | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>vacuumCostPageDirty | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>vacuumCostLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>bgwriterDelay | **integer** (int64)<br><p>Acceptable values are 10 to 10000, inclusive.</p> 
configSpec.<br>postgresqlConfig_10_1C.<br>bgwriterLruMaxpages | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>bgwriterLruMultiplier | **number** (double)
configSpec.<br>postgresqlConfig_10_1C.<br>bgwriterFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_10_1C.<br>backendFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_10_1C.<br>oldSnapshotThreshold | **integer** (int64)<br><p>Acceptable values are -1 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_10_1C.<br>walLevel | **string**
configSpec.<br>postgresqlConfig_10_1C.<br>synchronousCommit | **string**
configSpec.<br>postgresqlConfig_10_1C.<br>checkpointTimeout | **integer** (int64)<br><p>Acceptable values are 30000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_10_1C.<br>checkpointCompletionTarget | **number** (double)
configSpec.<br>postgresqlConfig_10_1C.<br>checkpointFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_10_1C.<br>maxWalSize | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>minWalSize | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>maxStandbyStreamingDelay | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>defaultStatisticsTarget | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>constraintExclusion | **string**
configSpec.<br>postgresqlConfig_10_1C.<br>cursorTupleFraction | **number** (double)
configSpec.<br>postgresqlConfig_10_1C.<br>fromCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_10_1C.<br>joinCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_10_1C.<br>forceParallelMode | **string**
configSpec.<br>postgresqlConfig_10_1C.<br>clientMinMessages | **string**
configSpec.<br>postgresqlConfig_10_1C.<br>logMinMessages | **string**
configSpec.<br>postgresqlConfig_10_1C.<br>logMinErrorStatement | **string**
configSpec.<br>postgresqlConfig_10_1C.<br>logMinDurationStatement | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>logCheckpoints | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>logConnections | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>logDisconnections | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>logDuration | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>logErrorVerbosity | **string**
configSpec.<br>postgresqlConfig_10_1C.<br>logLockWaits | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>logStatement | **string**
configSpec.<br>postgresqlConfig_10_1C.<br>logTempFiles | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>searchPath | **string**
configSpec.<br>postgresqlConfig_10_1C.<br>rowSecurity | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>defaultTransactionIsolation | **string**
configSpec.<br>postgresqlConfig_10_1C.<br>statementTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>lockTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>idleInTransactionSessionTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>byteaOutput | **string**
configSpec.<br>postgresqlConfig_10_1C.<br>xmlbinary | **string**
configSpec.<br>postgresqlConfig_10_1C.<br>xmloption | **string**
configSpec.<br>postgresqlConfig_10_1C.<br>ginPendingListLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>deadlockTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>maxLocksPerTransaction | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>maxPredLocksPerTransaction | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>arrayNulls | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>backslashQuote | **string**
configSpec.<br>postgresqlConfig_10_1C.<br>defaultWithOids | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>escapeStringWarning | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>loCompatPrivileges | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>operatorPrecedenceWarning | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>quoteAllIdentifiers | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>standardConformingStrings | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>synchronizeSeqscans | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>transformNullEquals | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>exitOnError | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>seqPageCost | **number** (double)
configSpec.<br>postgresqlConfig_10_1C.<br>randomPageCost | **number** (double)
configSpec.<br>postgresqlConfig_10_1C.<br>autovacuumMaxWorkers | **integer** (int64)<br><p>Acceptable values are 1 to 32, inclusive.</p> 
configSpec.<br>postgresqlConfig_10_1C.<br>autovacuumVacuumCostDelay | **integer** (int64)<br><p>Acceptable values are -1 to 100, inclusive.</p> 
configSpec.<br>postgresqlConfig_10_1C.<br>autovacuumVacuumCostLimit | **integer** (int64)<br><p>Acceptable values are -1 to 10000, inclusive.</p> 
configSpec.<br>postgresqlConfig_10_1C.<br>autovacuumNaptime | **integer** (int64)<br><p>Acceptable values are 1000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_10_1C.<br>archiveTimeout | **integer** (int64)<br><p>Acceptable values are 10000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_10_1C.<br>trackActivityQuerySize | **integer** (int64)<br><p>Acceptable values are 100 to 102400, inclusive.</p> 
configSpec.<br>postgresqlConfig_10_1C.<br>enableBitmapscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>enableHashagg | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>enableHashjoin | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>enableIndexscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>enableIndexonlyscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>enableMaterial | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>enableMergejoin | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>enableNestloop | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>enableSeqscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>enableSort | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>enableTidscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>maxWorkerProcesses | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
configSpec.<br>postgresqlConfig_10_1C.<br>maxParallelWorkers | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
configSpec.<br>postgresqlConfig_10_1C.<br>maxParallelWorkersPerGather | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
configSpec.<br>postgresqlConfig_10_1C.<br>autovacuumVacuumScaleFactor | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_10_1C.<br>autovacuumAnalyzeScaleFactor | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_10_1C.<br>defaultTransactionReadOnly | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>timezone | **string**
configSpec.<br>postgresqlConfig_10_1C.<br>effectiveIoConcurrency | **integer** (int64)<br><p>Acceptable values are 0 to 1000, inclusive.</p> 
configSpec.<br>postgresqlConfig_10_1C.<br>effectiveCacheSize | **integer** (int64)<br><p>Acceptable values are 0 to 549755813888, inclusive.</p> 
configSpec.<br>postgresqlConfig_10_1C.<br>sharedPreloadLibraries[] | **string**
configSpec.<br>postgresqlConfig_10_1C.<br>autoExplainLogMinDuration | **integer** (int64)<br><p>Acceptable values are -1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_10_1C.<br>autoExplainLogAnalyze | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>autoExplainLogBuffers | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>autoExplainLogTiming | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>autoExplainLogTriggers | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>autoExplainLogVerbose | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>autoExplainLogNestedStatements | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>autoExplainSampleRate | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_10_1C.<br>pgHintPlanEnableHint | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>pgHintPlanEnableHintTable | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>pgHintPlanDebugPrint | **string**
configSpec.<br>postgresqlConfig_10_1C.<br>pgHintPlanMessageLevel | **string**
configSpec.<br>postgresqlConfig_10_1C.<br>onlineAnalyzeEnable | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>plantunerFixEmptyTable | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>pgQualstatsEnabled | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>pgQualstatsTrackConstants | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>pgQualstatsMax | **integer** (int64)
configSpec.<br>postgresqlConfig_10_1C.<br>pgQualstatsResolveOids | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10_1C.<br>pgQualstatsSampleRate | **number** (double)
configSpec.<br>postgresqlConfig_10 | **object**<br>Configuration for a PostgreSQL 10 cluster. <br>`configSpec` includes only one of the fields `postgresqlConfig_9_6`, `postgresqlConfig_10_1C`, `postgresqlConfig_10`, `postgresqlConfig_11`, `postgresqlConfig_11_1C`, `postgresqlConfig_12`, `postgresqlConfig_12_1C`, `postgresqlConfig_13`, `postgresqlConfig_14`<br>
configSpec.<br>postgresqlConfig_10.<br>maxConnections | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>sharedBuffers | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>tempBuffers | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>maxPreparedTransactions | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>workMem | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>maintenanceWorkMem | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>replacementSortTuples | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>autovacuumWorkMem | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>tempFileLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>vacuumCostDelay | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>vacuumCostPageHit | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>vacuumCostPageMiss | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>vacuumCostPageDirty | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>vacuumCostLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>bgwriterDelay | **integer** (int64)<br><p>Acceptable values are 10 to 10000, inclusive.</p> 
configSpec.<br>postgresqlConfig_10.<br>bgwriterLruMaxpages | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>bgwriterLruMultiplier | **number** (double)
configSpec.<br>postgresqlConfig_10.<br>bgwriterFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_10.<br>backendFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_10.<br>oldSnapshotThreshold | **integer** (int64)<br><p>Acceptable values are -1 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_10.<br>walLevel | **string**
configSpec.<br>postgresqlConfig_10.<br>synchronousCommit | **string**
configSpec.<br>postgresqlConfig_10.<br>checkpointTimeout | **integer** (int64)<br><p>Acceptable values are 30000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_10.<br>checkpointCompletionTarget | **number** (double)
configSpec.<br>postgresqlConfig_10.<br>checkpointFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_10.<br>maxWalSize | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>minWalSize | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>maxStandbyStreamingDelay | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>defaultStatisticsTarget | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>constraintExclusion | **string**
configSpec.<br>postgresqlConfig_10.<br>cursorTupleFraction | **number** (double)
configSpec.<br>postgresqlConfig_10.<br>fromCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_10.<br>joinCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_10.<br>forceParallelMode | **string**
configSpec.<br>postgresqlConfig_10.<br>clientMinMessages | **string**
configSpec.<br>postgresqlConfig_10.<br>logMinMessages | **string**
configSpec.<br>postgresqlConfig_10.<br>logMinErrorStatement | **string**
configSpec.<br>postgresqlConfig_10.<br>logMinDurationStatement | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>logCheckpoints | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>logConnections | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>logDisconnections | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>logDuration | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>logErrorVerbosity | **string**
configSpec.<br>postgresqlConfig_10.<br>logLockWaits | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>logStatement | **string**
configSpec.<br>postgresqlConfig_10.<br>logTempFiles | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>searchPath | **string**
configSpec.<br>postgresqlConfig_10.<br>rowSecurity | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>defaultTransactionIsolation | **string**
configSpec.<br>postgresqlConfig_10.<br>statementTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>lockTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>idleInTransactionSessionTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>byteaOutput | **string**
configSpec.<br>postgresqlConfig_10.<br>xmlbinary | **string**
configSpec.<br>postgresqlConfig_10.<br>xmloption | **string**
configSpec.<br>postgresqlConfig_10.<br>ginPendingListLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>deadlockTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>maxLocksPerTransaction | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>maxPredLocksPerTransaction | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>arrayNulls | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>backslashQuote | **string**
configSpec.<br>postgresqlConfig_10.<br>defaultWithOids | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>escapeStringWarning | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>loCompatPrivileges | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>operatorPrecedenceWarning | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>quoteAllIdentifiers | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>standardConformingStrings | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>synchronizeSeqscans | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>transformNullEquals | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>exitOnError | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>seqPageCost | **number** (double)
configSpec.<br>postgresqlConfig_10.<br>randomPageCost | **number** (double)
configSpec.<br>postgresqlConfig_10.<br>autovacuumMaxWorkers | **integer** (int64)<br><p>Acceptable values are 1 to 32, inclusive.</p> 
configSpec.<br>postgresqlConfig_10.<br>autovacuumVacuumCostDelay | **integer** (int64)<br><p>Acceptable values are -1 to 100, inclusive.</p> 
configSpec.<br>postgresqlConfig_10.<br>autovacuumVacuumCostLimit | **integer** (int64)<br><p>Acceptable values are -1 to 10000, inclusive.</p> 
configSpec.<br>postgresqlConfig_10.<br>autovacuumNaptime | **integer** (int64)<br><p>Acceptable values are 1000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_10.<br>archiveTimeout | **integer** (int64)<br><p>Acceptable values are 10000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_10.<br>trackActivityQuerySize | **integer** (int64)<br><p>Acceptable values are 100 to 102400, inclusive.</p> 
configSpec.<br>postgresqlConfig_10.<br>enableBitmapscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>enableHashagg | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>enableHashjoin | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>enableIndexscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>enableIndexonlyscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>enableMaterial | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>enableMergejoin | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>enableNestloop | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>enableSeqscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>enableSort | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>enableTidscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>maxWorkerProcesses | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
configSpec.<br>postgresqlConfig_10.<br>maxParallelWorkers | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
configSpec.<br>postgresqlConfig_10.<br>maxParallelWorkersPerGather | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
configSpec.<br>postgresqlConfig_10.<br>autovacuumVacuumScaleFactor | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_10.<br>autovacuumAnalyzeScaleFactor | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_10.<br>defaultTransactionReadOnly | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>timezone | **string**
configSpec.<br>postgresqlConfig_10.<br>effectiveIoConcurrency | **integer** (int64)<br><p>Acceptable values are 0 to 1000, inclusive.</p> 
configSpec.<br>postgresqlConfig_10.<br>effectiveCacheSize | **integer** (int64)<br><p>Acceptable values are 0 to 549755813888, inclusive.</p> 
configSpec.<br>postgresqlConfig_10.<br>sharedPreloadLibraries[] | **string**
configSpec.<br>postgresqlConfig_10.<br>autoExplainLogMinDuration | **integer** (int64)<br><p>Acceptable values are -1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_10.<br>autoExplainLogAnalyze | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>autoExplainLogBuffers | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>autoExplainLogTiming | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>autoExplainLogTriggers | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>autoExplainLogVerbose | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>autoExplainLogNestedStatements | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>autoExplainSampleRate | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_10.<br>pgHintPlanEnableHint | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>pgHintPlanEnableHintTable | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>pgHintPlanDebugPrint | **string**
configSpec.<br>postgresqlConfig_10.<br>pgHintPlanMessageLevel | **string**
configSpec.<br>postgresqlConfig_10.<br>pgQualstatsEnabled | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>pgQualstatsTrackConstants | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>pgQualstatsMax | **integer** (int64)
configSpec.<br>postgresqlConfig_10.<br>pgQualstatsResolveOids | **boolean** (boolean)
configSpec.<br>postgresqlConfig_10.<br>pgQualstatsSampleRate | **number** (double)
configSpec.<br>postgresqlConfig_11 | **object**<br>Configuration for a PostgreSQL 11 cluster. <br>`configSpec` includes only one of the fields `postgresqlConfig_9_6`, `postgresqlConfig_10_1C`, `postgresqlConfig_10`, `postgresqlConfig_11`, `postgresqlConfig_11_1C`, `postgresqlConfig_12`, `postgresqlConfig_12_1C`, `postgresqlConfig_13`, `postgresqlConfig_14`<br>
configSpec.<br>postgresqlConfig_11.<br>maxConnections | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>sharedBuffers | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>tempBuffers | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>maxPreparedTransactions | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>workMem | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>maintenanceWorkMem | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>autovacuumWorkMem | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>tempFileLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>vacuumCostDelay | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>vacuumCostPageHit | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>vacuumCostPageMiss | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>vacuumCostPageDirty | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>vacuumCostLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>bgwriterDelay | **integer** (int64)<br><p>Acceptable values are 10 to 10000, inclusive.</p> 
configSpec.<br>postgresqlConfig_11.<br>bgwriterLruMaxpages | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>bgwriterLruMultiplier | **number** (double)
configSpec.<br>postgresqlConfig_11.<br>bgwriterFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_11.<br>backendFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_11.<br>oldSnapshotThreshold | **integer** (int64)<br><p>Acceptable values are -1 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_11.<br>walLevel | **string**
configSpec.<br>postgresqlConfig_11.<br>synchronousCommit | **string**
configSpec.<br>postgresqlConfig_11.<br>checkpointTimeout | **integer** (int64)<br><p>Acceptable values are 30000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_11.<br>checkpointCompletionTarget | **number** (double)
configSpec.<br>postgresqlConfig_11.<br>checkpointFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_11.<br>maxWalSize | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>minWalSize | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>maxStandbyStreamingDelay | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>defaultStatisticsTarget | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>constraintExclusion | **string**
configSpec.<br>postgresqlConfig_11.<br>cursorTupleFraction | **number** (double)
configSpec.<br>postgresqlConfig_11.<br>fromCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_11.<br>joinCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_11.<br>forceParallelMode | **string**
configSpec.<br>postgresqlConfig_11.<br>clientMinMessages | **string**
configSpec.<br>postgresqlConfig_11.<br>logMinMessages | **string**
configSpec.<br>postgresqlConfig_11.<br>logMinErrorStatement | **string**
configSpec.<br>postgresqlConfig_11.<br>logMinDurationStatement | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>logCheckpoints | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>logConnections | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>logDisconnections | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>logDuration | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>logErrorVerbosity | **string**
configSpec.<br>postgresqlConfig_11.<br>logLockWaits | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>logStatement | **string**
configSpec.<br>postgresqlConfig_11.<br>logTempFiles | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>searchPath | **string**
configSpec.<br>postgresqlConfig_11.<br>rowSecurity | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>defaultTransactionIsolation | **string**
configSpec.<br>postgresqlConfig_11.<br>statementTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>lockTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>idleInTransactionSessionTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>byteaOutput | **string**
configSpec.<br>postgresqlConfig_11.<br>xmlbinary | **string**
configSpec.<br>postgresqlConfig_11.<br>xmloption | **string**
configSpec.<br>postgresqlConfig_11.<br>ginPendingListLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>deadlockTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>maxLocksPerTransaction | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>maxPredLocksPerTransaction | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>arrayNulls | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>backslashQuote | **string**
configSpec.<br>postgresqlConfig_11.<br>defaultWithOids | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>escapeStringWarning | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>loCompatPrivileges | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>operatorPrecedenceWarning | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>quoteAllIdentifiers | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>standardConformingStrings | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>synchronizeSeqscans | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>transformNullEquals | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>exitOnError | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>seqPageCost | **number** (double)
configSpec.<br>postgresqlConfig_11.<br>randomPageCost | **number** (double)
configSpec.<br>postgresqlConfig_11.<br>autovacuumMaxWorkers | **integer** (int64)<br><p>Acceptable values are 1 to 32, inclusive.</p> 
configSpec.<br>postgresqlConfig_11.<br>autovacuumVacuumCostDelay | **integer** (int64)<br><p>Acceptable values are -1 to 100, inclusive.</p> 
configSpec.<br>postgresqlConfig_11.<br>autovacuumVacuumCostLimit | **integer** (int64)<br><p>Acceptable values are -1 to 10000, inclusive.</p> 
configSpec.<br>postgresqlConfig_11.<br>autovacuumNaptime | **integer** (int64)<br><p>Acceptable values are 1000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_11.<br>archiveTimeout | **integer** (int64)<br><p>Acceptable values are 10000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_11.<br>trackActivityQuerySize | **integer** (int64)<br><p>Acceptable values are 100 to 102400, inclusive.</p> 
configSpec.<br>postgresqlConfig_11.<br>enableBitmapscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>enableHashagg | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>enableHashjoin | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>enableIndexscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>enableIndexonlyscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>enableMaterial | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>enableMergejoin | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>enableNestloop | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>enableSeqscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>enableSort | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>enableTidscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>maxWorkerProcesses | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
configSpec.<br>postgresqlConfig_11.<br>maxParallelWorkers | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
configSpec.<br>postgresqlConfig_11.<br>maxParallelWorkersPerGather | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
configSpec.<br>postgresqlConfig_11.<br>autovacuumVacuumScaleFactor | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_11.<br>autovacuumAnalyzeScaleFactor | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_11.<br>defaultTransactionReadOnly | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>timezone | **string**
configSpec.<br>postgresqlConfig_11.<br>enableParallelAppend | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>enableParallelHash | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>enablePartitionPruning | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>enablePartitionwiseAggregate | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>enablePartitionwiseJoin | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>jit | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>maxParallelMaintenanceWorkers | **integer** (int64)<br><p>The minimum value is 0.</p> 
configSpec.<br>postgresqlConfig_11.<br>parallelLeaderParticipation | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>vacuumCleanupIndexScaleFactor | **number** (double)<br><p>Acceptable values are 0 to 10000000000, inclusive.</p> 
configSpec.<br>postgresqlConfig_11.<br>effectiveIoConcurrency | **integer** (int64)<br><p>Acceptable values are 0 to 1000, inclusive.</p> 
configSpec.<br>postgresqlConfig_11.<br>effectiveCacheSize | **integer** (int64)<br><p>Acceptable values are 0 to 549755813888, inclusive.</p> 
configSpec.<br>postgresqlConfig_11.<br>sharedPreloadLibraries[] | **string**
configSpec.<br>postgresqlConfig_11.<br>autoExplainLogMinDuration | **integer** (int64)<br><p>Acceptable values are -1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_11.<br>autoExplainLogAnalyze | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>autoExplainLogBuffers | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>autoExplainLogTiming | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>autoExplainLogTriggers | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>autoExplainLogVerbose | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>autoExplainLogNestedStatements | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>autoExplainSampleRate | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_11.<br>pgHintPlanEnableHint | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>pgHintPlanEnableHintTable | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>pgHintPlanDebugPrint | **string**
configSpec.<br>postgresqlConfig_11.<br>pgHintPlanMessageLevel | **string**
configSpec.<br>postgresqlConfig_11.<br>pgQualstatsEnabled | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>pgQualstatsTrackConstants | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>pgQualstatsMax | **integer** (int64)
configSpec.<br>postgresqlConfig_11.<br>pgQualstatsResolveOids | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11.<br>pgQualstatsSampleRate | **number** (double)
configSpec.<br>postgresqlConfig_11_1C | **object**<br>Configuration for a PostgreSQL 11 1C cluster. <br>`configSpec` includes only one of the fields `postgresqlConfig_9_6`, `postgresqlConfig_10_1C`, `postgresqlConfig_10`, `postgresqlConfig_11`, `postgresqlConfig_11_1C`, `postgresqlConfig_12`, `postgresqlConfig_12_1C`, `postgresqlConfig_13`, `postgresqlConfig_14`<br>
configSpec.<br>postgresqlConfig_11_1C.<br>maxConnections | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>sharedBuffers | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>tempBuffers | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>maxPreparedTransactions | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>workMem | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>maintenanceWorkMem | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>autovacuumWorkMem | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>tempFileLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>vacuumCostDelay | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>vacuumCostPageHit | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>vacuumCostPageMiss | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>vacuumCostPageDirty | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>vacuumCostLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>bgwriterDelay | **integer** (int64)<br><p>Acceptable values are 10 to 10000, inclusive.</p> 
configSpec.<br>postgresqlConfig_11_1C.<br>bgwriterLruMaxpages | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>bgwriterLruMultiplier | **number** (double)
configSpec.<br>postgresqlConfig_11_1C.<br>bgwriterFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_11_1C.<br>backendFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_11_1C.<br>oldSnapshotThreshold | **integer** (int64)<br><p>Acceptable values are -1 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_11_1C.<br>walLevel | **string**
configSpec.<br>postgresqlConfig_11_1C.<br>synchronousCommit | **string**
configSpec.<br>postgresqlConfig_11_1C.<br>checkpointTimeout | **integer** (int64)<br><p>Acceptable values are 30000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_11_1C.<br>checkpointCompletionTarget | **number** (double)
configSpec.<br>postgresqlConfig_11_1C.<br>checkpointFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_11_1C.<br>maxWalSize | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>minWalSize | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>maxStandbyStreamingDelay | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>defaultStatisticsTarget | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>constraintExclusion | **string**
configSpec.<br>postgresqlConfig_11_1C.<br>cursorTupleFraction | **number** (double)
configSpec.<br>postgresqlConfig_11_1C.<br>fromCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_11_1C.<br>joinCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_11_1C.<br>forceParallelMode | **string**
configSpec.<br>postgresqlConfig_11_1C.<br>clientMinMessages | **string**
configSpec.<br>postgresqlConfig_11_1C.<br>logMinMessages | **string**
configSpec.<br>postgresqlConfig_11_1C.<br>logMinErrorStatement | **string**
configSpec.<br>postgresqlConfig_11_1C.<br>logMinDurationStatement | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>logCheckpoints | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>logConnections | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>logDisconnections | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>logDuration | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>logErrorVerbosity | **string**
configSpec.<br>postgresqlConfig_11_1C.<br>logLockWaits | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>logStatement | **string**
configSpec.<br>postgresqlConfig_11_1C.<br>logTempFiles | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>searchPath | **string**
configSpec.<br>postgresqlConfig_11_1C.<br>rowSecurity | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>defaultTransactionIsolation | **string**
configSpec.<br>postgresqlConfig_11_1C.<br>statementTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>lockTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>idleInTransactionSessionTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>byteaOutput | **string**
configSpec.<br>postgresqlConfig_11_1C.<br>xmlbinary | **string**
configSpec.<br>postgresqlConfig_11_1C.<br>xmloption | **string**
configSpec.<br>postgresqlConfig_11_1C.<br>ginPendingListLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>deadlockTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>maxLocksPerTransaction | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>maxPredLocksPerTransaction | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>arrayNulls | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>backslashQuote | **string**
configSpec.<br>postgresqlConfig_11_1C.<br>defaultWithOids | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>escapeStringWarning | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>loCompatPrivileges | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>operatorPrecedenceWarning | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>quoteAllIdentifiers | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>standardConformingStrings | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>synchronizeSeqscans | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>transformNullEquals | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>exitOnError | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>seqPageCost | **number** (double)
configSpec.<br>postgresqlConfig_11_1C.<br>randomPageCost | **number** (double)
configSpec.<br>postgresqlConfig_11_1C.<br>autovacuumMaxWorkers | **integer** (int64)<br><p>Acceptable values are 1 to 32, inclusive.</p> 
configSpec.<br>postgresqlConfig_11_1C.<br>autovacuumVacuumCostDelay | **integer** (int64)<br><p>Acceptable values are -1 to 100, inclusive.</p> 
configSpec.<br>postgresqlConfig_11_1C.<br>autovacuumVacuumCostLimit | **integer** (int64)<br><p>Acceptable values are -1 to 10000, inclusive.</p> 
configSpec.<br>postgresqlConfig_11_1C.<br>autovacuumNaptime | **integer** (int64)<br><p>Acceptable values are 1000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_11_1C.<br>archiveTimeout | **integer** (int64)<br><p>Acceptable values are 10000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_11_1C.<br>trackActivityQuerySize | **integer** (int64)<br><p>Acceptable values are 100 to 102400, inclusive.</p> 
configSpec.<br>postgresqlConfig_11_1C.<br>enableBitmapscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>enableHashagg | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>enableHashjoin | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>enableIndexscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>enableIndexonlyscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>enableMaterial | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>enableMergejoin | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>enableNestloop | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>enableSeqscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>enableSort | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>enableTidscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>maxWorkerProcesses | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
configSpec.<br>postgresqlConfig_11_1C.<br>maxParallelWorkers | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
configSpec.<br>postgresqlConfig_11_1C.<br>maxParallelWorkersPerGather | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
configSpec.<br>postgresqlConfig_11_1C.<br>autovacuumVacuumScaleFactor | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_11_1C.<br>autovacuumAnalyzeScaleFactor | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_11_1C.<br>defaultTransactionReadOnly | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>timezone | **string**
configSpec.<br>postgresqlConfig_11_1C.<br>enableParallelAppend | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>enableParallelHash | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>enablePartitionPruning | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>enablePartitionwiseAggregate | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>enablePartitionwiseJoin | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>jit | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>maxParallelMaintenanceWorkers | **integer** (int64)<br><p>The minimum value is 0.</p> 
configSpec.<br>postgresqlConfig_11_1C.<br>parallelLeaderParticipation | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>vacuumCleanupIndexScaleFactor | **number** (double)<br><p>Acceptable values are 0 to 10000000000, inclusive.</p> 
configSpec.<br>postgresqlConfig_11_1C.<br>effectiveIoConcurrency | **integer** (int64)<br><p>Acceptable values are 0 to 1000, inclusive.</p> 
configSpec.<br>postgresqlConfig_11_1C.<br>effectiveCacheSize | **integer** (int64)<br><p>Acceptable values are 0 to 549755813888, inclusive.</p> 
configSpec.<br>postgresqlConfig_11_1C.<br>sharedPreloadLibraries[] | **string**
configSpec.<br>postgresqlConfig_11_1C.<br>autoExplainLogMinDuration | **integer** (int64)<br><p>Acceptable values are -1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_11_1C.<br>autoExplainLogAnalyze | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>autoExplainLogBuffers | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>autoExplainLogTiming | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>autoExplainLogTriggers | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>autoExplainLogVerbose | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>autoExplainLogNestedStatements | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>autoExplainSampleRate | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_11_1C.<br>pgHintPlanEnableHint | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>pgHintPlanEnableHintTable | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>pgHintPlanDebugPrint | **string**
configSpec.<br>postgresqlConfig_11_1C.<br>pgHintPlanMessageLevel | **string**
configSpec.<br>postgresqlConfig_11_1C.<br>pgQualstatsEnabled | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>pgQualstatsTrackConstants | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>pgQualstatsMax | **integer** (int64)
configSpec.<br>postgresqlConfig_11_1C.<br>pgQualstatsResolveOids | **boolean** (boolean)
configSpec.<br>postgresqlConfig_11_1C.<br>pgQualstatsSampleRate | **number** (double)
configSpec.<br>postgresqlConfig_12 | **object**<br>Configuration for a PostgreSQL 12 cluster. <br>`configSpec` includes only one of the fields `postgresqlConfig_9_6`, `postgresqlConfig_10_1C`, `postgresqlConfig_10`, `postgresqlConfig_11`, `postgresqlConfig_11_1C`, `postgresqlConfig_12`, `postgresqlConfig_12_1C`, `postgresqlConfig_13`, `postgresqlConfig_14`<br>
configSpec.<br>postgresqlConfig_12.<br>maxConnections | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>sharedBuffers | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>tempBuffers | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>maxPreparedTransactions | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>workMem | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>maintenanceWorkMem | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>autovacuumWorkMem | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>tempFileLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>vacuumCostDelay | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>vacuumCostPageHit | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>vacuumCostPageMiss | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>vacuumCostPageDirty | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>vacuumCostLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>bgwriterDelay | **integer** (int64)<br><p>Acceptable values are 10 to 10000, inclusive.</p> 
configSpec.<br>postgresqlConfig_12.<br>bgwriterLruMaxpages | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>bgwriterLruMultiplier | **number** (double)
configSpec.<br>postgresqlConfig_12.<br>bgwriterFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_12.<br>backendFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_12.<br>oldSnapshotThreshold | **integer** (int64)<br><p>Acceptable values are -1 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_12.<br>walLevel | **string**
configSpec.<br>postgresqlConfig_12.<br>synchronousCommit | **string**
configSpec.<br>postgresqlConfig_12.<br>checkpointTimeout | **integer** (int64)<br><p>Acceptable values are 30000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_12.<br>checkpointCompletionTarget | **number** (double)
configSpec.<br>postgresqlConfig_12.<br>checkpointFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_12.<br>maxWalSize | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>minWalSize | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>maxStandbyStreamingDelay | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>defaultStatisticsTarget | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>constraintExclusion | **string**
configSpec.<br>postgresqlConfig_12.<br>cursorTupleFraction | **number** (double)
configSpec.<br>postgresqlConfig_12.<br>fromCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_12.<br>joinCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_12.<br>forceParallelMode | **string**
configSpec.<br>postgresqlConfig_12.<br>clientMinMessages | **string**
configSpec.<br>postgresqlConfig_12.<br>logMinMessages | **string**
configSpec.<br>postgresqlConfig_12.<br>logMinErrorStatement | **string**
configSpec.<br>postgresqlConfig_12.<br>logMinDurationStatement | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>logCheckpoints | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>logConnections | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>logDisconnections | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>logDuration | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>logErrorVerbosity | **string**
configSpec.<br>postgresqlConfig_12.<br>logLockWaits | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>logStatement | **string**
configSpec.<br>postgresqlConfig_12.<br>logTempFiles | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>searchPath | **string**
configSpec.<br>postgresqlConfig_12.<br>rowSecurity | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>defaultTransactionIsolation | **string**
configSpec.<br>postgresqlConfig_12.<br>statementTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>lockTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>idleInTransactionSessionTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>byteaOutput | **string**
configSpec.<br>postgresqlConfig_12.<br>xmlbinary | **string**
configSpec.<br>postgresqlConfig_12.<br>xmloption | **string**
configSpec.<br>postgresqlConfig_12.<br>ginPendingListLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>deadlockTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>maxLocksPerTransaction | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>maxPredLocksPerTransaction | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>arrayNulls | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>backslashQuote | **string**
configSpec.<br>postgresqlConfig_12.<br>defaultWithOids | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>escapeStringWarning | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>loCompatPrivileges | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>operatorPrecedenceWarning | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>quoteAllIdentifiers | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>standardConformingStrings | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>synchronizeSeqscans | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>transformNullEquals | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>exitOnError | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>seqPageCost | **number** (double)
configSpec.<br>postgresqlConfig_12.<br>randomPageCost | **number** (double)
configSpec.<br>postgresqlConfig_12.<br>autovacuumMaxWorkers | **integer** (int64)<br><p>Acceptable values are 1 to 32, inclusive.</p> 
configSpec.<br>postgresqlConfig_12.<br>autovacuumVacuumCostDelay | **integer** (int64)<br><p>Acceptable values are -1 to 100, inclusive.</p> 
configSpec.<br>postgresqlConfig_12.<br>autovacuumVacuumCostLimit | **integer** (int64)<br><p>Acceptable values are -1 to 10000, inclusive.</p> 
configSpec.<br>postgresqlConfig_12.<br>autovacuumNaptime | **integer** (int64)<br><p>Acceptable values are 1000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_12.<br>archiveTimeout | **integer** (int64)<br><p>Acceptable values are 10000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_12.<br>trackActivityQuerySize | **integer** (int64)<br><p>Acceptable values are 100 to 102400, inclusive.</p> 
configSpec.<br>postgresqlConfig_12.<br>enableBitmapscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>enableHashagg | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>enableHashjoin | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>enableIndexscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>enableIndexonlyscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>enableMaterial | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>enableMergejoin | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>enableNestloop | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>enableSeqscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>enableSort | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>enableTidscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>maxWorkerProcesses | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
configSpec.<br>postgresqlConfig_12.<br>maxParallelWorkers | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
configSpec.<br>postgresqlConfig_12.<br>maxParallelWorkersPerGather | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
configSpec.<br>postgresqlConfig_12.<br>autovacuumVacuumScaleFactor | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_12.<br>autovacuumAnalyzeScaleFactor | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_12.<br>defaultTransactionReadOnly | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>timezone | **string**
configSpec.<br>postgresqlConfig_12.<br>enableParallelAppend | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>enableParallelHash | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>enablePartitionPruning | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>enablePartitionwiseAggregate | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>enablePartitionwiseJoin | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>jit | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>maxParallelMaintenanceWorkers | **integer** (int64)<br><p>The minimum value is 0.</p> 
configSpec.<br>postgresqlConfig_12.<br>parallelLeaderParticipation | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>vacuumCleanupIndexScaleFactor | **number** (double)<br><p>Acceptable values are 0 to 10000000000, inclusive.</p> 
configSpec.<br>postgresqlConfig_12.<br>logTransactionSampleRate | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_12.<br>planCacheMode | **string**
configSpec.<br>postgresqlConfig_12.<br>effectiveIoConcurrency | **integer** (int64)<br><p>Acceptable values are 0 to 1000, inclusive.</p> 
configSpec.<br>postgresqlConfig_12.<br>effectiveCacheSize | **integer** (int64)<br><p>Acceptable values are 0 to 549755813888, inclusive.</p> 
configSpec.<br>postgresqlConfig_12.<br>sharedPreloadLibraries[] | **string**
configSpec.<br>postgresqlConfig_12.<br>autoExplainLogMinDuration | **integer** (int64)<br><p>Acceptable values are -1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_12.<br>autoExplainLogAnalyze | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>autoExplainLogBuffers | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>autoExplainLogTiming | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>autoExplainLogTriggers | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>autoExplainLogVerbose | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>autoExplainLogNestedStatements | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>autoExplainSampleRate | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_12.<br>pgHintPlanEnableHint | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>pgHintPlanEnableHintTable | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>pgHintPlanDebugPrint | **string**
configSpec.<br>postgresqlConfig_12.<br>pgHintPlanMessageLevel | **string**
configSpec.<br>postgresqlConfig_12.<br>pgQualstatsEnabled | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>pgQualstatsTrackConstants | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>pgQualstatsMax | **integer** (int64)
configSpec.<br>postgresqlConfig_12.<br>pgQualstatsResolveOids | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12.<br>pgQualstatsSampleRate | **number** (double)
configSpec.<br>postgresqlConfig_12_1C | **object**<br>Configuration for a PostgreSQL 12 1C cluster. <br>`configSpec` includes only one of the fields `postgresqlConfig_9_6`, `postgresqlConfig_10_1C`, `postgresqlConfig_10`, `postgresqlConfig_11`, `postgresqlConfig_11_1C`, `postgresqlConfig_12`, `postgresqlConfig_12_1C`, `postgresqlConfig_13`, `postgresqlConfig_14`<br>
configSpec.<br>postgresqlConfig_12_1C.<br>maxConnections | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>sharedBuffers | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>tempBuffers | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>maxPreparedTransactions | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>workMem | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>maintenanceWorkMem | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>autovacuumWorkMem | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>tempFileLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>vacuumCostDelay | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>vacuumCostPageHit | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>vacuumCostPageMiss | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>vacuumCostPageDirty | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>vacuumCostLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>bgwriterDelay | **integer** (int64)<br><p>Acceptable values are 10 to 10000, inclusive.</p> 
configSpec.<br>postgresqlConfig_12_1C.<br>bgwriterLruMaxpages | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>bgwriterLruMultiplier | **number** (double)
configSpec.<br>postgresqlConfig_12_1C.<br>bgwriterFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_12_1C.<br>backendFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_12_1C.<br>oldSnapshotThreshold | **integer** (int64)<br><p>Acceptable values are -1 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_12_1C.<br>walLevel | **string**
configSpec.<br>postgresqlConfig_12_1C.<br>synchronousCommit | **string**
configSpec.<br>postgresqlConfig_12_1C.<br>checkpointTimeout | **integer** (int64)<br><p>Acceptable values are 30000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_12_1C.<br>checkpointCompletionTarget | **number** (double)
configSpec.<br>postgresqlConfig_12_1C.<br>checkpointFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_12_1C.<br>maxWalSize | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>minWalSize | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>maxStandbyStreamingDelay | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>defaultStatisticsTarget | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>constraintExclusion | **string**
configSpec.<br>postgresqlConfig_12_1C.<br>cursorTupleFraction | **number** (double)
configSpec.<br>postgresqlConfig_12_1C.<br>fromCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_12_1C.<br>joinCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_12_1C.<br>forceParallelMode | **string**
configSpec.<br>postgresqlConfig_12_1C.<br>clientMinMessages | **string**
configSpec.<br>postgresqlConfig_12_1C.<br>logMinMessages | **string**
configSpec.<br>postgresqlConfig_12_1C.<br>logMinErrorStatement | **string**
configSpec.<br>postgresqlConfig_12_1C.<br>logMinDurationStatement | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>logCheckpoints | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>logConnections | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>logDisconnections | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>logDuration | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>logErrorVerbosity | **string**
configSpec.<br>postgresqlConfig_12_1C.<br>logLockWaits | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>logStatement | **string**
configSpec.<br>postgresqlConfig_12_1C.<br>logTempFiles | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>searchPath | **string**
configSpec.<br>postgresqlConfig_12_1C.<br>rowSecurity | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>defaultTransactionIsolation | **string**
configSpec.<br>postgresqlConfig_12_1C.<br>statementTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>lockTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>idleInTransactionSessionTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>byteaOutput | **string**
configSpec.<br>postgresqlConfig_12_1C.<br>xmlbinary | **string**
configSpec.<br>postgresqlConfig_12_1C.<br>xmloption | **string**
configSpec.<br>postgresqlConfig_12_1C.<br>ginPendingListLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>deadlockTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>maxLocksPerTransaction | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>maxPredLocksPerTransaction | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>arrayNulls | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>backslashQuote | **string**
configSpec.<br>postgresqlConfig_12_1C.<br>defaultWithOids | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>escapeStringWarning | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>loCompatPrivileges | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>operatorPrecedenceWarning | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>quoteAllIdentifiers | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>standardConformingStrings | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>synchronizeSeqscans | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>transformNullEquals | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>exitOnError | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>seqPageCost | **number** (double)
configSpec.<br>postgresqlConfig_12_1C.<br>randomPageCost | **number** (double)
configSpec.<br>postgresqlConfig_12_1C.<br>autovacuumMaxWorkers | **integer** (int64)<br><p>Acceptable values are 1 to 32, inclusive.</p> 
configSpec.<br>postgresqlConfig_12_1C.<br>autovacuumVacuumCostDelay | **integer** (int64)<br><p>Acceptable values are -1 to 100, inclusive.</p> 
configSpec.<br>postgresqlConfig_12_1C.<br>autovacuumVacuumCostLimit | **integer** (int64)<br><p>Acceptable values are -1 to 10000, inclusive.</p> 
configSpec.<br>postgresqlConfig_12_1C.<br>autovacuumNaptime | **integer** (int64)<br><p>Acceptable values are 1000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_12_1C.<br>archiveTimeout | **integer** (int64)<br><p>Acceptable values are 10000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_12_1C.<br>trackActivityQuerySize | **integer** (int64)<br><p>Acceptable values are 100 to 102400, inclusive.</p> 
configSpec.<br>postgresqlConfig_12_1C.<br>enableBitmapscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>enableHashagg | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>enableHashjoin | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>enableIndexscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>enableIndexonlyscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>enableMaterial | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>enableMergejoin | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>enableNestloop | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>enableSeqscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>enableSort | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>enableTidscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>maxWorkerProcesses | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
configSpec.<br>postgresqlConfig_12_1C.<br>maxParallelWorkers | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
configSpec.<br>postgresqlConfig_12_1C.<br>maxParallelWorkersPerGather | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
configSpec.<br>postgresqlConfig_12_1C.<br>autovacuumVacuumScaleFactor | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_12_1C.<br>autovacuumAnalyzeScaleFactor | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_12_1C.<br>defaultTransactionReadOnly | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>timezone | **string**
configSpec.<br>postgresqlConfig_12_1C.<br>enableParallelAppend | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>enableParallelHash | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>enablePartitionPruning | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>enablePartitionwiseAggregate | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>enablePartitionwiseJoin | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>jit | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>maxParallelMaintenanceWorkers | **integer** (int64)<br><p>The minimum value is 0.</p> 
configSpec.<br>postgresqlConfig_12_1C.<br>parallelLeaderParticipation | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>vacuumCleanupIndexScaleFactor | **number** (double)<br><p>Acceptable values are 0 to 10000000000, inclusive.</p> 
configSpec.<br>postgresqlConfig_12_1C.<br>logTransactionSampleRate | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_12_1C.<br>planCacheMode | **string**
configSpec.<br>postgresqlConfig_12_1C.<br>effectiveIoConcurrency | **integer** (int64)<br><p>Acceptable values are 0 to 1000, inclusive.</p> 
configSpec.<br>postgresqlConfig_12_1C.<br>effectiveCacheSize | **integer** (int64)<br><p>Acceptable values are 0 to 549755813888, inclusive.</p> 
configSpec.<br>postgresqlConfig_12_1C.<br>sharedPreloadLibraries[] | **string**
configSpec.<br>postgresqlConfig_12_1C.<br>autoExplainLogMinDuration | **integer** (int64)<br><p>Acceptable values are -1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_12_1C.<br>autoExplainLogAnalyze | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>autoExplainLogBuffers | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>autoExplainLogTiming | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>autoExplainLogTriggers | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>autoExplainLogVerbose | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>autoExplainLogNestedStatements | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>autoExplainSampleRate | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_12_1C.<br>pgHintPlanEnableHint | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>pgHintPlanEnableHintTable | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>pgHintPlanDebugPrint | **string**
configSpec.<br>postgresqlConfig_12_1C.<br>pgHintPlanMessageLevel | **string**
configSpec.<br>postgresqlConfig_12_1C.<br>pgQualstatsEnabled | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>pgQualstatsTrackConstants | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>pgQualstatsMax | **integer** (int64)
configSpec.<br>postgresqlConfig_12_1C.<br>pgQualstatsResolveOids | **boolean** (boolean)
configSpec.<br>postgresqlConfig_12_1C.<br>pgQualstatsSampleRate | **number** (double)
configSpec.<br>postgresqlConfig_13 | **object**<br>Configuration for a PostgreSQL 13 cluster. <br>`configSpec` includes only one of the fields `postgresqlConfig_9_6`, `postgresqlConfig_10_1C`, `postgresqlConfig_10`, `postgresqlConfig_11`, `postgresqlConfig_11_1C`, `postgresqlConfig_12`, `postgresqlConfig_12_1C`, `postgresqlConfig_13`, `postgresqlConfig_14`<br>
configSpec.<br>postgresqlConfig_13.<br>maxConnections | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>sharedBuffers | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>tempBuffers | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>maxPreparedTransactions | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>workMem | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>maintenanceWorkMem | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>autovacuumWorkMem | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>tempFileLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>vacuumCostDelay | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>vacuumCostPageHit | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>vacuumCostPageMiss | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>vacuumCostPageDirty | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>vacuumCostLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>bgwriterDelay | **integer** (int64)<br><p>Acceptable values are 10 to 10000, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>bgwriterLruMaxpages | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>bgwriterLruMultiplier | **number** (double)
configSpec.<br>postgresqlConfig_13.<br>bgwriterFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>backendFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>oldSnapshotThreshold | **integer** (int64)<br><p>Acceptable values are -1 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>walLevel | **string**
configSpec.<br>postgresqlConfig_13.<br>synchronousCommit | **string**
configSpec.<br>postgresqlConfig_13.<br>checkpointTimeout | **integer** (int64)<br><p>Acceptable values are 30000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>checkpointCompletionTarget | **number** (double)
configSpec.<br>postgresqlConfig_13.<br>checkpointFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>maxWalSize | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>minWalSize | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>maxStandbyStreamingDelay | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>defaultStatisticsTarget | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>constraintExclusion | **string**
configSpec.<br>postgresqlConfig_13.<br>cursorTupleFraction | **number** (double)
configSpec.<br>postgresqlConfig_13.<br>fromCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>joinCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>forceParallelMode | **string**
configSpec.<br>postgresqlConfig_13.<br>clientMinMessages | **string**
configSpec.<br>postgresqlConfig_13.<br>logMinMessages | **string**
configSpec.<br>postgresqlConfig_13.<br>logMinErrorStatement | **string**
configSpec.<br>postgresqlConfig_13.<br>logMinDurationStatement | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>logCheckpoints | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>logConnections | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>logDisconnections | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>logDuration | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>logErrorVerbosity | **string**
configSpec.<br>postgresqlConfig_13.<br>logLockWaits | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>logStatement | **string**
configSpec.<br>postgresqlConfig_13.<br>logTempFiles | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>searchPath | **string**
configSpec.<br>postgresqlConfig_13.<br>rowSecurity | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>defaultTransactionIsolation | **string**
configSpec.<br>postgresqlConfig_13.<br>statementTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>lockTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>idleInTransactionSessionTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>byteaOutput | **string**
configSpec.<br>postgresqlConfig_13.<br>xmlbinary | **string**
configSpec.<br>postgresqlConfig_13.<br>xmloption | **string**
configSpec.<br>postgresqlConfig_13.<br>ginPendingListLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>deadlockTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>maxLocksPerTransaction | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>maxPredLocksPerTransaction | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>arrayNulls | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>backslashQuote | **string**
configSpec.<br>postgresqlConfig_13.<br>defaultWithOids | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>escapeStringWarning | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>loCompatPrivileges | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>operatorPrecedenceWarning | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>quoteAllIdentifiers | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>standardConformingStrings | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>synchronizeSeqscans | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>transformNullEquals | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>exitOnError | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>seqPageCost | **number** (double)
configSpec.<br>postgresqlConfig_13.<br>randomPageCost | **number** (double)
configSpec.<br>postgresqlConfig_13.<br>autovacuumMaxWorkers | **integer** (int64)<br><p>Acceptable values are 1 to 32, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>autovacuumVacuumCostDelay | **integer** (int64)<br><p>Acceptable values are -1 to 100, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>autovacuumVacuumCostLimit | **integer** (int64)<br><p>Acceptable values are -1 to 10000, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>autovacuumNaptime | **integer** (int64)<br><p>Acceptable values are 1000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>archiveTimeout | **integer** (int64)<br><p>Acceptable values are 10000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>trackActivityQuerySize | **integer** (int64)<br><p>Acceptable values are 100 to 102400, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>enableBitmapscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>enableHashagg | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>enableHashjoin | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>enableIndexscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>enableIndexonlyscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>enableMaterial | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>enableMergejoin | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>enableNestloop | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>enableSeqscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>enableSort | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>enableTidscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>maxWorkerProcesses | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>maxParallelWorkers | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>maxParallelWorkersPerGather | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>autovacuumVacuumScaleFactor | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>autovacuumAnalyzeScaleFactor | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>defaultTransactionReadOnly | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>timezone | **string**
configSpec.<br>postgresqlConfig_13.<br>enableParallelAppend | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>enableParallelHash | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>enablePartitionPruning | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>enablePartitionwiseAggregate | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>enablePartitionwiseJoin | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>jit | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>maxParallelMaintenanceWorkers | **integer** (int64)<br><p>The minimum value is 0.</p> 
configSpec.<br>postgresqlConfig_13.<br>parallelLeaderParticipation | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>vacuumCleanupIndexScaleFactor | **number** (double)<br><p>Acceptable values are 0 to 10000000000, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>logTransactionSampleRate | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>planCacheMode | **string**
configSpec.<br>postgresqlConfig_13.<br>effectiveIoConcurrency | **integer** (int64)<br><p>Acceptable values are 0 to 1000, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>effectiveCacheSize | **integer** (int64)<br><p>Acceptable values are 0 to 549755813888, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>sharedPreloadLibraries[] | **string**
configSpec.<br>postgresqlConfig_13.<br>autoExplainLogMinDuration | **integer** (int64)<br><p>Acceptable values are -1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>autoExplainLogAnalyze | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>autoExplainLogBuffers | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>autoExplainLogTiming | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>autoExplainLogTriggers | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>autoExplainLogVerbose | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>autoExplainLogNestedStatements | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>autoExplainSampleRate | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>pgHintPlanEnableHint | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>pgHintPlanEnableHintTable | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>pgHintPlanDebugPrint | **string**
configSpec.<br>postgresqlConfig_13.<br>pgHintPlanMessageLevel | **string**
configSpec.<br>postgresqlConfig_13.<br>hashMemMultiplier | **number** (double)<br><p>Acceptable values are 0 to 1000, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>logicalDecodingWorkMem | **integer** (int64)<br><p>Acceptable values are 65536 to 1099511627776, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>maintenanceIoConcurrency | **integer** (int64)<br><p>Acceptable values are 0 to 1000, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>maxSlotWalKeepSize | **integer** (int64)<br><p>Acceptable values are -1 to 2251799812636672, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>walKeepSize | **integer** (int64)<br><p>Acceptable values are -1 to 2251799812636672, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>enableIncrementalSort | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>autovacuumVacuumInsertThreshold | **integer** (int64)<br><p>Acceptable values are -1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>autovacuumVacuumInsertScaleFactor | **number** (double)<br><p>Acceptable values are 0 to 100, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>logMinDurationSample | **integer** (int64)<br><p>Acceptable values are -1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>logStatementSampleRate | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>logParameterMaxLength | **integer** (int64)<br><p>Acceptable values are -1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>logParameterMaxLengthOnError | **integer** (int64)<br><p>Acceptable values are -1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_13.<br>pgQualstatsEnabled | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>pgQualstatsTrackConstants | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>pgQualstatsMax | **integer** (int64)
configSpec.<br>postgresqlConfig_13.<br>pgQualstatsResolveOids | **boolean** (boolean)
configSpec.<br>postgresqlConfig_13.<br>pgQualstatsSampleRate | **number** (double)
configSpec.<br>postgresqlConfig_14 | **object**<br>Configuration for a PostgreSQL 14 cluster. <br>`configSpec` includes only one of the fields `postgresqlConfig_9_6`, `postgresqlConfig_10_1C`, `postgresqlConfig_10`, `postgresqlConfig_11`, `postgresqlConfig_11_1C`, `postgresqlConfig_12`, `postgresqlConfig_12_1C`, `postgresqlConfig_13`, `postgresqlConfig_14`<br>
configSpec.<br>postgresqlConfig_14.<br>maxConnections | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>sharedBuffers | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>tempBuffers | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>maxPreparedTransactions | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>workMem | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>maintenanceWorkMem | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>autovacuumWorkMem | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>tempFileLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>vacuumCostDelay | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>vacuumCostPageHit | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>vacuumCostPageMiss | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>vacuumCostPageDirty | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>vacuumCostLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>bgwriterDelay | **integer** (int64)<br><p>Acceptable values are 10 to 10000, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>bgwriterLruMaxpages | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>bgwriterLruMultiplier | **number** (double)
configSpec.<br>postgresqlConfig_14.<br>bgwriterFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>backendFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>oldSnapshotThreshold | **integer** (int64)<br><p>Acceptable values are -1 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>walLevel | **string**
configSpec.<br>postgresqlConfig_14.<br>synchronousCommit | **string**
configSpec.<br>postgresqlConfig_14.<br>checkpointTimeout | **integer** (int64)<br><p>Acceptable values are 30000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>checkpointCompletionTarget | **number** (double)
configSpec.<br>postgresqlConfig_14.<br>checkpointFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>maxWalSize | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>minWalSize | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>maxStandbyStreamingDelay | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>defaultStatisticsTarget | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>constraintExclusion | **string**
configSpec.<br>postgresqlConfig_14.<br>cursorTupleFraction | **number** (double)
configSpec.<br>postgresqlConfig_14.<br>fromCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>joinCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>forceParallelMode | **string**
configSpec.<br>postgresqlConfig_14.<br>clientMinMessages | **string**
configSpec.<br>postgresqlConfig_14.<br>logMinMessages | **string**
configSpec.<br>postgresqlConfig_14.<br>logMinErrorStatement | **string**
configSpec.<br>postgresqlConfig_14.<br>logMinDurationStatement | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>logCheckpoints | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>logConnections | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>logDisconnections | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>logDuration | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>logErrorVerbosity | **string**
configSpec.<br>postgresqlConfig_14.<br>logLockWaits | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>logStatement | **string**
configSpec.<br>postgresqlConfig_14.<br>logTempFiles | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>searchPath | **string**
configSpec.<br>postgresqlConfig_14.<br>rowSecurity | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>defaultTransactionIsolation | **string**
configSpec.<br>postgresqlConfig_14.<br>statementTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>lockTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>idleInTransactionSessionTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>byteaOutput | **string**
configSpec.<br>postgresqlConfig_14.<br>xmlbinary | **string**
configSpec.<br>postgresqlConfig_14.<br>xmloption | **string**
configSpec.<br>postgresqlConfig_14.<br>ginPendingListLimit | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>deadlockTimeout | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>maxLocksPerTransaction | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>maxPredLocksPerTransaction | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>arrayNulls | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>backslashQuote | **string**
configSpec.<br>postgresqlConfig_14.<br>defaultWithOids | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>escapeStringWarning | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>loCompatPrivileges | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>quoteAllIdentifiers | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>standardConformingStrings | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>synchronizeSeqscans | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>transformNullEquals | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>exitOnError | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>seqPageCost | **number** (double)
configSpec.<br>postgresqlConfig_14.<br>randomPageCost | **number** (double)
configSpec.<br>postgresqlConfig_14.<br>autovacuumMaxWorkers | **integer** (int64)<br><p>Acceptable values are 1 to 32, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>autovacuumVacuumCostDelay | **integer** (int64)<br><p>Acceptable values are -1 to 100, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>autovacuumVacuumCostLimit | **integer** (int64)<br><p>Acceptable values are -1 to 10000, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>autovacuumNaptime | **integer** (int64)<br><p>Acceptable values are 1000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>archiveTimeout | **integer** (int64)<br><p>Acceptable values are 10000 to 86400000, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>trackActivityQuerySize | **integer** (int64)<br><p>Acceptable values are 100 to 102400, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>enableBitmapscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>enableHashagg | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>enableHashjoin | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>enableIndexscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>enableIndexonlyscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>enableMaterial | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>enableMergejoin | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>enableNestloop | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>enableSeqscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>enableSort | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>enableTidscan | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>maxWorkerProcesses | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>maxParallelWorkers | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>maxParallelWorkersPerGather | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>autovacuumVacuumScaleFactor | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>autovacuumAnalyzeScaleFactor | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>defaultTransactionReadOnly | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>timezone | **string**
configSpec.<br>postgresqlConfig_14.<br>enableParallelAppend | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>enableParallelHash | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>enablePartitionPruning | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>enablePartitionwiseAggregate | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>enablePartitionwiseJoin | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>jit | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>maxParallelMaintenanceWorkers | **integer** (int64)<br><p>The minimum value is 0.</p> 
configSpec.<br>postgresqlConfig_14.<br>parallelLeaderParticipation | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>logTransactionSampleRate | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>planCacheMode | **string**
configSpec.<br>postgresqlConfig_14.<br>effectiveIoConcurrency | **integer** (int64)<br><p>Acceptable values are 0 to 1000, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>effectiveCacheSize | **integer** (int64)<br><p>Acceptable values are 0 to 549755813888, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>sharedPreloadLibraries[] | **string**
configSpec.<br>postgresqlConfig_14.<br>autoExplainLogMinDuration | **integer** (int64)<br><p>Acceptable values are -1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>autoExplainLogAnalyze | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>autoExplainLogBuffers | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>autoExplainLogTiming | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>autoExplainLogTriggers | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>autoExplainLogVerbose | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>autoExplainLogNestedStatements | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>autoExplainSampleRate | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>pgHintPlanEnableHint | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>pgHintPlanEnableHintTable | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>pgHintPlanDebugPrint | **string**
configSpec.<br>postgresqlConfig_14.<br>pgHintPlanMessageLevel | **string**
configSpec.<br>postgresqlConfig_14.<br>hashMemMultiplier | **number** (double)<br><p>Acceptable values are 0 to 1000, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>logicalDecodingWorkMem | **integer** (int64)<br><p>Acceptable values are 65536 to 1099511627776, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>maintenanceIoConcurrency | **integer** (int64)<br><p>Acceptable values are 0 to 1000, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>maxSlotWalKeepSize | **integer** (int64)<br><p>Acceptable values are -1 to 2251799812636672, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>walKeepSize | **integer** (int64)<br><p>Acceptable values are -1 to 2251799812636672, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>enableIncrementalSort | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>autovacuumVacuumInsertThreshold | **integer** (int64)<br><p>Acceptable values are -1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>autovacuumVacuumInsertScaleFactor | **number** (double)<br><p>Acceptable values are 0 to 100, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>logMinDurationSample | **integer** (int64)<br><p>Acceptable values are -1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>logStatementSampleRate | **number** (double)<br><p>Acceptable values are 0 to 1, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>logParameterMaxLength | **integer** (int64)<br><p>Acceptable values are -1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>logParameterMaxLengthOnError | **integer** (int64)<br><p>Acceptable values are -1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>clientConnectionCheckInterval | **integer** (int64)<br><p>Acceptable values are -1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>enableAsyncAppend | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>enableGathermerge | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>enableMemoize | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>logRecoveryConflictWaits | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>vacuumFailsafeAge | **integer** (int64)<br><p>Acceptable values are -1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>vacuumMultixactFailsafeAge | **integer** (int64)<br><p>Acceptable values are -1 to 2147483647, inclusive.</p> 
configSpec.<br>postgresqlConfig_14.<br>pgQualstatsEnabled | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>pgQualstatsTrackConstants | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>pgQualstatsMax | **integer** (int64)
configSpec.<br>postgresqlConfig_14.<br>pgQualstatsResolveOids | **boolean** (boolean)
configSpec.<br>postgresqlConfig_14.<br>pgQualstatsSampleRate | **number** (double)
databaseSpecs[] | **object**<br><p>Required. Descriptions of databases to be created in the PostgreSQL cluster.</p> 
databaseSpecs[].<br>name | **string**<br><p>Required. Name of the PostgreSQL database. 1-63 characters long.</p> <p>The maximum string length in characters is 63. Value must match the regular expression ``[a-zA-Z0-9_-]*``.</p> 
databaseSpecs[].<br>owner | **string**<br><p>Required. Name of the user to be assigned as the owner of the database. To get the list of available PostgreSQL users, make a <a href="/docs/managed-postgresql/api-ref/User/list">list</a> request.</p> <p>The maximum string length in characters is 63. Value must match the regular expression ``[a-zA-Z0-9_]*``.</p> 
databaseSpecs[].<br>lcCollate | **string**<br><p>POSIX locale for string sorting order. Can only be set at creation time.</p> <p>Value must match the regular expression ``\|[a-zA-Z_]+.UTF-8\|C``.</p> 
databaseSpecs[].<br>lcCtype | **string**<br><p>POSIX locale for character classification. Can only be set at creation time.</p> <p>Value must match the regular expression ``\|[a-zA-Z_]+.UTF-8\|C``.</p> 
databaseSpecs[].<br>extensions[] | **object**<br><p>PostgreSQL extensions to be enabled for the database.</p> 
databaseSpecs[].<br>extensions[].<br>name | **string**<br><p>Name of the extension, e.g. ``pg_trgm`` or ``pg_btree``. Extensions supported by Managed Service for PostgreSQL are <a href="/docs/managed-postgresql/operations/cluster-extensions">listed in the Developer's Guide</a>.</p> 
databaseSpecs[].<br>extensions[].<br>version | **string**<br><p>Version of the extension.</p> 
databaseSpecs[].<br>templateDb | **string**<br><p>Name of the PostgreSQL database template.</p> <p>The maximum string length in characters is 63. Value must match the regular expression ``[a-zA-Z0-9_-]*``.</p> 
userSpecs[] | **object**<br><p>Required. Descriptions of database users to be created in the PostgreSQL cluster.</p> 
userSpecs[].<br>name | **string**<br><p>Required. Name of the PostgreSQL user.</p> <p>The maximum string length in characters is 63. Value must match the regular expression ``[a-zA-Z0-9_]*``.</p> 
userSpecs[].<br>password | **string**<br><p>Required. Password of the PostgreSQL user.</p> <p>The string length in characters must be 8-128.</p> 
userSpecs[].<br>permissions[] | **object**<br><p>Set of permissions to grant to the user to access specific databases.</p> 
userSpecs[].<br>permissions[].<br>databaseName | **string**<br><p>Name of the database that the permission grants access to.</p> 
userSpecs[].<br>connLimit | **integer** (int64)<br><p>Maximum number of database connections that should be available to the user.</p> <p>When used in session pooling, this setting limits the number of connections to every single host in PostgreSQL cluster. In this case, the setting's value must be greater than the total number of connections that backend services can open to access the PostgreSQL cluster. The setting's value should not exceed the value of the <a href="/docs/managed-postgresql/api-ref/Cluster#representation">Cluster.config.postgresqlConfig_12.effectiveConfig.maxConnections</a> setting.</p> <p>When used in transaction pooling, this setting limits the number of user's active transactions; therefore, in this mode user can open thousands of connections, but only ``N`` concurrent connections will be opened, where ``N`` is the value of the setting.</p> <p>Minimum value: ``10`` (default: ``50``), when used in session pooling.</p> <p>The minimum value is 10.</p> 
userSpecs[].<br>settings | **object**<br><p>PostgreSQL settings for the user.</p> <p>PostgreSQL user settings.</p> 
userSpecs[].<br>settings.<br>defaultTransactionIsolation | **string**<br><p>SQL sets an isolation level for each transaction. This setting defines the default isolation level to be set for all new SQL transactions.</p> <p>See in-depth description in <a href="https://www.postgresql.org/docs/current/transaction-iso.html">PostgreSQL documentation</a>.</p> <ul> <li>TRANSACTION_ISOLATION_READ_UNCOMMITTED: this level behaves like ``TRANSACTION_ISOLATION_READ_COMMITTED`` in PostgreSQL.</li> <li>TRANSACTION_ISOLATION_READ_COMMITTED: (default) on this level query sees only data committed before the query began.</li> <li>TRANSACTION_ISOLATION_REPEATABLE_READ: on this level all subsequent queries in a transaction will see the same rows, that were read by the first ``SELECT`` or ``INSERT`` query in this transaction, unchanged (these rows are locked during the first query).</li> <li>TRANSACTION_ISOLATION_SERIALIZABLE: this level provides the strictest transaction isolation. All queries in the current transaction see only the rows that were fixed prior to execution of the first ``SELECT`` or ``INSERT`` query in this transaction. If read and write operations in a concurrent set of serializable transactions overlap and this may cause an inconsistency that is not possible during the serial transaction execution, then one of the transaction will be rolled back, triggering a serialization failure.</li> </ul> 
userSpecs[].<br>settings.<br>lockTimeout | **integer** (int64)<br><p>The maximum time (in milliseconds) for any statement to wait for acquiring a lock on an table, index, row or other database object. If the wait time is longer than the specified amount, then this statement is aborted.</p> <p>Default value: ``0`` (no control is enforced, a statement waiting time is unlimited).</p> 
userSpecs[].<br>settings.<br>logMinDurationStatement | **integer** (int64)<br><p>This setting controls logging of the duration of statements.</p> <p>The duration of each completed statement will be logged if the statement ran for at least the specified amount of time (in milliseconds). E.g., if this setting's value is set to ``500``, a statement that took 300 milliseconds to complete will not be logged; on the other hand, the one that took 2000 milliseconds to complete, will be logged.</p> <p>Value of ``0`` forces PostgreSQL to log the duration of all statements.</p> <p>Value of ``-1`` (default) disables logging of the duration of statements.</p> <p>See in-depth description in <a href="https://www.postgresql.org/docs/current/runtime-config-logging.html">PostgreSQL documentation</a>.</p> 
userSpecs[].<br>settings.<br>synchronousCommit | **string**<br><p>This setting defines whether DBMS will commit transaction in a synchronous way.</p> <p>When synchronization is enabled, cluster waits for the synchronous operations to be completed prior to reporting ``success`` to the client. These operations guarantee different levels of the data safety and visibility in the cluster.</p> <p>See in-depth description in <a href="https://www.postgresql.org/docs/current/runtime-config-wal.html#GUC-SYNCHRONOUS-COMMIT">PostgreSQL documentation</a>.</p> <ul> <li>SYNCHRONOUS_COMMIT_ON: (default value) success is reported to the client if the data is in WAL (Write-Ahead Log), and WAL is written to the storage of both the master and its synchronous standby server.</li> <li>SYNCHRONOUS_COMMIT_OFF: success is reported to the client even if the data is not in WAL. There is no synchronous write operation, data may be loss in case of storage subsystem failure.</li> <li>SYNCHRONOUS_COMMIT_LOCAL: success is reported to the client if the data is in WAL, and WAL is written to the storage of the master server. The transaction may be lost due to storage subsystem failure on the master server.</li> <li>SYNCHRONOUS_COMMIT_REMOTE_WRITE: success is reported to the client if the data is in WAL, WAL is written to the storage of the master server, and the server's synchronous standby indicates that it has received WAL and written it out to its operating system. The transaction may be lost due to simultaneous storage subsystem failure on the master and operating system's failure on the synchronous standby.</li> <li>SYNCHRONOUS_COMMIT_REMOTE_APPLY: success is reported to the client if the data is in WAL (Write-Ahead Log), WAL is written to the storage of the master server, and its synchronous standby indicates that it has received WAL and applied it. The transaction may be lost due to irrecoverably failure of both the master and its synchronous standby.</li> </ul> 
userSpecs[].<br>settings.<br>tempFileLimit | **integer** (int64)<br><p>The maximum storage space size (in kilobytes) that a single process can use to create temporary files. If a transaction exceeds this limit during execution, it will be aborted.</p> <p>A huge query may not fit into a server's RAM, therefore PostgreSQL will use some storage to store and execute such a query. Too big queries can make excessive use of the storage system, effectively making other quieries to run slow. This setting prevents execution of a big queries that can influence other queries by limiting size of temporary files.</p> 
userSpecs[].<br>settings.<br>logStatement | **string**<br><p>This setting specifies which SQL statements should be logged (on the user level).</p> <p>See in-depth description in <a href="https://www.postgresql.org/docs/current/runtime-config-logging.html">PostgreSQL documentation</a>.</p> <ul> <li>LOG_STATEMENT_NONE: (default) logs none of SQL statements.</li> <li>LOG_STATEMENT_DDL: logs all data definition statements (such as ``CREATE``, ``ALTER``, ``DROP`` and others).</li> <li>LOG_STATEMENT_MOD: logs all statements that fall in the ``LOG_STATEMENT_DDL`` category plus data-modifying statements (such as ``INSERT``, ``UPDATE`` and others).</li> <li>LOG_STATEMENT_ALL: logs all SQL statements.</li> </ul> 
userSpecs[].<br>login | **boolean** (boolean)<br><p>This flag defines whether the user can login to a PostgreSQL database.</p> <p>Default value: ``true`` (login is allowed).</p> 
userSpecs[].<br>grants[] | **string**<br><p>Roles and privileges that are granted to the user (``GRANT &lt;role&gt; TO &lt;user&gt;``).</p> <p>For more information, see <a href="/docs/managed-postgresql/operations/grant">the documentation</a>.</p> <p>The maximum string length in characters for each value is 63. Each value must match the regular expression ``[a-zA-Z0-9_]*``.</p> 
hostSpecs[] | **object**<br><p>Required. Individual configurations for hosts that should be created for the PostgreSQL cluster.</p> 
hostSpecs[].<br>zoneId | **string**<br><p>ID of the availability zone where the host resides. To get a list of available zones, use the <a href="/docs/compute/api-ref/Zone/list">list</a> request.</p> <p>The maximum string length in characters is 50.</p> 
hostSpecs[].<br>subnetId | **string**<br><p>ID of the subnet that the host should belong to. This subnet should be a part of the network that the cluster belongs to. The ID of the network is set in the field <a href="/docs/managed-postgresql/api-ref/Cluster#representation">Cluster.networkId</a>.</p> <p>The maximum string length in characters is 50.</p> 
hostSpecs[].<br>assignPublicIp | **boolean** (boolean)<br><p>Whether the host should get a public IP address on creation.</p> <p>After a host has been created, this setting cannot be changed. To remove an assigned public IP, or to assign a public IP to a host without one, recreate the host with ``assignPublicIp`` set as needed.</p> <p>Possible values:</p> <ul> <li>false - don't assign a public IP to the host.</li> <li>true - the host should have a public IP address.</li> </ul> 
hostSpecs[].<br>replicationSource | **string**<br><p>``name`` of the host to be used as the replication source (for cascading replication).</p> 
hostSpecs[].<br>priority | **integer** (int64)<br><p>Priority of the host as a replica. A higher value corresponds to higher priority.</p> <p>The host with the highest priority is the synchronous replica. All others are asynchronous. The synchronous replica replaces the master when needed.</p> <p>When a replica becomes the master, its priority is ignored.</p> 
hostSpecs[].<br>configSpec | **object**<br><p>Configuration of a PostgreSQL server for the host.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6 | **object**<br>Configuration for a host with PostgreSQL 9.6 server deployed. <br>`hostSpecs[].configSpec` includes only one of the fields `postgresqlConfig_9_6`, `postgresqlConfig_10_1C`, `postgresqlConfig_10`, `postgresqlConfig_11`, `postgresqlConfig_11_1C`, `postgresqlConfig_12`, `postgresqlConfig_12_1C`, `postgresqlConfig_13`, `postgresqlConfig_14`<br>
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>recoveryMinApplyDelay | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>sharedBuffers | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>tempBuffers | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>workMem | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>replacementSortTuples | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>tempFileLimit | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>backendFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>oldSnapshotThreshold | **integer** (int64)<br><p>Acceptable values are -1 to 86400, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>maxStandbyStreamingDelay | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>constraintExclusion | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>cursorTupleFraction | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>fromCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>joinCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>forceParallelMode | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>clientMinMessages | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>logMinMessages | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>logMinErrorStatement | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>logMinDurationStatement | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>logCheckpoints | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>logConnections | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>logDisconnections | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>logDuration | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>logErrorVerbosity | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>logLockWaits | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>logStatement | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>logTempFiles | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>searchPath | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>rowSecurity | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>defaultTransactionIsolation | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>statementTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>lockTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>idleInTransactionSessionTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>byteaOutput | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>xmlbinary | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>xmloption | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>ginPendingListLimit | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>deadlockTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>maxLocksPerTransaction | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>maxPredLocksPerTransaction | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>arrayNulls | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>backslashQuote | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>defaultWithOids | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>escapeStringWarning | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>loCompatPrivileges | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>operatorPrecedenceWarning | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>quoteAllIdentifiers | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>standardConformingStrings | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>synchronizeSeqscans | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>transformNullEquals | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>exitOnError | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>seqPageCost | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>randomPageCost | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>sqlInheritance | **boolean** (boolean)<br><p>This option has been removed in PostgreSQL 10.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>effectiveIoConcurrency | **integer** (int64)<br><p>Acceptable values are 0 to 1000, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_9_6.<br>effectiveCacheSize | **integer** (int64)<br><p>Acceptable values are 0 to 549755813888, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C | **object**<br>Configuration for a host with PostgreSQL 10 1C server deployed. <br>`hostSpecs[].configSpec` includes only one of the fields `postgresqlConfig_9_6`, `postgresqlConfig_10_1C`, `postgresqlConfig_10`, `postgresqlConfig_11`, `postgresqlConfig_11_1C`, `postgresqlConfig_12`, `postgresqlConfig_12_1C`, `postgresqlConfig_13`, `postgresqlConfig_14`<br>
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>recoveryMinApplyDelay | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>sharedBuffers | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>tempBuffers | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>workMem | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>replacementSortTuples | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>tempFileLimit | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>backendFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>oldSnapshotThreshold | **integer** (int64)<br><p>Acceptable values are -1 to 86400, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>maxStandbyStreamingDelay | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>constraintExclusion | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>cursorTupleFraction | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>fromCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>joinCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>forceParallelMode | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>clientMinMessages | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>logMinMessages | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>logMinErrorStatement | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>logMinDurationStatement | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>logCheckpoints | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>logConnections | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>logDisconnections | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>logDuration | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>logErrorVerbosity | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>logLockWaits | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>logStatement | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>logTempFiles | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>searchPath | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>rowSecurity | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>defaultTransactionIsolation | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>statementTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>lockTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>idleInTransactionSessionTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>byteaOutput | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>xmlbinary | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>xmloption | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>ginPendingListLimit | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>deadlockTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>maxLocksPerTransaction | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>maxPredLocksPerTransaction | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>arrayNulls | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>backslashQuote | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>defaultWithOids | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>escapeStringWarning | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>loCompatPrivileges | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>operatorPrecedenceWarning | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>quoteAllIdentifiers | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>standardConformingStrings | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>synchronizeSeqscans | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>transformNullEquals | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>exitOnError | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>seqPageCost | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>randomPageCost | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>enableBitmapscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>enableHashagg | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>enableHashjoin | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>enableIndexscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>enableIndexonlyscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>enableMaterial | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>enableMergejoin | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>enableNestloop | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>enableSeqscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>enableSort | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>enableTidscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>maxParallelWorkers | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>maxParallelWorkersPerGather | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>timezone | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>effectiveIoConcurrency | **integer** (int64)<br><p>Acceptable values are 0 to 1000, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10_1C.<br>effectiveCacheSize | **integer** (int64)<br><p>Acceptable values are 0 to 549755813888, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10 | **object**<br>Configuration for a host with PostgreSQL 10 server deployed. <br>`hostSpecs[].configSpec` includes only one of the fields `postgresqlConfig_9_6`, `postgresqlConfig_10_1C`, `postgresqlConfig_10`, `postgresqlConfig_11`, `postgresqlConfig_11_1C`, `postgresqlConfig_12`, `postgresqlConfig_12_1C`, `postgresqlConfig_13`, `postgresqlConfig_14`<br>
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>recoveryMinApplyDelay | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>sharedBuffers | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>tempBuffers | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>workMem | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>replacementSortTuples | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>tempFileLimit | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>backendFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>oldSnapshotThreshold | **integer** (int64)<br><p>Acceptable values are -1 to 86400, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>maxStandbyStreamingDelay | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>constraintExclusion | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>cursorTupleFraction | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>fromCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>joinCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>forceParallelMode | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>clientMinMessages | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>logMinMessages | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>logMinErrorStatement | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>logMinDurationStatement | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>logCheckpoints | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>logConnections | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>logDisconnections | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>logDuration | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>logErrorVerbosity | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>logLockWaits | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>logStatement | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>logTempFiles | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>searchPath | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>rowSecurity | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>defaultTransactionIsolation | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>statementTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>lockTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>idleInTransactionSessionTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>byteaOutput | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>xmlbinary | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>xmloption | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>ginPendingListLimit | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>deadlockTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>maxLocksPerTransaction | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>maxPredLocksPerTransaction | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>arrayNulls | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>backslashQuote | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>defaultWithOids | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>escapeStringWarning | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>loCompatPrivileges | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>operatorPrecedenceWarning | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>quoteAllIdentifiers | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>standardConformingStrings | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>synchronizeSeqscans | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>transformNullEquals | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>exitOnError | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>seqPageCost | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>randomPageCost | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>enableBitmapscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>enableHashagg | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>enableHashjoin | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>enableIndexscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>enableIndexonlyscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>enableMaterial | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>enableMergejoin | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>enableNestloop | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>enableSeqscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>enableSort | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>enableTidscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>maxParallelWorkers | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>maxParallelWorkersPerGather | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>timezone | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>effectiveIoConcurrency | **integer** (int64)<br><p>Acceptable values are 0 to 1000, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_10.<br>effectiveCacheSize | **integer** (int64)<br><p>Acceptable values are 0 to 549755813888, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11 | **object**<br>Configuration for a host with PostgreSQL 11 server deployed. <br>`hostSpecs[].configSpec` includes only one of the fields `postgresqlConfig_9_6`, `postgresqlConfig_10_1C`, `postgresqlConfig_10`, `postgresqlConfig_11`, `postgresqlConfig_11_1C`, `postgresqlConfig_12`, `postgresqlConfig_12_1C`, `postgresqlConfig_13`, `postgresqlConfig_14`<br>
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>recoveryMinApplyDelay | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>sharedBuffers | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>tempBuffers | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>workMem | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>tempFileLimit | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>backendFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>oldSnapshotThreshold | **integer** (int64)<br><p>Acceptable values are -1 to 86400, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>maxStandbyStreamingDelay | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>constraintExclusion | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>cursorTupleFraction | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>fromCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>joinCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>forceParallelMode | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>clientMinMessages | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>logMinMessages | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>logMinErrorStatement | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>logMinDurationStatement | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>logCheckpoints | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>logConnections | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>logDisconnections | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>logDuration | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>logErrorVerbosity | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>logLockWaits | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>logStatement | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>logTempFiles | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>searchPath | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>rowSecurity | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>defaultTransactionIsolation | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>statementTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>lockTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>idleInTransactionSessionTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>byteaOutput | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>xmlbinary | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>xmloption | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>ginPendingListLimit | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>deadlockTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>maxLocksPerTransaction | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>maxPredLocksPerTransaction | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>arrayNulls | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>backslashQuote | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>defaultWithOids | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>escapeStringWarning | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>loCompatPrivileges | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>operatorPrecedenceWarning | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>quoteAllIdentifiers | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>standardConformingStrings | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>synchronizeSeqscans | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>transformNullEquals | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>exitOnError | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>seqPageCost | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>randomPageCost | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>enableBitmapscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>enableHashagg | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>enableHashjoin | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>enableIndexscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>enableIndexonlyscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>enableMaterial | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>enableMergejoin | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>enableNestloop | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>enableSeqscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>enableSort | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>enableTidscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>maxParallelWorkers | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>maxParallelWorkersPerGather | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>timezone | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>effectiveIoConcurrency | **integer** (int64)<br><p>Acceptable values are 0 to 1000, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11.<br>effectiveCacheSize | **integer** (int64)<br><p>Acceptable values are 0 to 549755813888, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C | **object**<br>Configuration for a host with PostgreSQL 11 1C server deployed. <br>`hostSpecs[].configSpec` includes only one of the fields `postgresqlConfig_9_6`, `postgresqlConfig_10_1C`, `postgresqlConfig_10`, `postgresqlConfig_11`, `postgresqlConfig_11_1C`, `postgresqlConfig_12`, `postgresqlConfig_12_1C`, `postgresqlConfig_13`, `postgresqlConfig_14`<br>
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>recoveryMinApplyDelay | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>sharedBuffers | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>tempBuffers | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>workMem | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>tempFileLimit | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>backendFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>oldSnapshotThreshold | **integer** (int64)<br><p>Acceptable values are -1 to 86400, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>maxStandbyStreamingDelay | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>constraintExclusion | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>cursorTupleFraction | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>fromCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>joinCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>forceParallelMode | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>clientMinMessages | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>logMinMessages | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>logMinErrorStatement | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>logMinDurationStatement | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>logCheckpoints | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>logConnections | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>logDisconnections | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>logDuration | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>logErrorVerbosity | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>logLockWaits | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>logStatement | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>logTempFiles | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>searchPath | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>rowSecurity | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>defaultTransactionIsolation | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>statementTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>lockTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>idleInTransactionSessionTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>byteaOutput | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>xmlbinary | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>xmloption | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>ginPendingListLimit | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>deadlockTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>maxLocksPerTransaction | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>maxPredLocksPerTransaction | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>arrayNulls | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>backslashQuote | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>defaultWithOids | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>escapeStringWarning | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>loCompatPrivileges | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>operatorPrecedenceWarning | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>quoteAllIdentifiers | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>standardConformingStrings | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>synchronizeSeqscans | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>transformNullEquals | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>exitOnError | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>seqPageCost | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>randomPageCost | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>enableBitmapscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>enableHashagg | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>enableHashjoin | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>enableIndexscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>enableIndexonlyscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>enableMaterial | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>enableMergejoin | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>enableNestloop | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>enableSeqscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>enableSort | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>enableTidscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>maxParallelWorkers | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>maxParallelWorkersPerGather | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>timezone | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>effectiveIoConcurrency | **integer** (int64)<br><p>Acceptable values are 0 to 1000, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_11_1C.<br>effectiveCacheSize | **integer** (int64)<br><p>Acceptable values are 0 to 549755813888, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12 | **object**<br>Configuration for a host with PostgreSQL 12 server deployed. <br>`hostSpecs[].configSpec` includes only one of the fields `postgresqlConfig_9_6`, `postgresqlConfig_10_1C`, `postgresqlConfig_10`, `postgresqlConfig_11`, `postgresqlConfig_11_1C`, `postgresqlConfig_12`, `postgresqlConfig_12_1C`, `postgresqlConfig_13`, `postgresqlConfig_14`<br>
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>recoveryMinApplyDelay | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>sharedBuffers | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>tempBuffers | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>workMem | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>tempFileLimit | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>backendFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>oldSnapshotThreshold | **integer** (int64)<br><p>Acceptable values are -1 to 86400, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>maxStandbyStreamingDelay | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>constraintExclusion | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>cursorTupleFraction | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>fromCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>joinCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>forceParallelMode | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>clientMinMessages | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>logMinMessages | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>logMinErrorStatement | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>logMinDurationStatement | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>logCheckpoints | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>logConnections | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>logDisconnections | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>logDuration | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>logErrorVerbosity | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>logLockWaits | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>logStatement | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>logTempFiles | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>searchPath | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>rowSecurity | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>defaultTransactionIsolation | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>statementTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>lockTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>idleInTransactionSessionTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>byteaOutput | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>xmlbinary | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>xmloption | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>ginPendingListLimit | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>deadlockTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>maxLocksPerTransaction | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>maxPredLocksPerTransaction | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>arrayNulls | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>backslashQuote | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>defaultWithOids | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>escapeStringWarning | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>loCompatPrivileges | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>operatorPrecedenceWarning | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>quoteAllIdentifiers | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>standardConformingStrings | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>synchronizeSeqscans | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>transformNullEquals | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>exitOnError | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>seqPageCost | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>randomPageCost | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>enableBitmapscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>enableHashagg | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>enableHashjoin | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>enableIndexscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>enableIndexonlyscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>enableMaterial | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>enableMergejoin | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>enableNestloop | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>enableSeqscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>enableSort | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>enableTidscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>maxParallelWorkers | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>maxParallelWorkersPerGather | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>timezone | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>effectiveIoConcurrency | **integer** (int64)<br><p>Acceptable values are 0 to 1000, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12.<br>effectiveCacheSize | **integer** (int64)<br><p>Acceptable values are 0 to 549755813888, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C | **object**<br>Configuration for a host with PostgreSQL 12 1C server deployed. <br>`hostSpecs[].configSpec` includes only one of the fields `postgresqlConfig_9_6`, `postgresqlConfig_10_1C`, `postgresqlConfig_10`, `postgresqlConfig_11`, `postgresqlConfig_11_1C`, `postgresqlConfig_12`, `postgresqlConfig_12_1C`, `postgresqlConfig_13`, `postgresqlConfig_14`<br>
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>recoveryMinApplyDelay | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>sharedBuffers | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>tempBuffers | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>workMem | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>tempFileLimit | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>backendFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>oldSnapshotThreshold | **integer** (int64)<br><p>Acceptable values are -1 to 86400, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>maxStandbyStreamingDelay | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>constraintExclusion | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>cursorTupleFraction | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>fromCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>joinCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>forceParallelMode | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>clientMinMessages | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>logMinMessages | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>logMinErrorStatement | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>logMinDurationStatement | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>logCheckpoints | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>logConnections | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>logDisconnections | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>logDuration | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>logErrorVerbosity | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>logLockWaits | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>logStatement | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>logTempFiles | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>searchPath | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>rowSecurity | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>defaultTransactionIsolation | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>statementTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>lockTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>idleInTransactionSessionTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>byteaOutput | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>xmlbinary | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>xmloption | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>ginPendingListLimit | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>deadlockTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>maxLocksPerTransaction | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>maxPredLocksPerTransaction | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>arrayNulls | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>backslashQuote | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>defaultWithOids | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>escapeStringWarning | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>loCompatPrivileges | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>operatorPrecedenceWarning | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>quoteAllIdentifiers | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>standardConformingStrings | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>synchronizeSeqscans | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>transformNullEquals | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>exitOnError | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>seqPageCost | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>randomPageCost | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>enableBitmapscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>enableHashagg | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>enableHashjoin | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>enableIndexscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>enableIndexonlyscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>enableMaterial | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>enableMergejoin | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>enableNestloop | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>enableSeqscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>enableSort | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>enableTidscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>maxParallelWorkers | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>maxParallelWorkersPerGather | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>timezone | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>effectiveIoConcurrency | **integer** (int64)<br><p>Acceptable values are 0 to 1000, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_12_1C.<br>effectiveCacheSize | **integer** (int64)<br><p>Acceptable values are 0 to 549755813888, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13 | **object**<br>Configuration for a host with PostgreSQL 13 server deployed. <br>`hostSpecs[].configSpec` includes only one of the fields `postgresqlConfig_9_6`, `postgresqlConfig_10_1C`, `postgresqlConfig_10`, `postgresqlConfig_11`, `postgresqlConfig_11_1C`, `postgresqlConfig_12`, `postgresqlConfig_12_1C`, `postgresqlConfig_13`, `postgresqlConfig_14`<br>
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>recoveryMinApplyDelay | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>sharedBuffers | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>tempBuffers | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>workMem | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>tempFileLimit | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>backendFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>oldSnapshotThreshold | **integer** (int64)<br><p>Acceptable values are -1 to 86400, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>maxStandbyStreamingDelay | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>constraintExclusion | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>cursorTupleFraction | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>fromCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>joinCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>forceParallelMode | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>clientMinMessages | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>logMinMessages | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>logMinErrorStatement | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>logMinDurationStatement | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>logCheckpoints | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>logConnections | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>logDisconnections | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>logDuration | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>logErrorVerbosity | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>logLockWaits | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>logStatement | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>logTempFiles | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>searchPath | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>rowSecurity | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>defaultTransactionIsolation | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>statementTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>lockTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>idleInTransactionSessionTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>byteaOutput | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>xmlbinary | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>xmloption | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>ginPendingListLimit | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>deadlockTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>maxLocksPerTransaction | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>maxPredLocksPerTransaction | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>arrayNulls | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>backslashQuote | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>defaultWithOids | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>escapeStringWarning | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>loCompatPrivileges | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>operatorPrecedenceWarning | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>quoteAllIdentifiers | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>standardConformingStrings | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>synchronizeSeqscans | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>transformNullEquals | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>exitOnError | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>seqPageCost | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>randomPageCost | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>enableBitmapscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>enableHashagg | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>enableHashjoin | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>enableIndexscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>enableIndexonlyscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>enableMaterial | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>enableMergejoin | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>enableNestloop | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>enableSeqscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>enableSort | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>enableTidscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>maxParallelWorkers | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>maxParallelWorkersPerGather | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>timezone | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>effectiveIoConcurrency | **integer** (int64)<br><p>Acceptable values are 0 to 1000, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_13.<br>effectiveCacheSize | **integer** (int64)<br><p>Acceptable values are 0 to 549755813888, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14 | **object**<br>Configuration for a host with PostgreSQL 14 server deployed. <br>`hostSpecs[].configSpec` includes only one of the fields `postgresqlConfig_9_6`, `postgresqlConfig_10_1C`, `postgresqlConfig_10`, `postgresqlConfig_11`, `postgresqlConfig_11_1C`, `postgresqlConfig_12`, `postgresqlConfig_12_1C`, `postgresqlConfig_13`, `postgresqlConfig_14`<br>
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>recoveryMinApplyDelay | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>sharedBuffers | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>tempBuffers | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>workMem | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>tempFileLimit | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>backendFlushAfter | **integer** (int64)<br><p>Acceptable values are 0 to 2048, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>oldSnapshotThreshold | **integer** (int64)<br><p>Acceptable values are -1 to 86400, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>maxStandbyStreamingDelay | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>constraintExclusion | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>cursorTupleFraction | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>fromCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>joinCollapseLimit | **integer** (int64)<br><p>Acceptable values are 1 to 2147483647, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>forceParallelMode | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>clientMinMessages | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>logMinMessages | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>logMinErrorStatement | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>logMinDurationStatement | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>logCheckpoints | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>logConnections | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>logDisconnections | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>logDuration | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>logErrorVerbosity | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>logLockWaits | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>logStatement | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>logTempFiles | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>searchPath | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>rowSecurity | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>defaultTransactionIsolation | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>statementTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>lockTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>idleInTransactionSessionTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>byteaOutput | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>xmlbinary | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>xmloption | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>ginPendingListLimit | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>deadlockTimeout | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>maxLocksPerTransaction | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>maxPredLocksPerTransaction | **integer** (int64)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>arrayNulls | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>backslashQuote | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>defaultWithOids | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>escapeStringWarning | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>loCompatPrivileges | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>quoteAllIdentifiers | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>standardConformingStrings | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>synchronizeSeqscans | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>transformNullEquals | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>exitOnError | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>seqPageCost | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>randomPageCost | **number** (double)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>enableBitmapscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>enableHashagg | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>enableHashjoin | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>enableIndexscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>enableIndexonlyscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>enableMaterial | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>enableMergejoin | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>enableNestloop | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>enableSeqscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>enableSort | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>enableTidscan | **boolean** (boolean)
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>maxParallelWorkers | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>maxParallelWorkersPerGather | **integer** (int64)<br><p>Acceptable values are 0 to 1024, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>timezone | **string**
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>effectiveIoConcurrency | **integer** (int64)<br><p>Acceptable values are 0 to 1000, inclusive.</p> 
hostSpecs[].<br>configSpec.<br>postgresqlConfig_14.<br>effectiveCacheSize | **integer** (int64)<br><p>Acceptable values are 0 to 549755813888, inclusive.</p> 
networkId | **string**<br><p>Required. ID of the network to create the cluster in.</p> <p>The maximum string length in characters is 50.</p> 
securityGroupIds[] | **string**<br><p>User security groups</p> 
deletionProtection | **boolean** (boolean)<br><p>Deletion Protection inhibits deletion of the cluster</p> 
hostGroupIds[] | **string**<br><p>Host groups hosting VMs of the cluster.</p> 
 
## Response {#responses}
**HTTP Code: 200 - OK**

```json 
{
  "id": "string",
  "description": "string",
  "createdAt": "string",
  "createdBy": "string",
  "modifiedAt": "string",
  "done": true,
  "metadata": "object",

  //  includes only one of the fields `error`, `response`
  "error": {
    "code": "integer",
    "message": "string",
    "details": [
      "object"
    ]
  },
  "response": "object",
  // end of the list of possible fields

}
```
An Operation resource. For more information, see [Operation](/docs/api-design-guide/concepts/operation).
 
Field | Description
--- | ---
id | **string**<br><p>ID of the operation.</p> 
description | **string**<br><p>Description of the operation. 0-256 characters long.</p> 
createdAt | **string** (date-time)<br><p>Creation timestamp.</p> <p>String in <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a> text format.</p> 
createdBy | **string**<br><p>ID of the user or service account who initiated the operation.</p> 
modifiedAt | **string** (date-time)<br><p>The time when the Operation resource was last modified.</p> <p>String in <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a> text format.</p> 
done | **boolean** (boolean)<br><p>If the value is ``false``, it means the operation is still in progress. If ``true``, the operation is completed, and either ``error`` or ``response`` is available.</p> 
metadata | **object**<br><p>Service-specific metadata associated with the operation. It typically contains the ID of the target resource that the operation is performed on. Any method that returns a long-running operation should document the metadata type, if any.</p> 
error | **object**<br>The error result of the operation in case of failure or cancellation. <br> includes only one of the fields `error`, `response`<br>
error.<br>code | **integer** (int32)<br><p>Error code. An enum value of <a href="https://github.com/googleapis/googleapis/blob/master/google/rpc/code.proto">google.rpc.Code</a>.</p> 
error.<br>message | **string**<br><p>An error message.</p> 
error.<br>details[] | **object**<br><p>A list of messages that carry the error details.</p> 
response | **object** <br> includes only one of the fields `error`, `response`<br><br><p>The normal response of the operation in case of success. If the original method returns no data on success, such as Delete, the response is <a href="https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#empty">google.protobuf.Empty</a>. If the original method is the standard Create/Update, the response should be the target resource of the operation. Any method that returns a long-running operation should document the response type, if any.</p> 