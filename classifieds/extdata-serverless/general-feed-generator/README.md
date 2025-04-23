# Call the script

- with http call, query parameters: bucket_id, object_id (json with parsed profiles)
- via trigger on bucket

# Parse profiles

1. Put `input-*.csv` file in `avito-general` bucket in the format

    | url |
    | --- |
    | https://www.avito.ru/profile... |

2. Wait for sh to parse profiles from the input file

3. When profiles are parsed, the function will be triggered, generated feeds will be saved to 
`avito-general-feeds` bucket in the format `md5(url).xml`
