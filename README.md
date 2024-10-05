# Прототип инструмента для создания страховых продуктов согласно выдвинутым гипотезам

Прототип решения доступен по адресу https://odeal-admin.simplizio.com

Интерактивная документация доступна по адресу https://odeal-docs.simplizio.com

## Исходный код

Фронтенд:
    https://github.com/LeonidAlekseev/odeal-admin
Бекенд:
    https://github.com/spacesoldier/insuranceProductsPrototypeBackendNR

    https://github.com/LeonidAlekseev/odeal-cms
    

## Архитектура решения

Решение состоит из набора компонент, каждая из которых представляет собой сервис, развёрнутый в контейнеризованном виде на виртуальной машине, работающей под управлением ОС Ubuntu 22.04.
Каждый сервис запущен с помощью docker compose и включён в общую для всех сервисов docker network.
Список компонент:
| Наименование    | Название | Назначение |
| -------- | ------- | ------- |
| npm  | Nginx Proxy Manager    |  Реверс-прокси  |
| strcmsv4 | Strapi v4     |  Headless cms для хранения контента и метаданных  |
| strcmsv4postgres    | PostgreSQL    |  СУБД , используемая для хранения данных CMS  |
| odeal-admin    | Frontend    |  Приложение на базе Next.js , реализующее интерфейс пользователя  |
| nodered    | Node-RED    |  Приложение Node.js на базе Express.js , реализующее логику бекенда  |
| postgres    | PostgreSQL    |  СУБД , используемая для хранения данных бекенда  |
| pgbouncer    | PgBouncer    |  connection pooler СУБД бекенда  |


## Запуск решения

Для запуска решения понадобится машина под управлением ОС Ubuntu 22.04
Порядок действий по запуску решения:
- Установить (если отсутствует) Docker , Docker compose
- Клонировать данный репозиторий
- Проверить каждый файл docker-compose.yml на корректность указания секретов, таких как пароли для подключения к БД. Задать секреты любым удобным способом.
- Создать docker network для будущих сервисов
    ```shell
        docker network create hackersnet -d bridge
    ```
- Запустить сервисы один за другим, выполняя в каждой папке команду
  ```shell
        docker compose up -d
  ```

После запуска всех сервисов выполнить следующие действия:

- В случае запуска на виртуалной машине:
  - убедиться в доступности портов 81, 80, 443
  - выполнить настройку реверс-прокси Nginx Proxy Manager
  
- В случае запуска на локальной машине:
  - интерфейс пользователя доступен по адресу http://localhost:9090
  - интерфейс CMS доступен по адресу http://localhost:1347