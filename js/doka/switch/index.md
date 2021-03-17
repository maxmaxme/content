---
title: "switch"
name: switch
author: nlopin
contributors:
  - furtivite
summary:
  - условие
  - условный переход
  - свитч
  - выбор
---

## Кратко

Управляющая конструкция `switch` позволяет выполнять различные блоки кода, в зависимости от значения переменной.

Похож на `if...else`, но решает более узкую задачу.

## Как пишется

```js
switch (имя_переменной_значение_которой_сравниваем) {
  case значение:
    // код
    break
}
```

В круглых скобках указывается переменная, значение которой сравнивается. В фигурных скобках с помощью ключевого слова `case` указываются возможные значения и код, который нужно выполнить.

Пример приветствия пользователя в зависимости от статуса:

```js
switch (membershipStatus) {
  case "vip":
    // выполнится, если в переменной memberhipStatus хранится строка "vip"
    console.log("Приветствуем вас, ваше великолепие!")
    console.log("рады вас видеть!")
    break
  case "diamond":
    console.log("Здравствуйте, бриллиантовый клиент!")
    break
  case "gold":
    console.log("Привет, золотой мой!")
    break
  default:
    // выполнится, если ни один другой случай не сработал
    console.log("Прив")
    break
}
```

## Как понять

В программировании часто встречается задача выполнения разного кода в зависимости от какого-либо условия. Обычно, такие задачи решают с помощью конструкции [if...else](/js/doka/if-else).

Среди этих задач есть особый подтип — когда нужно посмотреть на значение переменной и выполнить разный код, в зависимости от этого значения. Например, применить разную скидку для клиентов разного статуса — самым любимым клиентам дать скидку 25%, с картой лояльности — 10%, а обычным покупателям не дать ничего.

Такую задачу тоже можно решить с помощью `if..else`:

```js
let discount
if (memberStatus === "vip") {
  discount = 0.25
} else if (memberStatus === "diamond") {
  discount = 0.2
} else if (memberStatus === "gold" || memberStatus === "silver") {
  // скидка 10% пользователям статуса золотой и серебряный
  discount = 0.1
} else {
  discount = 0
}
```

Код выше работает, но выглядит избыточно — в нем очень много сравнений с использованием `memberStatus`. Конструкция `switch` решает такую задачу меньшим объёмом кода:

```js
let discount
switch (memberStatus) {
  case "vip":
    discount = 0.25
    break
  case "diamond":
    discount = 0.2
    break
  case "gold":
  case "silver":
    // можно написать несколько кейсов и связать с одним блоком
    discount = 0.1
    break
  default:
    discount = 0
    break
}
```

В круглых скобках указана переменная, значение которой нужно сравнивать с различными возможными значениями — _кейсами_. Порядок обычно не имеет значения.

Внутри кейса пишется список команд, которые нужно выполнить. Список команд завершается оператором `break`.

Существует необязательный кейс `default`, который срабатывает, если ни одно значение не подошло.

### Что будет, если не поставить `break`?

Если вы забыли поставить `break`, то будут выполнены все команды, начиная со сработавшего кейса и до тех пор пока либо не встретится `break`, либо не закончится `switch`.

Сравните:

![блок кода, который выполнится с break](images/with-break.png)

![блок кода, который выполнится без break](images/without-break.png)

Выполняется весь код от текущего `case` до следующего `break`, даже если он вне текущего кейса.

В коде появился баг — значение для бриллиантового уровня будет установлено в `0.1` вместо `0.2`.