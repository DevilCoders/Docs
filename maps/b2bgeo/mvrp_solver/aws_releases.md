# Solver release process in AWS

1. Commit your changes to the repository. Check out commit revision.
    ```
    arc checkout r9638042
    ```

2. Build and push to AWS ECR docker image.
    `push.sh` script argument is an alias for the image. The built image has a tag in format `r{REVISION}_{ALIAS}`, in the example - `r9638042_metrics`.
   - asynchronous solver:
       ```
       arcadia/maps/b2bgeo/mvrp_solver/backend/async_backend/aws_docker $ ./push.sh metrics
       ```
       Result image example: [582601430203.dkr.ecr.us-east-2.amazonaws.com/async-solver:r9638042_metrics](https://us-east-2.console.aws.amazon.com/ecr/repositories/private/582601430203/async-solver?region=us-east-2).

   - synchronous solver:
        ```
        arcadia/maps/b2bgeo/mvrp_solver/backend/sync_backend/aws_docker $ ./push.sh metrics
        ```
        Result image example: [582601430203.dkr.ecr.us-east-2.amazonaws.com/sync-solver:r9638042_metrics](https://us-east-2.console.aws.amazon.com/ecr/repositories/private/582601430203/sync-solver?region=us-east-2).

    - solver binary image for launching on dynamically allocated on-demand instances:
        ```
        arcadia/maps/b2bgeo/mvrp_solver/aws_docker $ ./push.sh metrics
        ```
        Result image example: [582601430203.dkr.ecr.us-east-2.amazonaws.com/solver-binary:r9638042_metrics](https://us-east-2.console.aws.amazon.com/ecr/repositories/private/582601430203/solver-binary?region=us-east-2).

3. Deploy to testing.

    2.1. Commit to the repository updated k8s config for testing environment.
      - To update asynchronous solver renew docker image tag in [deployment.yaml](backend/async_backend/k8s/testing/deployment.yaml).
      - To update synchronous solver renew docker image tag in [deployment.yaml](backend/sync_backend/k8s/testing/deployment.yaml).
      - To update solver binary image for launching on dynamically allocated on-demand instances renew `VM_SCHEDULER_WORKER_IMAGE_VERSION` environment variable in [config-map.yaml](backend/async_backend/k8s/testing/config-map.yaml).

    2.2. After pull request is merged start the deploy process.
      - To deploy async or solver binary image run [apply-testing.sh](backend/async_backend/k8s/apply-testing.sh) script.
        ```
        arcadia/maps/b2bgeo/mvrp_solver/backend/async_backend/k8s $ ./apply-testing.sh
        ```
        If only environment variables were updated run `kubectl rollout restart deployments/asyncsolver-testing`.
      - To deploy sync solver run [apply-testing.sh](backend/sync_backend/k8s/apply-testing.sh) script.
      ```
      arcadia/maps/b2bgeo/mvrp_solver/backend/sync_backend/k8s $ ./apply-testing.sh
      ```

4. Run integration tests.

    4.1. Run solver intergation tests via [run_tests.sh](../mvrp_solver/backend/integration_tests/k8s/run_tests.sh) script.
    ```
    arcadia/maps/b2bgeo/mvrp_solver/backend/integration_tests/k8s $ ./run_tests.sh metrics
    ```
    4.2. Wait until tests are completed. To view the logs:
    ```
    kubectl logs -f job/solver-integr-tests-r9638215-metrics
    ```

5. The docker image should be kept in testing installation for no less than one day before releasing to production. This point makes sense when we set up traffic mirroring and monitoring on testing.

6. Deploy to production environment.

    6.1. Commit to the repository updated k8s config for stable environment.
      - To update asynchronous solver renew docker image tag in [deployment.yaml](backend/async_backend/k8s/stable/deployment.yaml).
      - To update synchronous solver renew docker image tag in [deployment.yaml](backend/sync_backend/k8s/stable/deployment.yaml).
      - To update solver binary image for launching on dynamically allocated on-demand instances renew `VM_SCHEDULER_WORKER_IMAGE_VERSION` environment variable in [config-map.yaml](backend/async_backend/k8s/stable/config-map.yaml).

    6.2. After pull request is merged start the deploy process.
      - To deploy async or solver binary image run [apply-stable.sh](backend/async_backend/k8s/apply-stable.sh) script.
        ```
        arcadia/maps/b2bgeo/mvrp_solver/backend/async_backend/k8s $ ./apply-stable.sh
        ```
        If only environment variables were updated run `kubectl rollout restart deployments/asyncsolver-stable`.
      - To deploy sync solver run [apply-stable.sh](backend/sync_backend/k8s/apply-stable.sh) script.
      ```
      arcadia/maps/b2bgeo/mvrp_solver/backend/sync_backend/k8s $ ./apply-stable.sh
      ```

7. To rollback the version, go through step 6 (commit the corresponding docker image tag).
