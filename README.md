# SI_lab2_236009

## Цикломатска комплексност

Цикломатската комплексност на дадениот код се пресметува преку формулата `E - V + 2`, каде што `E` е бројот на ребра, а `V` е бројот на јазли. Во добиениот Control Flow Graph има 21 јазол и 28 ребра:

```
28 - 21 + 2 = 9
```

Исто така може да се пресмета и со формулата `P + 1`, каде `P` е бројот на одлучувачки јазли:

```
P = 8 → P + 1 = 9
```

Одлучувачки јазли се на линиите: 52, 58, 60, 64, 68, 76, 79 и 81

---

## Control Flow Graph (CFG)

![d drawio](https://github.com/user-attachments/assets/475922dd-53db-47c7-9d30-02fed3bef649)


---

## Every Statement – тест случаи

### Тест 1
```java
allItems = null  
cardNumber = "1234567890123456"
```
Минува низ 52 и 53, фрла `allItems can’t be null!`

### Тест 2
```java
allItems = [Item("", 1, 100, 0)]  
cardNumber = "1234567890123456"
```
Минува низ 52–61, фрла `Invalid item!`

### Тест 3
```java
allItems = [Item("Laptop", 1, 500, 0.1)]  
cardNumber = "12345678901234561111"
```
Минува низ 64–70 и 87, фрла `Invalid card number`

### Тест 4
```java
allItems = [Item("Book", 1, 100, 0)]  
cardNumber = "1234abcd5678efgh"
```
Минува низ 72 и 76–82, фрла `Invalid character in card number!`

### Тест 5
```java
allItems = [Item("Pen", 2, 50, 0)]  
cardNumber = "1234567890123456"
```
Сè е валидно → се враќа сумата (влегува во `return sum`)

---

## Multiple Condition – тест случаи

Тестиран е овој услов:

```java
if (item.getPrice() > 300 || item.getDiscount() > 0 || item.getQuantity() > 10)
```
објаснување: P - price, D - discount, Q - quantity.

#### Тест 1 – Само цената задоволува, таа е над 300
```java
Item("A", 1, 400, 0)
```
`P=true, D=false, Q=false` → влегува во if

#### Тест 2 – Само попустот е над 0, задоволува
```java
Item("B", 1, 100, 0.1)
```
`P=false, D=true, Q=false` → влегува во if

#### Тест 3 – Само количината задоволува, таа е над 10
```java
Item("C", 11, 100, 0)
```
`P=false, D=false, Q=true` → влегува во if

#### Тест 4 – Сите услови неточни (false)
```java
Item("D", 5, 100, 0)
```
`P=false, D=false, Q=false` → не влегува во if

---

## Објаснување на unit тестовите

### Every Statement
Напишани се 5 тест случаи кои заедно ја покриваат секоја линија во методот `checkCart`.  
Се користат `assertThrows` за проверка на исклучоци и `assertEquals` за проверка на вредности.
Секој тест активира различна патека низ кодот.

---

### Multiple Condition
Напишани се 4 тест случаи за условот со `||`.  
Секој тест активира поинаква комбинација од логичките под-услови.  
Се користи `assertEquals` за проверка на резултатите.

---

Тестовите се извршени со JUnit 5 и Gradle. Сите поминаа успешно.
