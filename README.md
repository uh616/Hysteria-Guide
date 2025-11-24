# README --- Hysteria 2 Guide (RU + EN)

## 🇷🇺 Русский текст

🚀 **ГАЙД для Hysteria 2**\
616 минут · November 24, 2025\
🚀 **Hysteria 2: Настройка на VPS без домена (Self-signed)**

Этот гайд поможет поднять свой быстрый VPN на протоколе Hysteria 2.
Особенность метода: нам не нужен домен. Мы используем самоподписанные
сертификаты. Это бесплатно, быстро и работает так же надежно.

**Требования:** - Любой VPS сервер (Ubuntu 20.04 / 22.04) - 5 минут
времени - Купить VPS можно тут (по рефке +15% бонус):\
https://aeza.net/?ref=549012

------------------------------------------------------------------------

### 🛠 Шаг 1. Подготовка сервера

``` bash
apt update && apt upgrade -y
apt install curl openssl nano -y
```

### 🔑 Шаг 2. Генерация ключей

``` bash
mkdir -p /etc/hysteria

openssl req -x509 -nodes -newkey rsa:4096 -keyout /etc/hysteria/server.key -out /etc/hysteria/server.crt -days 36500 -subj "/CN=www.google.com"

chmod 644 /etc/hysteria/server.key
chmod 644 /etc/hysteria/server.crt
```

### 📥 Шаг 3. Установка Hysteria

``` bash
bash <(curl -fsSL https://get.hy2.sh/)
```

### ⚙️ Шаг 4. Конфигурация

``` yaml
listen: :5500

tls:
  cert: /etc/hysteria/server.crt
  key: /etc/hysteria/server.key

auth:
  type: password
  password: "ПРИДУМАЙ_ПАРОЛЬ"

masquerade: 
  type: proxy
  proxy:
    url: https://www.google.com/
    rewriteHost: true

obfs:
  type: salamander
  salamander:
    password: "ПРИДУМАЙ_OBFS_ПАРОЛЬ"
```

### 🛡 Шаг 5. Firewall + запуск

``` bash
ufw allow 5500/udp
systemctl enable hysteria-server
systemctl start hysteria-server
systemctl status hysteria-server
```

### 📱 Шаг 6. Клиент

Шаблон ссылки:

    hy2://ПАРОЛЬ@IP_СЕРВЕРА:5500/?insecure=1&obfs=salamander&obfs-password=OBFS_ПАРОЛЬ&sni=www.google.com#MyHysteria

------------------------------------------------------------------------

## 🇬🇧 English translation

🚀 **Hysteria 2 GUIDE**\
616 minutes · November 24, 2025\
🚀 **Hysteria 2: Setup on VPS without domain (Self‑signed)**

This guide walks you through setting up a fast VPN on the Hysteria 2
protocol. The cool part: no domain needed. We use self‑signed
certificates --- free, quick, and reliable.

**Requirements:** - Any VPS (Ubuntu 20.04 / 22.04) - 5 minutes of time -
Optional VPS recommendation (+15% bonus):\
https://aeza.net/?ref=549012

------------------------------------------------------------------------

### 🛠 Step 1. Server prep

``` bash
apt update && apt upgrade -y
apt install curl openssl nano -y
```

### 🔑 Step 2. Generate keys

``` bash
mkdir -p /etc/hysteria

openssl req -x509 -nodes -newkey rsa:4096 -keyout /etc/hysteria/server.key -out /etc/hysteria/server.crt -days 36500 -subj "/CN=www.google.com"

chmod 644 /etc/hysteria/server.key
chmod 644 /etc/hysteria/server.crt
```

### 📥 Step 3. Install Hysteria

``` bash
bash <(curl -fsSL https://get.hy2.sh/)
```

### ⚙️ Step 4. Configuration

``` yaml
listen: :5500

tls:
  cert: /etc/hysteria/server.crt
  key: /etc/hysteria/server.key

auth:
  type: password
  password: "CHOOSE_PASSWORD"

masquerade: 
  type: proxy
  proxy:
    url: https://www.google.com/
    rewriteHost: true

obfs:
  type: salamander
  salamander:
    password: "CHOOSE_OBFS_PASSWORD"
```

### 🛡 Step 5. Firewall + start

``` bash
ufw allow 5500/udp
systemctl enable hysteria-server
systemctl start hysteria-server
systemctl status hysteria-server
```

### 📱 Step 6. Client link

Template:

    hy2://PASSWORD@SERVER_IP:5500/?insecure=1&obfs=salamander&obfs-password=OBFS_PASSWORD&sni=www.google.com#MyHysteria

------------------------------------------------------------------------

Telegram channel: https://t.me/jennaortegasimp
