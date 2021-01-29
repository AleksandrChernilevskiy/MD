## **Точка с запятой.**

**1. Всегда ставь точку с запятой у последнего свойства в блоке.**
>eslint: [declaration-block-trailing-semicolon](https://stylelint.io/user-guide/rules/indentation#indentation)

:x: не надо так :point_down:
```
a { color: pink }
a { background: orange; color: pink }
a { @include foo }
```

:white_check_mark: надо так :point_down:
```
a { color: pink; }
a { background: orange; color: pink; }
a { @include foo; }
```

**2. Не ставь лишние точки с запятой.**
>eslint: [no-extra-semicolons](no-extra-semicolons)

:x: не надо так :point_down:
```
@import "x.css";;
@import "x.css";
;
a {
  color: pink;;
}

a {
  ;color: pink;
}

a {
  color: pink;
  ;
}

a {
  color: red;
}
;
b {
  color: white;
}
```

:white_check_mark: надо так :point_down:
```
@import "x.css";

a {
  color: pink;
}
```


## **В строку или в столбик.**

**1. Если свойств несколько, лучше писать их в столбик.**
>eslint: [declaration-block-single-line-max-declarations](declaration-block-single-line-max-declarations)

:x: не надо так :point_down:
```
a { color: pink; top: 3px; }

a,
b { color: pink; top: 3px; }
```

:white_check_mark: надо так :point_down:
```
b { color: pink; }

a {
  color: pink;
  top: 3px;
}
```

**2. В многострочных блоках пиши каждое свойство с новой строки(в столбик).**
>eslint: [declaration-block-semicolon-newline-after](declaration-block-semicolon-newline-after)

:x: не надо так :point_down:
```
a {
  color: pink; top: 0;
}
```

:white_check_mark: надо так :point_down:
```
a {
  color: pink;
  top: 0;
}
```

**3. Перечисляй селекторы в столбик (после запятой начинай с новой строки).**
>eslint: [selector-list-comma-newline-after](selector-list-comma-newline-after)

:x: не надо так :point_down:
```
a {
  color: pink; top: 0;
}
```

:white_check_mark: надо так :point_down:
```
a,
b { color: pink; }

a
,
b { color: pink; }
```


## **: или :: для псевдоэлементов.**

**Используй двойное двоеточие для псевдоэлементов.**
>eslint: [selector-pseudo-element-colon-notation](selector-pseudo-element-colon-notation)

:x: не надо так :point_down:
```
a:before { color: pink; }
a:after { color: pink; }
a:first-letter { color: pink; }
a:first-line { color: pink; }
```

:white_check_mark: надо так :point_down:
```
a::before { color: pink; }
a::after { color: pink; }
a::first-letter { color: pink; }
a::first-line { color: pink; }
input::placeholder { color: pink; }
li::marker { font-variant-numeric: tabular-nums; }
```


## **Пустые блоки.**

**Не оставляй пустые блоки со стилями.**
>eslint: [block-no-empty](block-no-empty)

:x: не надо так :point_down:
```
a {}

a { }

@media print {
  a {}
}
```

:white_check_mark: надо так :point_down:
```
a {
  /* foo */
}
@media print {
  a {
    color: pink;
  }
}
```


## **Ноль, что с ним делать.**

**1. Не ставь ведущий ноль у дробных чисел.**
>eslint: [number-leading-zero](number-leading-zero)

:x: не надо так :point_down:
```
a { line-height: 0.5; }
a { transform: translate(2px, 0.4px); }
```

:white_check_mark: надо так :point_down:
```
a { line-height: .5; }
a { transform: translate(2px, .4px); }
```

**2. Не ставь единицы измерения длины, если значение нулевое.**
>eslint: [length-zero-no-unit](length-zero-no-unit)

Длина - это измерение , которое представляет собой число, за которым сразу следует идентификатор единицы измерения . Однако для нулевой длины идентификатор единицы является необязательным. Единицы длины: em, ex, ch, vw, vh, cm, mm, in, pt, pc, px, rem, vmin, и vmax.

:x: не надо так :point_down:
```
a { top: 0px }
a { top: 0.000em }
```

:white_check_mark: надо так :point_down:
```
a { top: 0 } /* нет единицы */
a { transition-delay: 0s; } /* измерение*/
a { top: 2in; }
a { top: 1.001vh }
```
**3. Не ставь нули в конце чисел, если они не несут смысла.**
>eslint: [number-no-trailing-zeros](number-no-trailing-zeros)

:x: не надо так :point_down:
```
a { top: 1.0px }
a { top: 1.01000px }
```

:white_check_mark: надо так :point_down:
```
a { top: 1px }
a { top: 1.01px }
```


## **Специфичность.**

**1. Не пиши селекторы с меньшей специфичностью после селекторов с большей специфичностью.**
>eslint: [no-descending-specificity](no-descending-specificity)

Когда два селектора имеют одинаковую специфичность, приоритет имеет тот , который появляется последним . Однако ситуация отличается, когда один из селекторов имеет более высокую специфичность. В этом случае исходный порядок не имеет значения: селектор с более высокой специфичностью победит, даже если он появится первым.

:x: не надо так :point_down:
```
b a {}
a {}
 
a + a {}
a {}
 
b > a[foo] {}
a[foo] {}
 
a {
  & > b {}
}
b {}
 
@media print {
  #c a {}
  a {}
}
```

:white_check_mark: надо так :point_down:
```
a {}
b a {}
 
a {}
a + a {}
 
 
a[foo] {}
b > a[foo] {}
 
b {}
a {
  & > b {}
}
 
a::before {}
a:hover::before {}
a {}
a:hover {}
 
@media print {
  a {}
  #c a {}
}
 
a {}
@media print {
  #baz a {}
}
```

**2. Не пиши сокращенные свойства после связных свойств.**
>eslint: [declaration-block-no-shorthand-property-overrides](declaration-block-no-shorthand-property-overrides)

Сокращенные свойства могут переопределить связные свойства.

:x: не надо так :point_down:
```
a {
  padding-left: 10px;
  padding: 20px;
}
 
a {
  transition-property: opacity;
  transition: opacity 1s linear;
}
 
a {
  -webkit-transition-property: opacity;
  -webkit-transition: opacity 1s linear;
}
 
a {
  border-top-width: 1px;
  top: 0;
  bottom: 3px;
  border: 2px solid blue;
}
```

:white_check_mark: надо так :point_down:
```
a {
  padding: 10px;
  padding-left: 20px;
}
 
a {
  transition-property: opacity;
}

a {
  transition: opacity 1s linear;
}
 
a {
  transition-property: opacity;
  -webkit-transition: opacity 1s linear;
}
```


## **Шрифты.**

**Ставь всегда тип шрифта(serif, sans-serif, cursive, fantasy или monospace).**
>eslint: [font-family-no-missing-generic-family-keyword](font-family-no-missing-generic-family-keyword)

Тип шрифта:
+ может стоять в любом месте в списке шрифтов;
+ может быть опущен, если используется ключевое слово, связанное с наследованием свойств или системным шрифтом.

:x: не надо так :point_down:
```
a { font-family: Helvetica, Arial, Verdana, Tahoma; }
a { font: 1em/1.3 Times; }
```

:white_check_mark: надо так :point_down:
```
a { font-family: Helvetica, Arial, Verdana, Tahoma, sans-serif; }
a { font: 1em/1.3 Times, serif, Apple Color Emoji; }
a { font: inherit; }
a { font: caption; }
```


## **Строчные или заглавные буквы.**

**1. Называй at-rules (правила) строчными буквами.**
>eslint: [at-rule-name-case](at-rule-name-case)

:x: не надо так :point_down:
```
@Charset "UTF-8";
@cHarSeT "UTF-8";
@CHARSET "UTF-8";
@Media (min-width: 50em) {}
@mEdIa (min-width: 50em) {}
@MEDIA (min-width: 50em) {}
```

:white_check_mark: надо так :point_down:
```
@charset "UTF-8";
@media (min-width: 50em) {}
```

**2. Называй функции строчными буквами.**
>eslint: [function-name-case](function-name-case)

:x: не надо так :point_down:
```
a {
  width: Calc(5% - 10em);
}
a {
  width: cAlC(5% - 10em);
}
a {
  width: CALC(5% - 10em);
}
a {
  background: -WEBKIT-RADIAL-GRADIENT(red, green, blue);
}
```

:white_check_mark: надо так :point_down:
```
a {
  width: calc(5% - 10em);
}
a {
  background: -webkit-radial-gradient(red, green, blue);
}
```

**3. Для цветов в шестнадцетиричном формате используй строчные буквы.**
>eslint: [color-hex-case](color-hex-case)

:x: не надо так :point_down:
```
a { color: #FFF; }
```

:white_check_mark: надо так :point_down:
```
a { color: #000; }
a { color: #fff; }
```

**4. Для названий медиа-запрсов используй строчные буквы.**
>eslint: [media-feature-name-case](media-feature-name-case)

:x: не надо так :point_down:
```
@media (MIN-WIDTH: 700px) {}
@media not all and (MONOCHROME) {}
@media (min-width: 700px) and (ORIENTATION: landscape) {}
@media (WIDTH > 10em) {}
```

:white_check_mark: надо так :point_down:
```
@media (min-width: 700px) {}
@media not all and (monochrome) {}
@media (min-width: 700px) and (orientation: landscape) {}
@media (width > 10em) {}
```

**5. Пиши свойства строчными буквами.**
>eslint: [property-case](property-case)

:x: не надо так :point_down:
```
a {
  Width: 1px
}
a {
  WIDTH: 1px
}
a {
  widtH: 1px
}
a {
  border-Radius: 5px;
}
a {
  -WEBKIT-animation-duration: 3s;
}
@media screen and (orientation: landscape) {
  WiDtH: 500px;
}
```

:white_check_mark: надо так :point_down:
```
a {
  width: 1px
}
a {
  border-radius: 5px;
}
a {
  -webkit-animation-duration: 3s;
}
@media screen and (orientation: landscape) {
  width: 500px;
}
```

**6. Используй строчные буквы для селекоторов псевдоклассов.**
>eslint: [selector-pseudo-class-case](selector-pseudo-class-case)

:x: не надо так :point_down:
```
a:Hover {}
a:hOvEr {}
a:HOVER {}
:ROOT {}
:-MS-INPUT-PLACEHOLDER {}
```

:white_check_mark: надо так :point_down:
```
a:hover {}
:root {}
:-ms-input-placeholder {}
```

**7. Используй строчные буквы для селекоторов псевдоэлементов.**
>eslint: [selector-pseudo-element-case](selector-pseudo-element-case)

:x: не надо так :point_down:
```
a:Before {}
a:bEfOrE {}
a:BEFORE {}
a::Before {}
a::bEfOrE {}
a::BEFORE {}
input::-MOZ-PLACEHOLDER {}
```

:white_check_mark: надо так :point_down:
```
a:before {}
a::before {}
input::-moz-placeholder {}
```

**8. Используй строчные буквы для типов селекторов.**
>eslint: [selector-type-case](selector-type-case)

:x: не надо так :point_down:
```
A {}
LI {}
```

:white_check_mark: надо так :point_down:
```
a {}
li {}
```

**9. Используй строчные буквы для единиц измерений.**
>eslint: [unit-case](unit-case)

:x: не надо так :point_down:
```
a {
  width: 10PX;
}
a {
  width: 10Px;
}
a {
  width: 10pX;
}
a {
  width: 10PIXEL;
}
a {
  width: calc(10PX * 2);
}
```

:white_check_mark: надо так :point_down:
```
a {
  width: 10px;
}
a {
  width: calc(10px * 2);
}
```



## **Соглашение об именовании.**

**1. Избегайте однобуквенных названий.**
>eslint: [id-length](id-length)

:x: не надо так :point_down:
```
function q() {
  // ...
}
```

:white_check_mark: надо так :point_down:
```
function query() {
  // ...
}
```

**Используйте camelCase для названий переменных, объектов и функций.**
>eslint: [camelcase](camelcase)

:x: не надо так :point_down:
```
const OBJEcttsssss = {};
const this_is_my_object = {};
function c() {}
```

:white_check_mark: надо так :point_down:
```
const thisIsMyObject = {};
function thisIsMyFunction() {}
```

**3. Используйте PascalCase для именования конструкторов или классов.**
>eslint: [new-cap](new-cap)

:x: не надо так :point_down:
```
function user(options) {
  this.name = options.name;
}

const bad = new user({
  name: 'nope',
});
```

:white_check_mark: надо так :point_down:
```
class User {
  constructor(options) {
    this.name = options.name;
  }
}

const good = new User({
  name: 'yup',
});
```

**4. Не используйте нижнее подчеркивание в начале или конце названий.**
>eslint: [no-underscore-dangle](no-underscore-dangle)

:x: не надо так :point_down:
```
let name_ = 'Max';
foo._bar();
```

:white_check_mark: надо так :point_down:
```
let name = 'Max';
foo.bar();
```

**Исключения:**
+ разрешено использовать нижнее подчеркивание после this.
Так принято помечать псевдоприватные поля.

:white_check_mark: надо так :point_down:
```
this._bar();
let a = this.foo_;
```

## **Переменные.**

**1. Всегда используйте let или const для объявления переменных.**
>eslint: [no-undef, prefer-const](no-undef)

:x: не надо так :point_down:
```
uperPower = new SuperPower();
```

:white_check_mark: надо так :point_down:
```
const superPower = new SuperPower();
```

**2. Не нужно неинициализированной переменной задавать значение undefined, это значение присваивается автоматически.**
>eslint: [no-undef](no-undef)

:x: не надо так :point_down:
```
let foo = undefined;
let bar = undefined;
```

:white_check_mark: надо так :point_down:
```
let foo;
let bar;
```

**3. Используйте let и const для объявления каждой переменной.**
>eslint: [one-var](one-var)

:x: не надо так :point_down:
```
const items = getItems(),
    goSportsTeam = true,
    dragonball = 'z';
```

:white_check_mark: надо так :point_down:
```
const items = getItems();
const goSportsTeam = true;
const dragonball = 'z';
```

**4. Не используйте множественное присваивание. Такие конструкции создают неявные глобальные переменные.**
>eslint: [no-multi-assign, one-var](no-multi-assign)

:x: не надо так :point_down:
```
(function example() {
  let a = b = c = 1;
}());

console.log(a); // ошибка ReferenceError
console.log(b); // 1
console.log(c); // 1
```

:white_check_mark: надо так :point_down:
```
(function example() {
  let a = 1;
  let b = a;
  let c = a;
}());

console.log(a); // ошибка ReferenceError
console.log(b); // ошибка ReferenceError
console.log(c); // ошибка ReferenceError
```

**5. Не переноси строку после оператора присваивания.**
>eslint: [operator-linebreak](operator-linebreak)

При нарушении правила [max-len](max-len) оборачивай присваивание в скобки.

:x: не надо так :point_down:
```
const foo =
  superLongLongLongLongLongLongLongLongFunctionName();


const foo
  = 'superLongLongLongLongLongLongLongLongString';
```

:white_check_mark: надо так :point_down:
```
const foo = (
  superLongLongLongLongLongLongLongLongFunctionName()
);

const foo = 'superLongLongLongLongLongLongLongLongString';
```


**6. Не объявляй неиспользуемые переменные.**
>eslint: [no-unused-vars](no-unused-vars)

:x: не надо так :point_down:
```
let x = 0;
let y = 1; // Переменная не используется

function getX() {
    return x + 1;
}
```

:white_check_mark: надо так :point_down:
```
let x = 0;

function getX() {
    return x + 1;
}
```

## **Объявление переменных.**

**1. Если ты не переназначаешь переменную, то используй const для ее объявления. И наоборот.**
>eslint: [prefer-const, no-const-assign](no-undef)

:x: не надо так :point_down:
```
var a = 1;
var b = 2;

var count = 1;
if (true) {
  count += 1;
}
```

:white_check_mark: надо так :point_down:
```
const a = 1;
const b = 2;

let count = 1;
if (true) {
  count += 1;
}
```

**2. Не используй var. Используй let и const.**
>eslint: [no-var](no-var)

:x: не надо так :point_down:
```
var x = "y";
var CONFIG = {};
```

:white_check_mark: надо так :point_down:
```
let x = "y";
const CONFIG = {};
```


## **Запятые.**

** Запятые не должны быть в начале строки.**
>eslint: [comma-style](comma-style)

:x: не надо так :point_down:
```
const story = [
    once
  , upon
  , aTime
];
```

:white_check_mark: надо так :point_down:
```
const story = [
  once,
  upon,
  aTime,
];
```

**2. Ставь запятую после последнего свойства в объектах и массивах .Они делают git-diff более чистым**
>eslint: [comma-dangle](comma-dangle)

git-diff без использования оконечной запятой

```
const hero = {
     firstName: 'Florence',
-    lastName: 'Nightingale'
+    lastName: 'Nightingale',
+    inventorOf: ['coxcomb chart', 'modern nursing']
};
```
git diff с использованием оконечной запятой

```
const hero = {
     firstName: 'Florence',
     lastName: 'Nightingale',
+    inventorOf: ['coxcomb chart', 'modern nursing'],
};
```

:x: не надо так :point_down:
```
const hero = {
  firstName: 'Dana',
  lastName: 'Scully'
};
```

:white_check_mark: надо так :point_down:
```
const hero = {
  firstName: 'Dana',
  lastName: 'Scully',
};

// Но учтите, что ставить запятую после “rest” элемента нельзя
function createHero(
  firstName,
  lastName,
  inventorOf,
  ...heroArgs
) {
  // does nothing
}
```
