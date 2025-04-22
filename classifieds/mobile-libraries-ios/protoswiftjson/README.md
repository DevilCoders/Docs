## protoc-gen-swiftjson

### Preparation

1. Install `protoc` protobuf compiler
* Using Homebrew `brew install protobuf`
* Or download it from https://github.com/protocolbuffers/protobuf/releases
  * Unpack to `~/.bin` (so it will be `~/.bin/protoc`)
  * Add `$HOME/.bin/protoc/bin` to `$PATH` (e.g. add `export PATH="$HOME/.bin/protoc/bin:$PATH` to `~/.profile`)
2. Install RVM or rbenv using Homebrew or MacPorts
3. Install Ruby 3.0.0
4. Install bundler `gem install bundler`
5. Install gems `bundle install`

### Usage

```bash
protoc \
    --plugin=./bin/protoc-gen-swiftjson \
    --proto_path=../schema-registry/proto \
    --swiftjson_opt=options_file=options.yml \
    --swiftjson_out=./out \
    $(find ../schema-registry/proto -iname "*.proto") \
    --swiftjson_opt=log_level=0 \
    --swiftjson_opt=log_file=foo.log
```

`plugin` – path to `protoc-gen-swiftjson`
* `protoc-gen-swiftjson` must be executable (can be made with `chmod +x protoc-gen-swiftjson`)

`proto_path` – path to directory with proto-files (root for proto-file `#import` directives)

`swiftjson_out` – output directory (`swiftjson` is part from `protoc-gen-swiftjson`)

`swiftjson_opt` – plugin options
* `options_file` – project file with file list allowed to generate
```yaml
ALLOW:
  # Common (message with fields)
  .realty.GeoPoint:
    - latitude
    - longitude
    - defined
  # Offer (enum with cases)
  .realty.offer.PaymentType:
    - PT_UNKNOWN
    - PT_JURIDICAL_PERSON
    - PT_NATURAL_PERSON
```
* `log_level` – log-level (from 0 to 4)
* `log_file` – log-file path (used `STDERR` if not set)

`$(find ../schema-registry/proto -iname "*.proto")` – collect all proto-files in root proto-directory
