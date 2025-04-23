# Running test job
`./run_tests.sh <run_description> (test-name)`

Optional args:
- test-name: Only run such test file/test class/test name.

Examples:
- `./run_tests.sh only-smoke-tests SmokeTest` (run all tests of class SmokeTest, call job only-smoke-test)
- `./run_tests.sh one-test CalendarPlanningApikeyTest.test_invalid_apikey` (run one test, call job one-test)


# Logs
Logs of test execution are saved to K8S job logs as well as S3 bucket `solver-tests-logs` under job's name.
Script will print how to check logs, but here is examples:

Look k8s logs:
`kubectl logs -f jobs/$JOB_NAME`

Check s3 logs:
`aws s3 cp s3://solver-tests-logs/$JOB_NAME.log.gz - | gunzip -c | less`

# Troubleshooting 
If job can't pull image for execution, check that there is secret with docker credentials: 
`kubectl get secret registry-credentials`

## Putting secrets in job pod for accessing private registry
https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/

`kubectl create secret docker-registry registry-credentials --docker-server=582601430203.dkr.ecr.us-east-2.amazonaws.com --docker-username=AWS --docker-password=$(aws ecr get-login-password --region us-east-2) --docker-email=nikitakun@yandex-team.ru`

## Troubleshoot the job
You can check logs, or check job pod info.
Check script: run_tests.sh

# Cleaning up jobs
To remove all the history of jobs run:
`./cleanup_jobs.sh`
