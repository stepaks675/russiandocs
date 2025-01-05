---
title: Руководство по Story Network
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
> 🚧 Мы всё ещё на тестовой сети!
>
> Обратите внимание, что Story Network (наша L1 блокчейн-сеть) всё ещё находится в режиме тестовой сети. Это означает, что в процессе возможны изменения или ошибки.

# Обзор

Story Network — это специализированный L1 блокчейн, объединяющий преимущества EVM и Cosmos SDK. Сеть полностью совместима с EVM и имеет оптимизированный слой исполнения (execution layer), предназначенный для обработки сложных структур данных, связанных с IP, быстро и с минимальными затратами. Это достигается за счёт:
* использования предварительно скомпилированных примитивов для обработки сложных структур данных (например, IP-графов) за секунды с минимальными затратами;
* уровня консенсуса на основе зрелого стека CometBFT, который обеспечивает быструю финализацию и низкую стоимость транзакций;
* модульной архитектуры, разделяющей консенсус и выполнение с помощью Engine-API Ethereum.

# Ресурсы

## :link: RPC

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        RPC
      </th>

      <th style={{ textAlign: "left" }}>
        RPC URL
      </th>

      <th style={{ textAlign: "left" }}>
        Официальный
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        Story
      </td>

      <td style={{ textAlign: "left" }}>
        `https://rpc.odyssey.storyrpc.io/`
      </td>

      <td style={{ textAlign: "left" }}>
        :white_check_mark:
      </td>
    </tr>
  </tbody>
</Table>

## :mag: Обозреватели Блоков

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Обозреватель
      </th>

      <th style={{ textAlign: "left" }}>
        URL
      </th>

      <th style={{ textAlign: "left" }}>
        Официальный
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        <a href="https://odyssey.storyscan.xyz/" target="_blank">Обозреватель Blockscout ↗️</a>
      </td>

      <td style={{ textAlign: "left" }}>
        `https://odyssey.storyscan.xyz/`
      </td>

      <td style={{ textAlign: "left" }}>
        :white_check_mark:
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        <a href="https://odyssey.story.explorers.guru/" target="_blank">Обозреватель Nodes.Guru ↗️</a>
      </td>

      <td style={{ textAlign: "left" }}>
        `https://odyssey.story.explorers.guru/`
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        <a href="https://www.okx.com/web3/explorer/story-odyssey" target="_blank">Обозреватель OKX ↗️</a>
      </td>

      <td style={{ textAlign: "left" }}>
        `https://www.okx.com/web3/explorer/story-odyssey`
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        <a href="https://story.aurascan.io/" target="_blank">Story Scan от Aura Network ↗️</a>
      </td>

      <td style={{ textAlign: "left" }}>
        `https://story.aurascan.io/`
      </td>

      <td style={{ textAlign: "left" }}>

      </td>
    </tr>
  </tbody>
</Table>

## :mag: Обозреватель операций связанных с IP

Для транзакций, связанных с интеллектуальной собственностью, например, регистрации IPA, выпуска лицензии, прикрепления условий лицензии и т. д.

| Обозреватель                                                                                      | URL                                         |
| :------------------------------------------------------------------------------------------------ | :------------------------------------------ |
| <a href="https://odyssey.explorer.story.foundation" target="_blank">Обозреватель Story Odyssey ↗️</a> | `https://odyssey.explorer.story.foundation` |

## :money_with_wings: Краны

| Faucet                                                                                       | Количество  | Требования   |
| :------------------------------------------------------------------------------------------- | :------ | :------------- |
| <a href="https://odyssey.faucet.story.foundation/" target="_blank">Кран Story ↗️</a>       | 1 $IP   | Every 24 hours |
| <a href="https://faucet.quicknode.com/story/odyssey" target="_blank">Кран Quicknode ↗️</a> | 1-2 $IP | Every 24 hours |

## :moneybag: Стейкинг

| Dashboard                                                                           |
| :---------------------------------------------------------------------------------- |
| <a href="https://staking.story.foundation/" target="_blank">Валидаторы Story ↗️</a> |

## Порты

Доступные порты для клиентов `geth` и `story`:

Geth:

* RPC: 8545
* WS: 8546
* P2P: 30303

Metrics:

* Prometheus: 9100
* Geth: 6060
* Story: 26660

## Поставщики (провайдеры) инфраструктуры

### Кросс-чейн

* [LayerZero](https://docs.layerzero.network/v2/developers/evm/technical-reference/deployed-contracts#odyssey-testnet)

### Индексаторы/Данные

* [Simplehash](https://simplehash.com/)
* [Goldsky](https://goldsky.com/)
* [Zettablock](https://zettablock.com/)

### Оракулы/Автоматизация

* [Gelato](https://www.gelato.network/)

### Инструменты

* [Protofire](https://protofire.io/)

### Кошельки/AA

* [Dynamic](https://www.dynamic.xyz/)
* [Pimlico](https://www.pimlico.io/)
* [ZeroDev](https://zerodev.app/)

# Дополнительные Разделы

* [Настройка Кошелька](doc:odyssey-wallet-setup)
* [Установка Ноды](doc:odyssey-node-setup)
* [Операции Валидатора](doc:odyssey-validator-operations)
* [Токеномика и Стейкинг](doc:tokenomics-staking)