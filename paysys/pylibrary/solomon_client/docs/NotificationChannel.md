# NotificationChannel

## Properties
Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | **str** | unique identity for notification | 
**project_id** | **str** | ProjectId own this notification | 
**name** | **str** | Human-readable name of notification | 
**version** | **int** | actual version of notification | [optional] 
**notify_about_statuses** | **list[str]** | TNotification will send event only about specified alert evaluation status | [optional] 
**repeat_notify_delay_millis** | **int** | Delay between repeated notify about the same evaluation status, by default notify aboutparticular evaluation status only after change it. Negative duration means that repeatnotification not used. | [optional] 
**created_at** | **str** | Time when notification was created | [optional] 
**created_by** | **str** | User created notification channel | [optional] 
**method** | [**Method**](Method.md) |  | 
**updated_at** | **str** | Time when notification was updated last time | [optional] 
**updated_by** | **str** | User modified notification channel | [optional] 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

