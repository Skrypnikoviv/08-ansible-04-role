# Playbook для установки Clickhouse, Vector и LightHouse

Этот playbook предназначен для установки и настройки **Clickhouse**, **Vector** и **LightHouse** на указанных хостах. Он автоматически загружает необходимые пакеты, устанавливает их и запускает соответствующие сервисы.

## Описание задач

### 1. Установка Clickhouse
Playbook выполняет следующие шаги для установки Clickhouse:
- Загружает дистрибутивы Clickhouse из официального репозитория (с поддержкой резерва на случай неудачной загрузки).
- Устанавливает пакеты Clickhouse (`clickhouse-common-static`, `clickhouse-client`, `clickhouse-server`).
- Запускает сервис Clickhouse после установки.
- Создаёт базу данных `logs` (игнорирует ошибку, если база уже существует).

### 2. Установка Vector
Playbook выполняет следующие шаги для установки Vector:
- Загружает дистрибутив Vector из официального репозитория.
- Устанавливает пакет Vector.
- Запускает сервис Vector после установки.

### 3. Установка LightHouse и настройка Nginx
Playbook выполняет следующие шаги для установки LightHouse:
- Устанавливает **Nginx** и **Node.js**, необходимые для работы LightHouse.
- Клонирует репозиторий LightHouse из [официального источника](https://github.com/VKCOM/lighthouse).
- Устанавливает зависимости LightHouse с помощью `npm install`.
- Настраивает Nginx для запуска веб-интерфейса LightHouse.
- Запускает и включает автозапуск Nginx.

## Переменные

- `clickhouse_version`: Версия Clickhouse, которая будет установлена.
- `clickhouse_packages`: Список пакетов Clickhouse для загрузки и установки (например, `clickhouse-common-static`, `clickhouse-client`, `clickhouse-server`).
- `vector_version`: Версия Vector, которая будет установлена.
- `lighthouse_repo`: URL репозитория LightHouse (по умолчанию `https://github.com/VKCOM/lighthouse`).
- `lighthouse_version`: Версия LightHouse, которая будет установлена.
- `nginx_port`: Порт, на котором Nginx будет обслуживать LightHouse (по умолчанию `80`).

## Теги

- `clickhouse`: Тег для выполнения задач, связанных с установкой Clickhouse.
- `vector`: Тег для выполнения задач, связанных с установкой Vector.
- `lighthouse`: Тег для выполнения задач, связанных с установкой LightHouse и настройкой Nginx.

## Использование

Для запуска playbook'а используйте следующую команду:

```bash
ansible-playbook -i inventory/prod.yml site.yml
