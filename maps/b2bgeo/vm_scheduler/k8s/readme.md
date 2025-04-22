# How to deploy service

For stable:
```
sh apply-stable.sh
```

For testing:
```
sh apply-testing.sh
```

# How to update service

1. Push docker image
2. Set image tag in deployment.yaml (this is new tag, should be equal to revision number without 'r' prefix). You should do this after PR is merged (then you can get revision number).
3. Run apply-*.sh script
4. Execute this to restart service, if it is not restarted (in case when you are updating config-map, but not deployment, then deployment will not be restarted):

For stable:
```
kubectl rollout restart deployment/vm-scheduler-stable
```
For testing:
```
kubectl rollout restart deployment/vm-scheduler-testing
```
