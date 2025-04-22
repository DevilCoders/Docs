Pypi package with custom common utilites

# Change and upload
How to upload package to dist: [https://wiki.yandex-team.ru/pypi/](https://wiki.yandex-team.ru/pypi/)
1. add access / private keys to ~/.pypirc
2. Update package version in setup.py
3. build package:
    ```bash
    # pip3 install wheel # uncomment if wheel package isn't installed
    python3 setup.py sdist bdist_wheel
    ```
4. push to dist:
    ```bash
   # sudo pip3 install twine # uncomment if twine isn't installed
   twine upload -r yandex dist/*
    ```

# PyPi
[https://pypi.yandex-team.ru/simple/vsml-common](https://pypi.yandex-team.ru/simple/vsml-common)
  
# Install
```bash
pip install -i https://pypi.yandex-team.ru/simple/ vsml-common
# !pip install --upgrade -i https://pypi.yandex-team.ru/simple/ vsml-common 
```

# Usage

## yt utils:
```(python)
from vsml_common.utils.yt import download_from_yt, upload_to_yt

yt_path = '//home/verticals/realty/smartdeal/all_schemaful'
local_file_from = '../postprocess/final_db/all.all.1.db.tsv'
local_file_to = 'all.all.1.db.tsv.json'
# upload table to yt
basic_schema = {'area': float, 'building_year': int, 'cadastral_cost': float, 'num_rights': int}
upload_to_yt(local_file_from, 
             yt_path, 
             schema=basic_schema, 
             drop_if_exists=True)

#download from yt to local file
download_from_yt(yt_path, local_file_to, format_='json')
```