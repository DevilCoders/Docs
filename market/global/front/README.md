# Global Market


## Важно
1. b2b и b2c приложения используют разные версии node. Лучше настроить автоматическое преключение версий:

    #### bash

    ##### Automatically call `nvm use`

    Put the following at the end of your `$HOME/.bashrc`:

    ```bash
    cdnvm() {
        command cd "$@";
        nvm_path=$(nvm_find_up .nvmrc | tr -d '\n')

        # If there are no .nvmrc file, use the default nvm version
        if [[ ! $nvm_path = *[^[:space:]]* ]]; then

            declare default_version;
            default_version=$(nvm version default);

            # If there is no default version, set it to `node`
            # This will use the latest version on your machine
            if [[ $default_version == "N/A" ]]; then
                nvm alias default node;
                default_version=$(nvm version default);
            fi

            # If the current version is not the default version, set it to use the default version
            if [[ $(nvm current) != "$default_version" ]]; then
                nvm use default;
            fi

        elif [[ -s $nvm_path/.nvmrc && -r $nvm_path/.nvmrc ]]; then
            declare nvm_version
            nvm_version=$(<"$nvm_path"/.nvmrc)

            declare locally_resolved_nvm_version
            # `nvm ls` will check all locally-available versions
            # If there are multiple matching versions, take the latest one
            # Remove the `->` and `*` characters and spaces
            # `locally_resolved_nvm_version` will be `N/A` if no local versions are found
            locally_resolved_nvm_version=$(nvm ls --no-colors "$nvm_version" | tail -1 | tr -d '\->*' | tr -d '[:space:]')

            # If it is not already installed, install it
            # `nvm install` will implicitly use the newly-installed version
            if [[ "$locally_resolved_nvm_version" == "N/A" ]]; then
                nvm install "$nvm_version";
            elif [[ $(nvm current) != "$locally_resolved_nvm_version" ]]; then
                nvm use "$nvm_version";
            fi
        fi
    }
    alias cd='cdnvm'
    cd "$PWD"
    ```

    This alias would search 'up' from your current directory in order to detect a `.nvmrc` file. If it finds it, it will switch to that version; if not, it will use the default version.

    #### zsh

    ##### Calling `nvm use` automatically in a directory with a `.nvmrc` file

    Put this into your `$HOME/.zshrc` to call `nvm use` automatically whenever you enter a directory that contains an
    `.nvmrc` file with a string telling nvm which node to `use`:

    ```zsh
    # place this after nvm initialization!
    autoload -U add-zsh-hook
    load-nvmrc() {
    local node_version="$(nvm version)"
    local nvmrc_path="$(nvm_find_nvmrc)"

    if [ -n "$nvmrc_path" ]; then
        local nvmrc_node_version=$(nvm version "$(cat "${nvmrc_path}")")

        if [ "$nvmrc_node_version" = "N/A" ]; then
        nvm install
        elif [ "$nvmrc_node_version" != "$node_version" ]; then
        nvm use
        fi
    elif [ "$node_version" != "$(nvm version default)" ]; then
        echo "Reverting to nvm default version"
        nvm use default
    fi
    }
    add-zsh-hook chpwd load-nvmrc
    load-nvmrc
    ```

2. Сертификат должен лежать тут: common/.dev/cert.pem