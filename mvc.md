### Model View Controller (MVC) - Модель вид контроллер на примере

> Нету, наверное, другой такой столь удивительной технологии, как MVC.
При том, что большая часть девелоперов утверждает, что исправно использует сию баснословную парадигму, представления их о ней разнятся больше, чем представления средневековых учёных о лунной поверхности. (*c форума phpclub.ru*)

Паттерн Model View Controller (MVC) - Модель вид контроллер в последнее время стал очень популярен в среде веб-программистов. Популярен настолько, что если судить по многочисленным темам в профессиональных форумах, то можно смело сказать, что парадигма уже превратилась в повседневный китч, который уже сейчас трактуется настолько размыто, что четкого определения паттерна нет даже в Википедии. Аббревиатура MVC встречается в интернет-диалогах так часто, что порой кажется, что MVC для каждого разработчика свой. С одной стороны, в этом нет ничего удивительного, ведь MVC - это абстрактный паттерн, парадигма, а не пошаговое руководство к действию, но тем не менее, MVC не может называться какой угодно код.

В данной статье вы нейдете сложных диаграмм и сложных описаний данной парадигмы. В интернете статей про MVC достаточно много. Я лишь покажу парадигму MVC на очень абстрактном примере.

### MVC на примере

Посмотрите на эту картинку. **Это - приложение, построенное по принципу MVC - автомобиль.**

![](l8.jpg)

**Модели** - это все, что под капотом и под днищем авто. Элементы, отмеченные пунктами с 1 по 19 являются независимыми сущностями, каждая из которых выполняет определенную роль. Вместе они образуют слаженно работающий механизм, но по отдельности они бесполезны.

Что немаловажно - мы в любой момент можем заменить любую модель. К примеру, без особых проблем поставить более мощный генератор. Это - важно. Модели в MVC в идеале должны быть как запчасти автомобиля - иметь лишь интерфейс, своего рода API, что бы внедрение новой модели происходило максимально безболезненно для вашего кода.

> В MVC под моделью понимается доменный объект. Доменные объекты совсем никак не относятся к UI. (© [Фаулер, Мартин](http://web.archive.org/web/20161121013928/https://ru.wikipedia.org/wiki/%D0%A4%D0%B0%D1%83%D0%BB%D0%B5%D1%80,_%D0%9C%D0%B0%D1%80%D1%82%D0%B8%D0%BD))

Иными словами, все элементы автомобиля - модели. Двигатель, аккумулятор, фара, бочок с омывайкой - это модели, к которым из UI (кабины автомобиля) мы доступ напрямую не имеем.

Это - **контроллер** (да, да - он так и называется в реальности):

![](023734.jpg)

Задача этого устройства заключается в следующем:

> Контроллер обрабатывает информацию от датчиков системы управления двс, получает сигналы от выключателя кондиционера и управляет исполнительными устройствами, такими как топливный насос и форсунки, катушки зажигания, регулятор холостого хода, нагревательный элемент датчика концентрации кислорода, электромагнитный клапан продувки адсорбера, электровентиляторы системы охлаждения, электромагнитная муфта компрессора кондиционера.

Т.е. задача контроллера - получать сигналы и принимать решение, что делать дальше моделям. В веб-приложениях задача контроллера проверить правильность и корректность входящих запросов и вызывать для исполнения ту или иную модель.

В отличии от автомобильного контроллера (который отвечает лишь за систему управления двигателем), в веб-приложениях

> ...представление и контроллер существуют не в единственном числе. Мы должны иметь пару представление-контроллер для каждого элемента на экране, для каждого элемента управления (© [Фаулер, Мартин](http://web.archive.org/web/20161121013928/https://ru.wikipedia.org/wiki/%D0%A4%D0%B0%D1%83%D0%BB%D0%B5%D1%80,_%D0%9C%D0%B0%D1%80%D1%82%D0%B8%D0%BD))

Иными словами, нажатие любой кнопки или ссылки на экране провоцирует HTTP запрос, который обрабатывают независимые друг от друга контроллеры. Обработкой формы занимается один контроллер, показом страницы со списком новостей - другой контроллер.

**Вид** выглядит так:

![](2700338958.jpg)

Вид - обивка салона, торпеда, туннель пола. Элементы управления - руль и педали.

### В итоге

**Вид** (кабина автомобиля) ничего не знает о **моделях** (подкапотных элементах автомобиля и трансмиссии). Вид располагает лишь элементами управления (педаль газа, например), нажатие которой заставляет **контроллер** принимать решение о том, как должны работать форсунки, впрыскивающие в двигатель топливо и регулирует подачу воздуха с помощью регулятора холостого хода. Модели пассивны и подчиняются командам контроллера. Контроллер, получая некоторую информацию у моделей, может отдавать её в вид (спидометр, тахометр, диагностические коды).