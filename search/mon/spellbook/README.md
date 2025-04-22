# spellbook
Service hosts diagnostic tool based on skynet

### API

##### POST /api/spell/[spell_name]?[timeout=666]
**post data format:**
```json
// Content-Type: application/json
{
  "hosts": ["host1","host2"],           // Set hosts directly}
  "parameter1": "parameterValue"        // Spell parameters
}
```
**timeout:**

If ```timeout``` set, your request will be hanged until job is finished or ```timeout``` expired.
If ```timeout``` is not set, you instantly get your job info, at your request.

**Outputs**:
```json
{
  "id": "330d562c-30e2-4771-ae4c-8d11a9f89d75", // job id
  "status": "DONE",                             // job status RUNNING|DONE|ERROR
  "error": "",                                  // if there was an error   
  "data": {                                     // dict with hosts and command exec results
                                                // for each host
    "iva1-4147.qloud-h.yandex.net": {
      "stdout": "iva1-4147.qloud-h.yandex.net",
      "stderr": "",
      "json": null
    },
    "myt1-4782.qloud-h.yandex.net": {
      "stdout": "myt1-4782.qloud-h.yandex.net",
      "stderr": "",
      "json": null
    }
  }
}
```
or
```json
{
  "id": "330d562c-30e2-4771-ae4c-8d11a9f89d75", // job id
  "status": "RUNNING",                          // job status RUNNING|DONE|ERROR
  "error": "",                                  // if there was an error
  "data": { }
  }
}
```
if job is not done

#### GET /ping

Returns ```200 Pong``` if app is ok
or ```500 Error``` if app is broken.

#### GET /api/job/[job_id]

Returns job info, just like previous.

#### GET /api/jobs

Returns list of all jobs

#### GET /api/running

Returns list of all jobs with status RUNNING

#### GET /api/spells

List of spells with info

**Output Example**

```json
{
  "dir_size": {
    "info": "returns directory size",
    "returnsObject": false,
    "returnsS3": false,
    "requiredParameters": {
      "directory": "str"
    },
    "optionalParameters": {}
  },
  "free_space": {
    "info": "returns df -h result for directory filesystem",
    "returnsObject": false,
    "returnsS3": false,
    "requiredParameters": {
      "directory": "str"
    },
    "optionalParameters": {}
  },
  "get_file": {
    "info": "uploads specific file from host's FS to S3-MDS",
    "returnsObject": true,
    "returnsS3": true,
    "requiredParameters": {
      "path": "str"
    },
    "optionalParameters": {}
  }
}
```

### Spells

Add new .py files with spells in `app/spells/` dir

**BASH spell Example**

```python
user = None  # User to run bash script from
# required = dict() # Dict of required parameters with types
# optional = dict() # Dict of optional parameters with types
# Filled Example
required = { path : str }
optional = { count : int }

__doc__ = "Returns content of '/db/iss3/sync-exceptions.log' file"

def resolve_hosts(hosts, parameters): # Optional method
    return hosts # resolved hosts can be overriden

def bash(hosts, parameters): # Function returns bash script which will run on hosts
    return "cat /db/iss3/sync-exceptions.log" 
```

BASH spells returns only `stdout`, `stderr` in results

**Python spell Example**

```python
import json
import socket


user = None
required = dict()
optional = { count : int }

__doc__ = "Echo Test"

def resolve_hosts(hosts, parameters): # Optional method
    return hosts # resolved hosts can be overriden

def run(parameters): # Function that will be executed on hosts, closings are not allowed
    result = dict()
    result['parameters'] = parameters
    result['hostname'] = socket.gethostname()
    return result # Result will be serialized into json
```

Python spells returns only `json` objects in results

**Python spell with S3 Upload Example**

```python
user = None
required = { }
optional = { count : int }

__doc__ = "Echo Test"
s3 = True # This variable tells spellbook, that this is s3 spell

def resolve_hosts(hosts, parameters): # Optional method
    return hosts # resolved hosts can be overriden

def run(parameters): # Function that will be executed on hosts, closings are not allowed
    parameters['s3'].put_file('FILE_PATH_TO_UPLOAD') 
    # S3 client will be passed as parameter "s3" for s3 spells
    # function put_file uploads file to configured s3 bucket as object with name {job_id}-{hostname}
```

**S3 spell result example**
```json
{
  "id": "b09c8af7-d33b-4c04-aa23-362f281b14d3",
  "status": "DONE",
  "error": "",
  "data": {
    "sas2-1754.qloud-h.yandex.net": {
      "stdout": "",
      "stderr": "",
      "json": {
        "status": 200,
        "message": "OK"
      },
      "s3": {
        "endpoint": "s3.mds.yandex.net",
        "bucket": "berkanavt",
        "object": "b09c8af7-d33b-4c04-aa23-362f281b14d3-sas2-1754.qloud-h.yandex.net",
        "link": "https://s3.mds.yandex.net/berkanavt/b09c8af7-d33b-4c04-aa23-362f281b14d3-sas2-1754.qloud-h.yandex.net"
      }
    }
  }
}
```

New result section: `s3`, only for S3 spells

### SSH keys

Add private key files with owner names to the directory specified in the `sshKeys` parameter of the configuration file

### Configuration file

**json**
```json
{
  "skyLogPath": "/var/log/spellbook.log", // Logfile
  "dataExpire": "24h",                    // Diagnostic data TTL
  "dbFile": "./db.sqlite",                // Diagnostic data path
  "sshKeys": "./keys",                    // SSH keys for skynet
  "defaultUser": "root",                  // default ssh user if not specified
  "listenHost": "::",                     // listen address
  "listenPort": 8000                      // listen port
}
```
**yaml**
```yaml
skyLogPath: '/var/log/spellbook.log'
dataExpire: '24h'
dbFile: './db.sqlite'
sshKeys: './keys'
defaultUser: 'root'
listenHost: '::'
listenPort: 8000
```
### Environment variables

```bash
S3_ACCESS_KEY_ID="xxxxxxxxxxxxxxxx"                     # Access ID for S3
S3_ACCESS_SECRET_KEY="yyyyyyyyyyyyyyyyyyyyyyyy"         # Access Key for S3
S3_HOST="s3.mds.yandex.net"                             # S3 Endpoint
S3_BUCKET="berkanavt"                                   # S3 Bucket name
```

### USAGE

```
usage: spellbook_server.py [-h] [--json [JSON_FILE]] [--yaml [YAML_FILE]]
                           [--port [PORT]] [--ip [IP]]
                           [--expire [DATA_EXPIRE]] [--keys [SSH_KEYS_DIR]]
                           [--default_user [DEFAULT_USER]]
                           [--datafile [DB_FILE]]

Spellbook

optional arguments:
  -h, --help            show this help message and exit
  --json [JSON_FILE]    JSON Config
  --yaml [YAML_FILE]    YAML Config
  --port [PORT]         Listen Port
  --ip [IP]             Listen Ip
  --expire [DATA_EXPIRE]
                        Diagnostic Data Expiration
  --keys [SSH_KEYS_DIR]
                        SSH keys directory for skynet
  --default_user [DEFAULT_USER]
                        Default user for skynet
  --datafile [DB_FILE]  SQLite dbfile path
```


```bash
./start.sh
```