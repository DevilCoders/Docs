# Create asynsolver service

1. Create testing service in testing cluster.
    ```bash
    # First switch kubectl to 'testing' cluster.
    aws eks update-kubeconfig --name testing

    # Make sure testing/secrets.yaml has base64-encoded secret values.
    # Then apply testing configs.
    kubectl apply -f ./testing
    ```

2. Create stable service in default cluster.
    ```bash
    # First switch kubectl to 'default' cluster.
    aws eks update-kubeconfig --name default

    # Make sure stable/secrets.yaml has base64-encoded secret values.
    # Then apply stable configs.
    kubectl apply -f ./stable
    ```
