<!-- ### Паттерн «Фасад» -->

Дальше я предлагаю посмотреть «Фасад», паттерн проектирования, который играет
критическую роль в архитектуре, которую мы сегодня определяем.

Когда вы строите фасад, вы, как правило, поднимаете некоторую абстракцию,
за которой находится иная реальность. Паттерн «фасад» обеспечивает удобный
**интерфейс более высокого уровня** для больших блоков кода, скрывая за собой
свою истинную сложность. Думайте об этом как об упрощающем API, который будет
предоставляться другим разработчикам.

Фасад — это **структурный паттерн**, который часто можно увидеть в JavaScript
библиотеках и фреймворках, где, не смотря на то, что имплементация поддерживает
методы с широким диапазоном поведений, только фасад или ограниченная абстракция 
этих методов доступна для пользователя. 

Это позволяет взаимодействовать с фасадом, а не с подсистемами, которые
находятся за кадром.

Причина, по которой нас интересует фасад — возможность скрыть тело реализации
деталей конкретной функциональности, которая находится в отдельных модулях. 
Таким образом можно изменять реализацию, не ставя в известность пользователей.

Поддерживая крепкий фасад (упрощенное API), мы иможем не беспокоиться о том, что
какой-то модуль плотно связан с dojo, jQuery, YUI, zepto или другой библиотекой.
Это становится менее важным. Пока слой взаимодействия не изменяется, вы
сохраняете возможность перейти с одной библиотеки на другую. Например, с jQuery
на dojo. Становится возможным сделать это и на более позднем этапе, не затрагивая
остальной системы.

Ниже я написал очень простой пример фасада в действии. Как вы видите, наш
модуль содержит некоторое количество приватных методов. Фасад здесь используется
для того, чтобы реализовать более простой API для доступа к этим методам:

{% highlight javascript %}
var module = (function() {
    var _private = {
        i:5,
        get : function() {
            console.log('current value:' + this.i);
        },
        set : function( val ) {
            this.i = val;
        },
        run : function() {
            console.log('running');
        },
        jump: function(){
            console.log('jumping');
        }
    };
    return {
        facade : function( args ) {
            _private.set(args.val);
            _private.get();
            if ( args.run ) {
                _private.run();
            }
        }
    }
}());


module.facade({run: true, val:10});
//outputs current value: 10, running
{% endhighlight %}

Это и есть причина, по которой мы добавили фасад к нашей архитектуре.
Теперь перейдем к паттерну «Медиатор». Принципиальное различие между паттерном
«фасад» и «медиатор» заключается в том, что фасад (структурный паттерн)
всего лишь передает существующую функциональность в медиатор, в то время как
медиатор (поведенческий паттерн) может расширять функциональность.

{:class="message"}
**Ссылки по теме:**  
[Dustin Diaz, Ross Harmes - Pro JavaScript Design Patterns (Chapter 10, available to read on Google Books)][1]  

[1]: http://books.google.co.uk/books?id=za3vlnlWxb0C&lpg=PA141&ots=MD5BLTsSzH&dq=javascript%20facade%20pattern&pg=PA141#v=onepage&q=javascript facade pattern&f=false