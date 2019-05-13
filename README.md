[![Build Status](https://travis-ci.org/sanmai/otpravka-curl.svg?branch=master)](https://travis-ci.org/sanmai/otpravka-curl)

# Примеры использования API Онлайн-сервиса «Отправка» с помощью cURL

Для примера, отправка запроса для проверки телефона делается такой командой:

```bash
curl \
    -H 'X-User-Authorization: Basic $AUTH' \
    -H 'Authorization: AccessToken $TOKEN' \
    -H 'Content-Type: application/json;charset=UTF-8' \
    -H 'Accept: application/json;charset=UTF-8' \
    --request POST \
    --data '[
	{
		"id": "tel1",
		"original-phone": "2-08-14",
		"place": "Камышлов",
		"region": "Свердловская область"
	},
	{
		"id": "tel2",
		"original-phone": "8-499-257-44-56"
	}
]' https://otpravka-api.pochta.ru/1.0/clean/phone
```
Где `$AUTH` - [ключ авторизации](https://otpravka.pochta.ru/specification#/authorization-key), и `$TOKEN` - [токен авторизации](https://otpravka.pochta.ru/specification#/authorization-token). Аналогичным образом можно послать любые другие запросы.

Для удобства есть локальная обёртка `curl`, которая либо берет реквизиты доступа из переменных окружения, или из файлов `tkn.txt` и `auth.txt`. Тот же самый запрос с обёрткой будет выглядеть так:

```bash
./curl POST /1.0/clean/phone <<EOF
[
	{
		"id": "tel1",
		"original-phone": "2-08-14",
		"place": "Камышлов",
		"region": "Свердловская область"
	},
	{
		"id": "tel2",
		"original-phone": "8-499-257-44-56"
	}
]
EOF
```

Если установлена команда `jq` из одноименного пакета, то команда выше покажет красивый JSON-ответ с подсветкой кода.

Нет проблемы объединять команды одну с другой. Например можно посмотреть на скрипт `forms-zip-all`, который получает полный набор документации для тестовой отправки.
