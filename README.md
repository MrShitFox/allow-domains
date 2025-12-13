# Allow Domains — Списки маршрутизации

Этот репозиторий предоставляет автоматически обновляемые списки доменов и IP-адресов популярных сервисов и категорий. Списки предназначены для настройки выборочной маршрутизации (split-tunneling) или блокировки на сетевом оборудовании.

> **Назначение:** Помощь в настройке обхода блокировок или, наоборот, ограничении доступа к ресурсам на уровне роутера.

## 📋 Поддерживаемые форматы

Списки автоматически конвертируются в форматы для популярного ПО:

| Формат | Описание | Пример / Файл |
| :--- | :--- | :--- |
| **Sing-box** (`.srs`) | Бинарные наборы правил (Rule Set) для Sing-box 1.11+ | `russia_inside.srs` |
| **Xray / v2ray** (`.dat`) | GeoSite файлы с разбивкой по категориям | `geosite.dat` |
| **Dnsmasq** (`nfset`) | Конфиг для OpenWrt >= 23.05 (nftables) | `nftset=/example.com/4#inet#fw4#vpn_domains` |
| **Dnsmasq** (`ipset`) | Конфиг для OpenWrt <= 21.02 (ipset) | `ipset=/example.com/vpn_domains` |
| **Clash** | Правила для Clash/ClashX | `DOMAIN-SUFFIX,example.com` |
| **MikroTik** | Статические DNS записи (FWD) | `/ip dns static add type=FWD...` |
| **Kvas** | Простой список доменов для Kvas 1.1.8+ | `example.com` |
| **RAW** | "Сырой" список доменов | Текстовый файл |

## 🌍 Списки и Категории

### 🇷🇺 Россия (Russia)
| Название | Описание | Состав |
| :--- | :--- | :--- |
| **Russia Inside** | Ресурсы, заблокированные в РФ, а также сервисы, блокирующие доступ из РФ. | Anime, News, Porn, Instagram*, Facebook*, Twitter, LinkedIn, Rutracker и др. |
| **Russia Outside** | Российские ресурсы, доступные только с российских IP (Госуслуги, РЖД, банки). | `src/Russia-domains-outside.lst` |

### 🇺🇦 Украина (Ukraine)
Списки заблокированных ресурсов в Украине. Данные агрегируются с проектов [uablacklist.net](https://uablacklist.net/) и [zaborona.help](https://zaborona.help/).

### 📂 Категории (Categories)
Отдельные тематические подборки:
* **Anime**: Популярные аниме-ресурсы.
* **News**: Новостные издания.
* **Porn**: Порнографические ресурсы.
* **H.O.D.C.A**: Хостинг-провайдеры и CDN (Hetzner, OVH, Digital Ocean, Cloudflare, AWS).
* **GeoBlock**: Ресурсы с геоблокировкой.

### 📱 Сервисы (Services)
Списки для конкретных приложений, включая домены и (где возможно) IP-подсети:
* **Discord** (домены + подсети)
* **YouTube**
* **Telegram**
* **Instagram / Facebook (Meta)* **
* **Twitter (X)**
* **TikTok**
* **Cloudflare**
* **HDRezka**

> ⚠️ **Google AI**: Домены Google AI вынесены в [отдельный список](https://github.com/MrShitFox/allow-domains/blob/main/Services/google_ai.lst) и исключены из общего `GeoBlock`, так как Google часто меняет гео-привязку IP-адресов.

---

## 🔗 Прямые ссылки (Download)

<details>
  <summary><b>Раскрыть список ссылок</b></summary>

#### Общие файлы
* [Xray GeoSite (geosite.dat)](https://github.com/MrShitFox/allow-domains/releases/latest/download/geosite.dat)

#### Russia Inside
* [Sing-box SRS](https://github.com/MrShitFox/allow-domains/releases/latest/download/russia_inside.srs)
* [Dnsmasq (nfset)](https://raw.githubusercontent.com/MrShitFox/allow-domains/main/Russia/inside-dnsmasq-nfset.lst)
* [MikroTik](https://raw.githubusercontent.com/MrShitFox/allow-domains/refs/heads/main/Russia/inside-mikrotik-fwd.lst)
* [RAW список](https://raw.githubusercontent.com/MrShitFox/allow-domains/main/Russia/inside-raw.lst)

#### Russia Outside
* [Sing-box SRS](https://github.com/MrShitFox/allow-domains/releases/latest/download/russia_outside.srs)
* [RAW список](https://raw.githubusercontent.com/MrShitFox/allow-domains/main/Russia/outside-raw.lst)

#### Ukraine
* [Sing-box SRS](https://github.com/MrShitFox/allow-domains/releases/latest/download/ukraine_inside.srs)
* [Dnsmasq (nfset)](https://raw.githubusercontent.com/MrShitFox/allow-domains/main/Ukraine/inside-dnsmasq-nfset.lst)

#### Популярные сервисы (SRS)
* [YouTube](https://github.com/MrShitFox/allow-domains/releases/latest/download/youtube.srs)
* [Discord](https://github.com/MrShitFox/allow-domains/releases/latest/download/discord.srs)
* [Telegram](https://github.com/MrShitFox/allow-domains/releases/latest/download/telegram.srs)
* [Meta*](https://github.com/MrShitFox/allow-domains/releases/latest/download/meta.srs)

</details>

---

## 🛠 Использование и переход на этот репозиторий

> ⚠️ **Важно:** Оригинальный репозиторий [itdoginfo/allow-domains](https://github.com/MrShitFox/allow-domains) **заброшен и не обновляется**.
> 
> Данный репозиторий ([MrShitFox/allow-domains](https://github.com/MrShitFox/allow-domains)) является актуальным форком, который поддерживается сообществом. Чтобы получать свежие списки блокировок, необходимо изменить источник обновлений в настройках вашего роутера.

### ⚡ Быстрый переход для Podkop (OpenWrt)

Чтобы Podkop начал качать списки отсюда, нужно отредактировать всего один файл.

1.  **Установите редактор nano** (если еще нет):
    ```bash
    opkg update && opkg install nano
    ```

2.  **Откройте файл с настройками путей**:
    ```bash
    nano /usr/lib/podkop/constants.sh
    ```

3.  **Замените ссылки** в блоке `## Lists`.
    Найдите строки `GITHUB_RAW_URL` и `SRS_MAIN_URL`. Замените `itdoginfo` на `MrShitFox`.
    
    Должно получиться так:
    ```bash
    ## Lists
    GITHUB_RAW_URL="https://raw.githubusercontent.com/MrShitFox/allow-domains/main"
    SRS_MAIN_URL="https://github.com/MrShitFox/allow-domains/releases/latest/download"
    ```
    *(Нажмите `Ctrl+S` затем `Enter` для сохранения, и `Ctrl+X` для выхода).*

4.  **Обновите списки**:
    ```bash
    podkop list_update
    ```

Теперь ваш роутер использует актуальные базы.

---

### OpenWrt (Dnsmasq + NFTables)
Пример настройки точечной маршрутизации/блокировки для OpenWrt 23.05+:

1.  Скачайте список в папку конфигурации dnsmasq:
    ```bash
    cd /tmp/dnsmasq.d && wget [https://raw.githubusercontent.com/MrShitFox/allow-domains/main/Russia/inside-dnsmasq-nfset.lst](https://raw.githubusercontent.com/MrShitFox/allow-domains/main/Russia/inside-dnsmasq-nfset.lst) -O domains.conf
    ```
2.  Создайте Set и правило в Firewall:
    ```bash
    uci add firewall ipset
    uci set firewall.@ipset[-1].name='vpn_domains'
    uci set firewall.@ipset[-1].match='dst_net'
    
    uci add firewall rule
    uci set firewall.@rule[-1]=rule
    uci set firewall.@rule[-1].name='mark_domains' # Или block_domains
    uci set firewall.@rule[-1].src='lan'
    uci set firewall.@rule[-1].dest='*'
    uci set firewall.@rule[-1].proto='all'
    uci set firewall.@rule[-1].ipset='vpn_domains'
    uci set firewall.@rule[-1].target='MARK' # Или DROP для блокировки
    uci set firewall.@rule[-1].set_mark='0x1'
    uci commit firewall
    
    service firewall restart && service dnsmasq restart
    ```

---

## 🤝 Как помочь проекту

Мы приветствуем помощь в актуализации списков!

* **Добавить/Удалить домен**: Лучше всего написать в нужное обсуждение по ссылкам ниже. Но если вам удобнее — создавайте Issue или кидайте Pull Request.
    * [Обсуждение Russia Inside](https://github.com/MrShitFox/allow-domains/discussions/1)
    * [Обсуждение Russia Outside](https://github.com/MrShitFox/allow-domains/discussions/2)

### Полезные ссылки
* [Как найти все домены ресурса (инструкция)](https://itdog.info/analiziruem-trafik-i-opredelyaem-domeny-kotorye-ispolzuyut-sajty-i-prilozheniya/)
* [Telegram-канал с обновлениями](https://t.me/itdoginfo)

---
*\* Компания Meta признана экстремистской и запрещена на территории РФ.*
