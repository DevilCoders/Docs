# AlertEvaluationState

## Properties
Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**alert_id** | **str** | Unique identity for alert | [optional] 
**project_id** | **str** | Reference to project that contains alert | 
**alert_version** | **int** | Version of alert that will be use to evaluate latest time.Each change of alert reset state. | [optional] 
**status** | [**AlertEvaluationStatusDto**](AlertEvaluationStatusDto.md) |  | [optional] 
**since** | [**Instant**](Instant.md) |  | [optional] 
**latest_eval** | [**Instant**](Instant.md) |  | [optional] 
**previous_status** | [**AlertEvaluationStatusDto**](AlertEvaluationStatusDto.md) |  | [optional] 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

