# gate4ai-mail — коннектор «Почта (IMAP/SMTP)» для gate4.ai

Чтение писем, черновики и отправка с проверкой по «Отправленным». Соединения открывает хост и сам выполняет вход по алиасу пароля из Vault — коннектор пароль не видит. Входящие письма помечаются как недоверенный контент.

Коннектор — WASM-модуль для хоста [gate4ai](https://github.com/gate4ai/gate4ai): что ему можно, объявлено в [manifest.yaml](manifest.yaml) (`capabilities`) и показывается владельцу при установке; всё остальное хост запрещает (`capability_denied`). Написан на [sdk-go](https://github.com/gate4ai/sdk-go).

## Установка

```sh
gate4ai connectors install email                 # из магазина gate4.ai
# или своя сборка:
gate4ai connectors pack . -o email.g4c && gate4ai connectors install email.g4c --dev
```

Настройки — `connectors.email` в конфигурации gate4ai (секреты — только алиасы Vault, `@имя`).

## Разработка

```sh
go test ./...                                                    # нативно, на тестовом хосте sdk-go/hosttest
GOOS=wasip1 GOARCH=wasm go build -buildmode=c-shared -o connector.wasm .
```

## Лицензия

[AGPL-3.0-only](LICENSE) с [дополнительным разрешением](LICENSE-EXCEPTION) для хоста gate4ai: коннектор можно исполнять в хосте и распространять вместе с ним, не распространяя AGPL на хост. Изменения самого коннектора остаются под AGPL. Вклад — по DCO (`git commit -s`).
