`matrix_router_over_osm_data_validator` module validates data to be used by matrix
router over OSM. To do so, it compares routes built by matrix router in datavalidation
and stable matrix routers. If the validation is successful, the data is deployed
by `matrix_router_over_osm_data_deployment` module to stable.
