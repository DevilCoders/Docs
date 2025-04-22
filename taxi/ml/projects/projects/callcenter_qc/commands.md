```
python3 -m projects.callcenter_qc.score_aggregates from_single_table \
--input_table_path //home/taxi_ml/tmp/cc-recognize-demo-2022-02-23-01-scores \
--output_worst_dialogues_table_path //home/taxi_ml/tmp/cc-recognize-demo-2022-02-23-01-scores-top \
--output_per_user_score_table_path  //home/taxi_ml/tmp/cc-recognize-demo-2022-02-23-01-scores-agg
```

```
python3 -m projects.callcenter_qc.tickets from_table \
--input_table_path //home/taxi_ml/production/callcenter_qc/tickets/2022-02-23T11:00:00 \
--cc_stats_host callcenter-stats.taxi.tst.yandex.net \
--tvm_secret "3:serv:CNmhARCqhu2QBiIRCMTzehDm_XoguJmgkaXU_gE:FMEzAb0e_RM7H4MkxbeTkB38Tgp3LIpy60vr3-m_GwqQBpg8N7go2eTWmtFScgsEmIYbS78XeAYwupHeixBtq1aS10XrgVFFv7wUhDTAnP7dq88KeaQ9pS2-Fv8ERJRpP3jmXldiHf77kjjTLsISWal_Uj8ee16OZdCWk_7VjrAnBFcuM2W48zI-izVtw6Bag01sqtpCwjAGTD77uCZK5saqTT8Ub48IFLo6kmiuqXjSQkjC7IsQ4HAk1m9pDk3hIVYUmywTxMj4UKt5ZLOHek9eLxKt_ejEaHcezoE-z8orbdbbHp-SRWhFFbxUlJm3egVgtST16XFfbNmSeyY9kA"
```

```
python3 -m projects.callcenter_qc.tickets from_datetime \
--datetime 2022-02-23T11:00:00 \
--cc_stats_host callcenter-stats.taxi.tst.yandex.net \
--tvm_secret "3:serv:CNmhARCqhu2QBiIRCMTzehDm_XoguJmgkaXU_gE:FMEzAb0e_RM7H4MkxbeTkB38Tgp3LIpy60vr3-m_GwqQBpg8N7go2eTWmtFScgsEmIYbS78XeAYwupHeixBtq1aS10XrgVFFv7wUhDTAnP7dq88KeaQ9pS2-Fv8ERJRpP3jmXldiHf77kjjTLsISWal_Uj8ee16OZdCWk_7VjrAnBFcuM2W48zI-izVtw6Bag01sqtpCwjAGTD77uCZK5saqTT8Ub48IFLo6kmiuqXjSQkjC7IsQ4HAk1m9pDk3hIVYUmywTxMj4UKt5ZLOHek9eLxKt_ejEaHcezoE-z8orbdbbHp-SRWhFFbxUlJm3egVgtST16XFfbNmSeyY9kA"
```

```
python3 -m projects.callcenter_qc.tickets all_checked_tickets 
```

```
python3 -m projects.callcenter_qc.score_aggregates from_single_table \
--input_table_path //home/taxi_ml/leonsht/tmp/tickets-candidate-texts-scores \
--output_worst_dialogues_table_path //home/taxi_ml/leonsht/tmp/tickets-candidate-texts-tickets \
--output_per_user_score_table_path  //home/taxi_ml/leonsht/tmp/tickets-candidate-texts-scores-agg
```

```
python3 -m projects.callcenter_qc.dwh  
```