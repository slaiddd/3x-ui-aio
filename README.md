
# 3x-ui-aio

## Запуск

### 1. Создайте два поддомена:
Например:
- `panel.example.com` - панель 3x-ui 
- `cloud.example.com` - xray/сайт-заглушка

A-записи этих поддоменов должны содержать IP вашего VPS

### 2. Установите Docker

Инструкции по установке Docker: [https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/)

### 3. Клонируйте репозиторий

```bash
git clone https://github.com/ampetelin/3x-ui-aio.git && cd 3x-ui-aio
```

### 4. Отредактируйте файл `angie.conf`

#### Вариант 1: автоматически (рекомендуется)

Выполните команду:

```bash
sed -i \
    -e "s|<your_panel_domain>|panel.example.com|g" \
    -e "s|<your_xray_domain>|cloud.example.com|g" \
    angie.conf
```

Не забудьте заменить `panel.example.com` и `cloud.example.com` на свои поддомены.

#### Вариант 2: вручную

Откройте файл `angie.conf` в любом редакторе:

```bash
nano angie.conf
```

И вручную замените:
- `<your_panel_domain>` → на поддомен для панели (например, `panel.example.com`) 
- `<your_xray_domain>` → на поддомен для xray (например, `cloud.example.com`) 

Сохраните изменения после редактирования.

### 5. Запустите Docker Compose

```bash
docker compose up -d
```

### 6. Перейдите в панель

Откройте браузер и перейдите по адресу: [https://panel.example.com](https://panel.example.com)

**Дефолтные данные для авторизации:**  
- Логин: `admin`  
- Пароль: `admin`

> [!CAUTION]
> Обязательно измените дефолтный логин и пароль в разделе **Panel Settings -> Authentication**.

> [!WARNING]
> Для повышения безопасности рекомендуется изменить путь до панели в разделе **Panel Settings -> URI Path**.
> 
> Например, при изменении URI Path на `/my-secret-panel-path/` панель будет доступна только по адресу [https://panel.example.com/my-secret-panel-path/](https://panel.example.com/my-secret-panel-path/)

### 7. Добавьте inbound в панели 3x-ui

При добавлении inbound настройте следующие обязательные параметры:

- **Protocol:** vless
- **Port:** 443
- **Proxy Protocol:** Enabled
- **External Proxy:** cloud.example.com:443
- **Security:** Reality
- **Xver:** 2
- **Dest (Target):** angie:2443
- **SNI:** cloud.example.com


<img width="517" height="872" alt="image" src="https://github.com/user-attachments/assets/cab0e272-03ef-444f-b055-aee322a5e711" />
<img width="501" height="888" alt="image" src="https://github.com/user-attachments/assets/6fae43d2-2580-43e4-8aa6-730776546697" />


### 8. Подписка

Для корректной работоспособности подписок 3x-ui, необходимо перейти в **Panel Settings -> Subscription** и настроить `Reverse Proxy URI` следующим образом:

<img width="1667" height="729" alt="image" src="https://github.com/user-attachments/assets/02f550e6-5074-4419-be82-4995a6d85f1f" />



Для корректной работоспособности подписок Clash / Mihomo необходимо перейти в **Panel Settings -> Subscription** и настроить `Reverse Proxy URI` следующим образом:

<img width="1105" height="578" alt="image" src="https://github.com/user-attachments/assets/c0e0fd27-cdc7-4d08-86e7-1b3d23be93da" />


Не забудьте заменить `panel.example.com` на свой поддомен.

