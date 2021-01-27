**## Точка с запятой.**
***

**1. Всегда ставь точку с запятой у последнего свойства в блоке.**
>stylelint: ```[declaration-block-trailing-semicolon](https://)```

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
>stylelint: ```[no-extra-semicolons](no-extra-semicolons)```

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


##**В строку или в столбик.**
***

**1. Если свойств несколько, лучше писать их в столбик.**
>stylelint: ```[declaration-block-single-line-max-declarations](declaration-block-single-line-max-declarations)```

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
>stylelint: ```[declaration-block-semicolon-newline-after](declaration-block-semicolon-newline-after)```

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
>stylelint: ```[selector-list-comma-newline-after](selector-list-comma-newline-after)```

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


##**: или :: для псевдоэлементов.**
***

**Используй двойное двоеточие для псевдоэлементов.**
>stylelint: ```[selector-pseudo-element-colon-notation](selector-pseudo-element-colon-notation)```

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


##**Пустые блоки.**
***

**Не оставляй пустые блоки со стилями.**
>stylelint: ```[block-no-empty](block-no-empty)```

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


##**Ноль, что с ним делать.**
***

**1. Не ставь ведущий ноль у дробных чисел.**
>stylelint: ```[number-leading-zero](number-leading-zero)```

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
>stylelint: ```[length-zero-no-unit](length-zero-no-unit)```

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
>stylelint: ```[number-no-trailing-zeros](number-no-trailing-zeros)```

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


##**Специфичность.**
***

**1. Не пиши селекторы с меньшей специфичностью после селекторов с большей специфичностью.**
>stylelint: ```[no-descending-specificity](no-descending-specificity)```

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
>stylelint: ```[declaration-block-no-shorthand-property-overrides](declaration-block-no-shorthand-property-overrides)```

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

##**Шрифты.**
***

**Ставь всегда тип шрифта(serif, sans-serif, cursive, fantasy или monospace).**
>stylelint: ```[font-family-no-missing-generic-family-keyword](font-family-no-missing-generic-family-keyword)```

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

##**Строчные или заглавные буквы.**
***

**1. Называй at-rules (правила) строчными буквами.**
>stylelint: ```[at-rule-name-case](at-rule-name-case)```

Тип шрифта:
+ может стоять в любом месте в списке шрифтов;
+ может быть опущен, если используется ключевое слово, связанное с наследованием свойств или системным шрифтом.

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
>stylelint: ```[function-name-case](function-name-case)```

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
>stylelint: ```[color-hex-case](color-hex-case)```

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
>stylelint: ```[media-feature-name-case](media-feature-name-case)```

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
>stylelint: ```[property-case](property-case)```

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
>stylelint: ```[selector-pseudo-class-case](selector-pseudo-class-case)```

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
>stylelint: ```[selector-pseudo-element-case](selector-pseudo-element-case)```

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
>stylelint: ```[selector-type-case](selector-type-case)```

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
>stylelint: ```[unit-case](unit-case)```

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


#**CSS**
***

###**Форматирование**
+Используйте мягкие табуляции (2 пробела) для отступов.
+Подчеркивание и PascalCasing допустимы, если вы используете БЭМ (см. OOCSS и BEM ниже).
+Не используйте селекторы ID.
+При использовании нескольких селекторов в объявлении правила дайте каждому селектору отдельную строку.
+В {объявлениях правил ставьте пробел перед открывающей скобкой .
+В свойствах ставьте пробел после :символа , но не перед ним .
+Поместите закрывающие фигурные скобки }объявлений правил на новую строку.
+Между объявлениями правил вставляйте пустые строки.

####**Bad**

```
.avatar{
    border-radius:50%;
    border:2px solid white; }
.no, .nope, .not_good {
    // ...
}
#lol-no {
  // ...
}
```
####**Good**

```
.avatar {
  border-radius: 50%;
  border: 2px solid white;
}

.one,
.selector,
.per-line {
  // ...
}
```

###**Комментарии**
+Предпочитайте строчные комментарии ( ```//```в Sass-land), чтобы блокировать комментарии.
+Предпочитайте комментарии в их собственной строке. Избегайте комментариев в конце строки.
+Напишите подробные комментарии для кода, который не самодокументируется:
 -Использование z-индекса
 -Совместимость или специфичные для браузера хаки


###**Хуки JavaScript**

Избегайте привязки к одному и тому же классу как в CSS, так и в JavaScript. Объединение этих двух часто приводит, как минимум, к потере времени на рефакторинг, когда разработчик должен ссылаться на каждый класс, который они изменяют, и в худшем случае разработчики боятся вносить изменения из-за страха нарушить функциональность.

Мы рекомендуем создавать для привязки классы, специфичные для JavaScript, с префиксом .js-:
```
< button  class = " btn btn-primary js-request-to-book " > Запрос на бронирование </ button >
```

###**Граница**

Используйте ```0``` вместо, ```none``` чтобы указать, что у стиля нет границы.

###**Bad**

```
.foo {
  border: none;
}
```

###**Good**

```
.foo {
  border: 0;
}
```


