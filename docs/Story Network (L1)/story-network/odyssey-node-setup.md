---
title: Установка Ноды
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---

Этот раздел поможет вам настроить ноду Story. Story черпает вдохновение из PoS Ethereum, разделяя исполнение и консенсус. Клиент исполнения `story-geth` передает блоки EVM в клиент консенсуса `story` через Engine API, используя адаптер ABCI++ для совместимости состояния EVM с состоянием CometBFT. Такая архитектура обеспечивает эффективность консенсуса, не ограниченную пропускной способностью выполнения транзакций.

![](https://files.readme.io/7dee0e873bcb2aeeaf12c3c0d63db44692c1bfe5cee599c52ea5c465240967a4-image.png)

Бинарные файлы `story` и `geth`, необходимые для запуска узлов Story, доступны на страницах наших последних релизов:

* **Клиент исполнения `story-geth`:**
  * Релизы: [**тут**](https://github.com/piplabs/story-geth/releases)
  * Последний стабильный релиз (v0.10.1): [**тут**](https://github.com/piplabs/story-geth/releases/tag/v0.10.1)
* **Клиент консенсуса `story`:**
  * Релизы: [**тут**](https://github.com/piplabs/story/releases)
  * Последний стабильный релиз (v0.13.0): [**тут**](https://github.com/piplabs/story/releases/tag/v0.13.0)

***ВАЖНО: Для тестовой сети Odyssey необходимо начать с версии v0.12.0, поскольку эта версия обязательна перед применением любых последующих обновлений. Сначала скачайте эту версию, чтобы обеспечить совместимость с тестовой сетью. Также убедитесь, что вы загружаете бинарные файлы, соответствующие архитектуре вашей системы.***

## Системные требования

| Аппаратное обеспечение  | Требования |
| --------- | ----------- |
| CPU       | 4 Ядра    |
| RAM       | 16 ГБ       |
| Диск     | 200 ГБ      |
| Сеть | 25 МБит/с   |

На AWS рекомендуется использовать серии M6i, R6i или C6i.

## Порты

*Убедитесь, что все необходимые порты для работы узла открыты, как указано ниже:*

* `story-geth`
  * 8545
    * Требуется, если вы хотите взаимодействовать с нодой через JSON-RPC API по HTTP.
  * 8546
    * Требуется для взаимодействия через WebSockets.
  * 30303 (TCP + API)
    * ДОЛЖЕН быть открыт для p2p-коммуникации.
* `story`
  * 26656
    * ДОЛЖЕН быть открыт для p2p-коммуникации консенсуса.
  * 26657
    * Требуется для взаимодействия с RPC Tendermint.
  * 26660
    * Нужен для предоставления метрик Prometheus.

## Стандартные пути

По умолчанию создаются следующие папки данных для клиентов консенсуса и исполнения:

* Mac OS X
  * `story` корневая папка: `~/Library/Story/story`
  * `story-geth` корневая папка: `~/Library/Story/geth`
* Linux
  * `story` корневая папка: `~/.story/story`
  * `story-geth` корневая папка:  `~/.story/geth`

*В дальнейшем в документации корневую папку данных `story` будем называть `${STORY_DATA_ROOT}`, а `story-geth` — `${GETH_DATA_ROOT}`.*

*Вы можете переопределить эти настройки на стороне клиента `story`, указав `--home ${STORY_CONFIG_FOLDER}`, а для клиента `geth` — `--config ${GETH_CONFIG_FOLDER}`. Дополнительную информацию о переопределении конфигурации можно найти в [руководстве по созданию частной сети](https://github.com/piplabs/story?tab=readme-ov-file#creating-a-private-network). *

После загрузки бинарных файлов Story обратите внимание, что имя файла зависит от операционной системы. Например, на Linux с архитектурой AMD64 файл может называться `story-linux-amd64` или `geth-linux-amd`. Для упрощения работы рекомендуется переименовать файл в `story` после загрузки:

```
mv story-linux-amd64 story
```

Теперь вы можете запускать программу, используя команду `story` в терминале. В дальнейшем в документации будем использовать название `story`.

## Настройка клиента исполнения (`story-geth`)

1. (Mac OS X)  Бинарные файлы для Mac OS X еще не подписаны, поэтому их может потребоваться снять с карантина вручную:

   ```bash
   sudo xattr -rd com.apple.quarantine ./geth
   ```
2. Теперь вы можете запустить `geth` следующей командой:

   ```bash
   ./geth --odyssey --syncmode full
   ```

   * Режим синхронизации `snap` (по умолчанию) все еще находится в разработке.

### Сброс

Если у вас возникли проблемы, и вы хотите попробовать подключиться к сети с чистого состояния, выполните следующую команду:

```bash
rm -rf ${GETH_DATA_ROOT} && ./geth --odyssey --syncmode full
```

* Mac OS X: `rm -rf ~/Library/Story/geth/* && ./geth --odyssey --syncmode full`
* Linux: `rm -rf ~/.story/geth/* && ./geth --odyssey --syncmode full`

### Отладка

Чтобы проверить статус работы `geth`, полезно использовать встроенный IPC-RPC сервер, запустив следующую команду:

```bash
geth attach ${GETH_DATA_ROOT}/geth.ipc
```

* Mac OS X:
  * `geth attach ~/Library/Story/geth/odyssey/geth.ipc`
* Linux:
  * `geth attach ~/.story/geth/odyssey/geth.ipc`

Подключившись к IPC серверу, вы можете использовать следующие команды:

* `eth.blockNumber` покажет последний блок, до которого синхронизирован geth. Если результат `undefined`, возможно, есть проблема с подключением к пиру или синхронизацией.
* `admin.peers` отобразит список других нод `geth`, с которыми ваш клиент подключен. Если список пуст, проблема в подключении к пиру.
* `eth.syncing` вернет `true`, если geth синхронизируется, и `false` в противном случае.

## Настройка клиента консенсуса (`story`)

1. (Mac OS X Only) Бинарные файлы для Mac OS X еще не подписаны, поэтому их может потребоваться снять с карантина вручную:

   ```bash
   sudo xattr -rd com.apple.quarantine ./story
   ```
2. Инициализируйте клиент `story` с помощью команды:

   ```bash
   ./story init --network odyssey 
   ```

   * По умолчанию в качестве монникера (идентификатора вашей ноды) используется имя пользователя. Вы можете переопределить его, передав флаг `--moniker ${NODE_MONIKER}`.
   * Если вы хотите использовать свою собственную директорию данных, укажите её через флаг `--home ${STORY_DATA_DIR}`.
   * Если у вас уже есть файлы конфигурации и данных, но вы хотите полностью их сбросить, добавьте флаг `--clean`.
3. Теперь запустите `story` командой:

   ```bash
   ./story run
   ```

***ВАЖНО: Если вы настраиваете новый узел, начните с версии v0.12.0***, так как эта версия является базовой перед установкой последующих обновлений. После этого установите каждое обновление по порядку. Следуйте этим шагам:

1. Скачайте [версию v0.12.0](https://github.com/piplabs/story/releases/tag/v0.12.0), выбрав бинарный файл, подходящий для вашей архитектуры.
2. Инициализируйте и запустите версию v0.12.0, следуя инструкциям выше.
3. Скачайте и обновите клиент до следующих версий, используя [это руководство](https://medium.com/story-protocol/story-v0-10-0-node-upgrade-guide-42e2fbcfcb9a):
   1. [v0.12.1 ](https://github.com/piplabs/story/releases/tag/v0.12.1) обновление на высоте блока 322000

Примечание: в процессе работы вы можете увидеть сообщения `Stopping peer for error`. Это известная проблема, связанная с нестабильностью соединения с узлами, но она не влияет на прогресс блоков.

### Сброс

*Если вы столкнулись с проблемами и хотите попробовать повторно подключиться к сети **СОХРАНИВ ВАШ КЛЮЧ**, выполните следующую команду:*

```bash
rm -rf ${STORY_DATA_ROOT}/data/* && \
echo '{"height": "0", "round": 0, "step": 0}' > ${STORY_DATA_ROOT}/data/priv_validator_state.json && \
./story run
```

* Mac OS X:
  ```bash
  rm -rf ~/Library/Story/story/data/* && \
  echo '{"height": "0", "round": 0, "step": 0}' > ~/Library/Story/story/data/priv_validator_state.json && \
  ./story run
  ```
* Linux:
  ```bash
  rm -rf ~/.story/story/data/* && \
  echo '{"height": "0", "round": 0, "step": 0}' > ~/.story/story/data/priv_validator_state.json && \
  ./story run
  ```

\*Если вы хотите начать с **ПОЛНОСТЬЮ** чистого состояния (**\*ВНИМАНИЕ: ЭТО УДАЛИТ ВАШ ФАЙЛ priv_validator_key.json**):

```bash
rm -rf ${STORY_DATA_ROOT} && ./story init --network odyssey && ./story run
```

* Mac OS X:
  * `rm -rf ~/Library/Story/story/* && ./story init --network odyssey && ./story run`
* Linux:
  * `rm -rf ~/.story/story/* && ./story init --network odyssey && ./story run`

Чтобы проверить, синхронизируется ли узел:

* Проверьте RPC-эндпоинт geth, чтобы убедиться, что блоки увеличиваются:
  ```bash
  curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}' [http://localhost:8545](http://localhost:8545/)
  ```
* Подключитесь к `geth` и проверьте, увеличивается ли eth.blockNumber.

### Пользовательская Конфигурация

Вы можете настроить ноду, изменив следующие файлы:

* `${STORY_DATA_ROOT}/config/config.toml` — изменение сетевых и консенсусных настроек.
* `${STORY_DATA_ROOT}/config/story.toml` — обновление конфигураций клиента.
* `${STORY_DATA_ROOT}/priv_validator_key.json` — файл с ключом валидатора, его можно заменить своим собственным.

### Пользовательская Автоматизация

Пример конфигурации `Systemd` для Linux:

```bash
# geth
[Unit]
Description=Node-Geth
After=network.target

[Service]
Type=simple
Restart=always
RestartSec=1
User=${USER_NAME}
WorkingDirectory=${YOUR_HOME_DIR}
ExecStart=geth --odyssey  --syncmode full
StandardOutput=journal
StandardError=journal
SyslogIdentifier=node-geth
StartLimitInterval=0
LimitNOFILE=65536
LimitNPROC=65536

[Install]
WantedBy=multi-user.target
```

```bash
# story
[Unit]
Description=Node-story
After=network.target node-geth.service

[Service]
Type=simple
Restart=always
RestartSec=1
User=ec2-user
WorkingDirectory=${YOUR_HOME_DIR}
ExecStart=story run
StandardOutput=journal
StandardError=journal
SyslogIdentifier=node-story
StartLimitInterval=0
LimitNOFILE=65536
LimitNPROC=65536

[Install]
WantedBy=multi-user.target

```

### Отладка

Для проверки статуса `story` можно выполнить запрос к его внутреннему JSONRPC/HTTP-эндпоинту. Полезные команды:

* `curl localhost:26657/net_info | jq '.result.peers[].node_info.moniker'`
  * Получить список подключённых узлов
* `curl localhost:26657/health`
  * Проверить состояние узла: - `{}` — узел работает корректно.

### Распостранённые проблемы

1. `auth failure: secret conn failed: read tcp ${IP_A}:${PORT_A}->${IP_B}:{PORT_B}: i/o timeout`
   * Эта ошибка случается, когда `external_address` по умолчанию, находящийся в `config.toml` (`””`) не считывается слушателем. Решение: удалите файл `addrbook.json` в `{STORY_DATA_ROOT}/config/addrbook.json` и добавьте `external_address = {ВАШ_ПУБЛИЧНЫЙ_IP}` в `config.toml`.

### Автоматические обновления
Для упрощения обновлений клиента консенсуса, особенно во время хардфорков, рекомендуется использовать [Cosmovisor](https://docs.cosmos.network/v0.45/run-node/cosmovisor.html). Это позволяет автоматизировать процесс обновления без необходимости перезапускать клиента.

Для начала клиент **должен быть обновлён хотя бы до версии 0.9.13**. Подробное руководство по настройке Cosmovisor можно найти [здесь](https://medium.com/story-protocol/story-v0-10-0-node-upgrade-guide-42e2fbcfcb9a).