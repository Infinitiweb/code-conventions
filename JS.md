**в процессе ...**


* Наиболее разумный подход к JavaScript* от *AirBnB, GitHub, & Google
* Зачем нам это ¯\\_(ツ)_/¯ ?
* Весь код в любой кодовой базе должен выглядеть так, как будто его набрал один человек, независимо от того, сколько человек внесло свой вклад.

*Научитесь программировать как Google* и мы тебя потеряем 

## <a name='TOC'>Оглавление</a>
  1. [Имена файлов](#name-files);
  1. [Комментарии](#comments);
  1. [Пробелы](#whitespace);
  1. [Запятые](#commas);
  1. [Точки с запятой](#semicolons);
  1. [Типы](#types);
  1. [Объекты](#objects);
  
  
## <a name='name-files'>Имена файлов</a>
* Все имена файлов/папок должны быть строчными и могут содержать подчеркивания ( _) или тире ( -)
* Прификсы в файлах  `geo-ip.service.js`
* Следуйте соглашению, которое использует ваш проект.
* Расширение имени файла должно быть `.js`.

**[[⬆]](#Оглавление)**


## <a name='comments'>Комментарии</a>

* Однострочные комментарии на линию выше кода
* Комментарии в несколько строк тоже приветствуются
* Комментарии в конце строки запрещены!
* Стиль JSDoc хорош, но в нем нужно долго разбираться
* Описания сткруктуры обьекта в стиле JSDoc разрешены
 ```js
/**
 * @typedef {Object} DetectCtxParams
 * @property {String} userAgent
 */
```
* Если у вас есть временное решение (костыли), вы должны это пометить в коде через `// @todo hack`  

**[[⬆]](#Оглавление)**


## <a name='whitespace'>Пробелы</a>
- Используйте программную табуляцию (ее поддерживают все современные редакторы кода и IDE) из двух пробелов.

  ```javascript
  // плохо
  function() {
  ∙∙∙∙let name;
  }

  // плохо
  function() {
  ∙let name;
  }

  // хорошо
  function() {
  ∙∙let name;
  }
  ```
- Устанавливайте один пробел перед открывающей скобкой.

  ```javascript
  // плохо
  function test(){
    console.log('test');
  }

  // хорошо
  function test() {
    console.log('test');
  }

  // плохо
  dog.set('attr',{
    age: '1 year',
    breed: 'Bernese Mountain Dog'
  });

  // хорошо
  dog.set('attr', {
    age: '1 year',
    breed: 'Bernese Mountain Dog'
  });
  ```
- Оставляйте новую строку в конце файла.

  ```javascript
  // плохо
  (function(global) {
    // ...код...
  })(this);
  ```

  ```javascript
  // хорошо
  (function(global) {
    // ...код...
  })(this);

  ```

**[[⬆]](#Оглавление)**

## <a name='commas'>Запятые</a>

- Запятые в начале строки: **Нет.**

  ```javascript
  // плохо
  let once
    , upon
    , aTime;

  // хорошо
  let once,
      upon,
      aTime;

  // плохо
  let hero = {
      firstName: 'Bob'
    , lastName: 'Parr'
    , heroName: 'Mr. Incredible'
    , superPower: 'strength'
  };

  // хорошо
  let hero = {
    firstName: 'Bob',
    lastName: 'Parr',
    heroName: 'Mr. Incredible',
    superPower: 'strength'
  };
  ```


## <a name='semicolons'>Точки с запятой</a>

  ```javascript
  // плохо
  (function() {
    var name = 'Skywalker'
    return name
  })()

  // хорошо
  (function() {
    var name = 'Skywalker';
    return name;
  })();

  // хорошо
  ;(function() {
    var name = 'Skywalker';
    return name;
  })();
  ```

**[[⬆]](#Оглавление)**


## <a name='objects'>Объекты</a>
- Для создания объекта используйте фигурные скобки. Не создавайте объекты через конструктор `new Object`.

```js
// плохо
let item = new Object();

// хорошо
let item = {};
```

Используйте сокращённую запись метода объекта. eslint: [object-shorthand](https://eslint.org/docs/rules/object-shorthand.html)
```js
// плохо
const atom = {
  value: 1,

  addValue: function (value) {
    return atom.value + value;
  },
};

// хорошо
const atom = {
  value: 1,

  addValue(value) {
    return atom.value + value;
  },
};
```
Только недопустимые идентификаторы помещаются в кавычки. eslint: [quote-props](https://eslint.org/docs/rules/quote-props.html)
```js
// плохо
const bad = {
  'foo': 3,
  'bar': 4,
  'data-blah': 5,
};

// хорошо
const good = {
  foo: 3,
  bar: 4,
  'data-blah': 5,
};
```

* Используйте оператор расширения `...` вместо Object.assign для поверхностного копирования объектов. 
* Используйте синтаксис оставшихся свойств, чтобы получить новый объект с некоторыми опущенными свойствами.

```js
// очень плохо
const original = { a: 1, b: 2 };
// эта переменная изменяет      `original` ಠ_ಠ
const copy = Object.assign(original, { c: 3 }); 
// если сделать так
delete copy.a; 

// плохо (но можно использовать)
const original = { a: 1, b: 2 };
const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1, b: 2, c: 3 }

// хорошо
const original = { a: 1, b: 2 };
const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }

const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
```

**[[⬆]](#Оглавление)**

