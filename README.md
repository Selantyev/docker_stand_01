# docker_stand_01

# Создайте свой кастомный образ nginx на базе alpine. После запуска nginx должен отдавать кастомную страницу (достаточно изменить дефолтную страницу nginx).

`mkdir -p /opt/docker/mynginx`

`cd /opt/docker/mynginx`

Создать Dockerfile:

`vi Dockerfile`

```
FROM nginx:1.19.6-alpine
WORKDIR /usr/share/nginx/html
COPY index.html index.html
EXPOSE 80
```

Создать дефолтную страницу:

`vi index.html`

```
<p style="text-align: center;"><span style="font-size: 24px;"><strong>Hello, Docker!</strong></span></p>
```

Создать образ:

`docker build -t vselantyev/nginx:v1 .`

Проверить список образов:

`docker images`

```
REPOSITORY         TAG             IMAGE ID       CREATED         SIZE
vselantyev/nginx   v1              209e9228f3fb   7 seconds ago   22.3MB
nginx              1.19.6-alpine   629df02b47c8   7 weeks ago     22.3MB
hello-world        latest          bf756fb1ae65   13 months ago   13.3kB
```

Запустить контейнер из образа:

`docker run -d -p 8080:80 209e9228f3fb`

Проверить запуск:

`docker ps`

```
CONTAINER ID   IMAGE          COMMAND                  CREATED              STATUS              PORTS                  NAMES
1e9d39502cb6   209e9228f3fb   "/docker-entrypoint.…"   About a minute ago   Up About a minute   0.0.0.0:8080->80/tcp   mystifying_feynman
```

Проверить дефолтную страницу:

`curl localhost:8080`

`<p style="text-align: center;"><span style="font-size: 24px;"><strong>Hello, Docker!</strong></span></p>`


# Определите разницу между контейнером и образом. Вывод опишите в домашнем задании.
Образ — это "шаблон" только для чтения (RO). Образ может содержать в себе операционную систему и приложения (например Alpine Linux + nginx + MySQL + ...). Из образов создаются контейнеры. Образы можно создавать самостоятельно или скачивать готовые из хаба.

В контейнере содержится окружение, которое нужно для работы приложения в нём. Каждый контейнер создается из образа. Каждый контейнер изолирован и является безопасной средой для приложения.

# Ответьте на вопрос: Можно ли в контейнере собрать ядро?
Нет. Docker контейнер использует ядро операционной системы, в контейнере нет собственного или дополнительного ядра.

# Собранный образ необходимо запушить в docker hub и дать ссылку на ваш репозиторий.


