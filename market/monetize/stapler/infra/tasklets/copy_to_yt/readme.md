# Copy To Yt tasklet


Берет ресурсы и складывает их на YT по пути

    os.path.join(self.input.config.yt_path, f'{app.name}_{self.input.config.environment}_{revision}')

## config

    input:
        config:
            resource_type:
            yt_path:
            yt_proxy:
            environment:
            yt_token:
                uid:
                key:
            apps: []
