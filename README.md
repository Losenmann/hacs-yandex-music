Браузер медиа для плагина Yandex Station
========================================

[![Home Assistant](https://img.shields.io/badge/home_assistant-41BDF5.svg?style=for-the-badge&logo=home-assistant&logoColor=white)](https://www.home-assistant.io)
[![HACS](https://img.shields.io/badge/hacs-integration-41BDF5.svg?style=for-the-badge)](https://hacs.xyz/docs/use/repositories/type/integration/)
![License](https://img.shields.io/github/license/losenmann/hacs-yandex-music?style=for-the-badge&color=FF0000)
[![Release](https://img.shields.io/github/release/Losenmann/hacs-auth-aaa/all.svg?style=for-the-badge)](https://github.com/Losenmann/hacs-yandex-music/releases)
[![Maintainer](https://img.shields.io/badge/maintainer-@losenmann-FF6E00?style=for-the-badge)](https://github.com/Losenmann)
[![Donate](https://img.shields.io/badge/donate-yoomoney-8B3FFD.svg?style=for-the-badge)](https://yoomoney.ru/to/410015216730856)

> Включайте музыку, плейлисты и радио на Яндекс.Станции из Home Assistant!

## Скриншот
<details>
  <summary><b>Корневой раздел: Библиотека</b></summary>  
  <img src="https://raw.githubusercontent.com/losenmann/hass-yandex-music/main/images/library.png" alt="Библиотека">
</details>
<details>
  <summary><b>Раздел: Жанры</b></summary>  
  <img src="https://raw.githubusercontent.com/losenmann/hass-yandex-music/main/images/genres.png" alt="Жанры">
</details>
<details>
  <summary><b>Раздел: Новые релизы</b></summary>  
  <img src="https://raw.githubusercontent.com/losenmann/hass-yandex-music/main/images/new_releases.png" alt="Новые релизы">
</details>
<details>
  <summary><b>Работа компонента с плеером сторонней интеграции</b></summary>    
  <b>- Медиацентр Kodi:</b><br>
  <img src="https://raw.githubusercontent.com/losenmann/hass-yandex-music/main/images/generic_player.png" alt="Медиацентр Kodi">
</details>

## Введение

Проект вырос из Pull-request-а: https://github.com/AlexxIT/YandexStation/pull/133.

## Установка

> ⚠️ Для полноценной работы компонента сперва потребуется установить: [AlexxIT/YandexStation](https://github.com/AlexxIT/YandexStation)
> и настроить авторизацию. Информация по установке и конфигурации доступна по ссылке.

### Установка посредством HACS
> 👍 ️Рекомендованный способ

1. Откройте HACS (через `Extensions` в боковой панели)
1. Добавьте новый произвольный репозиторий:
   1. Выберите `Integration` (`Интеграция`) в качестве типа репозитория
   1. Введите ссылку на репозиторий: `https://github.com/losenmann/hass-yandex-music`
   1. Нажмите кнопку `Add` (`Добавить`)
   1. Дождитесь добавления репозитория (занимает до 10 секунд)
   1. Теперь вы должны видеть доступную интеграцию `Yandex Music Browser` (`Браузер Яндекс Музыки`) в списке новых интеграций.
1. Нажмите кнопку `Install` чтобы увидеть доступные версии
1. Установите последнюю версию нажатием кнопки `Install`
1. Перезапустите HomeAssistant

### Вручную
> ⚠️ Не рекомендуется

Клонируйте репозиторий во временный каталог, затем создайте каталог `custom_components` внутри папки конфигурации
вашего HomeAssistant (если она еще не существует). Затем переместите папку `yandex_music_browser` из папки `custom_components` 
репозитория в папку `custom_components` внутри папки конфигурации HomeAssistant.
Пример (при условии, что конфигурация HomeAssistant доступна по адресу `/mnt/homeassistant/config`) для Unix-систем:
```
git clone https://github.com/losenmann/hass-yandex-music.git hass-yandex-music
mkdir -p /mnt/homeassistant/config/custom_components
mv hass-yandex-music/custom_components/yandex_music_browser /mnt/homeassistant/config/custom_components/
```

## Конфигурация

### Из меню _Интеграции_

1. Найдите интеграцию `Yandex Music Browser` (`Браузер Яндекс Музыки`) в списке интеграций
1. Нажмите на найденную интеграцию
1. Следуйте инструкциям на экране для завершения настройки

### Используя `configuration.yaml`

1. Добавьте `yandex_music_browser:` куда-нибудь в Ваш файл `configuration.yaml` (двоеточие на конце обязательно!)
1. Перезапустите Home Assistant

#### Возможная конфигурация

```yaml
# Конфигурация интеграции
yandex_music_browser:
  # Язык для отображения
  # Поддерживаемые языки:
  # - en: Английский (поддерживается интеграцией)
  # - ru: Русский (поддерживается интеграцией)
  # - uk: Украинский (поддерживается интеграцией)
  # - az: Азербайджанский
  # - be: Белорусский
  # - he: Иврит
  # - hy: Армянский
  # - ka: Грузинский
  # - kk: Казахский
  # - tr: Турецкий
  # - uz: Узбекский
  #
  # Языки, не поддерживаемые интеграцией, будут отображать контент на выбранном языке,
  # но элементы управления будут на английском.
  language: ru
  
  # Опции для меню браузера
  menu_options:
    # Предустановка: Новые релизы
    - new_releases
    
    # Создание папки в корне:
    - title: "Юзвери"
      image: "http://www.pngall.com/wp-content/uploads/2016/06/Nyan-Cat-Free-Download-PNG.png"
      items:
        - user(abcd.ef)  # Добавление по имени пользователя: abcd.ef@yandex.ru
        - user(#12345)  # Добавление по ID
        
        # Иерархия многоуровневая и многотипная.
        - title: "И их любимые альбомы"
          class: "albums"
          items:
            # На одном уровне может находиться сколько угодно объектов каких-либо типов.
            - album(10413482)  # Carpenter Brut - Blood Machines
            - album(448629)  # The Karaoke Machine Presents - Gwen Stefani
            - track(24945454)  # Five Finger Death Punch - Wrong Side of Heaven
```

##### Скиншоты результирующей иерархии

<details>
  <summary><b>Корневой раздел</b></summary>  
  <img src="https://raw.githubusercontent.com/losenmann/hass-yandex-music/main/images/hierarchy/root.png" alt="Корневой раздел">
</details>
<details>
  <summary><b>Папка "Юзвери"</b></summary>  
  <img src="https://raw.githubusercontent.com/losenmann/hass-yandex-music/main/images/hierarchy/users.png" alt="Папка &quot;Юзвери&quot;">
</details>
<details>
  <summary><b>Папка "И их любимые альбомы"</b></summary>  
  <img src="https://raw.githubusercontent.com/losenmann/hass-yandex-music/main/images/hierarchy/albums.png" alt="Папка &quot;И их любимые альбомы&quot;">
</details>

#### Перечень доступных предустановок

| Код | Аргумент | Вид аргумента | Пример вызова |
| --- | -------- | ------------- | --- |
| `album` | `r'\d+'` | Согласно REGEX-шаблону | `album(r'\d+')` |
| `artist` | `r'\d+'` | Согласно REGEX-шаблону | `artist(r'\d+')` |
| `genre` | `r'.+'` | Согласно REGEX-шаблону | `genre(r'.+')` |
| `genres` | `None` | Обязательно без значения | `genres` |
| `mix_tag` | `<mix_tag_id>` | _Необязательный параметр_ | `mix_tag(<mix_tag_id>)`,<br>`mix_tag` |
| `new_playlists` | `None` | Обязательно без значения | `new_playlists` |
| `new_releases` | `None` | Обязательно без значения | `new_releases` |
| `personal_mixes` | `None` | Обязательно без значения | `personal_mixes` |
| `playlist` | `r'(\d+:)?\d+'` | Согласно REGEX-шаблону | `playlist(r'(\d+:)?\d+')` |
| `radio` | `<radio_id>` | _Необязательный параметр_ | `radio(<radio_id>)`,<br>`radio` |
| `track` | `r'\d+'` | Согласно REGEX-шаблону | `track(r'\d+')` |
| `user` | `<username>`,<br>`#<user_id>` | Имя пользователя / UID | `user(abcd.ef)`,<br>`user(#12345)` |
| `user_liked_albums` | `<username>`,<br>`#<user_id>` | Имя пользователя / UID | `user_liked_albums(abcd.ef)`,<br>`user_liked_albums(#12345)` |
| `user_liked_artists` | `<username>`,<br>`#<user_id>` | Имя пользователя / UID | `user_liked_artists(abcd.ef)`,<br>`user_liked_artists(#12345)` |
| `user_liked_playlists` | `<username>`,<br>`#<user_id>` | Имя пользователя / UID | `user_liked_playlists(abcd.ef)`,<br>`user_liked_playlists(#12345)` |
| `user_liked_tracks` | `<username>`,<br>`#<user_id>` | Имя пользователя / UID | `user_liked_tracks(abcd.ef)`,<br>`user_liked_tracks(#12345)` |
| `user_likes` | `<username>`,<br>`#<user_id>` | Имя пользователя / UID | `user_likes(abcd.ef)`,<br>`user_likes(#12345)` |
| `user_playlists` | `<username>`,<br>`#<user_id>` | Имя пользователя / UID | `user_playlists(abcd.ef)`,<br>`user_playlists(#12345)` |
| `yandex_mixes` | `None` | Обязательно без значения | `yandex_mixes` |

_Примечание:_ Вызовы к функции `library` (при фактической доступности таковой) невозможны. Это
обусловлено внутренней обработкой иерархии. Вызовы `library` с числовым аргументом выполняют роль
навигации по иерархии.

## Что поддерживается

Проект поддерживает проигрывание почти всех типов медиа, которые получаемы библиотекой `yandex-music`.

### Яндекс станции (_Мини_, колонки, и т.д.)

#### В локальном режиме

- Треки (любые)
- Альбомы (любые)
- Плейлисты (любые)
- Исполнители (любые)
- Радио (некоторые не воспроизводятся / не отображаются)

#### В облачном режиме

В облачном режиме есть множество огрехов относительно воспроизведения. При этом, доступны:

- Треки (некоторые; если трек не поддерживается, включится Skrillex...)
- Альбомы (некоторые)
- Плейлисты (только пользователя, авторизованного под станцией)
- Исполнители (некоторые)
- Радио (как повезёт!)

### Другие плееры

Плееры, принимающие на вход ссылку в службу `media_player.play_media`, смогут воспроизводить треки.

Протестировано на следующих интеграциях:

- `kodi` - открытие по ссылке **работает**
- `onkyo` - открытие по ссылке **работает**

Также плееры могут перехватывать `media_type == yandex`. В качестве `media_id` будет использоваться
тип и идентификатор объекта, к примеру: `track:12345`. Компонент попробует разобраться, что к чему.