# Тема для страниц новостей и мероприятий guap.ru/pubs

- [Общее](#общее)
   - [Сброс стилей](#сброс-стилей)
   - [Шрифты](#шрифты)
   - [Переменные](#переменные)
      - [Цветовая палитра](#цветовая-палитра)
      - [Система отступов и границ](#система-отступов-и-границ)
      - [Брейкпоинты](#брейкпоинты)
   - [Типографика](#типографика)
- [Компоненты](#компоненты)
   - [Дата](#дата)
   - [Кнопки поделиться](#кнопки-поделиться)
   - [Детали мероприятия](#детали-мероприятия)
   - [Галерея](#галерея)
   - [Текст](#текст)
   - [Теги](#теги)
   - [Шапка](#шапка)
      - [Desktop-меню](#desktop-меню)
      - [Mobile-меню](#mobile-меню)

## Общее
### Сброс стилей
Браузеры, обладающие разными движками под копотом обладают разными стилями по-умолчанию, несмотря на то, что имеются некоторые общие стандарты. Для того, чтобы избежать различий на разных устройствах, мной было использованы два файла, распространённых среди разработчиков, а именно `reset.css` и `normalize.css`.
```scss
@import "reset";
@import "normalize";
```

### Шрифты
Шрифт ГУАПа по фирстилю **Roboto**, поэтому **Roboto** и является главным шрифтом сайта. Соответственно и является главным шрифтом страницы новостей.
```scss
@import "kit/fonts/include-fonts";   // Подключение основного шрифта.
```

Самое занятное на сайте ГУАПа - это шрифты, поскольку иконки и логотипы в большинстве своём используются как текст при помощи подключённых шрифтов.
На странице сайта используются иконки из двух паков: guap_icons и bootstrap_icons.
Для использования необходимо подключить сначала шрифты `_include-fonts.scss`, а после этого файлы для работы с самими иконками `_guap-icons.scss` и `_bootstrap-icons.scss`.
```scss
@import "kit/fonts/bootstrap-icons"; // Всё для работы с bootstrap_icons
@import "kit/fonts/guap-icons";      // Всё для работы с guap_icons
```

### Переменные
Все переменные, использующиеся внутри системы стилей, хранятся внутри файла `_variables.scss`. Использование переменных удобно на случай, если будет резкая необходимость в смене каких-либо цветов, размеров шрифтов или блоков, а также отступов, поскольку необходимо будет изменить одну лишь переменную, вместо всех параметров в коде.
#### Цветовая палитра
Фирстиль ГУАПа крутится вокруг трёх цветов: циан, синий и розовый. В файле `_variables.scss` содержатся переменные, которые хранят в себе hex-коды всех этих цветов в разных оттенках, использующихся для разных целей, например: наведение на ссылку. <br/>
Плюс чёрный и белый, поскольку без них никуда. <br/>
Использование разных цветов происходит по следующему алгоритмы:
```scss
// $цвет-оттенок;
color: $blue-500;
```
С градиентами такая же ситуация, основные градиенты, представленные в макете, для упрощения их использования, заданы при помощи переменных.
```scss
$gradient_it: linear-gradient($direction-90, $gradient_it-start, $gradient_it-end);
$gradient_block_light: linear-gradient($direction-135, $gradient_block_light-start, $gradient_block_light-end);
$gradient_block_dark: linear-gradient($direction-135, $gradient_block_dark-start, $gradient_block_dark-end);
$gradient_primary: linear-gradient($direction-180, $gradient_primary-start, $gradient_primary-end);
$gradient_secondary: linear-gradient($direction-180, $gradient_secondary-start, $gradient_secondary-dark);
$gradient_line-90: linear-gradient($direction-90, $gradient_line-start, $gradient_line-center, $gradient_line-end);
$gradient_line-180: linear-gradient($direction-180, $gradient_line-start, $gradient_line-center, $gradient_line-end);
```

#### Система отступов и границ
**system paddings** (система внутренних отступов) создана для упрощения наложения стиля padding, поскольку они должны быть систематично одинаковы везде и не требовать длительных разбирательств для изменений. <br/>
Используются по следующему алгоритму: `$sp-Ax;`, где `A` это `A * 4px` (работает до 40px, макс A = 10).
```scss
$sp-1x: 4px;
$sp-2x: $sp-1x * 2;
$sp-3x: $sp-1x * 3;
$sp-4x: $sp-1x * 4;
$sp-5x: $sp-1x * 5;
// ... и т.д.
```
Ровно также и с радиусами для рамок кнопок или каких-либо блоков, для небольшой систематизации, применение скругления рамок происходит при помощи переменных `$rad-Ax;`. Ниже приведены значения этих переменных
```scss
// Границы/Радиусы
$rad-1x: 4px;
$rad-2x: $rad-1x * 1.5; // 6px
$rad-3x: $rad-1x * 2;   // 8px
$rad-4x: $rad-1x * 3;   // 12px
$rad-5x: $rad-1x * 4;   // 16px
$rad-6x: $rad-1x * 5;   // 20px
```

#### Брейкпоинты
Брейкпоинты для медиа-запросов используются идентичные тем, что используются bootstrap'ом.
```scss
$breakpoint-sm: 576px;
$breakpoint-md: 768px;
$breakpoint-lg: 992px;
$breakpoint-xl: 1200px;
$breakpoint-xxl: 1400px;
```
Пример использования: 
```scss
@media screen and (max-width: $breakpoint-sm) {
   body {
      color: $secondary-color;
   }
}
```

### Типографика
Базовые переменные для размеров шрифтов, высоты строки и высоты заголовков, заданы как переменные для `:root` внутри файла `_typography.scss` как для desktop-версии, так и для mobile-версии:
```scss
:root {
    --font-size-base: 20px;
    --line-height-base: 1.5;
    --heading-line-height: 1.3;
    @media screen and (max-width: $breakpoint-sm) {
        --font-size-base: 16px;
        --line-height-base: 1.4;
        --heading-line-height: 1.2;
    }
}
```
Размеры заголовков и шрифтов в целом тесно связаны с переменными, заданными в `:root`, поскольку мы бежим за адаптивностью, нам необходимо, чтобы размер шрифтов изменялся динамически поэтому шрифты напрямую зависят от переменной в `:root`, которая в свою очередь зависит от ширины экрана, и на мобильном устройстве размер базового шрифта отличается от десктопа.
```scss
$small-font-size: 0.7em; // desktop 14px mobile 11px
$h6-font-size: 1em;      // desktop 20px mobile 16px
$h5-font-size: 1.25em;   // desktop 25px mobile 20px
$h4-font-size: 1.5em;    // desktop 30px mobile 24px
$h3-font-size: 1.75em;   // desktop 35px mobile 28px
$h2-font-size: 2em;      // desktop 40px mobile 32px
$h1-font-size: 2.25em;   // desktop 45px mobile 36px
```
### Сетка страницы
???

## Компоненты

### Дата
Все стили, касающиеся данного компонента, хранятся в файле по адресу `kit/components/_date.scss`. Для использования, необходимо скопировать данный кусок кода:
```html
<div class="date">
    <span class="date-day">15</span>
    <div class="date-inner_wrapper">
        <span class="date-month">июля</span> 
        <span class="date-year">2024</span>
    </div>
</div>
```
Цвет текста по-умолчанию базовый чёрный для страницы `#222222` для новостей. Для мероприятий к классу `date` добавляется класс `event`, который перекрашивает текст в синий, а если мероприятие сегодня, то добавляется ещё один класс `now`, который перекрашивает в розовый. <br>
В случае необходимости создать какой-либо кастомный цвет, можно добавить свойство аналогично представленному ниже примеру:
```scss
.date {
    &.event {
        color: $primary-guap;
        &.now {
            color: $secondary-guap;
        }
    }
}
```

### Кнопки поделиться
Стилизация: `kit/components/_repost.scss`
```html
<div class="repost">
    <a href="#" class="repost_link">
        <i class="gi-logo-telegram"></i>
    </a>
    <a href="#" class="repost_link">
        <i class="gi-logo-vk"></i>
    </a>
    <a href="#" class="repost_link">
        <i class="gi-logo-ok"></i>
    </a>
</div>
```

### Детали мероприятия
Стилизация: `kit/components/_event-datails.scss`
```html
<div class="event-dateils">
   <p class="event-dateils_time">11:00</p>
   <p class="event-dateils_location">Якубовича 26, актовый зал</p>
</div>
<div class="event-registration">
   <a class="event-registration_button" href="#">
       Регистрация
       <small>до 14 июля</small>
   </a>
   <small>Регистрация обязательна</small>
</div>
```
### Галерея
Для галереи используется библиотека [blueimp](https://blueimp.github.io/Gallery/), использующая несколько вспомогательных элементов на странице для отображения. <br>
Для функционирования самой галереи, отображения кнопок переходов по фотографиям.
```html
    <link rel="stylesheet" href="blueimp-gallery/css/blueimp-gallery.css">
    <link rel="stylesheet" href="blueimp-gallery/css/blueimp-gallery-indicator.css">
```
```html
<div id="blueimp-gallery"
        class="blueimp-gallery blueimp-gallery-svgasimg blueimp-gallery-smil blueimp-gallery-display blueimp-gallery-controls"
        aria-label="image gallery" aria-modal="true" role="dialog" style="display: none;">
        <div class="slides" aria-live="polite"></div>
        <h3 class="title"></h3>
        <a class="prev" aria-controls="blueimp-gallery" aria-label="previous slide" aria-keyshortcuts="ArrowLeft"></a>
        <a class="next" aria-controls="blueimp-gallery" aria-label="next slide" aria-keyshortcuts="ArrowRight"></a>
        <a class="close" aria-controls="blueimp-gallery" aria-label="close" aria-keyshortcuts="Escape"></a>
        <a class="play-pause" aria-controls="blueimp-gallery" aria-label="play slideshow" aria-keyshortcuts="Space"
            aria-pressed="false" role="button"></a>
        <ol class="indicator"></ol>
    </div>
```
Функциональная часть библиотеки. Для её работы необходим jQuery, а также несколько строчек для того, чтобы привязать к определённому списку фотографий. В данном случае `id="gallery"`.<br>
Кроме этого написан скрипт, который будет скрывать список фотографий, в случае, если в медиатеке всего одна фотография. Если ссылок на фотографии внутри этого списка нет, то списка не будет.
```html
<!-- Gallery -->
 <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
 <script src="blueimp-gallery/js/blueimp-gallery.js"></script>
 <script src="blueimp-gallery/js/blueimp-gallery-indicator.js"></script>
 <script>
     document.getElementById('gallery').onclick = function (event) {
         event = event || window.event
         var target = event.target || event.srcElement
         var link = target.src ? target.parentNode : target
         var options = { index: link, event: event }
         var links = this.getElementsByTagName('a')
         blueimp.Gallery(links, options)
     }
 </script>
 <script>
     document.getElementById('gallery').onclick = function (event) {
         event = event || window.event
         var target = event.target || event.srcElement
         var link = target.src ? target.parentNode : target
         var options = { index: link, event: event }
         var links = this.getElementsByTagName('a')
         blueimp.Gallery(links, options)
     }
     document.addEventListener("DOMContentLoaded", function () {
         const galleryItems = document.querySelectorAll(".gallery-items li");
         let hasLinks = false;

         galleryItems.forEach(item => {
             const link = item.querySelector("a");
             if (link) {
                 hasLinks = true;
             }
         });

         if (!hasLinks) {
             document.querySelector(".gallery-items").style.display = "none";
         }
     });
 </script>
 <!-- /Gallery -->
```
Поскольку медиатека GUAP позволяет получать на выходе фотографии в разных разрешениях, то для оптимизации страницы, можно отрисовывать фотографии, обращаясь к медиатеки с `s=xxl`, на выходе будет квадратная фотография, а ссылаться на `s=xl`, чтобы фотография была наилучшего качества. <br>
Шаблон галерии:
```html
<div id="gallery" class="gallery">
   <a href="https://media.guap.ru/ {mediaCatalog} /_title.jpg?s=xl" title="{gallery.number.name}">
      <img src="https://media.guap.ru/ {mediaCatalog} /_title.jpg?s=xl" class="gallery gallery-first" alt="{gallery.number.name}">
   </a>
   <ul class="gallery-list">
      <li><a href="https://media.guap.ru/ {mediaCatalog} / {gallery.number.name} ?s=xl" title="{gallery.number.name}"><img class="gallery-list-item" src="https://media.guap.ru/ {mediaCatalog} / {gallery.number.name} ?s=xxl" alt="{gallery.number.name}"></a></li>
      <li><a href="https://media.guap.ru/ {mediaCatalog} / {gallery.number.name} ?s=xl" title="{gallery.number.name}"><img class="gallery-list-item" src="https://media.guap.ru/ {mediaCatalog} / {gallery.number.name} ?s=xxl" alt="{gallery.number.name}"></a></li>
      <li><a href="https://media.guap.ru/ {mediaCatalog} / {gallery.number.name} ?s=xl" title="{gallery.number.name}"><img class="gallery-list-item" src="https://media.guap.ru/ {mediaCatalog} / {gallery.number.name} ?s=xxl" alt="{gallery.number.name}"></a></li>
      <li><a href="https://media.guap.ru/ {mediaCatalog} / {gallery.number.name} ?s=xl" title="{gallery.number.name}"><img class="gallery-list-item" src="https://media.guap.ru/ {mediaCatalog} / {gallery.number.name} ?s=xxl" alt="{gallery.number.name}"></a></li>
      <li><a href="https://media.guap.ru/ {mediaCatalog} / {gallery.number.name} ?s=xl" title="{gallery.number.name}"><img class="gallery-list-item" src="https://media.guap.ru/ {mediaCatalog} / {gallery.number.name} ?s=xxl" alt="{gallery.number.name}"></a></li>
      <li><a href="https://media.guap.ru/ {mediaCatalog} / {gallery.number.name} ?s=xl" title="{gallery.number.name}"><img class="gallery-list-item" src="https://media.guap.ru/ {mediaCatalog} / {gallery.number.name} ?s=xxl" alt="{gallery.number.name}"></a></li>
      <li><a href="https://media.guap.ru/ {mediaCatalog} / {gallery.number.name} ?s=xl" title="{gallery.number.name}"><img class="gallery-list-item" src="https://media.guap.ru/ {mediaCatalog} / {gallery.number.name} ?s=xxl" alt="{gallery.number.name}"></a></li>
      <li><a href="https://media.guap.ru/ {mediaCatalog} / {gallery.number.name} ?s=xl" title="{gallery.number.name}"><img class="gallery-list-item" src="https://media.guap.ru/ {mediaCatalog} / {gallery.number.name} ?s=xxl" alt="{gallery.number.name}"></a></li>
      <li><a href="https://media.guap.ru/ {mediaCatalog} / {gallery.number.name} ?s=xl" title="{gallery.number.name}"><img class="gallery-list-item" src="https://media.guap.ru/ {mediaCatalog} / {gallery.number.name} ?s=xxl" alt="{gallery.number.name}"></a></li>
      <li><a href="https://media.guap.ru/ {mediaCatalog} / {gallery.number.name} ?s=xl" title="{gallery.number.name}"><img class="gallery-list-item" src="https://media.guap.ru/ {mediaCatalog} / {gallery.number.name} ?s=xxl" alt="{gallery.number.name}"></a></li>
   </ul>
</div>
```
### Текст
Внутри файла `kit/main.scss` описаны все стили, стилизующие все стандартные теги, встречающиеся внутри JSON'а новостей, поэтому необходимости в использовании каких-либо классов нет. Можно брать и вставлять в любую точку страницы текст и на выходе он будет стилизован так, как это необходимо.

### Теги
Стилизация: `kit/_links.scss`.
```html
<div class="tags">
   <a href="https://new.guap.ru/pubs?nodes = {id}" class="link-tag">{nodes.title}</a>
   <a href="https://new.guap.ru/pubs?nodes = {id}" class="link-tag">{nodes.shortTitle}</a>
   <a href="https://new.guap.ru/pubs?categories = {id}" class="link-tag">{categories.title}</a>
   <a href="https://new.guap.ru/pubs?categories = {id}" class="link-tag">{categories.title}</a>
   <a href="https://new.guap.ru/pubs?targets = {id}" class="link-tag">{targets.title}</a>
   <a href="https://new.guap.ru/pubs?tags = {id}" class="link-tag">{tags.title}</a>
</div>
```

### Шапка
#### Desktop меню
Desktop меню немного отличается от меню для мобильных устойств тем, что уровней вложенности списков на один меньше, поскольку один уровень выходит прямо в шапку сайта для переключения между группами пунктов меню. Внутри самого списка пунктов меню всё реализовано обычным вложенным списком, где `.header-menu_title` — заголовок подгруппы внутри определённой категории, а содержимое `.header-menu_list.inner` элементы того самого меню.
```html
<nav class="header-menu" id="desktopMenuTabs">
    <button class="btn-header active" id="desktopMenuTab-1">Университет</button>
    <button class="btn-header" id="desktopMenuTab-2">Образование</button>
    <button class="btn-header" id="desktopMenuTab-3">Наука</button>
    <button class="btn-header" id="desktopMenuTab-4">Сотрудничество</button>
    <button class="btn-header" id="desktopMenuTab-5">Вне учебы</button>
</nav>

...

<ul class="header-menu_list wrapper active" id="desktopMenuNode-1">
   <li class="header-menu_title">
       О вузе
       <ul class="header-menu_list inner">
           <li><a href="#">Администрация</a></li>
           <li><a href="#">Антимонопольный комплаенс</a></li>
           <li><a href="#">Преподаватели</a></li>
       </ul>
   </li>
   <li class="header-menu_title">
       О вузе
       <ul class="header-menu_list inner">
           <li><a href="#">Администрация</a></li>
           <li><a href="#">Антимонопольный комплаенс</a></li>
           <li><a href="#">Преподаватели</a></li>
       </ul>
   </li>
   <li class="header-menu_title">
       О вузе
       <ul class="header-menu_list inner">
           <li><a href="#">Администрация</a></li>
           <li><a href="#">Антимонопольный комплаенс</a></li>
           <li><a href="#">Преподаватели</a></li>
       </ul>
   </li>
</ul>
```

#### Mobile меню
Меню для мобильных устойств отличается от Desktop тем, что уровень вложенности списков на один больше. <br>
Пример того самого списка:
```html
<ul class="mobile-menu_list">
   <li>Университет
       <ul class="mobile-menu_list_inner">
           <li class="mobile-menu_list_inner-next">О вузе
               <ul class="mobile-menu_list_inner">
                   <li><a href="#">Приветствие ректора</a></li>
               </ul>
           </li>
           <li class="mobile-menu_list_inner-next">Институты и факультеты
               <ul class="mobile-menu_list_inner">
                   <li><a href="#">Институт аэрокосмических приборов и систем (институт 1)</a></li>
                   <li><a href="#">Институт радиотехники и инфокоммуникационных технологий (институт 2)</a></li>
                   <li><a href="#">Институт киберфизических систем (институт 3)</a></li>
               </ul>
           </li>
       </ul>
   </li>
   <li>Университет
       <ul class="mobile-menu_list_inner">
           <li class="mobile-menu_list_inner-next">О вузе
               <ul class="mobile-menu_list_inner">
                   <li><a href="#">Приветствие ректора</a></li>
               </ul>
           </li>
           <li class="mobile-menu_list_inner-next">Институты и факультеты
               <ul class="mobile-menu_list_inner">
                   <li><a href="#">Институт аэрокосмических приборов и систем (институт 1)</a></li>
                   <li><a href="#">Институт радиотехники и инфокоммуникационных технологий (институт 2)</a></li>
                   <li><a href="#">Институт киберфизических систем (институт 3)</a></li>
               </ul>
           </li>
       </ul>
   </li>
</ul>
```
