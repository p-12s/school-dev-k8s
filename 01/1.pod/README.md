# Pod

## 0. Устанавливаем конфиг стенда
Вид конфига (нам выдал админ, но его можно получить самому, если вы администратор кластера):
```bash
apiVersion: v1
clusters:
- cluster:
    insecure-skip-tls-verify: true
    server: https://you-server:port
  name: this-is-my-cluster-name
contexts:
- context:
    cluster: cluster-name
    namespace: this-is-my-cluster-login
    user: this-is-my-cluster-login
  name: this-is-my-cluster-name
current-context: cluster-name
kind: Config
preferences: {}
users:
- name: this-is-my-cluster-login
  user:
    token: this-is-my-secret-cluster-token
```
Путь к конфигу (заменяем содержимое):  
```
~/.kube/config
kubectl get pods
```
Либо при запуске команд явно указываем путь конфига (неудобнее):
```
kubectl --kubeconfig ~/.kube/MY-CUSTOM-CONFIG-FILE get pods
```

## 1. Создаем Pod

Для этого выполним команду:

```bash
kubectl apply -f pod.yaml
```

Проверим результат, для чего выполним команду:

```bash
kubectl get pod
```

Результат должен быть примерно следующим:

```bash
NAME      READY     STATUS              RESTARTS   AGE
my-pod    0/1       ContainerCreating   0          2s
```

Через какое-то время Pod должен перейти в состояние `Running`
и вывод команды `kubectl get po` станет таким:

```bash
NAME      READY     STATUS    RESTARTS   AGE
my-pod    1/1       Running   0          59s
```

## 2. Скейлим приложение

Открываем файл pod.yaml редактором:

```bash
vim pod.yaml
```

Входим в режим редактирования нажатием `i`  и заменяем там строку:

```diff
-  name: my-pod
+  name: my-pod-1
```

Сохраняем и выходим.

> Для vim нужно нажать последовательность кнопок
>
> `<Esc>:wq<Enter>`
> **Esc** - выход из режима редактирования,
> комбинация **:wq** - сохраняет внесенные изменения

Применяем изменения, для этого выполним команду:

```bash
kubectl apply -f pod.yaml
```

Проверяем результат, для этого выполним команду:

```bash
kubectl get pod
```

Результат должен быть примерно следующим:

```bash
NAME      READY     STATUS    RESTARTS   AGE
my-pod    1/1       Running   0          10m
my-pod-1  1/1       Running   0          59s
```

## 3. Чистим за собой кластер

Для этого выполним команду:

```bash
kubectl delete pod --all
```
