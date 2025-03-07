---
title: 💸 Модуль Роялти
excerpt: Узнайте, как распределяется доход между родительскими и дочерними IP-активами на платформе
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Модуль Роялти определяет, как распределяется доход между родительскими и дочерними IP-активами. Существуют два основных сценария, при которых происходит распределение дохода:

1. Создание лицензии — иногда за выпуск [Лицензионного Токена](doc:license-token) для IP-актива взимается плата. Когда она оплачивается (кем-то, кто хочет зарегистрировать производный актив или просто владеть лицензией), доход распределяется вверх по цепочке.
2. Прямое вознаграждение — если кто-то отправляет доход непосредственно на IP-актив, он также распределяется вверх по цепочке.

В следующем примере (с использованием [Ликвидного абсолютного процента (LAP)](doc:policy-liquid-absolute-percentage)) показано, что происходит, когда IP-актив 4 (IPA4) отправляет 1 миллион USDC в пользу IPA3.

1. Доход сначала поступает в контракт Модуля Роялти.
2. Модуль Роялти распределяет USDC между IPA3 и контрактом LAP на основе **стека роялти** (15%).
3. LAP распределяет средства среди других предков, так как они заключили лицензионное соглашение, в соответствии с которым они имеют право на часть дохода IPA3.

**Не переживайте, если вы не понимаете все детали на изображении, оно лишь дает общий обзор работы Модуля Роялти.**

![](https://files.readme.io/25e44cabafe06886fef078422c3d48c472f25a12b6ea60207ffa0b63ef2cd65b-image.png)

## Политики Роялти

Политики Роялти являются частью лицензионного соглашения между двумя IP-активами. Они определяют, как именно происходит распределение дохода.

Модуль Роялти поддерживает как одобренные/встроенные политики, созданные нашей командой, так и внешние политики, которые можно создать самостоятельно.

> 📘 Примечание по Политике Роялти
>
> IP-актив, у которого нет родителей, может создавать лицензии с разными Политиками Роялти, в то время как производный IP-актив наследует Политику Роялти своих родителей.
>
> Кроме того, каждая связь IP-актива с производным активом всегда регулируется одной Политикой Роялти.

### Одобренные/Встроенные Политики Роялти

Эти политики требуют одобрения сообществом и гарантируют распределение токенов роялти среди предков.

1. [Ликвидный Абсолютный Процент (LAP)](doc:liquid-absolute-percentage)
2. [Ликвидный Относительный Процент(LRP)](doc:liquid-relative-percentage)

### Внешние политики роялти

Эти политики могут быть зарегистрированы без разрешений и включать собственные правила распределения доходов и роялти.

* [Внешняя Политика Роялти](doc:external-royalty-policies)

<br />

#### Роялти Токен % vs Роялти Стек %

При создании производного актива создателю необходимо ответить на вопрос: «Какой процент дохода от моей IP я сохраню для себя, а сколько достанется родительским IP?»

Для этого важны два понятия:

1. Токены Роялти — Каждый IP-актив имеет 100,000,000 Токенов Роялти, где каждый токен представляет 0.000001% капитала, поступающего в Хранилище Роялти IP. Владельцы этих токенов могут требовать доход, находящийся в связанном Хранилище Роялти IP.
2. Стек Роялти — это процент дохода IP, который необходимо выплатить предкам через встроенные политики роялти. Внешние Политики Роялти не используют процент Стека Роялти, только встроенные.

Представим следующий сценарий:

* IP1 — корневой IP-актив.
* IP2 — производный актив IP1.
* Пользователь A владеет 100% Токенов Роялти IP1.
* Пользователь B владеет 20% Токенов Роялти IP2.
* Пользователь C владеет 80% Токенов Роялти IP2.
* Стек роялти IP2 составляет 10% — это значит, что все его предки через встроенные политики роялти требуют, чтобы IP2 выплачивал 10% своего дохода. В данном случае предок только один — это IP1. IP1 требует 10% будущего дохода IP2.

На изображении ниже показан пример выплаты в размере 1 миллиона USDC на адрес IP2. На нем видно, как распределяется доход среди владельцев Токенов Роялти всей цепочки производных активов.

![](https://files.readme.io/a96e7d196a85f69dceb2b125ce70008115e15d0aa76b4e14b0dff2007525051b-image.png)

* Владелец RT A — из одного миллиона USDC получает 100k USDC. Сначала выплачивается процент Стека Роялти, и владелец RT A, имеющий 100% Токенов Роялти IP1, получает всю сумму 100k USDC.
* Владелец RT B — из одного миллиона USDC получает 180k USDC. Владельцы IP2 в целом получают 900k USDC. Эти 900k USDC распределяются между владельцами Токенов Роялти IP2: B и C. B имеет 20% Токенов Роялти IP2, поэтому получает 900k USDC \* 20% = 180k.
* Владелец RT C — из одного миллиона USDC получает 720k USDC. Владельцы IP2 в целом получают 900k USDC, которые распределяются между B и C. C имеет 80% Токенов Роялти IP2, поэтому получает 900k USDC * 80% = 720k.

<br />

## Конфигурации цепочки производных активов

![](https://files.readme.io/79bd27f-image.png)

Цепочка производных активов может принимать различные конфигурации.

Каждый IP-актив ограничен максимальным процентом роялти в 100%. При попытке создать лицензию, которая зарезервирует более 100% токенов роялти для предков, транзакция будет отклонена, так как это не имеет смысла.