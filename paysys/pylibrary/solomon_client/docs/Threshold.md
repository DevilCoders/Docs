# Threshold

## Properties
Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**selectors** | **str** | Label selectors to define sensors to check | 
**time_aggregation** | **str** | Define criteria by that will be check alert | [optional] 
**predicate** | **str** | Predicate uses for compare point with threshold | [optional] 
**threshold** | **float** | Target threshold that will be use with sensors data on specified period | [optional] 
**transformations** | **str** | Transformations that are applied before testing predicates rules | [optional] 
**predicate_rules** | [**list[PredicateRule]**](PredicateRule.md) | A list of predicate rules to test against the data | [optional] 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

