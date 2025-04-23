# Alert

## Properties
Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | **str** | unique identity for alert | 
**project_id** | **str** | Project if own by this alert | 
**name** | **str** | Human-readable name of alert | 
**version** | **int** | actual version of notification | [optional] 
**created_by** | **str** | User created alert | [optional] 
**created_at** | **str** | Time when alert was created | [optional] 
**updated_by** | **str** | User updated alert | [optional] 
**updated_at** | **str** | Time when alert was updated last time | [optional] 
**state** | **str** | State of current alert, only ACTIVE alerts will be periodically checked | 
**group_by_labels** | **list[str]** | List of label key that should be use to group sensors, each group it&#x27;s separate sub alert that check independently from other group | [optional] 
**notification_channels** | **list[str]** | Deprecated. Notification channel ids that will be use to notify about alert evaluation status | [optional] 
**channels** | [**list[AssociatedChannel]**](AssociatedChannel.md) | Notification channels that will receive events | 
**type** | [**Type**](Type.md) |  | 
**annotations** | **dict(str, str)** | Templates that explain alert evaluation status, and what todo when alert occurs. Variables available to use into template depends on alert type. | [optional] 
**period_millis** | **int** | Deprecated. Alert evaluation period in milliseconds. Period plus aggregate allow smooth frequently change parameter. | 
**delay_seconds** | **int** | Deprecated. Time (in seconds) to delay evaluation relatively now. Useful for delayed sensors like cluster aggregation. Should be a non negative integer. | [optional] 
**window_secs** | **int** | Alert window width in seconds | [optional] 
**delay_secs** | **int** | Alert delay in seconds | [optional] 
**description** | **str** | Description about alert in markdown format | [optional] 
**resolved_empty_policy** | **str** | NO_DATA policy for selectors that resolve to empty set of metrics | [optional] 
**no_points_policy** | **str** | NO_DATA policy for timeseries without data points | [optional] 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

