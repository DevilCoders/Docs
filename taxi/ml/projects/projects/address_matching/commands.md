Install Aux Libraries:
```
pip3 install --index-url https://pypi.yandex-team.ru/simple \
hydra-core==1.1.1 \
pytorch-lightning==1.3.8 \
torchmetrics==0.7.0 \
ytreader==5653749
```

Get Dialogues:
```
python3 -m projects.address_matching.dataset.dialogues from_table \
--input_table_path //home/taxi_ml/dev/cc_address_matching/dataset-2022-04 \
--output_table_path //home/taxi_ml/dev/cc_address_matching/iterations/2022-04/dialogues
```

Get Pairwise Candidates:
```
python3 -m projects.address_matching.dataset.candidates from_table \
--input_table_path //home/taxi_ml/dev/cc_address_matching/iterations/2022-04/dialogues \
--output_table_path //home/taxi_ml/dev/cc_address_matching/iterations/2022-04/candidates
```

Split Whatever:
```
python3 -m projects.address_matching.dataset.common split_table \
--val_fraction 0.02 \
--split_salt dialogues_val_split \
--input_table_path //home/taxi_ml/dev/cc_address_matching/iterations/2022-04/dialogues \
--train_output_table_path //home/taxi_ml/dev/cc_address_matching/iterations/2022-04/dialogues-major \
--val_output_table_path //home/taxi_ml/dev/cc_address_matching/iterations/2022-04/dialogues-val
```

Product Validation:
```
python3 -m projects.address_matching.dataset.dialogues validation_from_table \
--negative_fraction 0.5 \
--input_table_path //home/taxi_ml/dev/cc_address_matching/iterations/2022-04/dialogues-val \
--output_table_path //home/taxi_ml/dev/cc_address_matching/iterations/2022-04/synthetic-val
```

Get Production Verdicts:
```
python3 -m projects.address_matching.validation validation_from_table_api \
--input_table_path //home/taxi_ml/dev/cc_address_matching/iterations/2022-04/synthetic-val \
--output_table_path //home/taxi_ml/dev/cc_address_matching/iterations/internal/synthetic-val-production-2022-04 \
--headers "{'X-Ya-Service-Ticket': '....'}"
```

Shuffle Table:
```
python3 -m projects.address_matching.dataset.common shuffle_table \
--input_table_path //home/taxi_ml/dev/cc_address_matching/iterations/2022-04/candidates-train \
--output_table_path //home/taxi_ml/dev/cc_address_matching/iterations/internal/shuffled-train
```

Get Production Outcomes:
```
python3 -m projects.address_matching.validation outcomes_from_table \
--input_table_path //home/taxi_ml/dev/cc_address_matching/iterations/internal/synthetic-val-new-2022-04 \
--output_table_path //home/taxi_ml/dev/cc_address_matching/iterations/internal/val-new-2022-04 \
--match_thresholds '[0.9, 0.8, 0.7]' \
--relevance_thresholds '[0.1, 0.2, 0.3, 1.0]' \
--suggest_rank_col suggest_rank \
--zero_suggest_items_col scored_zerosuggest_items
```

