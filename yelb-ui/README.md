## Важно
При первом запуске создайте секрет:
```
kubectl create secret docker-registry gitlab-ci-token --docker-server=<registry> --docker-username=gitlab-ci-token --docker-password=<token> --docker-email=<email>
```