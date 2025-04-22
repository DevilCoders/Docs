
`python -m prepare_data_for_mxnet \
           --split-date 2019-06-01 \
           --yt-path-full-data //home/taxi_ml/dev/drivers/competition/sample_with_features_targets_3 \
           --features-window-sizes 7,14,21,28 \
           --target-offset 3`
           
python -m fit_model --target-offset 3 --model-path './model_resources_3_weights'
           
python -m apply_model \
    --target-offset 3 \
    --model-path './model_resources_3_weights' \
    --predictions-yt-path //home/taxi_ml/dev/drivers/competition/model_offset_3_weights/2019-08-17 \
    --apply-data-yt-path '//home/taxi_ml/dev/drivers/prod_features/2019-08-17' \
    --features-window-sizes 7,14,21,28
    
    
