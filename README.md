# dieHard
Для создания Docker контейнера на основе Alpine Linux и запуска Nginx с стартовой страницей index.html, выполните следующие шаги:

1. Создайте файл Dockerfile в вашем проекте. Этот файл будет содержать инструкции для сборки образа Docker.

2. Откройте редактор и вставьте следующий код в файл Dockerfile:
```bash
# Using Alpine Linux as the base image
FROM alpine:latest

# Update package list and upgrade packages
RUN apk update && apk upgrade

# Install Nginx
RUN apk add --no-cache nginx

# Copy the index.html file to the Nginx directory
COPY index.html /usr/share/nginx/html/index.html

# Expose port 80 for HTTP traffic
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
```
1. Создайте файл index.html в том же каталоге, где находится файл Dockerfile. Этот файл будет использоваться в качестве стартовой страницы Nginx.

Вставьте следующий код в файл index.html:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welcome</title>
</head>
<body>
    <h1>Welcome to Nginx on Alpine!</h1>
    <p>This is a simple Nginx server running inside a Docker container based on Alpine Linux.</p>
</body>
</html>
```
1. Соберите Docker образ, выполнив следующую команду в терминале:
```bash
docker build -t my-nginx-app .
```
Здесь `my-nginx-app` - это имя образа, которое можно заменить на любое имя, которое вы предпочитаете.

1. Запустите контейнер на основе созданного образа, выполнив следующую команду:
```bash
docker run -d -p 8080:80 my-nginx-app
```
Здесь `-d` запускает контейнер в фоновом режиме, а `-p 8080:80` определяет порт на хостовой машине, на котором будет доступен ваш Nginx-сервер (в этом примере порт 8080).

Теперь вы можете проверить работу Nginx в контейнере, отправив запрос на http://localhost:8080 или http://127.0.0.1:8080.
