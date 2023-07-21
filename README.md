# Приложение Yelb

## Задача

Необходимо построить инфраструктуру в облаке Yandex Cloud, настроить управление инфраструктурой через Terraform и развернуть приложение из репозитория.

## Описание проекта

**Описание:** Проект для разработки приложения и деплоем в кластер **Kubernetes**

**Содержимое:**
  * `.helm` - Helm-чарт
  * `deployments` - Скрипты деплоя (*Legacy*)
  * `images` - Схемы взаимодействия на разных архитектурах
  * `yelb-appserver` - Бэкенд приложения
  * `yelb-db` - PostgreSQL с созданием таблицы и записами
  * `yelb-ui` - Фронтенд приложения

## DNS-зона

> После деплоя приложения, а именно создание балансера для ингресс контроллера, DNS-зона может обновляться от 5 минут до 24 часов.

> Временно можно добавить внешний адрес балансера в hosts

Установите **yc** (YandexCloud CLI) и настройте его по [инструкции](https://cloud.yandex.ru/docs/cli/quickstart#install).

Cкачайте **kubectl** [документация](https://kubernetes.io/docs/tasks/tools/)

Получитесь к кластеру **Kubernetes
```
yc managed-kubernetes cluster get-credentials k8s-cluster --external
```

Выведите список сервисов:
```
kubectl get svc
```

Отобразится список сервисов (в NS Default):
```
NAME                                 TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)                      AGE
ingress-nginx-controller             LoadBalancer   10.96.139.99    158.160.32.244   80:31323/TCP,443:30708/TCP   23m
ingress-nginx-controller-admission   ClusterIP      10.96.183.226   <none>           443/TCP                      23m
kubernetes                           ClusterIP      10.96.128.1     <none>           443/TCP                      92m
```

Скопируйте значение **EXTERNAL-IP** у сервиса с типом *LoadBalancer*.

Поместите в **hosts** (*Windows*: `C:\Windows\System32\drivers\etc`, *Linux*: `/etc/hosts`) строку:
```
158.160.32.244 yelb.s053278.ru
```