## Acquire propositions history by segment_id:

```
select contractor_id,history_action, history_timestamp, proposition_id, history_user_id from route_propositions_history where proposition_id in (
    select distinct(dispatch_proposition_id) from courier_advice_calculation_log where transfer_id in (
        select transfer_id from planned_transfers_history where request_id in (
            select request_id from requests_history where request_code = 'd59b65b5-717f-4c82-bc85-01287b25c3ea'
        )
    )
) order by history_event_id desc;
```

## Acquire all segment_ids from proposition

```
select distinct(request_code) from requests where request_id in (
    select request_id from planned_transfers_history where transfer_id in (
        select transfer_id from courier_advice_calculation_log where dispatch_proposition_id = 'a9d771c2-d7f1-430e-be32-654eae9e4e01'
    )
);
```

## Acquire propositions, which were removed for unnatural reason

```
select proposition_id from route_propositions_history where history_action = 'remove' and history_timestamp > 1601067600 and history_user_id = 'propositions_journal' and proposition_id in (
    select dispatch_proposition_id from courier_advice_calculation_log where transfer_id in (
        select transfer_id from planned_transfers_history where request_id in (
            select request_id from requests_history where employer_code = 'eats'
        )
    )
);
```

## Acquire segment ids, for which propositions were removed for unnatural reasons

```
select distinct(request_code) from requests_history where request_id in (
    select distinct(request_id) from planned_transfers_history where transfer_id in (
        select transfer_id from courier_advice_calculation_log where dispatch_proposition_id in (
            select proposition_id from route_propositions_history where history_action = 'remove' and history_timestamp > 1601067600 and history_user_id = 'propositions_journal' and proposition_id in (
    select dispatch_proposition_id from courier_advice_calculation_log where transfer_id in (
        select transfer_id from planned_transfers_history where request_id in (
            select request_id from requests_history where employer_code = 'eats'
        )
    )
))));
```

## Get segment ids by proposition id

```
select request_code from requests_history where request_id in (
    select distinct(request_id) from planned_transfers_history where transfer_id in (
        select transfer_id from courier_advice_calculation_log where dispatch_proposition_id = '202d7f1e-dd47-442a-b25a-1d8cf243abea'
    )
);
```


## Get all propositions which were not accepted from the first attempt

```
select proposition_id, count(proposition_id) as c from route_propositions_history
where history_timestamp > 1601499600 and history_timestamp < 1601586000 and history_action = 'drop_performer'
group by proposition_id
order by c desc;
```

## Get all segment_ids with no propositions

```
select distinct(request_code) from requests_history where request_id not in (
    select distinct(request_id) from planned_transfers_history where transfer_id in (
        select distinct(transfer_id) from courier_advice_calculation_log
    )
) and employer_code = 'eats' and history_timestamp > 1602018000;
```
