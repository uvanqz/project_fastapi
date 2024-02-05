6. Система управления персоналом с использованием Fast Api
   - Модели: Пользователи, Сотрудники, Отпуска
   - Идея проекта: Создание системы для управления персоналом с возможностью добавления новых сотрудников, учета отпусков и запросов на отпуск.
___
**Логика работы**

Администратор создает учетную запись сотруднику (модель User).

Администратор вносит данные сотрудника (модель Employee).

Выдает логин/пароль сотруднику.

Администратор может сам создать/назначить отпуск сотруднику.

Сотрудник может запросить отпуск самостоятельно. Администратор должен его одобрить (поле approved = True) или отклонить (approved = False).
___
**Стэк технологий**
___
+ :rocket: Framework: FAST API
+ ORM: SQLAlchemy2.0
+ Pydantic
+ :scroll: Poetry
+ :ship: Docker
+ :snake: Python 3.11
___
Перед запуском проекта необходимо создать:
1. Файл `.env` в папке `/grafana`. Пример находится в файле '/grafana/env.example'
2. Файл `.env` в папке `/conf`. Пример находится в файле '/conf/env.example'
___
Для запуска проекта:
```
docker-compose up --build
```
___
**После запуска проекта доступны:**

|Название     |URL  |
|-------------|-----|
|Документация | http://0.0.0.0:8000/swagger|
|Метрика      | http://0.0.0.0:8000/metrics|
|Prometheus   | http://0.0.0.0:9090|
|Grafana      | http://0.0.0.0:3000/login|

**Эндпоинты**

- [X] Создание учетной записи сотрудника:
* [POST] /employees
* Описание: Создает новую учетную запись сотрудника в системе.

- [X] Заполнение учетных данных сотрудника:
* [PATCH] /employees/{employee_id}
* Описание: Обновляет учетные данные сотрудника по его идентификатору.

- [X] Список всех сотрудников:
* [GET] /employees
* Описание: Возвращает список всех сотрудников в системе.

- [X] Создание отпуска администратором:
* [POST] /vacations
* Описание: Позволяет администратору создать новый отпуск для сотрудника.

- [X] Запрос на отпуск от сотрудника:
* [POST] /vacation-requests
* Описание: Сотрудник отправляет запрос на отпуск.

- [X] Список отпусков без статуса:
* [GET] /vacations/pending
* Описание: Возвращает список отпусков, ожидающих рассмотрения администратором.

- [X] Подтверждение/отклонение отпуска администратором:
* [PUT] /vacations/{vacation_id}/approval
* Описание: Администратор может подтвердить или отклонить отпуск сотрудника.

- [X] Детали отпуска:
* [GET] /vacations/{vacation_id}
* Описание: Возвращает подробную информацию о конкретном отпуске.

- [X] Удаление отпуска:
* [DELETE] /vacations/{vacation_id}
* Описание: Удаляет отпуск сотрудника (возможно только администратором).

- [X] Список отпусков для конкретного сотрудника:
* [GET] /employees/{employee_id}/vacations
* Описание: Возвращает список отпусков для определенного сотрудника.

- [X] Информация о сотруднике:
* [GET] /employees/{employee_id}
* Описание: Возвращает информацию о конкретном сотруднике.

- [X] Список отпусков с фильтрацией по статусу:
* [GET] /vacations
* Параметры запроса: approved (пример: /vacations?approved=['';true;false])
* Описание: Возвращает список отпусков с возможностью фильтрации по статусу (утвержденные, отклоненные).

- [X] Список отпусков на рассмотрение:
* [GET] /vacations/pending
* Описание: Возвращает список отпусков по которым нет решения.

- [X] Удаление сотрудника:
* [DELETE] /employees/{employee_id}
* Описание: Удаляет учетную запись сотрудника (возможно только администратором).