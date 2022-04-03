# Браузер, события

## отличие методов querySelector oт getElements

getElements ищет только внутри  document.  
querySelector  может искать как в document, так и в др элементах.  

## фазы события  

При наступлении события – самый глубоко вложенный элемент, на котором оно произошло, помечается как «целевой» (event.target).

Затем событие сначала двигается вниз от корня документа к event.target, по пути вызывая обработчики, поставленные через addEventListener(...., true), где true – это сокращение для {capture: true}.  
Далее обработчики вызываются на целевом элементе.  
Далее событие двигается от event.target вверх к корню документа, по пути вызывая обработчики, поставленные через on<event> и addEventListener без третьего аргумента или с третьим аргументом равным false.  
  Каждый обработчик имеет доступ к свойствам события event:

event.target – самый глубокий элемент, на котором произошло событие.  
  event.currentTarget (=this) – элемент, на котором в данный момент сработал обработчик (тот, на котором «висит» конкретный обработчик)  
  event.eventPhase – на какой фазе он сработал (погружение=1, фаза цели=2, всплытие=3).  
  Любой обработчик может остановить событие вызовом event.stopPropagation()  
  
  Стандарт DOM Events описывает 3 фазы прохода события:

Фаза погружения (capturing phase) – событие сначала идёт сверху вниз.
Фаза цели (target phase) – событие достигло целевого(исходного) элемента.
Фаза всплытия (bubbling stage) – событие начинает всплывать.



## 26 методы отмены события event.prevent  

JavaScript метод preventDefault() объекта Event при вызове отменяет действие события по умолчанию. Событие продолжает распространяться как обычно, только с тем исключением, что событие ничего не делает.  

Интерфейс Event представляет собой любое событие, которое происходит в объектной модели документа (DOM). Некоторые события создаются непосредственно пользователем (например, события мыши, или клавиатуры), а другие генерируются программным интерфейсом приложения (API), например, такие события как завершение анимации, или приостановка видео.

Когда вызывается какой-либо обработчик события, то в этом случае ему передается объект Event, свойства этого объекта содержат дополнительную информацию о событии, например, такую как тип события и объект, который отправил событие. С помощью методов объекта Event можно управлять распространением события по дереву DOM. 

  
 **Расскажите что содержит в себе браузерное окружение (DOM, BOM, JS)?**  
https://learn.javascript.ru/browser-environment

**Поиск DOM элементов:querySelector querySelectorAll getElementById getElementsByName getElementsByTagName getElementsByClassName closest matches**  
Document метод querySelector() возвращает первый элемент (Element) документа, который соответствует указанному селектору или группе селекторов. Если совпадений не найдено, возвращает значение null.  
Метод Element.closest() возвращает ближайший родительский элемент (или сам элемент), который соответствует заданному CSS-селектору или null, если таковых элементов вообще нет.  
Метод Element.matches() вернёт true или false, в зависимости от того, соответствует ли элемент указанному css-селектору.


**Что делает метод getComputedStyle?**   
Функция getComputedStyle позволяет получить значение любого CSS свойства элемента, даже из CSS файла.
Как оно работает (внимание: не так как мы ожидаем): параметром функция принимает элемент, а возвращает объект, который содержит в себе все CSS свойства переданного элемента.
Давайте положим этот объект в переменную style. Название произвольное, это просто переменная - как придумаем, так и будем обращаться:
```
let elem = document.querySelector('#elem'); let style = getComputedStyle(
	elem); // в style 
лежат CSS свойства 
	
```
```
let elem = document.querySelector(".box");
console.log(elem);
let style = window.getComputedStyle(elem).getPropertyValue("height");
console.log(style);	
```

**Чем отличается event.target от event.currentTarget?**   
event.target – самый глубокий элемент, на котором произошло событие.  
event.currentTarget (=this) – элемент, на котором в данный момент сработал обработчик (до которого «доплыло» событие).

**Что делает метод event.preventDefault()?** 
Метод preventDefault () интерфейса Event сообщает User agent, что если событие не обрабатывается явно, его действие по умолчанию не должно выполняться так, как обычно.

**За что отвечает событие DOMContentLoaded?**

Событие DOMContentLoaded  запускается когда первоначальный HTML документ будет полностью загружен и разобран, без ожидания полной загрузки таблиц стилей, изображений и фреймов.  DOMContentLoaded – браузер полностью загрузил HTML, было построено DOM-дерево, но внешние ресурсы, такие как картинки <img> и стили, могут быть ещё не загружены.  
Событие DOMContentLoaded – DOM готов, так что обработчик может искать DOM-узлы и инициализировать интерфейс.  
Событие DOMContentLoaded срабатывает на объекте document.  
Мы должны использовать addEventListener, чтобы поймать его:
```
document.addEventListener("DOMContentLoaded", ready);
// не "document.onDOMContentLoaded = ..."
```
