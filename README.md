# Касьянс посынка

Идея: как пасьянс косынка, но на джеке и хуже.

Что нам нравится:
* Перестановка массива [0..51]
```
let rnd = Random.new(17);
let i = 51;
while (i > -1) {
	let j = rnd.randRange(0, i);
	let tmp = ints[i];
	let ints[i] = ints[j];
	let ints[j] = tmp;
	let i = i - 1;
}
```
* Генерация карт из перестановки массива [0..51]

Game.jack:
```
while (i < 52) {
    let suit = ints[i] / 13;
    let value = ints[i] - (suit * 13) + 1;
	let cards[i] = Card.new(value, suit, false, false);
	let i = i + 1;
}
```
* Реализовано перемещение множества карт (и куча проверок)

![](/img/Screenshot_1.png)
![](/img/Screenshot_2.png)
* Вся графика (и её эпичные баги)

![](/img/Screenshot_3.png)
![](/img/Screenshot_10.png)

![](/img/Screenshot_4.png)
![](/img/Screenshot_9.png)
![](/img/Screenshot_6.png)
![](/img/Screenshot_5.png)

* Настоящий стек на связном списке для стопок карт (Stack.jack)
* Много диспоузов

Game.jack:
```
method void dispose() {
    var Pile tmpPile;
    var int i;
    
    let i = 0;
    while (i < 4) {
        let tmpPile = foundations[i];
        do tmpPile.dispose();
        let i = i + 1;
    }
    
    let i = 0;
    while (i < 7) {
        let tmpPile = tableau[i];
        do tmpPile.dispose();
        let i = i + 1;
    }
    
    let i = 0;
    while (i < 2) {
        let tmpPile = stock[i];
        do tmpPile.dispose();
        let i = i + 1;
    }
    
    do foundations.dispose();
    do tableau.dispose();
    do stock.dispose();
    do Memory.deAlloc(this);
    return;
}
```

* Гордимся тем, что из нашей игры можно выйти по esc, в отличие от созвона по разработке игры.
![](/img/no-escape.png)