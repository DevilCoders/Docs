# VM Scheduler release process in AWS

1. Commit your changes to the repository. Check out commit revision.
    ```
    arc checkout r9638042
    ```

2. Build and push to AWS ECR docker image.
    `push.sh` script argument is an alias for the image. The built image has a tag in format `r{REVISION}_{ALIAS}`, in the example - `r9638042_metrics`.
   - agent:
       ```
       arcadia/maps/b2bgeo/vm_scheduler/agent/aws_docker $ ./push.sh metrics
       ```
       Result image example: [582601430203.dkr.ecr.us-east-2.amazonaws.com/vm-agent:r9638042_metrics](https://us-east-2.console.aws.amazon.com/ecr/repositories/private/582601430203/vm-agent?region=us-east-2).

   - server:
        ```
        arcadia/maps/b2bgeo/vm_scheduler/server/aws_docker $ ./push.sh metrics
        ```
        Result image example: [582601430203.dkr.ecr.us-east-2.amazonaws.com/vm-scheduler:r9638042_metrics](https://us-east-2.console.aws.amazon.com/ecr/repositories/private/582601430203/vm-scheduler?region=us-east-2).

3. Deploy to testing.

    2.1. Commit to the repository updated k8s config for testing environment.
      - To update agent docker image renew `VMS_AGENT_DOCKER_IMAGE_VERSION` variable in [config-map.yaml](k8s/testing/config-map.yaml).
      - To update server image renew docker image tag in [deployment.yaml](k8s/testing/deployment.yaml).

    2.2. After pull request is merged start the deploy process. Run [apply-testing.sh](k8s/apply-testing.sh) script.
    ```
    arcadia/maps/b2bgeo/vm_scheduler/k8s $ ./apply-testing.sh
    ```

4. Run integration tests.

    4.1. Run solver intergation tests (are used for VM Scheduler testing) via [run_tests.sh](../mvrp_solver/backend/integration_tests/k8s/run_tests.sh) script.
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
      - To update agent docker image renew `VMS_AGENT_DOCKER_IMAGE_VERSION` variable in [config-map.yaml](k8s/stable/config-map.yaml)
      - To update server image renew docker image tag in [deployment.yaml](k8s/stable/deployment.yaml)

    6.2. After pull request is merged start the deploy process. Run [apply-stable.sh](k8s/apply-stable.sh) script.
    ```
    arcadia/maps/b2bgeo/vm_scheduler/k8s $ ./apply-stable.sh
    ```
    If only environment variables were updated run `kubectl rollout restart deployments/vm-scheduler-stable`.

7. To rollback the version, go through step 6 (commit the corresponding docker image tag).
