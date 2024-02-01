# Домашнее задание к занятию «Базовые объекты K8S»

### Цель задания

В тестовой среде для работы с Kubernetes, установленной в предыдущем ДЗ, необходимо развернуть Pod с приложением и подключиться к нему со своего локального компьютера. 

------

### Чеклист готовности к домашнему заданию

1. Установленное k8s-решение (например, MicroK8S).
2. Установленный локальный kubectl.
3. Редактор YAML-файлов с подключенным Git-репозиторием.

------

### Инструменты и дополнительные материалы, которые пригодятся для выполнения задания

1. Описание [Pod](https://kubernetes.io/docs/concepts/workloads/pods/) и примеры манифестов.
2. Описание [Service](https://kubernetes.io/docs/concepts/services-networking/service/).

------

### Задание 1. Создать Pod с именем hello-world

1. Создать манифест (yaml-конфигурацию) Pod.
2. Использовать image - gcr.io/kubernetes-e2e-test-images/echoserver:2.2.

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    app: one
  name: hello-world
  namespace: default
spec:
  containers:
  - name: hello-world
    image: gcr.io/kubernetes-e2e-test-images/echoserver:2.2
    ports:
    - containerPort: 8080
```

3. Подключиться локально к Pod с помощью `kubectl port-forward` и вывести значение (curl или в браузере).

<p align="center">
    <img width="1200 height="600" src="/img/pod-hello-world.png">
</p>
<br>
<p align="center">
    <img width="1200 height="600" src="/img/p-f-hello-world.png">
</p>

------

### Задание 2. Создать Service и подключить его к Pod

1. Создать Pod с именем netology-web.
2. Использовать image — gcr.io/kubernetes-e2e-test-images/echoserver:2.2.

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    app: netology
  name: netology-web
  namespace: default
spec:
  containers:
  - name: hello-world
    image: gcr.io/kubernetes-e2e-test-images/echoserver:2.2
    ports:
    - containerPort: 8080
```

3. Создать Service с именем netology-svc и подключить к netology-web.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: netology-svc
  namespace: default
spec:
  ports:
    - name: web
      port: 80
      targetPort: 8080
  selector:
    app: netology
```

4. Подключиться локально к Service с помощью `kubectl port-forward` и вывести значение (curl или в браузере).

<p align="center">
    <img width="1200 height="600" src="/img/pods-get-svc.png">
</p>
<br>
<p align="center">
    <img width="1200 height="600" src="/img/p-f-netology-svc.png">
</p>

------

### Правила приёма работы

1. Домашняя работа оформляется в своем Git-репозитории в файле README.md. Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.
2. Файл README.md должен содержать скриншоты вывода команд `kubectl get pods`, а также скриншот результата подключения.
3. Репозиторий должен содержать файлы манифестов и ссылки на них в файле README.md.

------

### Критерии оценки
Зачёт — выполнены все задания, ответы даны в развернутой форме, приложены соответствующие скриншоты и файлы проекта, в выполненных заданиях нет противоречий и нарушения логики.

На доработку — задание выполнено частично или не выполнено, в логике выполнения заданий есть противоречия, существенные недостатки.
