---
title: 🗂️ Реестр
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
Различные реестры в Story функционируют как основная директория/хранилище для глобальных состояний протокола. Кроме того, они содержат функции для обновления этого хранилища.

В отличие от [IP-аккаунтов](doc:ip-account), которые управляют состоянием конкретных IP, **реестр** отвечает за более широкие состояния протокола.

# Типы реестров

Ниже перечислены все реестры в Story.

## [Реестр IP-активов](doc:ip-asset-registry)

Отвечает за регистрацию IP в протоколе.

## [Реестр групповых IP-активов](doc:group-ip-asset-registry)

Отвечает за регистрацию и поддержку групповых IP-активов.

## [Реестр лицензий](doc:license-registry)

Хранит все данные, связанные с лицензиями в протоколе, включая прикрепление условий лицензии к IP-активам, регистрацию производных работ, создание новых Шаблонов Лицензий и так далее.

## [Реестр модулей](doc:module-registry)

Поддерживает и обновляет глобальный список модулей и хуков, зарегистрированных без разрешений в Story.
