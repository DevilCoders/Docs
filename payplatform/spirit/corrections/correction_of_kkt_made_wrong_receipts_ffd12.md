Where all data will be processed

    fold=/tmp/my
    mkdir -p ${fold}

Specify invalid user_requisite values to correct

    cat > ${fold}/invalid_user_req_values.csv <<EOF
    ae5e12452242803b06e9789d9d82e9ac
    b3dd9c979269cac4a5c787830ceb14d3
    EOF

If file is large split it to smaller files and use splitted files in further commands

    python3 main_ffd12.py -e test --log-file-fpath ${fold}/log_split.log split-lines --out-folder ${fold}/process --max-lines 1000 ${fold}/wrong_inn_1p.csv

Convert data to download_task initial data or generate it by other ways, note function `process_line` to change
initial format and use `DownloadReceipt.extra_info` to store additional info.

    python3 main_ffd12.py -e test --log-file-fpath ${fold}/log_csv_to_download.log convert-csv-to-download-receipt --requisite-name trust_purchase_token --fin ${fold}/invalid_user_req_values.csv --fout ${fold}/download.iter.0

Next step will download receipts with specified requisite values
 One requisite value may map to multiple checks, we can filter and drop some
 downloaded receipts by changing function `download_ds_receipts.filter_doc` in code
 see `main_ffd12.py:download_ds_receipts` for more info

Download ds recipes for specified user requisite values with 10 async jobs

    python3 main_ffd12.py -e test --log-file-fpath ${fold}/log_ds_download.log download-ds-receipts --fin ${fold}/download.iter.0 --fout ${fold}/downloaded.json --fout-failed ${fold}/download.iter.1 --async-task-count 10

Check log or download.iter.1 for failed downloads

    wc download.iter.1

If some of them failed retry as many times as needed changing --fin and --fout-failed

    python3 main_ffd12.py -e test --log-file-fpath ${fold}/log_ds_download.log download-ds-receipts --fin ${fold}/download.iter.1 --fout ${fold}/downloaded.json --fout-failed ${fold}/download.iter.2 --async-task-count 10

When we downloaded all wrong receipts we can examine them by reading file `${fold}/downloaded.json`
Correction of existing doc means we have to change something in doc, change
  `main_ffd12.py:convert_download_to_correction.fix_receipt` function in code
Convert downloaded receipts to correction requests

    python3 main_ffd12.py -e test --log-file-fpath ${fold}/log_convert_download_to_correction.log convert-download-to-correction --fin ${fold}/downloaded.json --fout ${fold}/correction.iter.0

Check file ${fold}/correction.iter.0 to see which correction receipts would be made

    less ${fold}/correction.iter.0

!!!! Can not be undone
Make actual corrections

    python3 main_ffd12.py -e test --log-file-fpath ${fold}/log_make_corrections.log make-wrong-receipts-corrections --fin ${fold}/correction.iter.0 --fout-ok ${fold}/corrections_ok --fout-failed ${fold}/correction.iter.1

Check log or ${fold}/correction.iter.1 for failed corrections

    wc download.iter.1

If some of them failed retry as many times as needed changing --fin and --fout-failed

    python3 main_ffd12.py -e test --log-file-fpath ${fold}/log_make_corrections.log make-wrong-receipts-corrections --fin ${fold}/correction.iter.1 --fout-ok ${fold}/corrections_ok --fout-failed ${fold}/correction.iter.2

Result info about corrections will be in ${fold}/corrections_ok

    less ${fold}/corrections_ok




