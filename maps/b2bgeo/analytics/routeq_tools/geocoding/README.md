## A script for batch geocoding.

You can either use this as a standalone CLI script, or import geocode_df() function from inside Python.

### Geocode pandas dataframe from Python
```python
import pandas as pd
from geocoding import geocoding
df = pd.read_excel('data_from_client.xls')
geocoding.geocode_df(df, address_column_name='адрес')
```
For detailed description see docstring to geocode_df()

### Geocode excel file from command line

#### Example: 
```
geocode-excel data_from_client.xls --column 'адрес доставки' -- bbox 53.0 35.0 57.0 39.0 --hard_bbox --clean --small_place_ok --show_stats
```

#### Important caveats:

- make sure your excel file doesn't have empty lines in the top, or the script will fail;
- use --bbox and --hard_bbox to avoid getting your addresses geocoded to Zimbabwe;
- even if the precision is 'exact', it's not a guarantee that the addresses were geocoded correctly;
- if you use Google, even with  you will probably have a few points geocoded to far away locations. The current version of the script doesn't check for that;
- if you use Google, watch for your quota to avoid paying actual money.

#### Detailed description

The standalone version takes an Excel file with a column of addresses and geocodes the addresses using Yandex and Google
geocoder APIs. 

Note that you need a google maps API key to be able to use Google geocoding API. 

For each address, an attempt to geocode using yandex API is made. If the attempt is unsuccessfull, the script then
tries to use Google API.

The result is an Excel file with the same data as in the input file, but with five new columns: *geocoded_lat,
geocoded_lon, geocoded_precision, geocoded_address, geocoded_ok*.

*geocoded_precision* is one of the following: *exact, number, near, street, other* (Yandex API precision levels),
*google_ROOFTOP, google_RANGE_INTERPOLATED, google_GEOMETRIC_CENTER, google_APPROXIMATE* (Google API location types),
and *failed, google_failed, wrong_address_format*.

*geocoded_ok* is True if precision is one of *exact, number, near, google_ROOFTOP, google_RANGE_INTERPOLATED*. There are
options to also consider geocoding succesful in the following cases: 
- when precision is *street*. See --street_ok parameter below
- when the geocoded address is of lower precision but describes a small territory. See --small_place_ok parameter below. 


usage: geocoding.py [-h] [--column [COLUMN]] [--sheet [SHEET]]
                    [--yamaps_apikey [YAMAPS_APIKEY]]
                    [--google_apikey [GOOGLE_APIKEY]] [--clean] [--street_ok]
                    [--small_place_ok] [--bbox min_lat min_lon max_lat max_lon]
                    [--hard_bbox]
                    filenames [filenames ...]

positional arguments:
  
  filenames             input_file [output_file]. If output_file not specified, *'geocoded_' + input_file* is used

optional arguments:
  
  -h, --help            show this help message and exit
  
  --sheet [SHEET]       name/number of sheet in Excel file. First sheet by default.
  
  --column [COLUMN]     name of column containing addresses in Excel file
  
  --yamaps_apikey [YAMAPS_APIKEY]
  
  --google_apikey [GOOGLE_APIKEY]
  
  --clean               clean up address before geocoding, removing frequent
                        junk postfixes
  
  --street_ok           consider "street" precision to be success
  
  --small_place_ok      if geocoded address contains a name of a small territory, consider geocoding succesful
  
  --bbox min_lat min_lon max_lat max_lon
                        limit the geocoding area, syntax: --bbox min_lat min_lon max_lat max_lon
  
  --hard_bbox           make the bbox for Yandex geocoder hard. Google bbox is
                        always soft

  
  --google_limit GOOGLE_LIMIT
                        maximal number of Google API calls

  --show_stats          during geocoding, display how many addresses were geocoded with which precision
  
