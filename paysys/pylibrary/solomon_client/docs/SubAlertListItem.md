# SubAlertListItem

## Properties
Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | **str** | unique identity for alert | [optional] 
**project_id** | **str** | Project if own by this alert | [optional] 
**parent_id** | **str** | Parent id contains definition for alert | 
**labels** | **dict(str, str)** | Unique list of labels of sub alert | 
**evaluation_status_code** | **str** | Latest evaluation status | 
**latest_eval** | **str** | Latest evaluation time | 
**notification_stats** | [**NotificationStatistics**](NotificationStatistics.md) |  | 
**annotations** | **dict(str, str)** | Filtered annotations | 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

