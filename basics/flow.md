# Управляющие структуры

## Ветвление

### if

В отличие от PHP нет скобок вокруг условий.

```go
if a == 1 {
  // do something
}
```

Перед условием, возможно добавление так называемого предусловия (в англ. документации - short statement,
лучшего перевода к сожалению не нашел). В следующем примере сначала будет
вызвана функция `foo` и ее значение будет присвоено переменной `t`. Далее будет выполнено
сравнение `t == 1`. Обратие внимание, что в данном случае областью видимости `t` будет
блок `if else`

```go
if t := foo(); t == 1 {
  // do something
} else {
  // do something else
}
```

В PHP иногда меняют значение и переменную в условии, чтобы обезопасить себя
на случай опечатки `=` вместо `==`

```php
if (1 == $a) {
  ...
}
```

В Go так делать не нужно, если вы случайно напишите так, то программа просто не
скомпилируется.

```go
if 1 = a {
  ...
}
```

### switch

Опять не нужны скобки после `switch` и не нужен `break`!

```php
// php
switch ($i) {
    case 0:
      zero();
      break;
    case 1:
      one();
      break;
    case 2:
      two();
      break;
    default:
      foo();
}
```

```go
// go
switch i {
  case 0:
    zero()
  case 1:
    one()
  case 2:
    two()
  default:
    foo()
}
```

Для замены ряда if-else-if-else "лесенок", можно возпользоваться `switch`:
```go
// go
switch i {
   case i < 0:
       // less then zero
   case 0 >= i && i < 10:
       // first ten
   case i >= 10:
       // more then ten
}
```

Кроме этого в `case` можно передавать список, разделенный запятой:
```go
// go
switch c {
    case '#', '@', '%':
        // do something
}
```

## Циклы

В Go всего одно ключевое слово для циклов `for`.

### For

PHP версия for идентична версии в go, только без скобок:

```php
// php
for ($i = 0; $i <= 10; $i++) {
  foo();
}
```

```go
// go
for i := 0; i <= 10; i++ {
    foo()
}
```

### while

```php
// php
while ($x < 1) {
  foo();
}
```

```go
// go
for x < 1 {
    foo()
}
```
Кстати вместо часто используемого для
бесконечных циклов в php `while (true) { ... }` можно использовать
просто `for { ... }`

### do while

```php
// php
do {
  $x = foo();
} while ($x < 2)
```

```go
// go
for {
  if x := foo(); x < 2 {
    break
  }  
}
```

### foreach

Используем ключевое слово `range`

```php
// php
foreach ($array as $key => $value) {
  foo($key, $value)
}
```

```go
// go
for k, v := range arr {
  foo(k, v)
}
```
