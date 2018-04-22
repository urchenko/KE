CL2 (Competent)
Qualification Requirements Overview: Understanding framework architecture.
Implementing advanced concepts using core library and ajax manipulations.

## Object - Object
Улучшения в описании свойств:

Запись name: name можно заменить на просто name
Если имя свойства находится в переменной или задано выражением expr, то его можно указать в квадратных скобках [expr].
Свойства-функции можно оформить как методы: "prop: function() {}" → "prop() {}".
В методах работает обращение к свойствам прототипа через super.parentProperty.

Для работы с прототипом:

Object.setPrototypeOf(obj, proto) – метод для установки прототипа.
obj.__proto__ – ссылка на прототип.
Дополнительно:

Метод Object.assign(target, src1, src2...) – копирует свойства из всех аргументов в первый объект.
Метод Object.is(value1, value2) проверяет два значения на равенство.
В отличие от === считает +0 и -0 разными числами. А также считает, что NaN равно самому себе.

## Regular Expressions
Регулярные выражения – мощный способ поиска и замены для строк.

Регулярное выражение состоит из шаблона и необязательных флагов g, i и m.
Поиск по регулярному выражению без флагов и спец. символов,
 которые мы изучим далее – это то же самое, что и обычный поиск подстроки в строке.
 Но флаги и спец. символы, как мы увидим далее, могут сделать его гораздо мощнее.
Метод строки str.search(regexp) возвращает индекс, на котором найдено совпадение.

Методы становятся гораздо понятнее, если разбить их использование по задачам, которые нужны в реальной жизни.

Для поиска только одного совпадения:
Найти позицию первого совпадения – str.search(reg).
Найти само совпадение – str.match(reg).
Проверить, есть ли хоть одно совпадение – regexp.test(str) или str.search(reg) != -1.
Найти совпадение с нужной позиции – regexp.exec(str), начальную позицию поиска задать в regexp.lastIndex.
Для поиска всех совпадений:
Найти массив совпадений – str.match(reg), с флагом g.
Получить все совпадения, с подробной информацией о каждом – regexp.exec(str) с флагом g, в цикле.
Для поиска-и-замены: : - Замена на другую строку или результат функции -- `str.replace(reg, str|func)`
Для разбивки строки на части:
str.split(str|reg)
Зная эти методы, мы уже можем использовать регулярные выражения.

Конечно, для этого желательно хорошо понимать их синтаксис и возможности, так что переходим к ним дальше.

Мы рассмотрели классы для поиска типов символов:

\d – цифры.
\D – не-цифры.
\s – пробельные символы, переводы строки.
\S – всё, кроме \s.
\w – латинница, цифры, подчёркивание '_'.
\W – всё, кроме \w.
'.' – точка обозначает любой символ, кроме перевода строки.
Если хочется поискать именно сочетание "\d" или символ «точка», то его экранируют обратным слэшем, вот так: \.

Заметим, что регулярное выражение может также содержать перевод строки \n, табуляцию \t 
и прочие спецсимволы для строк. Конфликта с классами не происходит, так как для них зарезервированы другие буквы.

Квантификаторы имеют два режима работы:

Жадный
Режим по умолчанию – движок регулярных выражений повторяет его по-максимуму. Когда повторять уже нельзя,
 например нет больше цифр для \d+, он продолжает поиск с оставшейся части текста.
 Если совпадение найти не удалось – отступает обратно, уменьшая количество повторений.
Ленивый
При указании после квантификатора символа ? он работает в ленивом режиме.
 То есть, он перед каждым повторением проверяет совпадение оставшейся части шаблона на текущей позиции.
Как мы видели в примере выше, ленивый режим – не панацея от «слишком жадного» забора символов.
 Альтернатива – более аккуратно настроенный «жадный», с исключением символов.
 Как мы увидим далее, можно исключать не только символы, но и целые подшаблоны.

 В мультистрочном режиме:

Символ ^ означает начало строки.
Символ $ означает конец строки.
Оба символа являются проверками, они не добавляют ничего к результату. Про них также говорят, что «они имеют нулевую длину».


## Dependancy injection (common, AMD, namespase)
In software engineering, **dependency injection** is a technique whereby one object supplies the dependencies of another object. A dependency is an object that can be used (a service). An injection is the passing of a dependency to a dependent object (a client) that would use it. The service is made part of the client's state.[1] Passing the service to the client, rather than allowing a client to build or find the service, is the fundamental requirement of the pattern.

* AMD – одна из самых древних систем организации модулей, требует лишь наличия клиентской библиотеки, к примеру, require.js, но поддерживается и серверными средствами.
* CommonJS – система модулей, встроенная в сервер Node.JS. Требует поддержки на клиентской и серверной стороне

AMD
Асинхронное определение модуля (англ. asynchronous module definition, AMD) — это подход к разработке на Javascript, при котором модули и их зависимости могут быть загружены асинхронно. Асинхронная загрузка модулей позволяет улучшить скорость загрузки веб-страницы в целом, так как модули загружаются одновременно с остальным контентом сайта.

Кроме того, AMD может быть использован во время разработки для разбиения JavaScript-кода по разным файлам.

Похожие механизмы имеются и в других языках программирования, например Java, где для определения модулей используются ключевые слова import, package и Class.

Для промышленной эксплуатации JavaScript-файлы рекомендуется объединить и сжать в один маленький файл.

CommonJS
 is a project with the goal of specifying an ecosystem for JavaScript outside the browser
  (for example, on the server or for native desktop applications).

Why Is AMD A Better Choice For Writing Modular JavaScript?
Provides a clear proposal for how to approach defining flexible modules.
Significantly cleaner than the present global namespace and script tag solutions many of us rely on. There's a clean way to declare stand-alone modules and dependencies they may have.
Module definitions are encapsulated, helping us to avoid pollution of the global namespace.
Works better than some alternative solutions (eg. CommonJS, which we'll be looking at shortly). Doesn't have issues with cross-domain, local or debugging and doesn't have a reliance on server-side tools to be used. Most AMD loaders support loading modules in the browser without a build process.
Provides a 'transport' approach for including multiple modules in a single file. Other approaches like CommonJS have yet to agree on a transport format.
It's possible to lazy load scripts if this is needed

## Inheritance
Объекты в языке JavaScript обладают множеством «собственных свойств» 
и могут также наследовать множество свойств от объекта-прототипа.

``` javascript
    var ­o­=­{}­­­­­­­­­//­o­на­сле­ду­ет­ме­то­ды­объ­ек­та­Object.prototype
    o.x­=­1;­­­­­­­­­­­­­­//­и­об­ла­да­ет­соб­ст­вен­ным­свой­ст­вом­x.
    var­ p­=­inherit(o);­­­//­p­на­сле­ду­ет­свой­ст­ва­объ­ек­тов­o­и­Object.prototype
    p.y­=­2;­­­­­­­­­­­­­­//­и­об­ла­да­ет­соб­ст­вен­ным­свой­ст­вом­y.
    var­ q­=­inherit(p);­­­//­q­на­сле­ду­ет­свой­ст­ва­объ­ек­тов­p,­o­и­Object.prototype
    q.z­=­3;­­­­­­­­­­­­­­//­и­об­ла­да­ет­соб­ст­вен­ным­свой­ст­вом­z.
    var ­s­=­q.toString();­//­toString­на­сле­ду­ет­ся­от­Object.prototype
    q.x­+­q.y­­­­­­­­­­­­­//­=>­3:­x­и­y­на­сле­ду­ют­ся­от­o­и­p
```
``` javascript
var­ unitcircle­=­{­r:1­};­­­­//­Объ­ект,­от­ко­то­ро­го­на­сле­ду­ет­ся­свой­ст­во
var ­c­=­inherit(unitcircle);­//­c­на­сле­ду­ет­свой­ст­во­r
c.x­=­1;­c.y­=­1;­­­­­­­­­­­­//­c­оп­ре­де­ля­ет­два­соб­ст­вен­ных­свой­ст­ва
c.r­=­2;­­­­­­­­­­­­­­­­­­­­­//­c­пе­ре­оп­ре­де­ля­ет­унас­ле­до­ван­ное­свой­ст­во
unitcircle.r;­­­­­­­­­­­­­­­­//­=>­1:­объ­ект-про­то­тип­не­из­ме­нил­ся
```
## Currying

``` javascript
function bind(func, context) {
  return function() { // (*)
    return func.apply(context, arguments);
  };
}
```

В результате вызова bind(func, context) мы получаем «функцию-обёртку», которая прозрачно передаёт вызов в func, с теми же аргументами, но фиксированным контекстом context.

До этого мы говорили о привязке контекста. Теперь пойдём на шаг дальше. Привязывать можно не только контекст, но и аргументы. Используется это реже, но бывает полезно.

**Карринг** (currying) или каррирование – термин функционального программирования, который означает создание новой функции путём фиксирования аргументов существующей.

Вызов bind также позволяет фиксировать первые аргументы функции («каррировать» её), и таким образом из общей функции получить её «частные» варианты – чтобы использовать их многократно без повтора одних и тех же аргументов каждый раз.

## ES6: Classes

``` javascript
class Point {
    constructor(x, y) {
        this.x = x;
        this.y = y;
    }
    toString() {
        return '(' + this.x + ', ' + this.y + ')';
    }
}

class ColorPoint extends Point {
    constructor(x, y, color) {
        super(x, y);
        this.color = color;
    }
    toString() {
        return super.toString() + ' in ' + this.color;
    }
}

let cp = new ColorPoint(25, 8, 'green');
cp.toString(); // '(25, 8) in green'

console.log(cp instanceof ColorPoint); // true
console.log(cp instanceof Point); // true
```

* Class declarations are not hoisted

Новая конструкция **class** – удобный «синтаксический сахар» для задания конструктора вместе с прототипом.

**статические свойства**
Класс, как и функция, является объектом. Статические свойства класса User – это свойства непосредственно User, то есть доступные из него «через точку».

Для их объявления используется ключевое слово static.

``` javascript
'use strict';

class User {
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }

  static createGuest() {
    return new User("Гость", "Сайта");
  }
};

let user = User.createGuest();

alert( user.firstName ); // Гость

alert( User.createGuest ); // createGuest ... (функция)
```

Как правило, они используются для операций, не требующих наличия объекта, например – для фабричных, как в примере выше, то есть как альтернативные варианты конструктора. Или же, можно добавить метод User.compare, который будет сравнивать двух пользователей для целей сортировки.

* Вызвать конструктор родителя можно только изнутри конструктора потомка. В частности, super() нельзя вызвать из произвольного метода.
* В конструкторе потомка мы обязаны вызвать super() до обращения к this. До вызова super не существует this, так как по спецификации в этом случае именно super инициализирует this
* При наследовании вызов конструктора родителя осуществляется через super(...args), вызов родительских методов – через super.method(...args)

## ES6: Destructuring assignment

Деструктуризация (destructuring assignment) – это особый синтаксис присваивания, при котором можно присвоить массив или объект сразу нескольким переменным, разбив его на части.

``` javascript
'use strict';

let [firstName, lastName] = ["Илья", "Кантор"];

alert(firstName); // Илья
alert(lastName);  // Кантор
```

Если мы хотим получить и последующие значения массива, но не уверены в их числе – можно добавить ещё один параметр, который получит «всё остальное», при помощи оператора "..." («spread», троеточие):

``` javascript
'use strict';

let [firstName, lastName, ...rest] = "Юлий Цезарь Император Рима".split(" ");

alert(firstName); // Юлий
alert(lastName);  // Цезарь
alert(rest);      // Император,Рима (массив из 2х элементов)
```

Деструктуризацию можно использовать и с объектами. При этом мы указываем, какие свойства в какие переменные должны «идти».

Базовый синтаксис:

``` javascript
let {var1, var2} = {var1: …, var2: …};
```

Деструктуризация позволяет разбивать объект или массив на переменные при присвоении.

Синтаксис:

``` javascript
let {prop : varName = default, ...} = object
```

Здесь двоеточие : задаёт отображение свойства prop в переменную varName, а равенство =default задаёт выражение, которое будет использовано, если значение отсутствует (не указано или undefined).

Для массивов имеет значение порядок, поэтому нельзя использовать :, но значение по умолчанию – можно:

``` javascript
let [var1 = default, var2, ...rest] = array
```

Объявление переменной в начале конструкции не обязательно. Можно использовать и существующие переменные. Однако при деструктуризации объекта может потребоваться обернуть выражение в скобки.

Вложенные объекты и массивы тоже работают, при деструктуризации нужно лишь сохранить ту же структуру, что и исходный объект/массив.

## Template strings

Улучшения:

* Строки-шаблоны – для удобного задания строк (многострочных, с переменными), плюс возможность      использовать функцию шаблонизации для самостоятельного форматирования.
* Юникод – улучшена работа с суррогатными парами.
* Полезные методы для проверок вхождения одной строки в другую.

Добавлен ряд полезных методов общего назначения:

* `str.includes(s)` – проверяет, включает ли одна строка в себя другую, возвращает true/false.
* `str.endsWith(s)` – возвращает true, если строка str заканчивается подстрокой s.
* `str.startsWith(s)` – возвращает true, если строка str начинается со строки s.
* `str.repeat(times)` – повторяет строку str times раз.

## ES6: Super

Needing to remember to use Object.getPrototypeOf() and .call(this) to call a method on the
prototype is a bit involved, so ECMAScript 6 introduced super.
At it’s simplest, super acts as a pointer to the current object’s prototype, effectively acting like
Object.getPrototypeOf(this). So you can simplify the getGreeting() method by rewriting it as:

``` javascript
    let friend = {
    __proto__: person,
    getGreeting() {
        // same as Object.getPrototypeOf(this).getGreeting.call(this)
        // or this.\__proto__.getGreeting.call(this)return super.getGreeting() + ", hi!";
        return super.getGreeting() + ", hi!";
    }
};
```

The call to super.getGreeting() is the same as
Object.getPrototypeOf(this).getGreeting.call(this) or
this.\__proto__.getGreeting.call(this). Similarly, you can call any method on an object’s
prototype by using a super reference.
If you’re calling a prototype method with the exact same name, then you can also call super as a function,
for example:

``` javascript
    let friend = {
    __proto__: person,
    getGreeting() {
        // same as Object.getPrototypeOf(this).getGreeting.call(this)
        // or this.\__proto__.getGreeting.call(this)
        // or super.getGreeting()
        return super() + ", hi!";
    }
};
```

## Module Loaders

Современный стандарт описывает, как организовать код в модули, экспортировать и импортировать значения.

### Экспорт:

* export можно поставить прямо перед объявлением функции, класса, переменной.
* Если export стоит отдельно от объявления, то значения в нём указываются в фигурных скобках: export {…}.
* Также можно экспортировать «значение по умолчанию» при помощи export default.

### Импорт:

* В фигурных скобках указываются значения, а затем – модуль, откуда их брать: import {a, b, c as d} from "module".
* Можно импортировать все значения в виде объекта при помощи import * as obj from "module".
* Без фигурных скобок будет импортировано «значение по умолчанию»: import User from "user".

На текущий момент модули требуют системы сборки на сервере. Автор этого текста преимущественно использует webpack, но есть и другие варианты.

## Proxies, Reflect

**Прокси** (proxy) – особый объект, смысл которого – перехватывать обращения к другому объекту и, при необходимости, модифицировать их.

Синтаксис:

``` javascript
let proxy = new Proxy(target, handler)
```

Здесь:

* `target`– объект, обращения к которому надо перехватывать.
* `handler` – объект с «ловушками»: функциями-перехватчиками для операций к target.

Почти любая операция может быть перехвачена и обработана прокси до или даже вместо доступа к объекту target, например: чтение и запись свойств, получение списка свойств, вызов функции (если target – функция) и т.п.

Полный список возможных функций-перехватчиков, которые может задавать handler:

* `getPrototypeOf` – перехватывает обращение к методу getPrototypeOf.
* `setPrototypeOf` – перехватывает обращение к методу setPrototypeOf.
* `isExtensible` – перехватывает обращение к методу isExtensible.
* `preventExtensions` – перехватывает обращение к методу preventExtensions.
* `getOwnPropertyDescripto` – перехватывает обращение к методу getOwnPropertyDescriptor.
* `defineProperty` – перехватывает обращение к методу defineProperty.
* `has` – перехватывает проверку существования свойства, которая используется в операторе in и в некоторых других методах встроенных объектов.
* `get` – перехватывает чтение свойства.
* `set` – перехватывает запись свойства.
* `deleteProperty` – перехватывает удаление свойства оператором delete.
* `enumerate` – срабатывает при вызове for..in или for..of, возвращает итератор для свойств объекта.
* `ownKeys` – перехватывает обращения к методу getOwnPropertyNames.
* `apply` – перехватывает вызовы target().
* `construct` – перехватывает вызовы new target().

Каждый перехватчик запускается с handler в качестве this. Это означает, что handler кроме ловушек может содержать и другие полезные свойства и методы.

Каждый перехватчик получает в аргументах target и дополнительные параметры в зависимости от типа.

Если перехватчик в handler не указан, то операция совершается, как если бы была вызвана прямо на target.

Proxy позволяет модифицировать поведение объекта как угодно, перехватывать любые обращения к его свойствам и методам, включая вызовы для функций.

Особенно приятна возможность перехватывать обращения к отсутствующим свойствам, разработчики ожидали её уже давно.

Что касается поддержки, то возможности полифиллов здесь ограничены. «Переписать» прокси на старом JavaScript сложновато, учитывая низкоуровневые возможности, которые он даёт.

Поэтому нужна именно браузерная поддержка. Постепенно она реализуется.

### Reflect

Reflect - это не конструктор
**Reflect** - это встроенный объект, который предоставляет методы для перехватывания JavaScript операций. Эти методы аналогичны методам proxy handler`ов. Reflect - это не функциональный, а простой объект, он не является сконструированным.

Объект **Reflect** обеспечивает работу статических функций, называющиеся так же, как методы proxy handler`а. Некоторые из этих методов - те же, что и соответствующие им методы класса Object.

* `Reflect.apply()` Вызывает целевую функцию с аргументами, переданными в параметре args. См. так же Function.prototype.apply().
* `Reflect.construct()`  Оператор new как функция. Аналогично new target(...args).
* `Reflect.defineProperty()` Похож на Object.defineProperty(). Возвращает Boolean.
* `Reflect.deleteProperty()` Оператор delete как функция. Аналогично delete target[name].
* `Reflect.enumerate()` Подобно циклу for...in. Возвращает итератор с собственными перечисляемыми и наследованными свойствами целевого объекта.
* `Reflect.get()` Функция, которая возвращает значение свойств.
* `Reflect.getOwnPropertyDescriptor()` Аналогично Object.getOwnPropertyDescriptor(). Возвращает дескриптор указанного свойства если присутствует в объекте, иначе undefined.
* `Reflect.getPrototypeOf()` Аналогично Object.getPrototypeOf().
* `Reflect.has()` Оператор in как функция. Возвращает значение Boolean в зависимости от факта наличия собственного или наследованного свойства.
* `Reflect.isExtensible()` Аналогично Object.isExtensible().
* `Reflect.ownKeys()` Возвращает массив строк с именами собственных (не наследованных) свойств.
* `Reflect.preventExtensions()` Аналогично Object.preventExtensions(). Возвращает Boolean.
* `Reflect.set()` Функция, присваивающая значения свойствам. Возвращает Boolean значение true при успешном выполнении.
* `Reflect.setPrototypeOf()` Функция, присваивающая прототип целевому объекту.

## Async/await

```javascript
async function name([param[, param[, ... param]]]) {
   statements
}
```

When an async function is called, it returns a Promise. When the async function returns a value, the Promise will be resolved with the returned value.  When the async function throws an exception or some value, the Promise will be rejected with the thrown value.

An async function can contain an await expression, that pauses the execution of the async function and waits for the passed Promise's resolution, and then resumes the async function's execution and returns the resolved value.

The purpose of async/await functions is to simplify the behavior of using promises synchronously and to perform some behavior on a group of Promises. Just as Promises are similar to structured callbacks, async/await is similar to combining generators and promises.

Do not confuse await for Promise.all
In add1, execution suspends 2 seconds for the first await, and then again another 2 seconds for the second await. The second timer is not created until the first has already fired. In add2,  both timers are created, and then both are awaited. This leads it to resolve in 2 rather than 4 seconds, because the timers are running concurrently. But both of the await calls are still run in series, not in parallel: this is not some automatic application of Promise.all. If you wish to await two or more promises in parallel, you must still use Promise.all

## Chaining

### Constructor and Method Chaining

### Вызов конструктора и методов базового класса

Классы наследники
Ключевое слово extends позволяет создать класс-наследник существующего конструктора (который возможно был определен с помощью класса):

```javascript
class Point {
    constructor(x, y) {
        this.x = x;
        this.y = y;
    }
    toString() {
        return '(' + this.x + ', ' + this.y + ')';
    }
}

class ColorPoint extends Point {
    constructor(x, y, color) {
        super(x, y); // (A)
        this.color = color;
    }
    toString() {
        return super.toString() + ' in ' + this.color; // (B)
    }
}
```

Этот класс используется как и ожидалось:

```javascript
> let cp = new ColorPoint(25, 8, 'green');
> cp.toString()
'(25, 8) in green'
> cp instanceof ColorPoint
true
> cp instanceof Point
true
```

В данном случае мы имеем два вида классов:

Point — это базовый класс, потому что он не имеет выражения extends.
ColorPoint — производный класс.
Есть два способа использовать ключевое слово super:

Конструктор класса (псевдо-метод «constructor» в теле класса), использует его как вызов функции (_super(•••)_), для того, чтобы вызвать базовый конструктор (строка A).
Определения методов (в объектах, заданных через литерал, или классах, статических или нет), используют это для вызова свойства (_super.prop_), или вызова метода (_super.method(•••)_), для ссылки на свойства базового класса (строка B).