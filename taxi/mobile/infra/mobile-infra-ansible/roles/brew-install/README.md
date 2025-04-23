Brew install
----
Role for install brew package

Parameters
----
```yaml
brew_package_info:
    name: string|required - name of installing package
    with_link: bool|optional - if true, role calls brew link {{ brew_package_name }}
    formulae: string|optional - formulae name
    tap_url: string|optional - url for tap formulae
    options: string|optional - install options (for example ignore-dependencies)
    link_options: string|optional - link options (for example overwrite)
```

* **bin_path_env*** (string|required) - env for brew path. For example /opt/homebrew/bin:/opt/homebrew/sbin:/usr/local/bin).

