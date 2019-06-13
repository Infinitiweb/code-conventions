** документ в процессе наполнения... но некоторые правила уже можно и нужно использовать***


*Наиболее разумный подход к JavaScript* от *AirBnB, GitHub, & Google*

Зачем нам это ¯\\_(ツ)_/¯ ?

>Весь код в любой кодовой базе должен выглядеть так, как будто его набрал один человек, 
независимо от того, сколько человек внесло свой вклад.

*Научитесь программировать как Google*

## <a name='TOC'>Оглавление</a>
  1. [Имена файлов](#name-files);
  1. [Комментарии](#comments);  
  1. [Типы](#types);
  1. [Пробелы](#whitespace);
  1. [Запятые](#commas);
  1. [Точки с запятой](#semicolons);
  1. [Объявление переменных](#var-references)
  1. [Объекты](#objects);
  1. [Деструктуризация](#destructuring)
  1. [Соглашение об именовании](#con-names)
  
  
## <a name='name-files'>Имена файлов</a>
* Все имена файлов/папок должны быть строчными и могут содержать подчеркивания ( _) или тире ( -)
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
## <a name='types'>Типы</a>
* **Простые типы:** Когда вы взаимодействуете с простым типом, вы напрямую работаете с его значением.
   * string
   * number
   * boolean
   * null
   * undefined
   * symbol

    ```javascript
    const foo = 1;
    let bar = foo;
    
    bar = 9;
    
    console.log(foo, bar); // => 1, 9
    ```
   * Символы не могут быть полностью заполифиллены, поэтому они не должны использоваться, если разработка ведётся для браузеров/сред, которые не поддерживают их нативно.

* **Сложные типы:** Когда вы взаимодействуете со сложным типом, вы работаете со ссылкой на его значение.
  * object
  * array
  * function
  ```javascript
  const foo = [1, 2];
  const bar = foo;
  
  bar[0] = 9;
  
  console.log(foo[0], bar[0]); // => 9, 9
  ```


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
## <a name='var-references'>Объявление переменных</a>
 Используйте `const` для объявления переменных; избегайте `var`. eslint: [prefer-const](https://eslint.org/docs/rules/prefer-const.html), [no-const-assign](https://eslint.org/docs/rules/no-const-assign.html)

> Почему? Это гарантирует, что вы не сможете переопределять значения, т.к. это может привести к ошибкам и к усложнению понимания кода.
 
 ```javascript
// плохо
var a = 1;
var b = 2;

// хорошо
const a = 1;
const b = 2;
```

Если вам необходимо переопределять значения, то используйте `let` вместо `var`. eslint: [no-var](https://eslint.org/docs/rules/no-var.html)

> Почему? Область видимости `let` — блок, у `var` — функция.

```javascript
// плохо
var count = 1;
if (true) {
  count += 1;
}

// хорошо, используйте let.
let count = 1;
if (true) {
  count += 1;
}
```
Помните, что у `let` и `const` блочная область видимости.
```javascript
// const и let существуют только в том блоке, в котором они определены.
{
  let a = 1;
  const b = 1;
}
console.log(a); // ReferenceError
console.log(b); // ReferenceError
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
// эта переменная изменяет      `original`
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

## <a name='destructuring'>Деструктуризация</a>
При обращении к нескольким свойствам объекта используйте деструктуризацию объекта. eslint: [prefer-destructuring](https://eslint.org/docs/rules/prefer-destructuring)
> Почему? Деструктуризация избавляет вас от создания временных переменных для этих свойств.

```javascript
    // плохо
    function getFullName(user) {
      const firstName = user.firstName;
      const lastName = user.lastName;

      return `${firstName} ${lastName}`;
    }

    // хорошо
    function getFullName(user) {
      const { firstName, lastName } = user;
      return `${firstName} ${lastName}`;
    }

    // отлично
    function getFullName({ firstName, lastName }) {
      return `${firstName} ${lastName}`;
    }
```
Используйте деструктуризацию массивов. eslint: [prefer-destructuring](https://eslint.org/docs/rules/prefer-destructuring)

```javascript
const arr = [1, 2, 3, 4];

// плохо
const first = arr[0];
const second = arr[1];

// хорошо
const [first, second] = arr;
```
Используйте деструктуризацию объекта для множества возвращаемых значений, но не делайте тоже самое с массивами.
> Почему? Вы сможете добавить новые свойства через некоторое время или изменить порядок без последствий.


```javascript
    // плохо
    function processInput(input) {
      // затем происходит чудо
      return [left, right, top, bottom];
    }

    // при вызове нужно подумать о порядке возвращаемых данных
    const [left, __, top] = processInput(input);

    // хорошо
    function processInput(input) {
      // затем происходит чудо
      return { left, right, top, bottom };
    }

    // при вызове выбираем только необходимые данные
    const { left, top } = processInput(input);
```

С промимаси + `await` можно использовать деструктуризацию в одном блоке. 
```js
const [result1, result2, result3] = await Promise.all([
  Promise1,
  Promise2,
  Promise3
]);
```

**[[⬆]](#Оглавление)**

## <a name='con-names'>Соглашение об именовании</a>
Избегайте названий из одной буквы. Имя должно быть наглядным. eslint: [id-length](https://eslint.org/docs/rules/id-length)
```javascript
// плохо
function q() {
  // ...
}

// хорошо
function query() {
  // ...
}
```
Используйте camelCase для именования объектов, функций и экземпляров. eslint: [camelcase](https://eslint.org/docs/rules/camelcase.html)
```javascript
// плохо
const OBJEcttsssss = {};
const this_is_my_object = {};
function c() {}

// хорошо
const thisIsMyObject = {};
function thisIsMyFunction() {}
```

Используйте PascalCase только для именования конструкторов и классов. eslint: [new-cap](https://eslint.org/docs/rules/new-cap.html)
```javascript
// плохо
function user(options) {
  this.name = options.name;
}

const bad = new user({
  name: 'nope',
});

// хорошо
class User {
  constructor(options) {
    this.name = options.name;
  }
}

const good = new User({
  name: 'yup',
});
```

Не используйте `_` в начале или в конце названий. eslint: [no-underscore-dangle](https://eslint.org/docs/rules/no-underscore-dangle.html)

> Почему? JavaScript не имеет концепции приватности свойств или методов. 
Хотя подчёркивание в начале имени является распространённым соглашением, которое показывает «приватность»,
 фактически эти свойства являются такими же доступными, как и часть вашего публичного API.
Это соглашение может привести к тому, что разработчики будут ошибочно думать, 
что изменения не приведут к поломке или что тесты не нужны.

> Итог: если вы хотите, чтобы что-то было «приватным», то оно не должно быть доступно извне.

```javascript
// плохо
this.__firstName__ = 'Panda';
this.firstName_ = 'Panda';
this._firstName = 'Panda';

// хорошо
this.firstName = 'Panda';

// хорошо, в средах, где поддерживается WeakMaps
// смотрите https://kangax.github.io/compat-table/es6/#test-WeakMap
const firstNames = new WeakMap();
firstNames.set(this, 'Panda');
```

Исключение только для приватных свойств класса
```javascript
export default class User { 
  #_id;
}
```

Не сохраняйте ссылку на this. Используйте стрелочные функции или метод [bind()](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Function/bind).
```javascript
// плохо
function foo() {
  const self = this;
  return function () {
    console.log(self);
  };
}

// плохо
function foo() {
  const that = this;
  return function () {
    console.log(that);
  };
}

// хорошо
function foo() {
  return () => {
    console.log(this);
  };
}
```

<!-- @todo подумать ... 

Название файла точно должно совпадать с именем его экспорта по умолчанию.
```javascript
// содержание файла 1
class CheckBox {
  // ...
}
export default CheckBox;

// содержание файла 2
export default function fortyTwo() { return 42; }

// содержание файла 3
export default function insideDirectory() {}

// в других файлах
// плохо
import CheckBox from './checkBox'; // PascalCase import/export, camelCase filename
import FortyTwo from './FortyTwo'; // PascalCase import/filename, camelCase export
import InsideDirectory from './InsideDirectory'; // PascalCase import/filename, camelCase export

// плохо
import CheckBox from './check_box'; // PascalCase import/export, snake_case filename
import forty_two from './forty_two'; // snake_case import/filename, camelCase export
import inside_directory from './inside_directory'; // snake_case import, camelCase export
import index from './inside_directory/index'; // requiring the index file explicitly
import insideDirectory from './insideDirectory/index'; // requiring the index file explicitly

// хорошо
import CheckBox from './CheckBox'; // PascalCase export/import/filename
import fortyTwo from './fortyTwo'; // camelCase export/import/filename
import insideDirectory from './insideDirectory'; // camelCase export/import/directory name/implicit "index"
// ^ поддерживает оба варианта: insideDirectory.js и insideDirectory/index.js
```
-->

**[[⬆]](#Оглавление)**