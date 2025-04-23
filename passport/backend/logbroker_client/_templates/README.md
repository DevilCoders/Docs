# Logbroker client templates

## Usage:
```
./render_template.sh <template_name> <output_dir>
```

Set alternative python path with $PYTHON_BIN

## Example:
```
PYTHON_BIN=python3 ./render_template.sh lbc_http ../my_cool_client
```

## Available templates:
* **lbc_http** - legacy HTTP protocol client (py2, easy-to-convert to py3)
* **lbc_proto_py3** - protobuf-based client (py3)
