Brew uninstall
----
Role for uninstall brew package. Execute brew uninstall and clear folders :
- {{ brew_prefix }}/bin
- {{ brew_prefix }}/doc
- {{ brew_prefix }}/Cellar
- {{ brew_prefix }}/opt

Parameters
----
```yaml
brew_package_info:
    name: string|required - name of uninstalling package
    options: string|optional - install options (for example ignore-dependencies)
```

* **brew_prefix*** (string|required) - brew prefix. Сan be obtained using `command: brew --prefix`.

* **bin_path_env*** (string|required) - env for brew path. For example /opt/homebrew/bin:/opt/homebrew/sbin:/usr/local/bin).
