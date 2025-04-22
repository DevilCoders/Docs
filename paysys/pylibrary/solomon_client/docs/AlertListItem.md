# AlertListItem

## Properties
Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | **str** | unique identity for alert | 
**project_id** | **str** | Project if own by this alert | 
**name** | **str** | Human-readable name of alert | 
**type** | **str** | Type of alert | 
**state** | **str** | State of current alert, only ACTIVE alerts will be periodically checked | 
**multi_alert** | **bool** | True if current alert it&#x27;s multi alert that unroll into multiple sub alerts, otherwise false | 
**evaluation_stats** | [**EvaluationStatistics**](EvaluationStatistics.md) |  | 
**notification_stats** | [**NotificationStatistics**](NotificationStatistics.md) |  | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

