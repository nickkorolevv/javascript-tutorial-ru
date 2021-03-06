importance: 5

---

# Что выведет после setInterval?

В коде ниже запускается `setInterval` каждые 10 мс, и через 50 мс запланирована его отмена.

После этого запущена тяжёлая функция `f`, выполнение которой (мы точно знаем) потребует более 100 мс.

Сработает ли `setInterval`, как и когда?

Варианты:

1. Да, несколько раз, *в процессе* выполнения `f`.
2. Да, несколько раз, *сразу после* выполнения `f`.
3. Да, один раз, *сразу после* выполнения `f`.
4. Нет, не сработает.
5. Может быть по-разному, как повезёт.

Что выведет `alert` в строке `(*)`?

```js
var i;
var timer = setInterval(function() { // планируем setInterval каждые 10 мс
  i++;
}, 10);

setTimeout(function() { // через 50 мс - отмена setInterval
  clearInterval(timer);
*!*
  alert( i ); // (*)
*/!*
}, 50);

// и запускаем тяжёлую функцию
function f() {
  // точное время выполнения не играет роли
  // здесь оно заведомо больше 100 мс
  for (i = 0; i < 1e8; i++) f[i % 2] = i;
}

f();
```

