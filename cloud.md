# Облачный функционал

В шлюз включен облачный функционал. Он необходим для возможности удаленного мониторинга и управления шлюзом и устройствами.

## Что реализовано в данный момент

- Личный кабинет для объединении нескольких шлюзов
- Мониторинг работы шлюза
- Получение данных с устройств

## Что будет реализовано дальше

- Управление устройствами
- Мобильное приложение
- Интеграция с Яндекс.Алиса
- Обновление шлюза из облака
- Бэкап шлюза в облако
- Облачные автоматизации
- Отправка данных по ресурсам в УК

## Как использовать

- Через веб интерфейс
- Через HTTP API
- Получить информацию о настройках `Cloud` в шлюзе `/api/cloud`
  
## Веб-мониторинг

В данный момент не требуется регистрация личного кабинета и возможен доступ к шлюзу по токену, который шлюз получает при первом подключении к облаку.
Держите ваш токен в секрете!

```http
https://cloud.slsys.io/monitoring?device={TOKEN}
```

## Настройки в шлюзе

Вы можете включить подключение к облаку в настройках `Settings -> Link -> Cloud Setup`.

Возможно отключение отправки данных по устройствам и прием команд управления из облака. Также здесь можно получить API токен.

![](/img/cloud.png)

## HTTP API

### Получение данных об устройстве по его токену. Метод GET

```http
https://cloud.slsys.io/api/device/TOKEN
```

### Проверяем есть ли данный email

Если нет - отправляет код подтверждения на него, который необходим для регистрации. Методы GET/POST

```http
https://cloud.slsys.io/api/user/check
```

Параметры:

- email (*)
  
### Регистрирует новый аккаунт

Методы GET/POST

```http
https://cloud.slsys.io/api/user/reg
```

Параметры:

- email (*)
- email_code (*)
- name (*)  
- password (*)

Возвращает ok при успешной регистрации

### Вход в аккаунт

Методы GET/POST

```http
https://cloud.slsys.io/api/user/reg
```

Параметры:

- email (*)
- password (*)  
- application - Идентификатор приложения для сессии, по умолчанию default

Возвращает sid при успешном входе

### Получение данных по аккаунту (email и name)

Методы GET/POST

```http
https://cloud.slsys.io/api/user/profile
```

Параметры:

- access_token (*)  

Возвращает информацию профиля