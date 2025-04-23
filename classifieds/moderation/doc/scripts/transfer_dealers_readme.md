transfer dealers with whitelist/blacklist statuses from MySQL
============================================================

Queries to get whitelisted/blacklisted dealers [db: cabinet_autoru]:
    select client_id from loyalty_white_list;
    select client_id from loyalty_black_list;

Query to get list of all dealers [db: office7]:
    select id from clients;

Export to csv without field names in first row and run:
    python3 scripts/transfer_dealer_loyalty.py --env PROD --host-port localhost:5555 --all all.csv --blacklisted blacklisted.csv --whitelisted whitelisted.csv
