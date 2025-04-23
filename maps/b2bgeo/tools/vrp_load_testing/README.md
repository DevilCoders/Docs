This script is designed to perform load testing of various ya-courier backend services.

#Description

The script works by sending requests to ya-courier backend during simulation of delivery waves (a wave is 'all deliveries from single depot'). The only requests simulated at the moment are MVRP (async), SVRP (sync), push position.

Supported parameters:
    * '-w' or '--waves': JSON file(s) with delivery wave(s) data. For example baltika.json.
    * '-e' or '--environment': Environment to use ('dev' or 'stable').
    * '-a' or '--oauth-token': Valid OAuth token for ya-courier-backend instance'.
    * '-l' or '--logfile': Log filename.
    * '-v' or '--verbose': Print more info.

#File formats

The script expects two kinds of files as input (both are json):
  * delivery wave file (see baltika.json for example) - it contains parameters for a delivery wave(s). The file is specified as '-w' parameter of the script.
  * a file which is used as the source of simulated locations and vehicles - it should be a mvrp request file with sufficient number of locations an vehicles. The  file is specified as 'template' parameter inside of the wave file.  

#Downloading template files

 * curl https://proxy.sandbox.yandex-team.ru/709270443 -o msk_loc6481_veh174.json
 * curl https://proxy.sandbox.yandex-team.ru/711824375 -o spb_loc475_veh61.json

#Uploading/deleting template files

To upload a file to sandbox run the folloing command:
    ya upload --ttl=inf <filename>
and keep returned resource id. To download the file later you will need the id:
    curl https://proxy.sandbox.yandex-team.ru/<id> -o <filename>
To delete a template on sandbox you should go to https://sandbox.yandex-team.ru, search file by resource id, and remove it. Before deleting you have to edit 'ttl' attribute there (set it to 1 instead of inf), otherwse removing will complain and fail.