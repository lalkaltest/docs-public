## Загрузка образов в Kubernetes, используя Docker Registry

Данная статья поможет вам в создании пода, использующего Секрет, для загрузки образа из частного реестра Docker или репозитория.

Docker Registry — это серверное приложение, предназначенное для хранения и распространения Docker-образов.

## Для чего может использоваться Docker Registry

- контроль над местом хранения образов
- контроль над распространением образов
- интеграция хранения и распространения образов в процесс разработки

Запуск Docker

Авторизуйтесь:

```bash
docker login
```

Введите свой логин и пароль.

Данная команда создаст или изменит файл config.json. В нем будет храниться информация, необходимая для авторизации.

Просмотреть содержимое можно через выполнение команды:

```bash
cat ~/.docker/config.json
```

Результат выполнения будет примерно следующим:

```json
{
  "auths": {
    "https://index.docker.io/v1/": {
      "auth": "c3R...zE2"
    }
  }
}
```

## Создание Секрета на основе существующих учетных данных Docker

Кластер Kubernetes использует для авторизации Секрет, входящий в состав docker-registry. Если **docker login** уже запущен, то можно скопировать учетные данные в Kubernetes:

kubectl create secret generic regcred \\     --from-file=".dockerconfigjson=<path/to/."docker/config.json> \\     -- необходимо внести какие-либо изменения (например, изменить имя нового секрета), то Вы можете внести изменения в Секрет перед тем, как сохранить его. Убедитесь, что:

- указан type для kubernetes.io/dockerconfigjson
- задано имя для элемента .dockerconfigjson
- base64 кодирует файл docker и вставляет эту строку, непрерывную как значение для данных поля data[".dockerconfigjson"]

Например:

```
apiVersion: v1 kind: Secret metadata:   name: myregistrykey   namespace: awesomeapps data:   .dockerconfigjson: UmVhbGx5IHJlYWxseSByZWVlZWVlZWVlZWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWxsbGxsbGxsbGxsbGxsbGxsbGxsbGxsbGxsbGxsbGx5eXl5eXl5eXl5eXl5eXl5eXl5eSBsbGxsbGxsbGxsbGxsbG9vb29vb29vb29vb29vb29vb29vb29vb29vb25ubm5ubm5ubm5ubm5ubm5ubm5ubm5ubmdnZ2dnZ2dnZ2dnZ2dnZ2dnZ2cgYXV0aCBrZXlzCg==" type: "kubernetes.io/dockerconfigjson
```

## Создание пода, используя Секрет

Ниже приведен конфигурационный файл для создания пода использующего учетные данные указанные в regcred:

```
apiVersion: v1 kind: Pod metadata:   name: private-reg spec:   containers:   - name: private-reg-container     image: <your-private-image>   imagePullSecrets:   - name: regcred
```

В файле my-private-reg-pod.yaml замените<your-private-image> на путь к требуемому образу из Вашего реестра. Например:

```bash
example/exmpl-private:v1
```

Создаем под, используя имеющийся Секрет, и проверяем, что под запущен:

```bash
kubectl apply -f my-private-reg-pod.yaml kubectl get pod private-reg
```
