Brew install
----
Role for install list of brew packages

Parameters
----
```yaml
brew_package_info_list:
#   Params from brew-install rule
  - name: string|required
    with_link: bool|optional 
    formulae: string|optional
    tap_url: string|optional 
  - name: string|required
    with_link: bool|optional
    formulae: string|optional
    tap_url: string|optional
```

* **bin_path_env*** (string|required) - env for brew path. For example /opt/homebrew/bin:/opt/homebrew/sbin:/usr/local/bin).

