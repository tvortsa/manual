# Fetch data

## Concepts

- Как браузеры, Deno реализует API web стандартов такие как
  [fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API).
- Deno безопасен по-умолчанию, это означает, что для доступа к сети
 должно быть предоставлено явное разрешение.
- Смю также: модель Deno [разрешений](../getting_started/permissions.md).

## Обзор

При создании любого типа веб-приложений разработчикам обычно требуется получать
данные откуда-нибудь в Интернете. В Deno это работает не иначе чем в любом другом
приложении JavaScript, просто вызовите метод `fetch ()`. 
Больше информации о fetch читайте в
[MDN documentation](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API).

Исключение с Deno возникает при запуске сценария, который выполняет вызов через
Интернет. Deno по умолчанию безопасен, что означает, что доступ к IO (вводу/выводу)
запрещен. Чтобы вызывать через Интернет, Deno нужно прямо сказать, что это можно делать.
Это достигается добавлением флага `--allow-net` к строке` node run`.

## Пример

**Command:** `deno run --allow-net fetch.ts`

```js
/**
 * Output: JSON Data
 */
const jsonResponse = await fetch("https://api.github.com/users/denoland");
const jsonData = await jsonResponse.json();
console.log(jsonData);

/**
 * Output: HTML Data
 */
const textResponse = await fetch("https://deno.land/");
const textData = await textResponse.text();
console.log(textData);

/**
 * Output: Error Message
 */
try {
  await fetch("https://does.not.exist/");
} catch (error) {
  console.log(error);
}
```
